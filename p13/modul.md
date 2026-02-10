# Modul 13: Heap dan Priority Queue

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 13  
**Topik:** Heap dan Priority Queue

> **Capaian Pembelajaran:** Sub-CPMK-5.3, Sub-CPMK-4.2 — Mampu mengimplementasikan heap dan priority queue serta menerapkan heap sort

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.6; Weiss Ch.6; Hubbard Ch.12

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** konsep heap dan membedakan antara min-heap dan max-heap
2. **Mengidentifikasi** properti heap (complete binary tree + heap property)
3. **Menerapkan** representasi heap menggunakan array
4. **Mengimplementasikan** operasi heap: insert (percolate up), extract-min/max (percolate down), dan heapify
5. **Membangun** heap dari array dengan kompleksitas O(n)
6. **Mengimplementasikan** ADT Priority Queue menggunakan heap
7. **Menerapkan** algoritma Heap Sort dan menganalisis kompleksitasnya O(n log n)

---

## 1. Konsep Heap

### 1.1 Definisi Heap

> **Definisi:** Heap adalah struktur data berbentuk **complete binary tree** yang memenuhi **heap property**, yaitu hubungan tertentu antara nilai node parent dan nilai node child-nya.

Heap merupakan salah satu struktur data paling penting dalam ilmu komputer karena menyediakan cara efisien untuk mengakses elemen dengan prioritas tertinggi atau terendah dalam waktu konstan O(1).

### 1.2 Jenis-Jenis Heap

Terdapat dua jenis heap berdasarkan heap property:

| Jenis Heap | Heap Property | Penggunaan Utama |
|------------|---------------|------------------|
| **Max-Heap** | Nilai parent ≥ nilai semua child-nya | Mengakses elemen terbesar |
| **Min-Heap** | Nilai parent ≤ nilai semua child-nya | Mengakses elemen terkecil |

![Perbandingan Max-Heap dan Min-Heap](images/gambar-13-1.png)

*Gambar 13.1: Perbandingan struktur Max-Heap dan Min-Heap*

### 1.3 Properti Complete Binary Tree

> **Definisi:** Complete Binary Tree adalah binary tree di mana semua level terisi penuh kecuali mungkin level terakhir, dan pada level terakhir semua node terisi dari kiri ke kanan.

Properti ini memastikan bahwa heap selalu **balanced** dan dapat direpresentasikan secara efisien menggunakan array.

**Karakteristik Complete Binary Tree:**
- Tinggi tree dengan n node adalah ⌊log₂ n⌋
- Semua node internal memiliki tepat 2 child (kecuali mungkin satu node di level terakhir)
- Tidak ada "lubang" di level terakhir (node diisi dari kiri ke kanan)

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Tentukan apakah tree berikut merupakan heap yang valid! Jika ya, tentukan jenisnya (max-heap atau min-heap).

```
Tree A:        Tree B:        Tree C:
    50             10             30
   /  \           /  \           /  \
  30   20        20   15        50   40
 / \            / \   
8   25         30  25          
```

**Penyelesaian:**

**Tree A:**
- Complete binary tree? Ya ✓
- Heap property: 50 ≥ 30 dan 50 ≥ 20 ✓; 30 ≥ 8 dan 30 ≥ 25 ✓
- **Jawaban: Valid MAX-HEAP**

**Tree B:**
- Complete binary tree? Ya ✓
- Heap property: 10 ≤ 20 dan 10 ≤ 15 ✓; 20 ≤ 30 dan 20 ≤ 25 ✓
- **Jawaban: Valid MIN-HEAP**

**Tree C:**
- Complete binary tree? Ya ✓
- Heap property: 30 ≤ 50 ✓ dan 30 ≤ 40 ✓ (jika min-heap)
- Tapi 30 di root bukan minimum!
- **Jawaban: BUKAN HEAP yang valid** (tidak memenuhi heap property secara konsisten)

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Dalam konteks sistem pertahanan, mengapa heap cocok digunakan untuk sistem prioritas alert?

**Penyelesaian:**

Sistem alert pertahanan memerlukan respons cepat terhadap ancaman dengan prioritas tertinggi. Heap sangat cocok karena:

1. **Akses O(1) ke prioritas tertinggi**: Alert paling kritis selalu berada di root
2. **Insert O(log n)**: Menambah alert baru tetap efisien meski ada ribuan alert
3. **Extract O(log n)**: Mengambil alert prioritas tertinggi untuk diproses
4. **Automatic ordering**: Tidak perlu sorting manual setiap ada alert baru

**Contoh Implementasi:**
```cpp
struct AlertPertahanan {
    int prioritas;      // 1 = tertinggi (serangan langsung)
    string lokasi;
    string jenis;       // "udara", "laut", "darat", "cyber"
    time_t timestamp;
};

// Menggunakan min-heap berdasarkan prioritas
// Prioritas 1 (paling rendah nilainya) = paling penting
```

---

## 2. Representasi Heap dengan Array

### 2.1 Konsep Representasi Array

Karena heap adalah complete binary tree, kita dapat merepresentasikannya secara efisien menggunakan array tanpa pointer. Node-node disimpan level-by-level dari kiri ke kanan.

![Representasi Heap dalam Array](images/gambar-13-2.png)

*Gambar 13.2: Representasi heap dalam array — hubungan indeks parent dan child*

### 2.2 Formula Navigasi Heap

Untuk heap yang disimpan dalam array dengan indeks dimulai dari 0:

| Operasi | Formula | Contoh (i = 2) |
|---------|---------|----------------|
| **Parent** | `(i - 1) / 2` | Parent(2) = 0 |
| **Left Child** | `2 * i + 1` | Left(2) = 5 |
| **Right Child** | `2 * i + 2` | Right(2) = 6 |

### 2.3 Implementasi Dasar

```cpp
#include <iostream>
#include <vector>
using namespace std;

class MaxHeap {
private:
    vector<int> heap;
    
    int parent(int i) { return (i - 1) / 2; }
    int leftChild(int i) { return 2 * i + 1; }
    int rightChild(int i) { return 2 * i + 2; }
    
public:
    bool isEmpty() { return heap.empty(); }
    int size() { return heap.size(); }
    
    // Mendapatkan elemen maksimum tanpa menghapus
    int getMax() {
        if (isEmpty()) {
            throw runtime_error("Heap kosong!");
        }
        return heap[0];
    }
    
    // Method lain akan dibahas di bagian berikutnya
};
```

---

### SOLVED PROBLEM 3 ⭐

**Soal:** Diberikan array heap `[90, 85, 70, 40, 50, 30, 20]`. Tentukan:
a) Parent dari node di indeks 4
b) Left child dari node di indeks 1
c) Right child dari node di indeks 2

**Penyelesaian:**

Array: `[90, 85, 70, 40, 50, 30, 20]`
Indeks:  `[0,  1,  2,  3,  4,  5,  6]`

**a) Parent dari indeks 4:**
- Formula: `parent(i) = (i - 1) / 2`
- `parent(4) = (4 - 1) / 2 = 3 / 2 = 1`
- **Jawaban: Indeks 1, nilai 85**

**b) Left child dari indeks 1:**
- Formula: `leftChild(i) = 2 * i + 1`
- `leftChild(1) = 2 * 1 + 1 = 3`
- **Jawaban: Indeks 3, nilai 40**

**c) Right child dari indeks 2:**
- Formula: `rightChild(i) = 2 * i + 2`
- `rightChild(2) = 2 * 2 + 2 = 6`
- **Jawaban: Indeks 6, nilai 20**

---

### SOLVED PROBLEM 4 ⭐

**Soal:** Gambarkan heap tree dari array berikut: `[100, 90, 80, 70, 60, 50, 40]`. Tentukan apakah ini max-heap atau min-heap!

**Penyelesaian:**

**Konstruksi tree:**
```
Level 0:        100 (indeks 0)
               /    \
Level 1:     90      80 (indeks 1, 2)
            /  \    /  \
Level 2:  70   60  50   40 (indeks 3, 4, 5, 6)
```

**Verifikasi heap property:**
- 100 ≥ 90 dan 100 ≥ 80 ✓
- 90 ≥ 70 dan 90 ≥ 60 ✓
- 80 ≥ 50 dan 80 ≥ 40 ✓

**Jawaban:** Ini adalah **MAX-HEAP** yang valid karena setiap parent ≥ semua child-nya.

---

### SOLVED PROBLEM 5 ⭐⭐

**Soal:** Implementasikan fungsi untuk memeriksa apakah sebuah array merupakan valid max-heap!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isValidMaxHeap(const vector<int>& arr) {
    int n = arr.size();
    
    // Cek setiap node internal (yang memiliki child)
    // Node internal berada di indeks 0 sampai (n/2 - 1)
    for (int i = 0; i <= (n / 2) - 1; i++) {
        int leftIdx = 2 * i + 1;
        int rightIdx = 2 * i + 2;
        
        // Cek left child
        if (leftIdx < n && arr[i] < arr[leftIdx]) {
            return false;
        }
        
        // Cek right child
        if (rightIdx < n && arr[i] < arr[rightIdx]) {
            return false;
        }
    }
    
    return true;
}

int main() {
    vector<int> heap1 = {90, 85, 70, 40, 50, 30, 20};
    vector<int> heap2 = {90, 95, 70, 40, 50, 30, 20};  // Invalid
    
    cout << "heap1 valid: " << (isValidMaxHeap(heap1) ? "Ya" : "Tidak") << endl;
    cout << "heap2 valid: " << (isValidMaxHeap(heap2) ? "Ya" : "Tidak") << endl;
    
    return 0;
}
```

**Output:**
```
heap1 valid: Ya
heap2 valid: Tidak
```

**Kompleksitas:** O(n) karena memeriksa setiap node internal sekali.

---

## 3. Operasi Insert (Percolate Up)

### 3.1 Algoritma Insert

Proses insert pada heap terdiri dari dua langkah:
1. Tambahkan elemen baru di posisi terakhir (menjaga complete binary tree property)
2. **Percolate up** (bubble up): Pindahkan elemen ke atas sampai heap property terpenuhi

![Proses Insert pada Max-Heap](images/gambar-13-3.png)

*Gambar 13.3: Proses insert pada max-heap dengan percolate up*

### 3.2 Implementasi Insert

```cpp
void insert(int value) {
    // Step 1: Tambahkan di posisi terakhir
    heap.push_back(value);
    
    // Step 2: Percolate up
    int current = heap.size() - 1;
    
    while (current > 0) {
        int parentIdx = parent(current);
        
        // Untuk max-heap: jika current > parent, tukar
        if (heap[current] > heap[parentIdx]) {
            swap(heap[current], heap[parentIdx]);
            current = parentIdx;
        } else {
            break;  // Heap property sudah terpenuhi
        }
    }
}
```

### 3.3 Analisis Kompleksitas Insert

| Aspek | Kompleksitas | Penjelasan |
|-------|--------------|------------|
| **Waktu (Worst Case)** | O(log n) | Percolate dari leaf ke root |
| **Waktu (Best Case)** | O(1) | Elemen sudah di posisi benar |
| **Ruang** | O(1) | Hanya variabel tambahan |

---

### SOLVED PROBLEM 6 ⭐

**Soal:** Tunjukkan langkah-langkah insert nilai 95 ke dalam max-heap `[90, 85, 70, 40, 50]`!

**Penyelesaian:**

**State awal:**
```
      90
     /  \
   85    70
  /  \
40   50
Array: [90, 85, 70, 40, 50]
```

**Step 1: Insert 95 di akhir**
```
      90
     /  \
   85    70
  /  \   /
40  50  95
Array: [90, 85, 70, 40, 50, 95]
```

**Step 2: Percolate up - Compare 95 dengan parent (70)**
- 95 > 70 → Swap!
```
      90
     /  \
   85    95
  /  \   /
40  50  70
Array: [90, 85, 95, 40, 50, 70]
```

**Step 3: Percolate up - Compare 95 dengan parent (90)**
- 95 > 90 → Swap!
```
      95
     /  \
   85    90
  /  \   /
40  50  70
Array: [95, 85, 90, 40, 50, 70]
```

**Hasil akhir:** `[95, 85, 90, 40, 50, 70]`

---

### SOLVED PROBLEM 7 ⭐⭐

**Soal:** Implementasikan insert untuk min-heap dan tunjukkan trace untuk memasukkan nilai 5 ke heap `[10, 20, 15, 30, 25]`!

**Penyelesaian:**

```cpp
void insertMinHeap(vector<int>& heap, int value) {
    heap.push_back(value);
    int current = heap.size() - 1;
    
    while (current > 0) {
        int parentIdx = (current - 1) / 2;
        
        // Untuk min-heap: jika current < parent, tukar
        if (heap[current] < heap[parentIdx]) {
            swap(heap[current], heap[parentIdx]);
            current = parentIdx;
        } else {
            break;
        }
    }
}
```

**Trace insert 5:**

```
State awal: [10, 20, 15, 30, 25]
      10
     /  \
   20    15
  /  \
30   25

Insert 5 di akhir: [10, 20, 15, 30, 25, 5]
      10
     /  \
   20    15
  /  \   /
30  25  5

Compare 5 dengan parent 15: 5 < 15 → Swap
      10
     /  \
   20    5
  /  \   /
30  25  15
Array: [10, 20, 5, 30, 25, 15]

Compare 5 dengan parent 10: 5 < 10 → Swap
      5
     /  \
   20    10
  /  \   /
30  25  15
Array: [5, 20, 10, 30, 25, 15]

5 sudah di root → selesai
```

**Hasil akhir:** `[5, 20, 10, 30, 25, 15]`

---

## 4. Operasi Extract (Percolate Down)

### 4.1 Algoritma Extract-Max / Extract-Min

Operasi extract menghapus dan mengembalikan elemen root (nilai maksimum untuk max-heap atau minimum untuk min-heap):

1. Simpan nilai root untuk dikembalikan
2. Pindahkan elemen terakhir ke posisi root
3. Hapus posisi terakhir
4. **Percolate down** (sift down): Pindahkan root ke bawah sampai heap property terpenuhi

![Proses Extract pada Max-Heap](images/gambar-13-4.png)

*Gambar 13.4: Proses extract-max dengan percolate down*

### 4.2 Implementasi Extract-Max

```cpp
int extractMax() {
    if (isEmpty()) {
        throw runtime_error("Heap kosong!");
    }
    
    // Simpan nilai maksimum
    int maxValue = heap[0];
    
    // Pindahkan elemen terakhir ke root
    heap[0] = heap.back();
    heap.pop_back();
    
    // Percolate down dari root
    if (!isEmpty()) {
        percolateDown(0);
    }
    
    return maxValue;
}

void percolateDown(int index) {
    int n = heap.size();
    int largest = index;
    int left = leftChild(index);
    int right = rightChild(index);
    
    // Cari yang terbesar antara current, left child, dan right child
    if (left < n && heap[left] > heap[largest]) {
        largest = left;
    }
    if (right < n && heap[right] > heap[largest]) {
        largest = right;
    }
    
    // Jika largest bukan current, tukar dan lanjutkan
    if (largest != index) {
        swap(heap[index], heap[largest]);
        percolateDown(largest);  // Rekursif
    }
}
```

### 4.3 Analisis Kompleksitas Extract

| Aspek | Kompleksitas | Penjelasan |
|-------|--------------|------------|
| **Waktu (Worst Case)** | O(log n) | Percolate dari root ke leaf |
| **Waktu (Best Case)** | O(1) | Elemen terakhir sudah valid di root |
| **Ruang** | O(log n) | Stack rekursi (bisa O(1) dengan iteratif) |

---

### SOLVED PROBLEM 8 ⭐

**Soal:** Lakukan extract-max pada heap `[90, 85, 70, 40, 50, 30, 20]` dan tunjukkan heap setelahnya!

**Penyelesaian:**

**State awal:**
```
      90
     /  \
   85    70
  /  \   /  \
40  50  30  20
Array: [90, 85, 70, 40, 50, 30, 20]
```

**Step 1: Ambil root (90), pindahkan 20 ke root**
```
      20
     /  \
   85    70
  /  \   /
40  50  30
Array: [20, 85, 70, 40, 50, 30]
```

**Step 2: Percolate down - Compare 20 dengan children (85, 70)**
- Largest adalah 85
- 20 < 85 → Swap!
```
      85
     /  \
   20    70
  /  \   /
40  50  30
Array: [85, 20, 70, 40, 50, 30]
```

**Step 3: Percolate down - Compare 20 dengan children (40, 50)**
- Largest adalah 50
- 20 < 50 → Swap!
```
      85
     /  \
   50    70
  /  \   /
40  20  30
Array: [85, 50, 70, 40, 20, 30]
```

**Hasil:**
- Nilai yang di-extract: **90**
- Heap setelah extract: `[85, 50, 70, 40, 20, 30]`

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Implementasikan versi iteratif dari percolate down untuk max-heap!

**Penyelesaian:**

```cpp
void percolateDownIterative(int index) {
    int n = heap.size();
    
    while (true) {
        int largest = index;
        int left = 2 * index + 1;
        int right = 2 * index + 2;
        
        // Cari yang terbesar
        if (left < n && heap[left] > heap[largest]) {
            largest = left;
        }
        if (right < n && heap[right] > heap[largest]) {
            largest = right;
        }
        
        // Jika current sudah terbesar, selesai
        if (largest == index) {
            break;
        }
        
        // Tukar dan lanjutkan
        swap(heap[index], heap[largest]);
        index = largest;
    }
}
```

**Keuntungan versi iteratif:**
- Kompleksitas ruang O(1) (tidak ada stack rekursi)
- Lebih efisien untuk heap yang sangat besar
- Tidak ada risiko stack overflow

---

### SOLVED PROBLEM 10 ⭐⭐

**Soal:** Dalam sistem pertahanan, sebuah Command Center menggunakan max-heap untuk mengelola task berdasarkan prioritas (1 = terendah, 10 = tertinggi). Simulasikan operasi berikut dan tunjukkan state heap setiap langkah:
1. Insert task dengan prioritas: 7, 3, 9, 5, 8
2. Extract 2 task dengan prioritas tertinggi

**Penyelesaian:**

**Insert 7:**
```
Heap: [7]
```

**Insert 3:**
```
    7
   /
  3
Heap: [7, 3]
3 < 7, tidak perlu percolate up
```

**Insert 9:**
```
    7           9
   / \    →    / \
  3   9       3   7
Heap: [7, 3, 9] → [9, 3, 7]
9 > 7, swap!
```

**Insert 5:**
```
    9
   / \
  3   7
 /
5
Heap: [9, 3, 7, 5]
5 > 3, swap dengan parent
    9
   / \
  5   7
 /
3
Heap: [9, 5, 7, 3]
```

**Insert 8:**
```
    9               9
   / \             / \
  5   7     →     8   7
 / \             / \
3   8           3   5
Heap: [9, 5, 7, 3, 8] → [9, 8, 7, 3, 5]
8 > 5, swap!
```

**Extract pertama (prioritas 9):**
```
Move 5 to root:    Percolate down:
    5                   8
   / \                 / \
  8   7       →       5   7
 /                   /
3                   3
Heap: [5, 8, 7, 3] → [8, 5, 7, 3]
```
**Task dengan prioritas 9 diproses**

**Extract kedua (prioritas 8):**
```
Move 3 to root:    Percolate down:
    3                   7
   / \                 / \
  5   7       →       5   3
Heap: [3, 5, 7] → [7, 5, 3]
```
**Task dengan prioritas 8 diproses**

**Heap final:** `[7, 5, 3]`

---

## 5. Build Heap (Heapify)

### 5.1 Algoritma Build Heap

Ada dua pendekatan untuk membangun heap dari array:

| Pendekatan | Metode | Kompleksitas |
|------------|--------|--------------|
| **Top-down** | Insert elemen satu per satu | O(n log n) |
| **Bottom-up (Floyd)** | Heapify dari node internal terakhir | O(n) |

### 5.2 Algoritma Floyd (Bottom-up)

> **Insight:** Semua leaf node sudah merupakan heap yang valid (heap dengan 1 elemen). Kita hanya perlu memperbaiki node internal.

```cpp
void buildHeap(vector<int>& arr) {
    int n = arr.size();
    
    // Mulai dari node internal terakhir
    // Node internal terakhir = parent dari node terakhir = (n/2 - 1)
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
}

void heapify(vector<int>& arr, int n, int index) {
    int largest = index;
    int left = 2 * index + 1;
    int right = 2 * index + 2;
    
    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }
    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }
    
    if (largest != index) {
        swap(arr[index], arr[largest]);
        heapify(arr, n, largest);
    }
}
```

![Proses Build Heap Bottom-up](images/gambar-13-5.png)

*Gambar 13.5: Proses build heap menggunakan algoritma Floyd (bottom-up)*

### 5.3 Analisis Kompleksitas Build Heap

Mengapa build heap O(n) bukan O(n log n)?

**Analisis matematis:**
- Node di level h dari bawah memerlukan maksimal h operasi swap
- Jumlah node di level h dari bawah ≈ n/2^(h+1)
- Total operasi = Σ (h × n/2^(h+1)) untuk h = 0 sampai log n
- Hasilnya konvergen ke **O(n)**

| Metode | Kompleksitas | Penjelasan |
|--------|--------------|------------|
| Insert satu per satu | O(n log n) | n insert × O(log n) per insert |
| Floyd's algorithm | O(n) | Lebih banyak node di level bawah dengan jarak pendek ke posisi final |

---

### SOLVED PROBLEM 11 ⭐

**Soal:** Bangun max-heap dari array `[4, 10, 3, 5, 1]` menggunakan algoritma Floyd!

**Penyelesaian:**

Array: `[4, 10, 3, 5, 1]`
n = 5, node internal terakhir = 5/2 - 1 = 1

**State awal (sebagai tree):**
```
      4
     / \
   10   3
  /  \
 5    1
```

**Step 1: Heapify indeks 1 (nilai 10)**
- Left child: indeks 3, nilai 5
- Right child: indeks 4, nilai 1
- Largest = 10 (sudah benar)
- Tidak ada perubahan

**Step 2: Heapify indeks 0 (nilai 4)**
- Left child: indeks 1, nilai 10
- Right child: indeks 2, nilai 3
- Largest = 10 (indeks 1)
- Swap 4 dengan 10

```
      10
     /  \
    4    3
   / \
  5   1
Array: [10, 4, 3, 5, 1]
```

**Step 3: Lanjutkan heapify indeks 1 (nilai 4)**
- Left child: indeks 3, nilai 5
- Right child: indeks 4, nilai 1
- Largest = 5 (indeks 3)
- Swap 4 dengan 5

```
      10
     /  \
    5    3
   / \
  4   1
Array: [10, 5, 3, 4, 1]
```

**Hasil akhir:** `[10, 5, 3, 4, 1]` ✓

---

### SOLVED PROBLEM 12 ⭐⭐

**Soal:** Jelaskan mengapa algoritma Floyd memiliki kompleksitas O(n) dengan bukti informal!

**Penyelesaian:**

**Struktur heap:**
Untuk heap dengan n node dan tinggi h = ⌊log₂ n⌋:
- Level 0 (root): 1 node, perlu maksimal h swap
- Level 1: 2 node, perlu maksimal h-1 swap
- Level 2: 4 node, perlu maksimal h-2 swap
- ...
- Level h-1: ~n/4 node, perlu maksimal 1 swap
- Level h (leaf): ~n/2 node, tidak perlu swap

**Kalkulasi total swap:**
```
Total = Σ (jumlah node di level i) × (jarak ke leaf)
      = 1×h + 2×(h-1) + 4×(h-2) + ... + (n/4)×1 + (n/2)×0
```

**Observasi kunci:**
- Setengah node adalah leaf → 0 operasi
- Seperempat node perlu ≤ 1 operasi
- Semakin tinggi level, semakin sedikit node tapi semakin banyak operasi

**Hasil:**
Menggunakan analisis deret geometri, total operasi adalah **O(n)**.

**Intuisi:** Mayoritas node (leaf) tidak memerlukan operasi, dan node yang memerlukan banyak operasi jumlahnya sangat sedikit.

---

## 6. Priority Queue

### 6.1 Definisi ADT Priority Queue

> **Definisi:** Priority Queue adalah ADT yang menyimpan elemen-elemen dengan prioritas tertentu, di mana elemen dengan prioritas tertinggi selalu diakses terlebih dahulu.

### 6.2 Operasi Priority Queue

| Operasi | Deskripsi | Implementasi Heap |
|---------|-----------|-------------------|
| `insert(elem, priority)` | Menambah elemen dengan prioritas | O(log n) |
| `extractMax()` / `extractMin()` | Mengambil elemen prioritas tertinggi | O(log n) |
| `peek()` / `getMax()` / `getMin()` | Melihat tanpa menghapus | O(1) |
| `isEmpty()` | Cek apakah kosong | O(1) |
| `changePriority(elem, newPriority)` | Mengubah prioritas | O(log n)* |

*Memerlukan tambahan data structure untuk tracking posisi

### 6.3 Implementasi Priority Queue dengan Heap

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Task {
    string nama;
    int prioritas;
    
    Task(string n, int p) : nama(n), prioritas(p) {}
};

class PriorityQueue {
private:
    vector<Task> heap;
    
    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return 2 * i + 1; }
    int right(int i) { return 2 * i + 2; }
    
    void percolateUp(int index) {
        while (index > 0 && heap[index].prioritas > heap[parent(index)].prioritas) {
            swap(heap[index], heap[parent(index)]);
            index = parent(index);
        }
    }
    
    void percolateDown(int index) {
        int n = heap.size();
        int largest = index;
        int l = left(index);
        int r = right(index);
        
        if (l < n && heap[l].prioritas > heap[largest].prioritas) {
            largest = l;
        }
        if (r < n && heap[r].prioritas > heap[largest].prioritas) {
            largest = r;
        }
        
        if (largest != index) {
            swap(heap[index], heap[largest]);
            percolateDown(largest);
        }
    }
    
public:
    void insert(const Task& task) {
        heap.push_back(task);
        percolateUp(heap.size() - 1);
    }
    
    Task extractMax() {
        if (heap.empty()) {
            throw runtime_error("Queue kosong!");
        }
        
        Task maxTask = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        
        if (!heap.empty()) {
            percolateDown(0);
        }
        
        return maxTask;
    }
    
    Task peek() {
        if (heap.empty()) {
            throw runtime_error("Queue kosong!");
        }
        return heap[0];
    }
    
    bool isEmpty() { return heap.empty(); }
    int size() { return heap.size(); }
};

int main() {
    PriorityQueue pq;
    
    pq.insert(Task("Laporan harian", 3));
    pq.insert(Task("Alert kritis", 10));
    pq.insert(Task("Backup data", 5));
    pq.insert(Task("Meeting rutin", 2));
    
    cout << "Proses task berdasarkan prioritas:" << endl;
    while (!pq.isEmpty()) {
        Task t = pq.extractMax();
        cout << "- " << t.nama << " (prioritas: " << t.prioritas << ")" << endl;
    }
    
    return 0;
}
```

**Output:**
```
Proses task berdasarkan prioritas:
- Alert kritis (prioritas: 10)
- Backup data (prioritas: 5)
- Laporan harian (prioritas: 3)
- Meeting rutin (prioritas: 2)
```

---

### SOLVED PROBLEM 13 ⭐

**Soal:** Jelaskan perbedaan antara Queue biasa (FIFO) dan Priority Queue!

**Penyelesaian:**

| Aspek | Queue (FIFO) | Priority Queue |
|-------|--------------|----------------|
| **Urutan keluar** | First In First Out | Berdasarkan prioritas |
| **Dequeue** | Elemen tertua | Elemen prioritas tertinggi |
| **Ordering** | Berdasarkan waktu masuk | Berdasarkan nilai prioritas |
| **Implementasi efisien** | Array/Linked List | Heap |
| **Insert** | O(1) | O(log n) |
| **Remove** | O(1) | O(log n) |
| **Contoh penggunaan** | Antrian kasir | Sistem penjadwalan task |

**Ilustrasi:**
```
Queue FIFO:     Insert A, B, C → Dequeue A, B, C (urut masuk)
Priority Queue: Insert A(3), B(1), C(5) → Dequeue C, A, B (urut prioritas)
```

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Implementasikan min-priority queue untuk sistem antrian pasien di rumah sakit militer, di mana prioritas lebih kecil = lebih darurat!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Pasien {
    string nama;
    int tingkatDarurat;  // 1 = paling darurat, 5 = ringan
    string keluhan;
    
    Pasien(string n, int t, string k) : nama(n), tingkatDarurat(t), keluhan(k) {}
};

class AntrianPasien {
private:
    vector<Pasien> heap;
    
    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return 2 * i + 1; }
    int right(int i) { return 2 * i + 2; }
    
    void percolateUp(int index) {
        // Min-heap: parent <= children
        while (index > 0 && heap[index].tingkatDarurat < heap[parent(index)].tingkatDarurat) {
            swap(heap[index], heap[parent(index)]);
            index = parent(index);
        }
    }
    
    void percolateDown(int index) {
        int n = heap.size();
        int smallest = index;
        int l = left(index);
        int r = right(index);
        
        if (l < n && heap[l].tingkatDarurat < heap[smallest].tingkatDarurat) {
            smallest = l;
        }
        if (r < n && heap[r].tingkatDarurat < heap[smallest].tingkatDarurat) {
            smallest = r;
        }
        
        if (smallest != index) {
            swap(heap[index], heap[smallest]);
            percolateDown(smallest);
        }
    }
    
public:
    void daftarPasien(const Pasien& p) {
        heap.push_back(p);
        percolateUp(heap.size() - 1);
        cout << "[DAFTAR] " << p.nama << " - Tingkat " << p.tingkatDarurat << endl;
    }
    
    Pasien panggilPasien() {
        if (heap.empty()) {
            throw runtime_error("Tidak ada pasien!");
        }
        
        Pasien p = heap[0];
        heap[0] = heap.back();
        heap.pop_back();
        
        if (!heap.empty()) {
            percolateDown(0);
        }
        
        return p;
    }
    
    void tampilkanAntrian() {
        cout << "\n=== Antrian Pasien ===" << endl;
        for (const auto& p : heap) {
            cout << "- " << p.nama << " (Tingkat " << p.tingkatDarurat << "): " 
                 << p.keluhan << endl;
        }
    }
    
    bool isEmpty() { return heap.empty(); }
};

int main() {
    AntrianPasien antrian;
    
    cout << "=== SISTEM ANTRIAN RS MILITER ===" << endl << endl;
    
    antrian.daftarPasien(Pasien("Kopral Budi", 3, "Demam"));
    antrian.daftarPasien(Pasien("Sersan Adi", 1, "Luka tembak"));
    antrian.daftarPasien(Pasien("Praka Deni", 4, "Sakit kepala"));
    antrian.daftarPasien(Pasien("Lettu Eko", 2, "Patah tulang"));
    antrian.daftarPasien(Pasien("Prada Fajar", 1, "Pendarahan"));
    
    antrian.tampilkanAntrian();
    
    cout << "\n=== PROSES PERAWATAN ===" << endl;
    while (!antrian.isEmpty()) {
        Pasien p = antrian.panggilPasien();
        cout << "[PANGGIL] " << p.nama << " - Tingkat " << p.tingkatDarurat 
             << " (" << p.keluhan << ")" << endl;
    }
    
    return 0;
}
```

**Output:**
```
=== SISTEM ANTRIAN RS MILITER ===

[DAFTAR] Kopral Budi - Tingkat 3
[DAFTAR] Sersan Adi - Tingkat 1
[DAFTAR] Praka Deni - Tingkat 4
[DAFTAR] Lettu Eko - Tingkat 2
[DAFTAR] Prada Fajar - Tingkat 1

=== Antrian Pasien ===
- Sersan Adi (Tingkat 1): Luka tembak
- Prada Fajar (Tingkat 1): Pendarahan
- Praka Deni (Tingkat 4): Sakit kepala
- Kopral Budi (Tingkat 3): Demam
- Lettu Eko (Tingkat 2): Patah tulang

=== PROSES PERAWATAN ===
[PANGGIL] Sersan Adi - Tingkat 1 (Luka tembak)
[PANGGIL] Prada Fajar - Tingkat 1 (Pendarahan)
[PANGGIL] Lettu Eko - Tingkat 2 (Patah tulang)
[PANGGIL] Kopral Budi - Tingkat 3 (Demam)
[PANGGIL] Praka Deni - Tingkat 4 (Sakit kepala)
```

---

### SOLVED PROBLEM 15 ⭐⭐⭐

**Soal:** Implementasikan operasi `decreaseKey` dan `increaseKey` untuk priority queue! Operasi ini mengubah prioritas elemen yang sudah ada dalam queue.

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
using namespace std;

class AdvancedPriorityQueue {
private:
    vector<pair<int, int>> heap;  // pair<id, priority>
    unordered_map<int, int> positionMap;  // id -> index di heap
    
    int parent(int i) { return (i - 1) / 2; }
    int left(int i) { return 2 * i + 1; }
    int right(int i) { return 2 * i + 2; }
    
    void swapNodes(int i, int j) {
        positionMap[heap[i].first] = j;
        positionMap[heap[j].first] = i;
        swap(heap[i], heap[j]);
    }
    
    void percolateUp(int index) {
        while (index > 0 && heap[index].second > heap[parent(index)].second) {
            swapNodes(index, parent(index));
            index = parent(index);
        }
    }
    
    void percolateDown(int index) {
        int n = heap.size();
        int largest = index;
        int l = left(index);
        int r = right(index);
        
        if (l < n && heap[l].second > heap[largest].second) largest = l;
        if (r < n && heap[r].second > heap[largest].second) largest = r;
        
        if (largest != index) {
            swapNodes(index, largest);
            percolateDown(largest);
        }
    }
    
public:
    void insert(int id, int priority) {
        heap.push_back({id, priority});
        positionMap[id] = heap.size() - 1;
        percolateUp(heap.size() - 1);
    }
    
    pair<int, int> extractMax() {
        if (heap.empty()) throw runtime_error("Queue kosong!");
        
        auto maxItem = heap[0];
        positionMap.erase(heap[0].first);
        
        heap[0] = heap.back();
        heap.pop_back();
        
        if (!heap.empty()) {
            positionMap[heap[0].first] = 0;
            percolateDown(0);
        }
        
        return maxItem;
    }
    
    // Meningkatkan prioritas (untuk max-heap)
    void increaseKey(int id, int newPriority) {
        if (positionMap.find(id) == positionMap.end()) {
            throw runtime_error("ID tidak ditemukan!");
        }
        
        int index = positionMap[id];
        if (newPriority <= heap[index].second) {
            throw runtime_error("Prioritas baru harus lebih besar!");
        }
        
        heap[index].second = newPriority;
        percolateUp(index);  // Naik ke atas
    }
    
    // Menurunkan prioritas (untuk max-heap)
    void decreaseKey(int id, int newPriority) {
        if (positionMap.find(id) == positionMap.end()) {
            throw runtime_error("ID tidak ditemukan!");
        }
        
        int index = positionMap[id];
        if (newPriority >= heap[index].second) {
            throw runtime_error("Prioritas baru harus lebih kecil!");
        }
        
        heap[index].second = newPriority;
        percolateDown(index);  // Turun ke bawah
    }
    
    void printHeap() {
        cout << "Heap: ";
        for (const auto& p : heap) {
            cout << "(" << p.first << "," << p.second << ") ";
        }
        cout << endl;
    }
};

int main() {
    AdvancedPriorityQueue pq;
    
    pq.insert(1, 10);  // Task 1, prioritas 10
    pq.insert(2, 20);  // Task 2, prioritas 20
    pq.insert(3, 15);  // Task 3, prioritas 15
    pq.insert(4, 5);   // Task 4, prioritas 5
    
    cout << "Setelah insert:" << endl;
    pq.printHeap();
    
    cout << "\nIncrease key Task 4 dari 5 ke 25:" << endl;
    pq.increaseKey(4, 25);
    pq.printHeap();
    
    cout << "\nDecrease key Task 2 dari 20 ke 8:" << endl;
    pq.decreaseKey(2, 8);
    pq.printHeap();
    
    cout << "\nExtract max:" << endl;
    while (true) {
        try {
            auto item = pq.extractMax();
            cout << "Extracted: Task " << item.first << " (prioritas " << item.second << ")" << endl;
        } catch (...) {
            break;
        }
    }
    
    return 0;
}
```

**Output:**
```
Setelah insert:
Heap: (2,20) (4,5) (3,15) (1,10) 

Increase key Task 4 dari 5 ke 25:
Heap: (4,25) (2,20) (3,15) (1,10) 

Decrease key Task 2 dari 20 ke 8:
Heap: (4,25) (1,10) (3,15) (2,8) 

Extract max:
Extracted: Task 4 (prioritas 25)
Extracted: Task 3 (prioritas 15)
Extracted: Task 1 (prioritas 10)
Extracted: Task 2 (prioritas 8)
```

**Kompleksitas:**
- `increaseKey`: O(log n) - percolate up
- `decreaseKey`: O(log n) - percolate down
- Memerlukan hash map untuk tracking posisi: O(1) lookup

---

## 7. Heap Sort

### 7.1 Algoritma Heap Sort

Heap Sort adalah algoritma sorting yang memanfaatkan struktur heap:

1. **Build max-heap** dari array input
2. **Extract max** berulang kali dan tempatkan di akhir array

```cpp
void heapSort(vector<int>& arr) {
    int n = arr.size();
    
    // Step 1: Build max-heap
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(arr, n, i);
    }
    
    // Step 2: Extract elements one by one
    for (int i = n - 1; i > 0; i--) {
        // Pindahkan root (max) ke akhir
        swap(arr[0], arr[i]);
        
        // Heapify reduced heap
        heapify(arr, i, 0);
    }
}

void heapify(vector<int>& arr, int n, int i) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    
    if (left < n && arr[left] > arr[largest]) largest = left;
    if (right < n && arr[right] > arr[largest]) largest = right;
    
    if (largest != i) {
        swap(arr[i], arr[largest]);
        heapify(arr, n, largest);
    }
}
```

![Proses Heap Sort](images/gambar-13-6.png)

*Gambar 13.6: Proses heap sort — build heap dan extract max berulang*

### 7.2 Analisis Kompleksitas Heap Sort

| Aspek | Kompleksitas | Penjelasan |
|-------|--------------|------------|
| **Build Heap** | O(n) | Algoritma Floyd |
| **Extract n kali** | O(n log n) | n extract × O(log n) per extract |
| **Total Waktu** | O(n log n) | Build + Extract |
| **Ruang** | O(1) | In-place sorting |
| **Stabilitas** | Tidak stabil | Elemen dengan nilai sama bisa bertukar posisi relatif |

### 7.3 Perbandingan dengan Sorting Lain

| Algoritma | Best | Average | Worst | Space | Stabil |
|-----------|------|---------|-------|-------|--------|
| **Heap Sort** | O(n log n) | O(n log n) | O(n log n) | O(1) | Tidak |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | Tidak |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Ya |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Ya |

---

### SOLVED PROBLEM 16 ⭐

**Soal:** Lakukan heap sort pada array `[4, 10, 3, 5, 1]` dan tunjukkan langkah-langkahnya!

**Penyelesaian:**

**Step 1: Build Max-Heap**

Array awal: `[4, 10, 3, 5, 1]`

Heapify dari i = 1 ke 0:
- i = 1: Node 10, children 5 dan 1. 10 > 5 dan 10 > 1. Tidak ada perubahan.
- i = 0: Node 4, children 10 dan 3. Largest = 10. Swap 4 dengan 10.
  - Array: `[10, 4, 3, 5, 1]`
  - Lanjut heapify di indeks 1: 4 < 5. Swap 4 dengan 5.
  - Array: `[10, 5, 3, 4, 1]`

Max-heap: `[10, 5, 3, 4, 1]`

**Step 2: Extract dan Sort**

| Iterasi | Swap | Heapify | Array | Sorted |
|---------|------|---------|-------|--------|
| 1 | arr[0]↔arr[4] | [1,5,3,4] → [5,4,3,1] | [5,4,3,1,10] | 10 |
| 2 | arr[0]↔arr[3] | [1,4,3] → [4,1,3] | [4,1,3,5,10] | 5,10 |
| 3 | arr[0]↔arr[2] | [3,1] → [3,1] | [3,1,4,5,10] | 4,5,10 |
| 4 | arr[0]↔arr[1] | [1] → [1] | [1,3,4,5,10] | 3,4,5,10 |

**Hasil akhir:** `[1, 3, 4, 5, 10]` ✓

---

### SOLVED PROBLEM 17 ⭐⭐

**Soal:** Mengapa heap sort tidak stabil? Berikan contoh!

**Penyelesaian:**

**Definisi stabilitas:** Sorting stabil mempertahankan urutan relatif elemen dengan nilai sama.

**Contoh ketidakstabilan heap sort:**

Array dengan objek: `[(A,3), (B,3), (C,1)]`
- A dan B memiliki nilai sama (3)
- Urutan awal: A sebelum B

**Proses:**
```
Build max-heap: [(A,3), (B,3), (C,1)] atau [(B,3), (A,3), (C,1)]
                (tergantung cara heapify)

Extract:
- Extract (B,3) atau (A,3) - bisa bertukar posisi
```

**Alasan ketidakstabilan:**
1. Build heap dapat mengubah urutan relatif elemen dengan nilai sama
2. Saat extract max, elemen terakhir (bisa berbeda urutan) dipindah ke root
3. Proses heapify tidak mempertimbangkan urutan asli

**Contoh konkret:**
```cpp
// Array: [5a, 5b, 3] (5a dan 5b adalah nilai 5 yang berbeda objek)
// Setelah heap sort: [3, 5b, 5a] atau [3, 5a, 5b]
// Urutan 5a dan 5b tidak dijamin sama dengan input
```

---

### SOLVED PROBLEM 18 ⭐⭐

**Soal:** Kapan sebaiknya menggunakan heap sort dibandingkan quick sort atau merge sort?

**Penyelesaian:**

**Gunakan Heap Sort ketika:**

1. **Worst case guarantee penting**
   - Heap sort selalu O(n log n)
   - Quick sort bisa O(n²) pada worst case

2. **Memory terbatas**
   - Heap sort O(1) space
   - Merge sort memerlukan O(n) space

3. **Partial sorting diperlukan**
   - Hanya butuh k elemen terbesar/terkecil
   - Build heap + k extract = O(n + k log n)

4. **Real-time systems**
   - Waktu eksekusi lebih predictable
   - Tidak ada worst case yang buruk

**Gunakan Quick Sort ketika:**
- Average case performance prioritas
- Cache efficiency penting
- Data random

**Gunakan Merge Sort ketika:**
- Stabilitas diperlukan
- External sorting (data terlalu besar untuk RAM)
- Linked list sorting

**Contoh penggunaan heap sort di pertahanan:**
- Sistem radar dengan memory terbatas
- Real-time threat assessment (perlu guarantee waktu)
- Mencari k ancaman paling berbahaya dari banyak deteksi

---

### SOLVED PROBLEM 19 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk mencari k elemen terbesar dari array menggunakan heap dengan efisiensi optimal!

**Penyelesaian:**

**Pendekatan optimal: Min-heap dengan ukuran k**

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

vector<int> findKLargest(const vector<int>& arr, int k) {
    if (k <= 0 || k > arr.size()) {
        return {};
    }
    
    // Min-heap dengan ukuran maksimal k
    priority_queue<int, vector<int>, greater<int>> minHeap;
    
    for (int num : arr) {
        if (minHeap.size() < k) {
            minHeap.push(num);
        } else if (num > minHeap.top()) {
            minHeap.pop();
            minHeap.push(num);
        }
    }
    
    // Extract hasil
    vector<int> result;
    while (!minHeap.empty()) {
        result.push_back(minHeap.top());
        minHeap.pop();
    }
    
    return result;
}

int main() {
    vector<int> data = {3, 2, 1, 5, 6, 4, 8, 9, 7};
    int k = 4;
    
    vector<int> largest = findKLargest(data, k);
    
    cout << k << " elemen terbesar: ";
    for (int num : largest) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

**Output:**
```
4 elemen terbesar: 6 7 8 9 
```

**Analisis kompleksitas:**

| Pendekatan | Waktu | Ruang |
|------------|-------|-------|
| Sort seluruh array | O(n log n) | O(1) atau O(n) |
| Max-heap + k extract | O(n + k log n) | O(n) |
| **Min-heap ukuran k** | **O(n log k)** | **O(k)** |

**Mengapa min-heap ukuran k optimal?**
- Hanya menyimpan k elemen terbesar yang ditemukan sejauh ini
- Elemen terkecil dari k terbesar ada di root → mudah dibandingkan
- Jika elemen baru > root, ganti root
- Cocok untuk k << n (misal mencari 10 terbesar dari 1 juta data)

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Dalam sistem pertahanan siber, implementasikan sistem deteksi anomali yang menyimpan k alert dengan severity tertinggi menggunakan heap!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <string>
#include <ctime>
using namespace std;

struct CyberAlert {
    string id;
    int severity;      // 1-100, lebih tinggi = lebih serius
    string source;     // IP source
    string type;       // jenis serangan
    time_t timestamp;
    
    CyberAlert(string i, int s, string src, string t) 
        : id(i), severity(s), source(src), type(t), timestamp(time(nullptr)) {}
    
    // Untuk min-heap: yang lebih kecil severity-nya = prioritas lebih tinggi di heap
    bool operator>(const CyberAlert& other) const {
        return severity > other.severity;
    }
};

class TopKAlertSystem {
private:
    priority_queue<CyberAlert, vector<CyberAlert>, greater<CyberAlert>> minHeap;
    int maxAlerts;
    int totalProcessed;
    
public:
    TopKAlertSystem(int k) : maxAlerts(k), totalProcessed(0) {}
    
    void processAlert(const CyberAlert& alert) {
        totalProcessed++;
        
        if (minHeap.size() < maxAlerts) {
            minHeap.push(alert);
            cout << "[STORED] Alert " << alert.id << " (severity " << alert.severity << ")" << endl;
        } else if (alert.severity > minHeap.top().severity) {
            cout << "[REPLACED] Alert " << alert.id << " (severity " << alert.severity 
                 << ") replaces " << minHeap.top().id << " (severity " 
                 << minHeap.top().severity << ")" << endl;
            minHeap.pop();
            minHeap.push(alert);
        } else {
            cout << "[IGNORED] Alert " << alert.id << " (severity " << alert.severity 
                 << ") - tidak masuk top " << maxAlerts << endl;
        }
    }
    
    void displayTopAlerts() {
        cout << "\n========================================" << endl;
        cout << "TOP " << maxAlerts << " ALERTS (dari " << totalProcessed << " total)" << endl;
        cout << "========================================" << endl;
        
        vector<CyberAlert> alerts;
        priority_queue<CyberAlert, vector<CyberAlert>, greater<CyberAlert>> tempHeap = minHeap;
        
        while (!tempHeap.empty()) {
            alerts.push_back(tempHeap.top());
            tempHeap.pop();
        }
        
        // Tampilkan dari severity tertinggi
        for (int i = alerts.size() - 1; i >= 0; i--) {
            const auto& a = alerts[i];
            cout << "- [" << a.id << "] Severity: " << a.severity 
                 << " | Type: " << a.type 
                 << " | Source: " << a.source << endl;
        }
    }
    
    int getMinimumSeverityStored() {
        return minHeap.empty() ? 0 : minHeap.top().severity;
    }
};

int main() {
    cout << "=== SISTEM DETEKSI ANOMALI SIBER ===" << endl;
    cout << "Menyimpan 5 alert dengan severity tertinggi\n" << endl;
    
    TopKAlertSystem system(5);
    
    // Simulasi stream alert
    system.processAlert(CyberAlert("ALT001", 45, "192.168.1.100", "Port Scan"));
    system.processAlert(CyberAlert("ALT002", 78, "10.0.0.55", "SQL Injection"));
    system.processAlert(CyberAlert("ALT003", 23, "172.16.0.99", "Failed Login"));
    system.processAlert(CyberAlert("ALT004", 92, "203.0.113.50", "DDoS Attack"));
    system.processAlert(CyberAlert("ALT005", 56, "198.51.100.22", "Malware Detected"));
    system.processAlert(CyberAlert("ALT006", 15, "192.168.1.150", "Info Leak"));
    system.processAlert(CyberAlert("ALT007", 88, "10.0.0.77", "Ransomware"));
    system.processAlert(CyberAlert("ALT008", 35, "172.16.0.50", "Brute Force"));
    system.processAlert(CyberAlert("ALT009", 95, "203.0.113.99", "APT Detected"));
    system.processAlert(CyberAlert("ALT010", 67, "198.51.100.88", "Data Exfil"));
    
    system.displayTopAlerts();
    
    cout << "\nThreshold minimum untuk masuk top 5: " 
         << system.getMinimumSeverityStored() << endl;
    
    return 0;
}
```

**Output:**
```
=== SISTEM DETEKSI ANOMALI SIBER ===
Menyimpan 5 alert dengan severity tertinggi

[STORED] Alert ALT001 (severity 45)
[STORED] Alert ALT002 (severity 78)
[STORED] Alert ALT003 (severity 23)
[STORED] Alert ALT004 (severity 92)
[STORED] Alert ALT005 (severity 56)
[REPLACED] Alert ALT007 (severity 88) replaces ALT003 (severity 23)
[IGNORED] Alert ALT006 (severity 15) - tidak masuk top 5
[IGNORED] Alert ALT008 (severity 35) - tidak masuk top 5
[REPLACED] Alert ALT009 (severity 95) replaces ALT001 (severity 45)
[REPLACED] Alert ALT010 (severity 67) replaces ALT005 (severity 56)

========================================
TOP 5 ALERTS (dari 10 total)
========================================
- [ALT009] Severity: 95 | Type: APT Detected | Source: 203.0.113.99
- [ALT004] Severity: 92 | Type: DDoS Attack | Source: 203.0.113.50
- [ALT007] Severity: 88 | Type: Ransomware | Source: 10.0.0.77
- [ALT002] Severity: 78 | Type: SQL Injection | Source: 10.0.0.55
- [ALT010] Severity: 67 | Type: Data Exfil | Source: 198.51.100.88

Threshold minimum untuk masuk top 5: 67
```

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Soal:** Implementasikan median finder menggunakan dua heap! Median harus dapat dihitung secara efisien setiap ada penambahan data baru.

**Penyelesaian:**

**Konsep:**
- Gunakan max-heap untuk menyimpan setengah elemen yang lebih kecil
- Gunakan min-heap untuk menyimpan setengah elemen yang lebih besar
- Median = top dari max-heap (jika ganjil) atau rata-rata kedua top (jika genap)

```cpp
#include <iostream>
#include <queue>
using namespace std;

class MedianFinder {
private:
    priority_queue<int> maxHeap;  // Elemen lebih kecil (setengah bawah)
    priority_queue<int, vector<int>, greater<int>> minHeap;  // Elemen lebih besar (setengah atas)
    
public:
    void addNum(int num) {
        // Tambahkan ke max-heap terlebih dahulu
        maxHeap.push(num);
        
        // Pindahkan elemen terbesar dari max-heap ke min-heap
        minHeap.push(maxHeap.top());
        maxHeap.pop();
        
        // Balance: max-heap boleh lebih banyak 1 elemen
        if (minHeap.size() > maxHeap.size()) {
            maxHeap.push(minHeap.top());
            minHeap.pop();
        }
    }
    
    double findMedian() {
        if (maxHeap.size() > minHeap.size()) {
            return maxHeap.top();
        } else {
            return (maxHeap.top() + minHeap.top()) / 2.0;
        }
    }
    
    void printState() {
        cout << "Max-heap (bawah): " << maxHeap.size() << " elemen, top = " << maxHeap.top() << endl;
        cout << "Min-heap (atas): " << minHeap.size() << " elemen";
        if (!minHeap.empty()) {
            cout << ", top = " << minHeap.top();
        }
        cout << endl;
    }
};

int main() {
    MedianFinder mf;
    
    cout << "=== MEDIAN FINDER DENGAN DUA HEAP ===" << endl << endl;
    
    vector<int> data = {5, 2, 8, 1, 9, 3, 7};
    
    for (int num : data) {
        mf.addNum(num);
        cout << "Tambah " << num << ":" << endl;
        mf.printState();
        cout << "Median saat ini: " << mf.findMedian() << endl << endl;
    }
    
    return 0;
}
```

**Output:**
```
=== MEDIAN FINDER DENGAN DUA HEAP ===

Tambah 5:
Max-heap (bawah): 1 elemen, top = 5
Min-heap (atas): 0 elemen
Median saat ini: 5

Tambah 2:
Max-heap (bawah): 1 elemen, top = 2
Min-heap (atas): 1 elemen, top = 5
Median saat ini: 3.5

Tambah 8:
Max-heap (bawah): 2 elemen, top = 5
Min-heap (atas): 1 elemen, top = 8
Median saat ini: 5

Tambah 1:
Max-heap (bawah): 2 elemen, top = 2
Min-heap (atas): 2 elemen, top = 5
Median saat ini: 3.5

Tambah 9:
Max-heap (bawah): 3 elemen, top = 5
Min-heap (atas): 2 elemen, top = 8
Median saat ini: 5

Tambah 3:
Max-heap (bawah): 3 elemen, top = 3
Min-heap (atas): 3 elemen, top = 5
Median saat ini: 4

Tambah 7:
Max-heap (bawah): 4 elemen, top = 5
Min-heap (atas): 3 elemen, top = 7
Median saat ini: 5
```

**Kompleksitas:**
- `addNum`: O(log n)
- `findMedian`: O(1)

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Jelaskan bagaimana heap digunakan dalam algoritma Dijkstra untuk shortest path, dan implementasikan contoh sederhana!

**Penyelesaian:**

**Peran heap dalam Dijkstra:**
- Priority queue menyimpan vertex dengan prioritas = jarak terpendek yang diketahui
- Extract-min mendapatkan vertex dengan jarak terpendek untuk diproses berikutnya
- Decrease-key mengupdate jarak ketika path lebih pendek ditemukan

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

typedef pair<int, int> pii;  // pair<jarak, vertex>

class Graph {
private:
    int V;  // Jumlah vertex
    vector<vector<pii>> adj;  // Adjacency list: pair<neighbor, weight>
    
public:
    Graph(int vertices) : V(vertices), adj(vertices) {}
    
    void addEdge(int u, int v, int weight) {
        adj[u].push_back({v, weight});
        adj[v].push_back({u, weight});  // Undirected
    }
    
    vector<int> dijkstra(int source) {
        vector<int> dist(V, INT_MAX);
        dist[source] = 0;
        
        // Min-heap: pair<jarak, vertex>
        priority_queue<pii, vector<pii>, greater<pii>> pq;
        pq.push({0, source});
        
        while (!pq.empty()) {
            int u = pq.top().second;
            int d = pq.top().first;
            pq.pop();
            
            // Skip jika jarak sudah diupdate ke nilai lebih kecil
            if (d > dist[u]) continue;
            
            // Proses semua neighbor
            for (auto& edge : adj[u]) {
                int v = edge.first;
                int weight = edge.second;
                
                // Relaxation
                if (dist[u] + weight < dist[v]) {
                    dist[v] = dist[u] + weight;
                    pq.push({dist[v], v});
                }
            }
        }
        
        return dist;
    }
    
    void printShortestPaths(int source) {
        vector<int> dist = dijkstra(source);
        
        cout << "Jarak terpendek dari vertex " << source << ":" << endl;
        for (int i = 0; i < V; i++) {
            cout << "  ke vertex " << i << ": ";
            if (dist[i] == INT_MAX) {
                cout << "tidak terjangkau" << endl;
            } else {
                cout << dist[i] << endl;
            }
        }
    }
};

int main() {
    cout << "=== DIJKSTRA DENGAN HEAP (PRIORITY QUEUE) ===" << endl << endl;
    
    // Contoh: Jaringan pos pertahanan
    // Vertex: 0=Markas, 1=Pos A, 2=Pos B, 3=Pos C, 4=Pos D
    Graph g(5);
    
    g.addEdge(0, 1, 10);  // Markas - Pos A: 10 km
    g.addEdge(0, 2, 5);   // Markas - Pos B: 5 km
    g.addEdge(1, 2, 2);   // Pos A - Pos B: 2 km
    g.addEdge(1, 3, 1);   // Pos A - Pos C: 1 km
    g.addEdge(2, 1, 3);   // Pos B - Pos A: 3 km
    g.addEdge(2, 3, 9);   // Pos B - Pos C: 9 km
    g.addEdge(2, 4, 2);   // Pos B - Pos D: 2 km
    g.addEdge(3, 4, 4);   // Pos C - Pos D: 4 km
    g.addEdge(4, 3, 6);   // Pos D - Pos C: 6 km
    
    cout << "Graf jaringan pos pertahanan:" << endl;
    cout << "0: Markas Pusat" << endl;
    cout << "1: Pos Alpha" << endl;
    cout << "2: Pos Bravo" << endl;
    cout << "3: Pos Charlie" << endl;
    cout << "4: Pos Delta" << endl << endl;
    
    g.printShortestPaths(0);  // Dari Markas
    
    return 0;
}
```

**Output:**
```
=== DIJKSTRA DENGAN HEAP (PRIORITY QUEUE) ===

Graf jaringan pos pertahanan:
0: Markas Pusat
1: Pos Alpha
2: Pos Bravo
3: Pos Charlie
4: Pos Delta

Jarak terpendek dari vertex 0:
  ke vertex 0: 0
  ke vertex 1: 8
  ke vertex 2: 5
  ke vertex 3: 9
  ke vertex 4: 7
```

**Analisis:**
- Tanpa heap (array): O(V²)
- Dengan binary heap: O((V + E) log V)
- Dengan Fibonacci heap: O(E + V log V)

**Kenapa heap penting?**
- Extract-min dalam O(log V) dibanding O(V) dengan array
- Decrease-key dalam O(log V)
- Sangat efisien untuk graf sparse (E << V²)

---

## Ringkasan

| Konsep | Deskripsi | Kompleksitas |
|--------|-----------|--------------|
| **Heap** | Complete binary tree dengan heap property | - |
| **Max-Heap** | Parent ≥ children, root = maximum | - |
| **Min-Heap** | Parent ≤ children, root = minimum | - |
| **Array Representation** | Parent(i) = (i-1)/2, Left(i) = 2i+1, Right(i) = 2i+2 | - |
| **Insert** | Tambah di akhir + percolate up | O(log n) |
| **Extract** | Ambil root, pindah last ke root + percolate down | O(log n) |
| **Peek** | Lihat root tanpa hapus | O(1) |
| **Build Heap** | Algoritma Floyd (bottom-up heapify) | O(n) |
| **Priority Queue** | ADT dengan akses elemen prioritas tertinggi | Insert/Extract: O(log n) |
| **Heap Sort** | Build heap + extract n kali | O(n log n), in-place |

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan. Jawaban singkat tersedia di bagian akhir.

### Problem S1 ⭐
Bangun min-heap dari array `[7, 2, 9, 4, 1, 5, 3]` menggunakan algoritma Floyd!

### Problem S2 ⭐⭐
Implementasikan fungsi untuk menggabungkan dua max-heap menjadi satu max-heap!

### Problem S3 ⭐⭐
Bagaimana cara mengimplementasikan stack menggunakan priority queue?

### Problem S4 ⭐⭐⭐
Implementasikan k-way merge menggunakan heap! (Menggabungkan k array terurut menjadi satu array terurut)

### Problem S5 ⭐⭐⭐
Jelaskan perbedaan binary heap dengan d-ary heap dan kapan d-ary heap lebih baik!

---

## Jawaban Supplementary Problems

**S1:**
Array: [7, 2, 9, 4, 1, 5, 3]
Setelah build min-heap: [1, 2, 3, 4, 7, 5, 9]

**S2:**
```cpp
vector<int> mergeHeaps(vector<int>& h1, vector<int>& h2) {
    vector<int> merged;
    merged.insert(merged.end(), h1.begin(), h1.end());
    merged.insert(merged.end(), h2.begin(), h2.end());
    // Build heap dari merged array
    buildMaxHeap(merged);
    return merged;
}
```
Kompleksitas: O(n + m)

**S3:**
Gunakan timestamp sebagai prioritas. LIFO = prioritas lebih tinggi untuk elemen terbaru.
```cpp
class StackUsingPQ {
    priority_queue<pair<int, int>> pq;  // pair<timestamp, value>
    int counter = 0;
    void push(int val) { pq.push({counter++, val}); }
    int pop() { int val = pq.top().second; pq.pop(); return val; }
};
```

**S4:**
Gunakan min-heap untuk menyimpan elemen pertama dari setiap array. Extract min, lalu masukkan elemen berikutnya dari array yang sama. Kompleksitas: O(N log k) di mana N = total elemen.

**S5:**
- Binary heap: 2 children per node
- d-ary heap: d children per node
- d-ary lebih baik ketika:
  - Insert lebih sering dari extract (percolate up lebih pendek)
  - d dipilih sesuai cache line size
- Kompleksitas: Insert O(log_d n), Extract O(d log_d n)

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 6.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 6.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 12.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
