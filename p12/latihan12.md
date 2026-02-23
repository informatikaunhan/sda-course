# Latihan Mandiri 12: Binary Search Tree (BST)

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 12  
**Topik:** Binary Search Tree (BST)  
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
Manakah properti yang **HARUS** dipenuhi oleh Binary Search Tree?

A. Setiap node memiliki tepat dua anak  
B. Nilai di subtree kiri < nilai node < nilai di subtree kanan  
C. Tree harus berbentuk complete binary tree  
D. Semua leaf berada pada level yang sama  
E. Setiap node harus memiliki minimal satu anak  

### Soal 2
Perhatikan BST berikut:
```
        50
       /  \
      30   70
     / \   / \
    20 40 60 80
```
Apa hasil traversal **inorder** dari BST di atas?

A. 50, 30, 20, 40, 70, 60, 80  
B. 20, 30, 40, 50, 60, 70, 80  
C. 20, 40, 30, 60, 80, 70, 50  
D. 50, 30, 70, 20, 40, 60, 80  
E. 80, 70, 60, 50, 40, 30, 20  

### Soal 3
Berapakah kompleksitas waktu **worst case** untuk operasi search pada BST?

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

### Soal 4
Pada BST dengan n node, kapan kompleksitas search mencapai O(n)?

A. Ketika mencari node root  
B. Ketika BST berbentuk skewed (miring)  
C. Ketika BST berbentuk complete  
D. Ketika mencari nilai minimum  
E. Ketika BST memiliki height = log n  

### Soal 5
Perhatikan BST berikut:
```
        40
       /  \
      20   60
       \   /
       25 50
```
Node manakah yang menjadi inorder successor dari 40?

A. 20  
B. 25  
C. 50  
D. 60  
E. Tidak ada  

### Soal 6
Jika kita melakukan insert urutan: 5, 3, 7, 2, 4, 6, 8 ke BST kosong, berapakah height dari BST yang terbentuk?

A. 1  
B. 2  
C. 3  
D. 4  
E. 7  

### Soal 7
Manakah pernyataan yang **BENAR** tentang operasi findMin pada BST?

A. Selalu berada di node paling kanan  
B. Selalu berada di node paling kiri  
C. Selalu berada di root  
D. Memerlukan traversal seluruh tree  
E. Memiliki kompleksitas O(n) selalu  

### Soal 8
Ketika menghapus node dengan **dua anak** dari BST, node tersebut diganti dengan:

A. Anak kiri  
B. Anak kanan  
C. Inorder predecessor atau inorder successor  
D. Node root  
E. Node leaf terdekat  

### Soal 9
Perhatikan BST berikut:
```
        30
       /  \
      15   45
     / \   / \
    10 20 35 50
```
Setelah menghapus node 30, BST yang valid adalah:

A. Root menjadi 35, sisanya tetap  
B. Root menjadi 20, sisanya tetap  
C. Root menjadi 35 dengan 20 di kiri  
D. Root menjadi 15 dengan 45 di kanan  
E. Semua node harus di-rebalance  

### Soal 10
Apa keuntungan utama BST dibanding array terurut untuk operasi insert?

A. BST memiliki kompleksitas search yang lebih baik  
B. BST tidak memerlukan memori tambahan  
C. BST tidak perlu menggeser elemen saat insert  
D. BST selalu balanced  
E. BST menggunakan memori lebih sedikit  

### Soal 11
Perhatikan kode berikut:
```cpp
Node* search(Node* root, int key) {
    if (root == nullptr || root->data == key)
        return root;
    if (key < root->data)
        return search(root->left, key);
    return search(root->right, key);
}
```
Berapa kali fungsi search dipanggil untuk mencari nilai 25 pada BST:
```
        50
       /  \
      30   70
     /
    25
```

A. 1  
B. 2  
C. 3  
D. 4  
E. 5  

### Soal 12
Manakah urutan insert yang menghasilkan BST **paling seimbang**?

A. 1, 2, 3, 4, 5, 6, 7  
B. 7, 6, 5, 4, 3, 2, 1  
C. 4, 2, 6, 1, 3, 5, 7  
D. 1, 7, 2, 6, 3, 5, 4  
E. 4, 1, 7, 2, 6, 3, 5  

### Soal 13
Apa yang terjadi jika kita insert nilai duplikat ke BST standar?

A. BST otomatis menolak duplikat  
B. Nilai duplikat masuk ke subtree kiri  
C. Nilai duplikat masuk ke subtree kanan  
D. Tergantung implementasi (biasanya kiri atau kanan)  
E. BST menjadi tidak valid  

### Soal 14
Perhatikan BST berikut:
```
        100
       /
      50
     /
    25
   /
  10
```
BST ini disebut:

A. Complete binary tree  
B. Perfect binary tree  
C. Left-skewed tree  
D. Full binary tree  
E. Balanced tree  

### Soal 15
Berapakah kompleksitas waktu untuk operasi findMax pada BST dengan height h?

A. O(1)  
B. O(h)  
C. O(n)  
D. O(log n)  
E. O(n log n)  

### Soal 16
Manakah yang merupakan balanced BST?

A. Splay Tree  
B. AVL Tree  
C. Red-Black Tree  
D. B dan C benar  
E. A, B, dan C benar  

### Soal 17
Perhatikan operasi delete pada BST. Jika node yang dihapus adalah **leaf node**, maka:

A. Perlu mencari inorder successor  
B. Perlu mencari inorder predecessor  
C. Langsung hapus node tersebut  
D. Perlu menyeimbangkan tree  
E. Tidak bisa dihapus  

### Soal 18
Pada BST yang seimbang dengan n node, berapakah perkiraan height tree?

A. n  
B. n/2  
C. log₂ n  
D. 2^n  
E. n²  

### Soal 19
Perhatikan BST berikut dan lakukan delete node 20:
```
        30
       /  \
      20   40
     /  \
    10  25
```
Bagaimana struktur setelah delete (menggunakan inorder successor)?

A. Node 25 menggantikan 20  
B. Node 10 menggantikan 20  
C. Node 30 menjadi parent langsung dari 10 dan 25  
D. A benar, dengan 10 menjadi anak kiri dari 25  
E. BST menjadi tidak valid  

### Soal 20
Manakah aplikasi yang PALING COCOK menggunakan BST?

A. Implementasi stack  
B. Implementasi queue  
C. Database indexing untuk range query  
D. Representasi graph  
E. Penyimpanan data sequential  

---

## Bagian B: Soal Uraian (8 Soal)

### Soal 1 (5 poin) ⭐
Jelaskan properti Binary Search Tree dan mengapa properti ini membuat operasi search menjadi efisien!

### Soal 2 (5 poin) ⭐
Gambarkan BST yang terbentuk jika kita insert nilai-nilai berikut secara berurutan: 45, 25, 65, 15, 35, 55, 75. Tunjukkan step-by-step proses pembentukan!

### Soal 3 (5 poin) ⭐
Jelaskan perbedaan antara inorder predecessor dan inorder successor! Kapan masing-masing digunakan dalam operasi delete?

### Soal 4 (6 poin) ⭐⭐
Perhatikan BST berikut:
```
        50
       /  \
      25   75
     / \   / \
    10 30 60 90
      \     \
      35    85
```
a. Tentukan inorder predecessor dari node 50  
b. Tentukan inorder successor dari node 50  
c. Jika node 50 dihapus menggunakan inorder successor, gambarkan BST hasilnya!

### Soal 5 (6 poin) ⭐⭐
Implementasikan fungsi `int countNodes(Node* root)` yang menghitung jumlah total node dalam BST secara rekursif!

### Soal 6 (6 poin) ⭐⭐
Implementasikan fungsi `bool isBST(Node* root, int min, int max)` yang memvalidasi apakah suatu binary tree memenuhi properti BST!

### Soal 7 (6 poin) ⭐⭐
Jelaskan tiga kasus dalam operasi delete pada BST lengkap dengan kompleksitas waktu masing-masing kasus!

### Soal 8 (6 poin) ⭐⭐⭐
Bandingkan BST dengan array terurut dan hash table untuk operasi search, insert, dan delete! Kapan BST menjadi pilihan yang lebih baik?

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Manajemen Inventaris Alutsista (7 poin)

**Latar Belakang:**
Pusat logistik pertahanan memerlukan sistem untuk mengelola inventaris alutsista (alat utama sistem senjata). Setiap item memiliki ID unik berbentuk numerik yang mencerminkan kategori dan nomor urut. Sistem harus mendukung:
- Pencarian cepat berdasarkan ID
- Penambahan item baru
- Penghapusan item yang sudah tidak operasional
- Pencarian range (misal: semua item dengan ID 1000-2000)

**Data Contoh:**
| ID | Nama Item | Kategori |
|----|-----------|----------|
| 1500 | Senapan Serbu SS2 | Senjata Ringan |
| 2300 | Tank Leopard 2A4 | Kendaraan Tempur |
| 1200 | Pistol Pindad G2 | Senjata Genggam |
| 3100 | Radar WEIBEL | Peralatan Deteksi |
| 1800 | Mortir 81mm | Senjata Berat |

**Tugas:**
a. **(2 poin)** Gambarkan BST yang terbentuk jika item di-insert sesuai urutan dalam tabel!

b. **(2 poin)** Jelaskan bagaimana melakukan range query untuk mendapatkan semua item dengan ID antara 1200-2000!

c. **(3 poin)** Implementasikan fungsi `void rangeSearch(Node* root, int low, int high)` yang mencetak semua item dalam range tertentu!

---

### Studi Kasus 2: Sistem Prioritas Target Radar (8 poin)

**Latar Belakang:**
Sistem pertahanan udara menggunakan radar untuk mendeteksi objek yang masuk ke wilayah udara. Setiap objek terdeteksi diberi skor ancaman berdasarkan kecepatan, jarak, dan trajectory. Sistem perlu dengan cepat:
- Menemukan objek dengan skor ancaman tertentu
- Menambahkan objek baru yang terdeteksi
- Menghapus objek yang sudah keluar dari jangkauan
- Menemukan objek dengan skor ancaman tertinggi/terendah

**Tugas:**
a. **(2 poin)** Rancang struktur node BST yang menyimpan data objek radar (minimal: ID, skor ancaman, jenis objek, posisi)!

b. **(3 poin)** Implementasikan fungsi `Node* findMaxThreat(Node* root)` untuk menemukan objek dengan skor ancaman tertinggi!

c. **(3 poin)** Jelaskan mengapa BST cocok untuk sistem ini dan apa kelemahannya! Sarankan perbaikan jika waktu respons harus dijamin konstan!

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | B | Properti dasar BST: left < node < right |
| 2 | B | Inorder BST menghasilkan urutan terurut |
| 3 | C | Worst case saat tree skewed (seperti linked list) |
| 4 | B | Skewed tree memiliki height = n |
| 5 | C | Inorder successor = nilai terkecil di subtree kanan |
| 6 | B | Insert 5, lalu 3 & 7, lalu 2,4,6,8 → height 2 |
| 7 | B | Nilai minimum selalu di node paling kiri |
| 8 | C | Diganti dengan predecessor atau successor |
| 9 | C | 35 menggantikan 30 sebagai root |
| 10 | C | BST tidak perlu geser elemen saat insert |
| 11 | C | Dipanggil 3x: root(50) → left(30) → left(25) |
| 12 | C | Urutan 4,2,6,1,3,5,7 menghasilkan perfect BST |
| 13 | D | Implementasi bervariasi, umumnya ke kiri atau kanan |
| 14 | C | Semua node hanya punya anak kiri = left-skewed |
| 15 | B | findMax traversal ke kanan, kompleksitas O(h) |
| 16 | D | AVL dan Red-Black adalah balanced BST |
| 17 | C | Leaf node langsung dihapus |
| 18 | C | BST seimbang memiliki height ≈ log₂ n |
| 19 | D | 25 menggantikan 20, 10 menjadi anak kiri 25 |
| 20 | C | BST ideal untuk indexing dan range query |

---

### Bagian B: Soal Uraian

#### Jawaban Soal 1 ⭐

**Properti Binary Search Tree:**
1. Untuk setiap node N, semua nilai di **subtree kiri** lebih kecil dari nilai N
2. Untuk setiap node N, semua nilai di **subtree kanan** lebih besar dari nilai N
3. Kedua subtree (kiri dan kanan) juga merupakan BST

**Mengapa efisien untuk search:**
- Setiap perbandingan mengeliminasi **setengah** dari kemungkinan node yang perlu diperiksa
- Mirip dengan binary search pada array terurut
- Pada BST seimbang dengan n node:
  - Height ≈ log₂ n
  - Maksimal perbandingan = log₂ n
  - Kompleksitas = O(log n)

**Contoh:** Mencari nilai 60 dalam BST dengan 1000 node seimbang hanya perlu ≈ 10 perbandingan, bukan 1000 seperti linear search.

---

#### Jawaban Soal 2 ⭐

**Proses Insert: 45, 25, 65, 15, 35, 55, 75**

**Step 1: Insert 45 (root)**
```
    45
```

**Step 2: Insert 25 (25 < 45, ke kiri)**
```
    45
   /
  25
```

**Step 3: Insert 65 (65 > 45, ke kanan)**
```
    45
   /  \
  25  65
```

**Step 4: Insert 15 (15 < 45, 15 < 25, ke kiri)**
```
    45
   /  \
  25  65
 /
15
```

**Step 5: Insert 35 (35 < 45, 35 > 25, ke kanan)**
```
    45
   /  \
  25  65
 /  \
15  35
```

**Step 6: Insert 55 (55 > 45, 55 < 65, ke kiri)**
```
    45
   /  \
  25  65
 /  \ /
15 35 55
```

**Step 7: Insert 75 (75 > 45, 75 > 65, ke kanan)**
```
      45
     /  \
   25    65
  /  \  /  \
 15  35 55  75
```

BST final adalah **perfect binary tree** dengan height 2.

---

#### Jawaban Soal 3 ⭐

**Inorder Predecessor:**
- Definisi: Node dengan nilai terbesar yang **lebih kecil** dari node saat ini
- Lokasi: Node paling kanan di **subtree kiri**
- Jika tidak ada subtree kiri, naik ke atas sampai menemukan ancestor yang node saat ini ada di subtree kanannya

**Inorder Successor:**
- Definisi: Node dengan nilai terkecil yang **lebih besar** dari node saat ini
- Lokasi: Node paling kiri di **subtree kanan**
- Jika tidak ada subtree kanan, naik ke atas sampai menemukan ancestor yang node saat ini ada di subtree kirinya

**Penggunaan dalam Delete:**
- Ketika menghapus node dengan **dua anak**, kita perlu pengganti yang mempertahankan properti BST
- **Inorder predecessor**: Mengganti dengan nilai terbesar di subtree kiri
- **Inorder successor**: Mengganti dengan nilai terkecil di subtree kanan
- Keduanya valid, pilihan tergantung implementasi

---

#### Jawaban Soal 4 ⭐⭐

**BST:**
```
        50
       /  \
      25   75
     / \   / \
    10 30 60 90
      \     \
      35    85
```

**a. Inorder Predecessor dari 50:**
- Predecessor = node terbesar di subtree kiri
- Subtree kiri: 25, 10, 30, 35
- Traversal ke kanan dari 25: 25 → 30 → 35
- **Inorder Predecessor = 35**

**b. Inorder Successor dari 50:**
- Successor = node terkecil di subtree kanan
- Subtree kanan: 75, 60, 90, 85
- Traversal ke kiri dari 75: 75 → 60
- **Inorder Successor = 60**

**c. BST setelah delete 50 (menggunakan inorder successor 60):**

```
        60
       /  \
      25   75
     / \     \
    10 30    90
      \     /
      35   85
```

Langkah:
1. Temukan inorder successor (60)
2. Copy nilai 60 ke posisi 50
3. Hapus node 60 dari posisi aslinya (node 60 hanya punya anak kanan, jadi langsung sambungkan)

---

#### Jawaban Soal 5 ⭐⭐

```cpp
int countNodes(Node* root) {
    // Base case: tree kosong
    if (root == nullptr) {
        return 0;
    }
    
    // Recursive: hitung node di kiri + kanan + 1 (current node)
    int leftCount = countNodes(root->left);
    int rightCount = countNodes(root->right);
    
    return leftCount + rightCount + 1;
}
```

**Penjelasan:**
- Base case: nullptr mengembalikan 0
- Recursive case: jumlah total = node kiri + node kanan + 1 (diri sendiri)
- Kompleksitas: O(n) karena mengunjungi setiap node tepat sekali

**Contoh penggunaan:**
```cpp
Node* root = /* BST */;
int total = countNodes(root);
cout << "Jumlah node: " << total << endl;
```

---

#### Jawaban Soal 6 ⭐⭐

```cpp
bool isBST(Node* root, int minVal, int maxVal) {
    // Base case: tree kosong adalah BST valid
    if (root == nullptr) {
        return true;
    }
    
    // Cek apakah nilai node dalam range yang valid
    if (root->data <= minVal || root->data >= maxVal) {
        return false;
    }
    
    // Rekursif: cek subtree kiri dan kanan dengan range yang diperbarui
    // Subtree kiri: semua nilai harus < root->data
    // Subtree kanan: semua nilai harus > root->data
    return isBST(root->left, minVal, root->data) &&
           isBST(root->right, root->data, maxVal);
}

// Fungsi wrapper
bool validateBST(Node* root) {
    return isBST(root, INT_MIN, INT_MAX);
}
```

**Penjelasan:**
- Setiap node harus berada dalam range (minVal, maxVal)
- Saat turun ke kiri, update maxVal = nilai node saat ini
- Saat turun ke kanan, update minVal = nilai node saat ini
- Kompleksitas: O(n)

---

#### Jawaban Soal 7 ⭐⭐

**Tiga Kasus Delete pada BST:**

**Kasus 1: Node adalah Leaf (tidak punya anak)**
- Langkah: Langsung hapus node
- Kompleksitas: O(h) untuk menemukan node + O(1) untuk hapus
- Contoh: Hapus node 35 dari BST

**Kasus 2: Node punya Satu Anak**
- Langkah: Ganti node dengan anaknya (bypass)
- Parent dari node yang dihapus langsung menunjuk ke anak
- Kompleksitas: O(h) untuk menemukan + O(1) untuk reconnect
- Contoh: Hapus node dengan satu anak kiri/kanan

**Kasus 3: Node punya Dua Anak**
- Langkah:
  1. Temukan inorder successor (atau predecessor)
  2. Copy nilai successor ke node yang dihapus
  3. Hapus node successor (yang pasti Kasus 1 atau 2)
- Kompleksitas: O(h) untuk menemukan + O(h) untuk cari successor + O(1) untuk operasi
- Total: O(h)

**Ringkasan Kompleksitas:**

| Kasus | Best Case | Worst Case |
|-------|-----------|------------|
| Leaf | O(log n) | O(n) |
| Satu anak | O(log n) | O(n) |
| Dua anak | O(log n) | O(n) |

Worst case O(n) terjadi saat BST skewed.

---

#### Jawaban Soal 8 ⭐⭐⭐

**Perbandingan BST vs Array Terurut vs Hash Table:**

| Operasi | BST (balanced) | Array Terurut | Hash Table |
|---------|----------------|---------------|------------|
| **Search** | O(log n) | O(log n) | O(1) avg |
| **Insert** | O(log n) | O(n) | O(1) avg |
| **Delete** | O(log n) | O(n) | O(1) avg |
| **Range Query** | O(k + log n)* | O(log n + k) | O(n) |
| **Min/Max** | O(log n) | O(1) | O(n) |
| **Ordered Traversal** | O(n) | O(n) | O(n log n)** |

*k = jumlah elemen dalam range  
**perlu sorting tambahan

**Kapan BST Lebih Baik:**

1. **Dibanding Array Terurut:**
   - Ketika data sering berubah (insert/delete)
   - Tidak perlu menggeser elemen
   - Contoh: Database yang frequently updated

2. **Dibanding Hash Table:**
   - Ketika perlu range query (nilai antara X dan Y)
   - Ketika perlu data terurut
   - Ketika perlu min/max dengan cepat
   - Contoh: Sistem scheduling, indexing database

3. **Keunggulan Utama BST:**
   - Mempertahankan urutan data
   - Mendukung operasi ordered dengan efisien
   - Fleksibel untuk insert/delete tanpa reorganisasi major

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Manajemen Inventaris Alutsista

**a. BST dari insert: 1500, 2300, 1200, 3100, 1800**

```
          1500
         /    \
      1200    2300
                / \
            1800 3100
```

**b. Range Query untuk ID 1200-2000:**

Algoritma Range Search pada BST:
1. Mulai dari root (1500)
2. Jika nilai node dalam range [1200, 2000], cetak dan cek kedua subtree
3. Jika nilai node < 1200, hanya cek subtree kanan
4. Jika nilai node > 2000, hanya cek subtree kiri

Langkah:
1. Root 1500: dalam range → cetak, cek kiri dan kanan
2. Node 1200: dalam range → cetak, cek subtree (kosong)
3. Node 2300: > 2000 → cek kiri saja
4. Node 1800: dalam range → cetak

**Hasil:** 1500, 1200, 1800

**c. Implementasi rangeSearch:**

```cpp
struct Node {
    int id;
    string namaItem;
    string kategori;
    Node* left;
    Node* right;
};

void rangeSearch(Node* root, int low, int high) {
    // Base case
    if (root == nullptr) {
        return;
    }
    
    // Jika nilai lebih besar dari low, ada kemungkinan
    // di subtree kiri
    if (root->id > low) {
        rangeSearch(root->left, low, high);
    }
    
    // Jika nilai dalam range, cetak
    if (root->id >= low && root->id <= high) {
        cout << "ID: " << root->id 
             << " | " << root->namaItem 
             << " | " << root->kategori << endl;
    }
    
    // Jika nilai lebih kecil dari high, ada kemungkinan
    // di subtree kanan
    if (root->id < high) {
        rangeSearch(root->right, low, high);
    }
}

// Contoh penggunaan
// rangeSearch(root, 1200, 2000);
```

---

#### Studi Kasus 2: Sistem Prioritas Target Radar

**a. Struktur Node BST untuk objek radar:**

```cpp
struct RadarTarget {
    int id;                    // ID unik objek
    int skorAncaman;           // Nilai untuk ordering BST
    string jenisObjek;         // "pesawat", "rudal", "drone", dll
    double latitude;           // Posisi
    double longitude;
    double altitude;           // Ketinggian
    double kecepatan;          // km/jam
    time_t waktuDeteksi;       // Timestamp deteksi
    RadarTarget* left;
    RadarTarget* right;
};
```

**b. Implementasi findMaxThreat:**

```cpp
RadarTarget* findMaxThreat(RadarTarget* root) {
    // Base case: tree kosong
    if (root == nullptr) {
        return nullptr;
    }
    
    // Nilai maksimum selalu di node paling kanan
    RadarTarget* current = root;
    while (current->right != nullptr) {
        current = current->right;
    }
    
    return current;
}

// Alternatif rekursif
RadarTarget* findMaxThreatRecursive(RadarTarget* root) {
    if (root == nullptr) {
        return nullptr;
    }
    
    if (root->right == nullptr) {
        return root;  // Node paling kanan ditemukan
    }
    
    return findMaxThreatRecursive(root->right);
}
```

**Kompleksitas:** O(h) dimana h = height of tree

**c. Analisis BST untuk Sistem Radar:**

**Kecocokan BST:**
1. **Search cepat** - Mencari objek dengan skor tertentu O(log n)
2. **Insert/Delete dinamis** - Objek masuk/keluar jangkauan
3. **FindMax efisien** - Prioritas tertinggi ditemukan cepat O(h)
4. **Range query** - Semua objek dengan skor > threshold

**Kelemahan:**
1. **Tidak guaranteed O(log n)** - BST bisa skewed jika skor masuk berurutan
2. **Waktu respons tidak konstan** - Untuk sistem real-time kritis, O(h) bisa terlalu lambat
3. **Rebalancing overhead** - Jika menggunakan balanced BST (AVL/RB)

**Saran Perbaikan untuk Waktu Respons Konstan:**

1. **Gunakan Max-Heap untuk prioritas tertinggi**
   - findMax O(1)
   - Insert/Delete O(log n)
   - Cocok untuk "selalu ambil ancaman tertinggi"

2. **Kombinasi BST + Heap**
   - BST untuk range query dan search by ID
   - Max-Heap terpisah untuk akses prioritas tertinggi
   - Trade-off: memori lebih besar, perlu sinkronisasi

3. **Balanced BST (AVL/Red-Black Tree)**
   - Menjamin O(log n) untuk semua operasi
   - Lebih predictable untuk sistem real-time

4. **B-Tree/B+ Tree**
   - Jika data sangat besar dan perlu disk access
   - Optimized untuk range query

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

- Soal mencakup semua Sub-CPMK untuk Pertemuan 12 (Sub-CPMK-5.2)
- Studi kasus menggunakan konteks pertahanan Indonesia yang relevan
- Tingkat kesulitan bervariasi: ⭐ Mudah, ⭐⭐ Sedang, ⭐⭐⭐ Sulit
- Soal programming memerlukan pemahaman rekursi dan pointer
- Studi kasus radar dapat diperluas untuk praktikum hands-on

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
