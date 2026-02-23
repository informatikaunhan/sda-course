# Latihan Mandiri 13: Heap dan Priority Queue

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 13  
**Topik:** Heap dan Priority Queue  
**Waktu:** 150 menit  
**Sifat:** Open Book

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal dengan teliti
2. Soal pilihan ganda bernilai 2 poin per soal (total 40 poin)
3. Soal uraian bernilai sesuai bobot yang tertera (total 45 poin)
4. Studi kasus bernilai 15 poin (total 15 poin)
5. Total nilai maksimum: 100 poin

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

Pilih jawaban yang paling tepat untuk setiap soal berikut.

### Soal 1
Manakah pernyataan yang **BENAR** tentang Max-Heap?

A. Setiap node memiliki nilai lebih kecil dari parent-nya  
B. Setiap node memiliki nilai lebih besar atau sama dengan anak-anaknya  
C. Elemen terkecil selalu berada di root  
D. Heap harus berupa perfect binary tree  
E. Heap tidak dapat direpresentasikan dengan array  

### Soal 2
Pada representasi array untuk heap, jika parent berada di indeks `i`, di manakah posisi left child?

A. `i - 1`  
B. `i + 1`  
C. `2i`  
D. `2i + 1`  
E. `2i + 2`  

### Soal 3
Perhatikan max-heap berikut dalam representasi array: `[90, 70, 80, 40, 50, 60, 75]`. Berapakah indeks parent dari node dengan nilai 60?

A. 0  
B. 1  
C. 2  
D. 3  
E. 4  

### Soal 4
Berapakah kompleksitas waktu operasi `insert` pada heap dengan n elemen?

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

### Soal 5
Apa yang dilakukan operasi **percolate up** (heapify up)?

A. Menukar node dengan anak terbesarnya berulang kali  
B. Menukar node dengan parent-nya sampai heap property terpenuhi  
C. Menghapus elemen dari heap  
D. Membangun heap dari array  
E. Mengurutkan array  

### Soal 6
Diberikan max-heap `[100, 85, 90, 70, 80, 60, 75]`. Setelah operasi `extractMax()`, manakah yang menjadi root baru?

A. 85  
B. 90  
C. 80  
D. 75  
E. 70  

### Soal 7
Berapakah kompleksitas waktu untuk membangun heap dari array n elemen menggunakan algoritma Floyd (bottom-up)?

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

### Soal 8
Manakah yang **BUKAN** merupakan operasi dasar pada ADT Priority Queue?

A. insert(element, priority)  
B. extractMax() / extractMin()  
C. peek()  
D. sort()  
E. isEmpty()  

### Soal 9
Pada min-heap, operasi mana yang memiliki kompleksitas O(1)?

A. insert  
B. extractMin  
C. getMin  
D. buildHeap  
E. heapify  

### Soal 10
Perhatikan operasi insert pada max-heap `[80, 60, 70, 40, 50]`. Jika kita insert nilai 85, berapa kali pertukaran yang terjadi pada percolate up?

A. 0  
B. 1  
C. 2  
D. 3  
E. 4  

### Soal 11
Dalam heap sort, setelah fase build heap, apa langkah selanjutnya?

A. Lakukan percolate up pada semua elemen  
B. Tukar root dengan elemen terakhir, kurangi ukuran heap, heapify root  
C. Insert semua elemen ke heap baru  
D. Traverse heap secara level-order  
E. Hapus semua leaf nodes  

### Soal 12
Berapakah kompleksitas waktu heap sort?

A. O(n)  
B. O(log n)  
C. O(n log n)  
D. O(n²)  
E. O(2ⁿ)  

### Soal 13
Jika sebuah complete binary tree memiliki 15 node, berapakah tinggi (height) dari tree tersebut?

A. 2  
B. 3  
C. 4  
D. 5  
E. 7  

### Soal 14
Manakah pernyataan yang **SALAH** tentang heap?

A. Heap adalah complete binary tree  
B. Max-heap memiliki elemen terbesar di root  
C. Heap dapat diimplementasikan dengan array secara efisien  
D. Semua leaf nodes berada di level terakhir atau kedua terakhir  
E. Heap selalu merupakan binary search tree  

### Soal 15
Pada operasi `extractMax` dari max-heap, mengapa kita menukar root dengan elemen terakhir terlebih dahulu?

A. Untuk menjaga complete binary tree property  
B. Untuk mempercepat proses heapify  
C. Untuk mengurangi jumlah pertukaran  
D. Untuk memudahkan pencarian  
E. Tidak ada alasan khusus  

### Soal 16
Diberikan array `[4, 10, 3, 5, 1]`. Setelah proses build max-heap, manakah yang menjadi representasi array yang valid?

A. `[1, 3, 4, 5, 10]`  
B. `[10, 5, 3, 4, 1]`  
C. `[10, 5, 4, 3, 1]`  
D. `[3, 4, 5, 10, 1]`  
E. `[4, 5, 10, 3, 1]`  

### Soal 17
Dalam konteks priority queue, kapan sebaiknya menggunakan min-heap daripada max-heap?

A. Ketika elemen dengan nilai terbesar harus diproses terlebih dahulu  
B. Ketika elemen dengan prioritas terendah (nilai terkecil) harus diproses terlebih dahulu  
C. Ketika semua elemen memiliki prioritas yang sama  
D. Ketika jumlah elemen sangat besar  
E. Ketika heap harus diurutkan  

### Soal 18
Perhatikan proses heapify down pada max-heap. Jika node yang di-heapify memiliki dua anak, node mana yang dipilih untuk pertukaran?

A. Selalu anak kiri  
B. Selalu anak kanan  
C. Anak dengan nilai lebih besar  
D. Anak dengan nilai lebih kecil  
E. Dipilih secara random  

### Soal 19
Berapakah kompleksitas ruang (space complexity) dari heap sort?

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

### Soal 20
Manakah aplikasi yang paling tepat menggunakan priority queue?

A. Menyimpan data terurut  
B. Implementasi undo/redo  
C. Algoritma Dijkstra untuk shortest path  
D. Menyimpan pasangan key-value  
E. Implementasi rekursi  

---

## Bagian B: Soal Uraian (8 Soal)

### Soal 1 (5 poin) — Mudah
Jelaskan perbedaan antara Max-Heap dan Min-Heap! Sertakan contoh representasi array untuk masing-masing dengan 5 elemen.

### Soal 2 (5 poin) — Mudah
Diberikan max-heap dalam representasi array: `[95, 80, 75, 50, 60, 40, 70]`

a) Gambarkan heap tersebut dalam bentuk tree  
b) Tentukan parent, left child, dan right child dari node dengan nilai 80  
c) Tentukan semua leaf nodes  

### Soal 3 (5 poin) — Mudah
Jelaskan langkah-langkah operasi `insert(85)` pada max-heap `[80, 70, 60, 50, 40]`! Tunjukkan setiap langkah percolate up yang terjadi.

### Soal 4 (6 poin) — Sedang
Diberikan max-heap `[100, 90, 80, 70, 85, 60, 75, 50, 40]`. Tunjukkan langkah-langkah operasi `extractMax()` secara detail, termasuk proses heapify down!

### Soal 5 (6 poin) — Sedang
Tuliskan fungsi C++ `void heapifyDown(int arr[], int n, int i)` untuk max-heap yang melakukan operasi percolate down pada indeks i!

### Soal 6 (6 poin) — Sedang
Jelaskan mengapa algoritma build heap Floyd memiliki kompleksitas O(n), bukan O(n log n)! Gunakan analisis matematis sederhana.

### Soal 7 (6 poin) — Sulit
Implementasikan class `MinPriorityQueue` dalam C++ dengan operasi:
- `insert(int priority, string data)`
- `extractMin()` yang mengembalikan data dengan prioritas terendah
- `peek()` untuk melihat elemen dengan prioritas terendah

### Soal 8 (6 poin) — Sulit
Diberikan array `[3, 1, 4, 1, 5, 9, 2, 6]`. Tunjukkan langkah-langkah heap sort untuk mengurutkan array tersebut secara ascending! Tunjukkan kondisi array setelah setiap extractMax.

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Prioritas Alert Keamanan Siber (7 poin)

**Latar Belakang:**
Pusat Operasi Keamanan Siber (Security Operations Center/SOC) memerlukan sistem untuk mengelola alert keamanan berdasarkan tingkat keparahan. Alert dengan severity tinggi harus ditangani terlebih dahulu. Setiap alert memiliki atribut: ID, timestamp, severity (1-10, dimana 10 paling parah), sumber (IP address), dan deskripsi.

**Data Contoh Alert:**
```
Alert-001: severity=7, source="192.168.1.100", desc="Brute force attempt"
Alert-002: severity=9, source="10.0.0.50", desc="Malware detected"
Alert-003: severity=5, source="172.16.0.25", desc="Failed login"
Alert-004: severity=10, source="192.168.1.200", desc="Data exfiltration"
Alert-005: severity=8, source="10.0.0.75", desc="Suspicious traffic"
```

**Tugas:**

a) **(2 poin)** Rancang struktur data `Alert` yang tepat dan jelaskan mengapa max-heap cocok untuk kasus ini!

b) **(2 poin)** Gambarkan max-heap yang terbentuk setelah semua alert di atas dimasukkan (berdasarkan severity sebagai prioritas)!

c) **(3 poin)** Implementasikan fungsi `Alert getNextAlert(MaxHeap& alertQueue)` yang mengambil alert dengan prioritas tertinggi dan jelaskan kompleksitasnya!

---

### Studi Kasus 2: Sistem Antrian Evakuasi Medis (8 poin)

**Latar Belakang:**
Rumah Sakit Lapangan Militer memerlukan sistem triase untuk menentukan urutan evakuasi pasien. Pasien dengan kondisi paling kritis (prioritas terendah secara numerik, misal 1 = paling kritis) harus dievakuasi terlebih dahulu. Sistem harus mendukung penambahan pasien baru, evakuasi pasien paling kritis, dan update kondisi pasien.

**Skenario:**
- Awalnya ada 5 pasien dengan prioritas: [3, 1, 4, 2, 5]
- Pasien paling kritis (prioritas 1) dievakuasi
- 2 pasien baru datang dengan prioritas 2 dan 6
- Kondisi pasien dengan prioritas 4 memburuk menjadi prioritas 1

**Tugas:**

a) **(2 poin)** Jelaskan mengapa min-heap lebih cocok daripada max-heap untuk sistem triase ini!

b) **(3 poin)** Gambarkan kondisi min-heap setelah setiap langkah dalam skenario di atas!

c) **(3 poin)** Implementasikan fungsi `void updatePriority(MinHeap& heap, int patientId, int newPriority)` untuk mengubah prioritas pasien! Jelaskan kapan perlu percolate up vs percolate down.

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | B | Max-heap: setiap node ≥ anak-anaknya |
| 2 | D | Left child di indeks 2i + 1 (0-indexed) |
| 3 | C | Node 60 di indeks 5, parent = (5-1)/2 = 2 |
| 4 | B | Insert heap: O(log n) untuk percolate up |
| 5 | B | Percolate up menukar dengan parent hingga valid |
| 6 | B | Setelah extractMax, heapify menghasilkan 90 sebagai root |
| 7 | C | Floyd's build heap: O(n) |
| 8 | D | sort() bukan operasi dasar priority queue |
| 9 | C | getMin() pada min-heap: O(1), langsung akses root |
| 10 | C | 85 naik dari indeks 5 → 2 → 0 (2 pertukaran) |
| 11 | B | Heap sort: tukar root-last, kurangi size, heapify |
| 12 | C | Heap sort: O(n log n) |
| 13 | B | 15 node → height = ⌊log₂(15)⌋ = 3 |
| 14 | E | Heap BUKAN BST, tidak ada urutan left < parent < right |
| 15 | A | Menjaga complete binary tree property |
| 16 | B | Valid max-heap: [10, 5, 3, 4, 1] |
| 17 | B | Min-heap untuk prioritas terendah diproses dahulu |
| 18 | C | Pilih anak dengan nilai lebih besar untuk max-heap |
| 19 | A | Heap sort in-place: O(1) extra space |
| 20 | C | Dijkstra menggunakan priority queue untuk vertex terdekat |

---

### Bagian B: Soal Uraian

#### Jawaban Soal 1

**Perbedaan Max-Heap dan Min-Heap:**

| Aspek | Max-Heap | Min-Heap |
|-------|----------|----------|
| Heap Property | Parent ≥ anak-anak | Parent ≤ anak-anak |
| Root | Elemen terbesar | Elemen terkecil |
| Operasi utama | extractMax() | extractMin() |
| Penggunaan | Mencari maksimum | Mencari minimum |

**Contoh Max-Heap (5 elemen):**
```
Array: [90, 70, 80, 40, 50]

        90
       /  \
      70   80
     /  \
    40   50
```

**Contoh Min-Heap (5 elemen):**
```
Array: [10, 20, 30, 40, 50]

        10
       /  \
      20   30
     /  \
    40   50
```

---

#### Jawaban Soal 2

**a) Representasi Tree:**
```
Array: [95, 80, 75, 50, 60, 40, 70]
Index:   0   1   2   3   4   5   6

            95 (0)
           /    \
        80 (1)   75 (2)
        /  \     /   \
    50(3) 60(4) 40(5) 70(6)
```

**b) Untuk node 80 (indeks 1):**
- Parent: indeks (1-1)/2 = 0 → nilai **95**
- Left child: indeks 2×1+1 = 3 → nilai **50**
- Right child: indeks 2×1+2 = 4 → nilai **60**

**c) Leaf nodes:**
- Node dengan indeks 3, 4, 5, 6
- Nilai: **50, 60, 40, 70**
- (Semua node yang tidak memiliki anak, yaitu i ≥ n/2)

---

#### Jawaban Soal 3

**Insert(85) pada max-heap `[80, 70, 60, 50, 40]`:**

**Langkah 1:** Tambahkan 85 di posisi terakhir
```
Array: [80, 70, 60, 50, 40, 85]
Index:   0   1   2   3   4   5

        80
       /  \
      70   60
     /  \  /
    50  40 85  ← elemen baru
```

**Langkah 2:** Percolate Up - Bandingkan 85 dengan parent (indeks (5-1)/2 = 2, nilai 60)
- 85 > 60, tukar!
```
Array: [80, 70, 85, 50, 40, 60]

        80
       /  \
      70   85  ← naik
     /  \  /
    50  40 60
```

**Langkah 3:** Percolate Up - Bandingkan 85 dengan parent (indeks (2-1)/2 = 0, nilai 80)
- 85 > 80, tukar!
```
Array: [85, 70, 80, 50, 40, 60]

        85  ← sekarang jadi root
       /  \
      70   80
     /  \  /
    50  40 60
```

**Langkah 4:** 85 sudah di root, selesai.

**Total pertukaran:** 2 kali

---

#### Jawaban Soal 4

**ExtractMax() pada `[100, 90, 80, 70, 85, 60, 75, 50, 40]`:**

**Kondisi Awal:**
```
           100
          /    \
        90      80
       /  \    /  \
      70   85 60   75
     /  \
    50   40
```

**Langkah 1:** Simpan nilai root (100) untuk dikembalikan

**Langkah 2:** Pindahkan elemen terakhir (40) ke root
```
Array: [40, 90, 80, 70, 85, 60, 75, 50]
Size: 8 (berkurang 1)

           40  ← dari posisi terakhir
          /    \
        90      80
       /  \    /  \
      70   85 60   75
     /
    50
```

**Langkah 3:** Heapify Down dari root
- Compare 40 dengan anak: left=90, right=80
- Anak terbesar: 90 > 40, tukar!
```
Array: [90, 40, 80, 70, 85, 60, 75, 50]

           90
          /    \
        40      80
       /  \    /  \
      70   85 60   75
     /
    50
```

**Langkah 4:** Continue heapify down pada indeks 1
- Compare 40 dengan anak: left=70, right=85
- Anak terbesar: 85 > 40, tukar!
```
Array: [90, 85, 80, 70, 40, 60, 75, 50]

           90
          /    \
        85      80
       /  \    /  \
      70   40 60   75
     /
    50
```

**Langkah 5:** Continue heapify down pada indeks 4
- Node 40 tidak punya anak (leaf), selesai

**Hasil akhir:** `[90, 85, 80, 70, 40, 60, 75, 50]`
**Nilai yang dikembalikan:** 100

---

#### Jawaban Soal 5

```cpp
void heapifyDown(int arr[], int n, int i) {
    int largest = i;        // Asumsikan root subtree adalah terbesar
    int left = 2 * i + 1;   // Indeks left child
    int right = 2 * i + 2;  // Indeks right child
    
    // Cek apakah left child lebih besar dari root
    if (left < n && arr[left] > arr[largest]) {
        largest = left;
    }
    
    // Cek apakah right child lebih besar dari largest sejauh ini
    if (right < n && arr[right] > arr[largest]) {
        largest = right;
    }
    
    // Jika largest bukan root, tukar dan lanjut heapify
    if (largest != i) {
        // Tukar
        int temp = arr[i];
        arr[i] = arr[largest];
        arr[largest] = temp;
        
        // Rekursif heapify subtree yang terpengaruh
        heapifyDown(arr, n, largest);
    }
}
```

**Penjelasan:**
1. Bandingkan node dengan kedua anaknya
2. Tentukan yang terbesar di antara ketiganya
3. Jika node bukan yang terbesar, tukar dengan anak terbesar
4. Rekursif pada posisi baru hingga heap property terpenuhi

---

#### Jawaban Soal 6

**Mengapa Build Heap Floyd = O(n):**

**Analisis:**

Floyd's algorithm melakukan heapify dari node non-leaf dari bawah ke atas. Key insight: node di level berbeda membutuhkan jumlah operasi berbeda.

**Distribusi node per level (untuk heap dengan n node):**
- Level h (leaf): ~n/2 node, heapify 0 langkah
- Level h-1: ~n/4 node, heapify maksimal 1 langkah
- Level h-2: ~n/8 node, heapify maksimal 2 langkah
- ...
- Level 0 (root): 1 node, heapify maksimal h langkah

**Total operasi:**
```
T(n) = Σ (jumlah node di level k) × (tinggi subtree di level k)
     = n/4 × 1 + n/8 × 2 + n/16 × 3 + ... + 1 × log(n)
     = n × Σ(k/2^(k+1)) untuk k = 1 hingga log(n)
```

**Deret konvergen:**
```
Σ(k/2^(k+1)) = 1/4 + 2/8 + 3/16 + ... ≤ 2
```

**Kesimpulan:**
```
T(n) ≤ n × 2 = O(n)
```

**Intuisi:** Sebagian besar node (leaf nodes, sekitar n/2) tidak perlu heapify sama sekali. Hanya sedikit node di dekat root yang perlu heapify panjang, tapi jumlah node tersebut sedikit.

---

#### Jawaban Soal 7

```cpp
#include <iostream>
#include <string>
#include <vector>
using namespace std;

struct PQElement {
    int priority;
    string data;
};

class MinPriorityQueue {
private:
    vector<PQElement> heap;
    
    void percolateUp(int idx) {
        while (idx > 0) {
            int parent = (idx - 1) / 2;
            if (heap[idx].priority < heap[parent].priority) {
                swap(heap[idx], heap[parent]);
                idx = parent;
            } else {
                break;
            }
        }
    }
    
    void percolateDown(int idx) {
        int n = heap.size();
        while (true) {
            int smallest = idx;
            int left = 2 * idx + 1;
            int right = 2 * idx + 2;
            
            if (left < n && heap[left].priority < heap[smallest].priority) {
                smallest = left;
            }
            if (right < n && heap[right].priority < heap[smallest].priority) {
                smallest = right;
            }
            
            if (smallest != idx) {
                swap(heap[idx], heap[smallest]);
                idx = smallest;
            } else {
                break;
            }
        }
    }
    
public:
    void insert(int priority, string data) {
        PQElement elem = {priority, data};
        heap.push_back(elem);
        percolateUp(heap.size() - 1);
    }
    
    string extractMin() {
        if (heap.empty()) {
            throw runtime_error("Priority queue kosong!");
        }
        
        string minData = heap[0].data;
        heap[0] = heap.back();
        heap.pop_back();
        
        if (!heap.empty()) {
            percolateDown(0);
        }
        
        return minData;
    }
    
    string peek() {
        if (heap.empty()) {
            throw runtime_error("Priority queue kosong!");
        }
        return heap[0].data;
    }
    
    bool isEmpty() {
        return heap.empty();
    }
};
```

**Kompleksitas:**
- `insert`: O(log n)
- `extractMin`: O(log n)
- `peek`: O(1)

---

#### Jawaban Soal 8

**Heap Sort pada `[3, 1, 4, 1, 5, 9, 2, 6]`:**

**Fase 1: Build Max-Heap**

Array awal: `[3, 1, 4, 1, 5, 9, 2, 6]`

Heapify dari indeks n/2-1 = 3 ke 0:

```
Heapify(3): [3, 1, 4, 6, 5, 9, 2, 1]  (swap 1↔6)
Heapify(2): [3, 1, 9, 6, 5, 4, 2, 1]  (swap 4↔9)
Heapify(1): [3, 6, 9, 1, 5, 4, 2, 1]  (swap 1↔6)
Heapify(0): [9, 6, 4, 1, 5, 3, 2, 1]  (9 turun ke root)
```

Max-heap: `[9, 6, 4, 1, 5, 3, 2, 1]`

**Fase 2: Extract & Sort**

| Langkah | Tukar | Heapify | Array Hasil |
|---------|-------|---------|-------------|
| 1 | 9↔1 | heapify(0) | `[6, 5, 4, 1, 1, 3, 2, |9]` |
| 2 | 6↔2 | heapify(0) | `[5, 2, 4, 1, 1, 3, |6, 9]` |
| 3 | 5↔3 | heapify(0) | `[4, 2, 3, 1, 1, |5, 6, 9]` |
| 4 | 4↔1 | heapify(0) | `[3, 2, 1, 1, |4, 5, 6, 9]` |
| 5 | 3↔1 | heapify(0) | `[2, 1, 1, |3, 4, 5, 6, 9]` |
| 6 | 2↔1 | heapify(0) | `[1, 1, |2, 3, 4, 5, 6, 9]` |
| 7 | 1↔1 | - | `[1, |1, 2, 3, 4, 5, 6, 9]` |

**Hasil akhir (ascending):** `[1, 1, 2, 3, 4, 5, 6, 9]`

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Prioritas Alert Keamanan Siber

**a) Struktur Data dan Justifikasi:**

```cpp
struct Alert {
    string id;
    long timestamp;
    int severity;        // 1-10, key untuk heap
    string sourceIP;
    string description;
    
    // Operator untuk perbandingan berdasarkan severity
    bool operator<(const Alert& other) const {
        return severity < other.severity;
    }
};
```

**Mengapa Max-Heap cocok:**
1. Alert dengan severity tertinggi (10) harus diproses pertama
2. extractMax() memberikan akses O(log n) ke alert paling urgent
3. Insert alert baru juga O(log n), cocok untuk high-throughput environment
4. Tidak perlu sorting ulang setiap ada alert baru

**b) Max-Heap setelah insert semua alert:**

Insert order: Alert-001(7), Alert-002(9), Alert-003(5), Alert-004(10), Alert-005(8)

```
Step 1: [7]
Step 2: [9, 7]
Step 3: [9, 7, 5]
Step 4: [10, 9, 5, 7]
Step 5: [10, 9, 5, 7, 8]

Final Max-Heap (by severity):
           10 (Alert-004)
          /        \
     9 (Alert-002)  5 (Alert-003)
        /    \
 7(Alert-001) 8(Alert-005)

Array: [10, 9, 5, 7, 8]
```

**c) Implementasi getNextAlert:**

```cpp
Alert getNextAlert(MaxHeap<Alert>& alertQueue) {
    if (alertQueue.isEmpty()) {
        throw runtime_error("Tidak ada alert dalam antrian!");
    }
    
    // Extract alert dengan severity tertinggi
    Alert highestPriority = alertQueue.extractMax();
    
    // Log untuk audit trail
    cout << "[SOC] Processing alert: " << highestPriority.id 
         << " | Severity: " << highestPriority.severity 
         << " | Source: " << highestPriority.sourceIP << endl;
    
    return highestPriority;
}
```

**Kompleksitas:**
- **Time:** O(log n) karena extractMax memerlukan heapify down
- **Space:** O(1) additional space
- **Justifikasi:** Dalam SOC dengan ribuan alert, O(log n) sangat efisien dibanding O(n) untuk linear search

---

#### Studi Kasus 2: Sistem Antrian Evakuasi Medis

**a) Mengapa Min-Heap lebih cocok:**

1. **Logika Triase:** Prioritas 1 = paling kritis, harus dievakuasi pertama
2. **Min-Heap Property:** Root adalah elemen dengan nilai terkecil → prioritas terendah = paling urgent
3. **Operasi extractMin():** Langsung mendapat pasien paling kritis dalam O(log n)
4. **Intuitif:** Dalam triase medis, angka kecil = kondisi lebih serius

Jika menggunakan max-heap, kita harus membalik nilai prioritas (misal: 10-prioritas), yang membingungkan dan rawan error.

**b) Kondisi Min-Heap setelah setiap langkah:**

**Kondisi Awal:** Insert [3, 1, 4, 2, 5]
```
Build min-heap: [1, 2, 4, 3, 5]

        1
       / \
      2   4
     / \
    3   5
```

**Setelah extractMin (pasien prioritas 1):**
```
[2, 3, 4, 5]

        2
       / \
      3   4
     /
    5
```

**Setelah insert prioritas 2 dan 6:**
```
Insert 2: [2, 2, 4, 5, 3]
Insert 6: [2, 2, 4, 5, 3, 6]

        2
       / \
      2   4
     /\   /
    5  3 6
```

**Setelah update prioritas 4→1:**
Cari node dengan prioritas 4, ubah ke 1, percolate up:
```
[1, 2, 2, 5, 3, 6]

        1  ← naik dari posisi 4
       / \
      2   2
     /\   /
    5  3 6
```

**c) Implementasi updatePriority:**

```cpp
void updatePriority(MinHeap& heap, int patientId, int newPriority) {
    // Cari indeks pasien (dalam implementasi real, gunakan hash map)
    int idx = -1;
    for (int i = 0; i < heap.size(); i++) {
        if (heap.getPatientId(i) == patientId) {
            idx = i;
            break;
        }
    }
    
    if (idx == -1) {
        throw runtime_error("Pasien tidak ditemukan!");
    }
    
    int oldPriority = heap.getPriority(idx);
    heap.setPriority(idx, newPriority);
    
    if (newPriority < oldPriority) {
        // Prioritas menurun (lebih urgent) → percolate UP
        // Karena min-heap, nilai kecil harus naik ke atas
        heap.percolateUp(idx);
    } else if (newPriority > oldPriority) {
        // Prioritas meningkat (kurang urgent) → percolate DOWN
        // Nilai besar harus turun ke bawah
        heap.percolateDown(idx);
    }
    // Jika sama, tidak perlu perubahan
}
```

**Kapan Percolate Up vs Down:**

| Kondisi | Aksi | Alasan |
|---------|------|--------|
| newPriority < oldPriority | Percolate UP | Pasien lebih kritis, perlu "naik" ke depan antrian |
| newPriority > oldPriority | Percolate DOWN | Pasien membaik, perlu "turun" dalam prioritas |
| newPriority = oldPriority | Tidak ada | Tidak ada perubahan posisi |

**Kompleksitas:** O(n) untuk search + O(log n) untuk percolate = O(n)
**Optimasi:** Gunakan hash map untuk tracking posisi → O(log n) total

---

## Kriteria Penilaian

| Bagian | Jumlah Soal | Poin per Soal | Total |
|--------|-------------|---------------|-------|
| Pilihan Ganda | 20 | 2 | 40 |
| Uraian | 8 | Bervariasi (5-6) | 45 |
| Studi Kasus | 2 | 7 + 8 | 15 |
| **Total** | | | **100** |

---

## Catatan untuk Pengajar

- Soal mencakup Sub-CPMK-5.3 (Heap dan Priority Queue) dan Sub-CPMK-4.2 (Heap Sort)
- Studi kasus menggunakan konteks pertahanan dan keamanan Indonesia
- Tingkat kesulitan bervariasi dari mudah hingga sulit
- Soal pilihan ganda menguji pemahaman konsep dasar
- Soal uraian menguji kemampuan implementasi dan analisis
- Studi kasus menguji kemampuan aplikasi dalam konteks nyata

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
