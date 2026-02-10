# Modul 12: Binary Search Tree (BST)

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 12  
**Topik:** Binary Search Tree (BST)

> **Capaian Pembelajaran:** Sub-CPMK-5.2 — Mampu mengimplementasikan Binary Search Tree (BST) dan operasi-operasinya

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.12; Weiss Ch.4.3; Hubbard Ch.11

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** properti dan karakteristik Binary Search Tree (BST)
2. **Mengimplementasikan** operasi search pada BST dengan benar
3. **Mengimplementasikan** operasi insert pada BST dengan benar
4. **Mengimplementasikan** operasi delete pada BST untuk tiga kasus (leaf, satu child, dua children)
5. **Mengimplementasikan** operasi findMin dan findMax pada BST
6. **Menganalisis** kompleksitas waktu BST untuk best case dan worst case
7. **Memahami** dampak BST tidak seimbang terhadap performa dan mengenal konsep balanced BST

---

## 1. Pendahuluan Binary Search Tree

### 1.1 Review Binary Tree

Pada pertemuan sebelumnya (Pertemuan 11), kita telah mempelajari Binary Tree — struktur data hierarkis di mana setiap node memiliki maksimal dua anak (left child dan right child). Binary Tree biasa tidak memiliki aturan khusus tentang bagaimana data disusun, sehingga operasi pencarian memerlukan traversal ke seluruh node dengan kompleksitas O(n).

**Binary Search Tree (BST)** adalah pengembangan dari Binary Tree dengan menambahkan **properti pengurutan** yang membuat operasi pencarian menjadi jauh lebih efisien.

### 1.2 Definisi Binary Search Tree

> **Binary Search Tree (BST)** adalah Binary Tree yang memenuhi properti berikut: untuk setiap node X, semua nilai di subtree kiri X **lebih kecil** dari nilai X, dan semua nilai di subtree kanan X **lebih besar** dari nilai X.

Secara formal, untuk setiap node dengan nilai `key`:
- Semua node di **left subtree** memiliki nilai < `key`
- Semua node di **right subtree** memiliki nilai > `key`

![BST Property](images/gambar-12-1.png)

*Gambar 12.1: Ilustrasi properti Binary Search Tree*

### 1.3 Struktur Node BST dalam C++

```cpp
struct BSTNode {
    int data;
    BSTNode* left;
    BSTNode* right;
    
    // Constructor
    BSTNode(int value) : data(value), left(nullptr), right(nullptr) {}
};
```

Atau menggunakan template untuk tipe data generik:

```cpp
template <typename T>
struct BSTNode {
    T data;
    BSTNode<T>* left;
    BSTNode<T>* right;
    
    BSTNode(T value) : data(value), left(nullptr), right(nullptr) {}
};
```

### 1.4 Keunggulan BST

| Aspek | Binary Tree Biasa | Binary Search Tree |
|-------|-------------------|-------------------|
| Pengurutan data | Tidak ada aturan | Terurut (left < parent < right) |
| Kompleksitas search | O(n) | O(log n) rata-rata |
| Kompleksitas insert | O(n) untuk cari posisi | O(log n) rata-rata |
| Kompleksitas delete | O(n) untuk cari posisi | O(log n) rata-rata |
| Inorder traversal | Urutan tidak teratur | Menghasilkan data terurut ascending |

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Diberikan Binary Tree berikut. Tentukan apakah tree tersebut merupakan BST yang valid!

```
        15
       /  \
      10   20
     / \   / \
    5  12 17  25
```

**Penyelesaian:**

Untuk memverifikasi BST, periksa setiap node apakah memenuhi properti BST:

**Node 15 (root):**
- Left subtree: {5, 10, 12} — semua < 15 ✓
- Right subtree: {17, 20, 25} — semua > 15 ✓

**Node 10:**
- Left child (5) < 10 ✓
- Right child (12) > 10 ✓

**Node 20:**
- Left child (17) < 20 ✓
- Right child (25) > 20 ✓

**Kesimpulan:** Ya, tree tersebut adalah **BST yang valid**.

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Diberikan Binary Tree berikut. Tentukan apakah tree tersebut merupakan BST yang valid!

```
        10
       /  \
      5    15
     / \
    3   12
```

**Penyelesaian:**

Periksa setiap node:

**Node 10 (root):**
- Left subtree harus semua < 10
- Node 5 < 10 ✓
- Node 3 < 10 ✓
- Node 12 < 10? **12 > 10** ✗

Meskipun 12 adalah child kanan dari 5, ia berada di **left subtree dari root 10**, sehingga harus bernilai < 10.

**Kesimpulan:** Bukan BST yang valid karena node 12 melanggar properti BST.

---

## 2. Operasi Search pada BST

### 2.1 Algoritma Pencarian

Operasi search pada BST memanfaatkan properti pengurutan untuk mengeliminasi setengah tree pada setiap langkah — mirip dengan binary search pada array.

**Algoritma:**
1. Mulai dari root
2. Jika nilai yang dicari sama dengan node saat ini, **ditemukan**
3. Jika nilai yang dicari **lebih kecil**, lanjut ke **left subtree**
4. Jika nilai yang dicari **lebih besar**, lanjut ke **right subtree**
5. Jika mencapai nullptr, **tidak ditemukan**

### 2.2 Implementasi Rekursif

```cpp
BSTNode* search(BSTNode* root, int key) {
    // Base case: root null atau ditemukan
    if (root == nullptr || root->data == key) {
        return root;
    }
    
    // Key lebih kecil, cari di left subtree
    if (key < root->data) {
        return search(root->left, key);
    }
    
    // Key lebih besar, cari di right subtree
    return search(root->right, key);
}
```

### 2.3 Implementasi Iteratif

```cpp
BSTNode* searchIterative(BSTNode* root, int key) {
    BSTNode* current = root;
    
    while (current != nullptr) {
        if (key == current->data) {
            return current;  // Ditemukan
        } else if (key < current->data) {
            current = current->left;  // Ke kiri
        } else {
            current = current->right;  // Ke kanan
        }
    }
    
    return nullptr;  // Tidak ditemukan
}
```

### 2.4 Visualisasi Proses Search

![BST Search Process](images/gambar-12-2.png)

*Gambar 12.2: Proses pencarian nilai 17 pada BST*

---

### SOLVED PROBLEM 3 ⭐

**Soal:** Diberikan BST dengan struktur berikut. Tuliskan urutan node yang dikunjungi saat mencari nilai 35!

```
        50
       /  \
      30   70
     / \   / \
    20 40 60  80
       /
      35
```

**Penyelesaian:**

**Langkah pencarian:**
1. Mulai dari root (50): 35 < 50, ke **kiri**
2. Di node 30: 35 > 30, ke **kanan**
3. Di node 40: 35 < 40, ke **kiri**
4. Di node 35: **Ditemukan!**

**Urutan node yang dikunjungi:** 50 → 30 → 40 → 35

**Jumlah perbandingan:** 4

---

### SOLVED PROBLEM 4 ⭐

**Soal:** Apa yang terjadi jika kita mencari nilai 45 pada BST di Solved Problem 3?

**Penyelesaian:**

**Langkah pencarian:**
1. Mulai dari root (50): 45 < 50, ke **kiri**
2. Di node 30: 45 > 30, ke **kanan**
3. Di node 40: 45 > 40, ke **kanan**
4. Right child dari 40 adalah nullptr

**Hasil:** Nilai 45 **tidak ditemukan** (return nullptr).

---

### SOLVED PROBLEM 5 ⭐⭐

**Soal:** Analisis kompleksitas waktu operasi search pada BST! Jelaskan best case, average case, dan worst case!

**Penyelesaian:**

**Best Case: O(1)**
- Terjadi ketika elemen yang dicari adalah root
- Hanya perlu satu perbandingan

**Average Case: O(log n)**
- Terjadi pada BST yang **relatif seimbang**
- Setiap langkah mengeliminasi sekitar setengah node
- Tinggi tree ≈ log₂(n)

**Worst Case: O(n)**
- Terjadi pada BST yang **tidak seimbang** (degenerate/skewed tree)
- Tree menjadi seperti linked list
- Harus traverse semua node

![BST Complexity Cases](images/gambar-12-3.png)

*Gambar 12.3: Perbandingan BST seimbang dan tidak seimbang*

---

## 3. Operasi Insert pada BST

### 3.1 Algoritma Insert

Operasi insert pada BST harus memastikan properti BST tetap terjaga setelah penyisipan.

**Algoritma:**
1. Jika tree kosong, buat node baru sebagai root
2. Bandingkan nilai baru dengan node saat ini
3. Jika nilai baru **lebih kecil**, rekursi ke **left subtree**
4. Jika nilai baru **lebih besar**, rekursi ke **right subtree**
5. Sisipkan node baru di posisi nullptr yang ditemukan

> **Catatan:** Pada implementasi BST standar, nilai duplikat biasanya **tidak diizinkan**. Jika ditemukan nilai sama, bisa diabaikan atau menimbulkan error.

### 3.2 Implementasi Rekursif

```cpp
BSTNode* insert(BSTNode* root, int value) {
    // Base case: posisi kosong ditemukan
    if (root == nullptr) {
        return new BSTNode(value);
    }
    
    // Rekursi ke subtree yang sesuai
    if (value < root->data) {
        root->left = insert(root->left, value);
    } else if (value > root->data) {
        root->right = insert(root->right, value);
    }
    // Jika value == root->data, diabaikan (no duplicates)
    
    return root;
}
```

### 3.3 Implementasi Iteratif

```cpp
BSTNode* insertIterative(BSTNode* root, int value) {
    BSTNode* newNode = new BSTNode(value);
    
    // Tree kosong
    if (root == nullptr) {
        return newNode;
    }
    
    BSTNode* current = root;
    BSTNode* parent = nullptr;
    
    // Cari posisi yang tepat
    while (current != nullptr) {
        parent = current;
        if (value < current->data) {
            current = current->left;
        } else if (value > current->data) {
            current = current->right;
        } else {
            // Nilai duplikat, tidak diinsert
            delete newNode;
            return root;
        }
    }
    
    // Sisipkan node baru
    if (value < parent->data) {
        parent->left = newNode;
    } else {
        parent->right = newNode;
    }
    
    return root;
}
```

### 3.4 Visualisasi Proses Insert

![BST Insert Process](images/gambar-12-4.png)

*Gambar 12.4: Proses penyisipan nilai 25 pada BST*

---

### SOLVED PROBLEM 6 ⭐

**Soal:** Gambarkan BST yang dihasilkan dari menyisipkan nilai-nilai berikut secara berurutan: 50, 30, 70, 20, 40, 60, 80

**Penyelesaian:**

**Langkah penyisipan:**

1. **Insert 50:** Tree kosong → 50 menjadi root
2. **Insert 30:** 30 < 50 → left child dari 50
3. **Insert 70:** 70 > 50 → right child dari 50
4. **Insert 20:** 20 < 50, 20 < 30 → left child dari 30
5. **Insert 40:** 40 < 50, 40 > 30 → right child dari 30
6. **Insert 60:** 60 > 50, 60 < 70 → left child dari 70
7. **Insert 80:** 80 > 50, 80 > 70 → right child dari 70

**BST yang dihasilkan:**
```
        50
       /  \
      30   70
     / \   / \
    20 40 60  80
```

---

### SOLVED PROBLEM 7 ⭐

**Soal:** Gambarkan BST yang dihasilkan dari menyisipkan nilai-nilai berikut secara berurutan: 10, 20, 30, 40, 50

**Penyelesaian:**

**Langkah penyisipan:**

1. **Insert 10:** Root
2. **Insert 20:** 20 > 10 → right child dari 10
3. **Insert 30:** 30 > 10, 30 > 20 → right child dari 20
4. **Insert 40:** Terus ke kanan → right child dari 30
5. **Insert 50:** Terus ke kanan → right child dari 40

**BST yang dihasilkan (Degenerate Tree):**
```
    10
      \
       20
         \
          30
            \
             40
               \
                50
```

**Catatan:** Jika data diinsert dalam urutan terurut (ascending atau descending), BST akan menjadi **degenerate tree** dengan tinggi O(n).

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Tuliskan urutan penyisipan yang berbeda untuk nilai {10, 20, 30, 40, 50, 60, 70} agar menghasilkan BST yang seimbang!

**Penyelesaian:**

Untuk mendapatkan BST seimbang, sisipkan nilai **median** terlebih dahulu, kemudian median dari subarray.

**Strategi:**
- Median keseluruhan: 40 (sisipkan pertama)
- Median kiri {10,20,30}: 20
- Median kanan {50,60,70}: 60
- Sisa: 10, 30, 50, 70

**Urutan penyisipan:** 40, 20, 60, 10, 30, 50, 70

**BST yang dihasilkan:**
```
          40
        /    \
      20      60
     /  \    /  \
    10  30  50  70
```

Tinggi tree = 3 (optimal untuk 7 node, karena log₂(7) ≈ 2.8)

---

## 4. Operasi findMin dan findMax

### 4.1 Konsep

Berdasarkan properti BST:
- **Nilai minimum** selalu berada di **node paling kiri** (left-most node)
- **Nilai maksimum** selalu berada di **node paling kanan** (right-most node)

### 4.2 Implementasi findMin

```cpp
BSTNode* findMin(BSTNode* root) {
    if (root == nullptr) {
        return nullptr;
    }
    
    // Terus ke kiri sampai tidak bisa lagi
    while (root->left != nullptr) {
        root = root->left;
    }
    
    return root;
}

// Versi rekursif
BSTNode* findMinRecursive(BSTNode* root) {
    if (root == nullptr || root->left == nullptr) {
        return root;
    }
    return findMinRecursive(root->left);
}
```

### 4.3 Implementasi findMax

```cpp
BSTNode* findMax(BSTNode* root) {
    if (root == nullptr) {
        return nullptr;
    }
    
    // Terus ke kanan sampai tidak bisa lagi
    while (root->right != nullptr) {
        root = root->right;
    }
    
    return root;
}

// Versi rekursif
BSTNode* findMaxRecursive(BSTNode* root) {
    if (root == nullptr || root->right == nullptr) {
        return root;
    }
    return findMaxRecursive(root->right);
}
```

### 4.4 Kompleksitas

| Operasi | Best Case | Average Case | Worst Case |
|---------|-----------|--------------|------------|
| findMin | O(1)* | O(log n) | O(n) |
| findMax | O(1)* | O(log n) | O(n) |

*Best case O(1) terjadi jika min/max adalah root (untuk tree dengan satu node atau skewed tree).

---

### SOLVED PROBLEM 9 ⭐

**Soal:** Pada BST berikut, tentukan nilai minimum dan maksimum!

```
        50
       /  \
      30   70
     / \   / \
    20 40 60  80
   /
  15
```

**Penyelesaian:**

**Mencari minimum:**
- Mulai dari root (50)
- Ke kiri → 30
- Ke kiri → 20
- Ke kiri → 15
- Left child = nullptr, **minimum = 15**

**Mencari maksimum:**
- Mulai dari root (50)
- Ke kanan → 70
- Ke kanan → 80
- Right child = nullptr, **maksimum = 80**

---

### SOLVED PROBLEM 10 ⭐⭐

**Soal:** Implementasikan fungsi `int findKthSmallest(BSTNode* root, int k)` yang mencari elemen terkecil ke-k dalam BST!

**Penyelesaian:**

Elemen ke-k terkecil dapat ditemukan menggunakan **inorder traversal** karena inorder traversal pada BST menghasilkan elemen terurut ascending.

```cpp
class Solution {
private:
    int count = 0;
    int result = -1;
    
    void inorderKth(BSTNode* root, int k) {
        if (root == nullptr || count >= k) {
            return;
        }
        
        // Kunjungi left subtree
        inorderKth(root->left, k);
        
        // Process current node
        count++;
        if (count == k) {
            result = root->data;
            return;
        }
        
        // Kunjungi right subtree
        inorderKth(root->right, k);
    }
    
public:
    int findKthSmallest(BSTNode* root, int k) {
        count = 0;
        result = -1;
        inorderKth(root, k);
        return result;
    }
};
```

**Contoh:** Untuk BST {15, 20, 30, 40, 50, 60, 70, 80}, k=3 menghasilkan **30**.

---

## 5. Operasi Delete pada BST

### 5.1 Tiga Kasus Penghapusan

Operasi delete pada BST adalah operasi paling kompleks karena harus mempertahankan properti BST. Ada **tiga kasus** yang perlu ditangani:

| Kasus | Kondisi | Solusi |
|-------|---------|--------|
| **Kasus 1** | Node adalah **leaf** (tidak punya anak) | Hapus langsung |
| **Kasus 2** | Node punya **satu anak** | Ganti node dengan anaknya |
| **Kasus 3** | Node punya **dua anak** | Ganti dengan inorder successor atau predecessor |

### 5.2 Kasus 1: Hapus Leaf Node

![BST Delete Leaf](images/gambar-12-5.png)

*Gambar 12.5: Penghapusan leaf node pada BST*

**Implementasi:**
```cpp
// Jika node adalah leaf, parent->left atau parent->right = nullptr
```

### 5.3 Kasus 2: Hapus Node dengan Satu Anak

![BST Delete One Child](images/gambar-12-6.png)

*Gambar 12.6: Penghapusan node dengan satu anak pada BST*

**Implementasi:**
```cpp
// Jika node punya satu anak, ganti node dengan anaknya
// parent->left/right = node->left atau node->right (yang tidak null)
```

### 5.4 Kasus 3: Hapus Node dengan Dua Anak

Ini adalah kasus paling kompleks. Ada dua pendekatan:
1. Ganti dengan **inorder successor** (nilai terkecil di right subtree)
2. Ganti dengan **inorder predecessor** (nilai terbesar di left subtree)

> **Inorder Successor** adalah node dengan nilai **terkecil yang lebih besar** dari node yang dihapus.

![BST Delete Two Children](images/gambar-12-7.png)

*Gambar 12.7: Penghapusan node dengan dua anak menggunakan inorder successor*

### 5.5 Implementasi Lengkap Delete

```cpp
BSTNode* deleteNode(BSTNode* root, int key) {
    // Base case: tree kosong
    if (root == nullptr) {
        return nullptr;
    }
    
    // Cari node yang akan dihapus
    if (key < root->data) {
        root->left = deleteNode(root->left, key);
    } else if (key > root->data) {
        root->right = deleteNode(root->right, key);
    } else {
        // Node ditemukan - ini yang akan dihapus
        
        // Kasus 1 & 2: Node leaf atau punya satu anak
        if (root->left == nullptr) {
            BSTNode* temp = root->right;
            delete root;
            return temp;
        } else if (root->right == nullptr) {
            BSTNode* temp = root->left;
            delete root;
            return temp;
        }
        
        // Kasus 3: Node punya dua anak
        // Cari inorder successor (nilai terkecil di right subtree)
        BSTNode* successor = findMin(root->right);
        
        // Copy nilai successor ke node ini
        root->data = successor->data;
        
        // Hapus inorder successor
        root->right = deleteNode(root->right, successor->data);
    }
    
    return root;
}
```

---

### SOLVED PROBLEM 11 ⭐

**Soal:** Pada BST berikut, tunjukkan hasil penghapusan node 20 (leaf node)!

```
        50
       /  \
      30   70
     / \
    20 40
```

**Penyelesaian:**

**Kasus:** Node 20 adalah **leaf** (tidak punya anak).

**Proses:**
1. Cari node 20: 20 < 50 → kiri, 20 < 30 → kiri → ditemukan
2. Node 20 tidak punya anak
3. Set parent->left (30->left) = nullptr
4. Dealokasi node 20

**Hasil:**
```
        50
       /  \
      30   70
       \
       40
```

---

### SOLVED PROBLEM 12 ⭐

**Soal:** Pada BST berikut, tunjukkan hasil penghapusan node 70 (node dengan satu anak)!

```
        50
       /  \
      30   70
     / \     \
    20 40    80
```

**Penyelesaian:**

**Kasus:** Node 70 punya **satu anak** (80).

**Proses:**
1. Cari node 70: 70 > 50 → kanan → ditemukan
2. Node 70 hanya punya right child (80)
3. Ganti link dari parent (50->right) ke child (80)
4. Dealokasi node 70

**Hasil:**
```
        50
       /  \
      30   80
     / \
    20 40
```

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Pada BST berikut, tunjukkan hasil penghapusan node 30 (node dengan dua anak)!

```
        50
       /  \
      30   70
     / \   / \
    20 40 60  80
```

**Penyelesaian:**

**Kasus:** Node 30 punya **dua anak** (20 dan 40).

**Proses dengan Inorder Successor:**
1. Cari inorder successor dari 30 = nilai terkecil di right subtree dari 30
2. Right subtree dari 30 hanya berisi 40
3. Inorder successor = 40
4. Copy nilai 40 ke node 30
5. Hapus node 40 yang asli (yang sekarang adalah leaf)

**Hasil:**
```
        50
       /  \
      40   70
     /     / \
    20    60  80
```

**Alternatif dengan Inorder Predecessor:**
- Inorder predecessor dari 30 = nilai terbesar di left subtree = 20
- Copy 20 ke posisi 30, hapus node 20 yang asli
- Hasil: node 30 diganti dengan 20

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Pada BST berikut, tunjukkan hasil penghapusan node 50 (root dengan dua anak)!

```
        50
       /  \
      30   70
     / \   / \
    20 40 60  80
           \
           65
```

**Penyelesaian:**

**Kasus:** Node 50 (root) punya **dua anak**.

**Proses dengan Inorder Successor:**
1. Inorder successor dari 50 = nilai terkecil di right subtree
2. Right subtree: {60, 65, 70, 80}
3. Nilai terkecil = 60 (left-most di right subtree)
4. Copy nilai 60 ke root
5. Hapus node 60 yang asli (node 60 punya satu anak: 65)
6. Saat menghapus 60, ganti dengan anaknya (65)

**Hasil:**
```
        60
       /  \
      30   70
     / \   / \
    20 40 65  80
```

---

### SOLVED PROBLEM 15 ⭐⭐⭐

**Soal:** Tuliskan fungsi `bool isBST(BSTNode* root)` yang memverifikasi apakah sebuah binary tree adalah BST yang valid!

**Penyelesaian:**

Pendekatan yang **salah** adalah hanya memeriksa apakah left < parent < right untuk setiap node. Kita harus memastikan **semua node** di left subtree lebih kecil dan **semua node** di right subtree lebih besar.

**Pendekatan yang benar:** gunakan range checking.

```cpp
bool isBSTUtil(BSTNode* root, int minVal, int maxVal) {
    // Base case: tree kosong adalah BST
    if (root == nullptr) {
        return true;
    }
    
    // Cek apakah nilai node dalam range yang valid
    if (root->data <= minVal || root->data >= maxVal) {
        return false;
    }
    
    // Rekursif: cek left subtree (semua harus < root->data)
    //           cek right subtree (semua harus > root->data)
    return isBSTUtil(root->left, minVal, root->data) &&
           isBSTUtil(root->right, root->data, maxVal);
}

bool isBST(BSTNode* root) {
    return isBSTUtil(root, INT_MIN, INT_MAX);
}
```

**Alternatif menggunakan inorder traversal:**

```cpp
bool isBSTInorder(BSTNode* root, int& prev) {
    if (root == nullptr) {
        return true;
    }
    
    // Cek left subtree
    if (!isBSTInorder(root->left, prev)) {
        return false;
    }
    
    // Cek current: harus lebih besar dari previous
    if (root->data <= prev) {
        return false;
    }
    prev = root->data;
    
    // Cek right subtree
    return isBSTInorder(root->right, prev);
}

bool isBST(BSTNode* root) {
    int prev = INT_MIN;
    return isBSTInorder(root, prev);
}
```

---

## 6. Analisis Kompleksitas BST

### 6.1 Ringkasan Kompleksitas

| Operasi | Best Case | Average Case | Worst Case |
|---------|-----------|--------------|------------|
| Search | O(1) | O(log n) | O(n) |
| Insert | O(1) | O(log n) | O(n) |
| Delete | O(1) | O(log n) | O(n) |
| findMin | O(1) | O(log n) | O(n) |
| findMax | O(1) | O(log n) | O(n) |
| Traversal | O(n) | O(n) | O(n) |

### 6.2 Faktor yang Mempengaruhi

**Kompleksitas BST sangat bergantung pada bentuk tree:**

| Bentuk Tree | Tinggi | Kompleksitas Operasi |
|-------------|--------|---------------------|
| Perfectly Balanced | ⌊log₂(n)⌋ | O(log n) |
| Reasonably Balanced | O(log n) | O(log n) |
| Skewed/Degenerate | n - 1 | O(n) |

### 6.3 Space Complexity

- **Penyimpanan tree:** O(n) untuk n node
- **Operasi rekursif:** O(h) untuk call stack, dimana h = tinggi tree
- **Operasi iteratif:** O(1) space tambahan

---

### SOLVED PROBLEM 16 ⭐⭐

**Soal:** Hitung jumlah perbandingan yang diperlukan untuk mencari nilai 75 pada kedua BST berikut:

**BST A (Balanced):**
```
          50
        /    \
      25      75
     /  \    /  \
    10  30  60  90
```

**BST B (Skewed):**
```
    10
      \
       25
         \
          30
            \
             50
               \
                60
                  \
                   75
```

**Penyelesaian:**

**BST A (Balanced):**
1. 75 > 50 → ke kanan (perbandingan 1)
2. 75 == 75 → **ditemukan** (perbandingan 2)

**Total perbandingan BST A: 2**

**BST B (Skewed):**
1. 75 > 10 → ke kanan (perbandingan 1)
2. 75 > 25 → ke kanan (perbandingan 2)
3. 75 > 30 → ke kanan (perbandingan 3)
4. 75 > 50 → ke kanan (perbandingan 4)
5. 75 > 60 → ke kanan (perbandingan 5)
6. 75 == 75 → **ditemukan** (perbandingan 6)

**Total perbandingan BST B: 6**

**Kesimpulan:** BST balanced (A) memerlukan **3x lebih sedikit** perbandingan dibanding BST skewed (B) untuk n=7 node.

---

## 7. BST Tidak Seimbang dan Dampaknya

### 7.1 Penyebab BST Tidak Seimbang

BST menjadi tidak seimbang ketika:
1. **Data diinsert dalam urutan terurut** (ascending atau descending)
2. **Data memiliki pola tertentu** yang menyebabkan satu sisi lebih berat
3. **Operasi delete yang berulang** pada satu sisi

### 7.2 Dampak BST Tidak Seimbang

| Aspek | BST Seimbang | BST Tidak Seimbang |
|-------|--------------|-------------------|
| Tinggi | O(log n) | O(n) |
| Search | O(log n) | O(n) |
| Insert | O(log n) | O(n) |
| Delete | O(log n) | O(n) |
| Memory overhead | Sama | Sama |

**Dalam konteks sistem pertahanan:** Jika sistem tracking menggunakan BST tidak seimbang dengan 1 juta data, pencarian bisa memerlukan hingga 1 juta operasi, dibandingkan hanya ~20 operasi pada BST seimbang (log₂(1.000.000) ≈ 20).

### 7.3 Pengenalan Balanced BST

Untuk mengatasi masalah BST tidak seimbang, dikembangkan berbagai jenis **Self-Balancing BST**:

| Tipe | Mekanisme | Kompleksitas Garanteed |
|------|-----------|----------------------|
| **AVL Tree** | Balance factor (-1, 0, +1), rotasi | O(log n) |
| **Red-Black Tree** | Pewarnaan node + rotasi | O(log n) |
| **Splay Tree** | Splaying (move to root) | Amortized O(log n) |
| **B-Tree** | Multi-way tree untuk disk | O(log n) |

> **Catatan:** Detail implementasi AVL Tree dan Red-Black Tree akan dipelajari lebih lanjut di mata kuliah lanjutan atau sebagai materi pengayaan. Untuk mata kuliah ini, cukup memahami **konsep** mengapa balanced BST diperlukan.

---

### SOLVED PROBLEM 17 ⭐⭐

**Soal:** Jelaskan mengapa menyisipkan data {1, 2, 3, 4, 5, 6, 7} secara berurutan menghasilkan BST dengan performa buruk, dan bagaimana menghindarinya!

**Penyelesaian:**

**Masalah:**

Menyisipkan {1, 2, 3, 4, 5, 6, 7} berurutan:
```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
           \
            7
```

Hasilnya adalah **right-skewed tree** dengan:
- Tinggi = 6 (bukan log₂(7) ≈ 2.8)
- Kompleksitas operasi = O(n) bukan O(log n)

**Solusi:**

1. **Acak urutan penyisipan:** Shuffle data sebelum insert
   - Contoh: {4, 2, 6, 1, 3, 5, 7}

2. **Gunakan strategi median-first:**
   - Insert median dulu (4), lalu median subarray, dst.
   - Urutan: {4, 2, 6, 1, 3, 5, 7}

3. **Gunakan Self-Balancing BST:**
   - AVL Tree atau Red-Black Tree akan otomatis menyeimbangkan

---

### SOLVED PROBLEM 18 ⭐⭐⭐

**Soal:** Implementasikan class BST lengkap dengan operasi insert, search, delete, findMin, findMax, dan inorder traversal!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
using namespace std;

class BST {
private:
    struct Node {
        int data;
        Node* left;
        Node* right;
        
        Node(int value) : data(value), left(nullptr), right(nullptr) {}
    };
    
    Node* root;
    
    // Helper functions (private)
    Node* insertHelper(Node* node, int value) {
        if (node == nullptr) {
            return new Node(value);
        }
        
        if (value < node->data) {
            node->left = insertHelper(node->left, value);
        } else if (value > node->data) {
            node->right = insertHelper(node->right, value);
        }
        
        return node;
    }
    
    Node* searchHelper(Node* node, int key) {
        if (node == nullptr || node->data == key) {
            return node;
        }
        
        if (key < node->data) {
            return searchHelper(node->left, key);
        }
        return searchHelper(node->right, key);
    }
    
    Node* findMinHelper(Node* node) {
        if (node == nullptr) return nullptr;
        while (node->left != nullptr) {
            node = node->left;
        }
        return node;
    }
    
    Node* findMaxHelper(Node* node) {
        if (node == nullptr) return nullptr;
        while (node->right != nullptr) {
            node = node->right;
        }
        return node;
    }
    
    Node* deleteHelper(Node* node, int key) {
        if (node == nullptr) return nullptr;
        
        if (key < node->data) {
            node->left = deleteHelper(node->left, key);
        } else if (key > node->data) {
            node->right = deleteHelper(node->right, key);
        } else {
            // Node ditemukan
            if (node->left == nullptr) {
                Node* temp = node->right;
                delete node;
                return temp;
            } else if (node->right == nullptr) {
                Node* temp = node->left;
                delete node;
                return temp;
            }
            
            // Dua anak: gunakan inorder successor
            Node* successor = findMinHelper(node->right);
            node->data = successor->data;
            node->right = deleteHelper(node->right, successor->data);
        }
        
        return node;
    }
    
    void inorderHelper(Node* node) {
        if (node == nullptr) return;
        inorderHelper(node->left);
        cout << node->data << " ";
        inorderHelper(node->right);
    }
    
    void destroyTree(Node* node) {
        if (node == nullptr) return;
        destroyTree(node->left);
        destroyTree(node->right);
        delete node;
    }
    
public:
    BST() : root(nullptr) {}
    
    ~BST() {
        destroyTree(root);
    }
    
    void insert(int value) {
        root = insertHelper(root, value);
    }
    
    bool search(int key) {
        return searchHelper(root, key) != nullptr;
    }
    
    int findMin() {
        Node* minNode = findMinHelper(root);
        if (minNode == nullptr) {
            throw runtime_error("Tree is empty");
        }
        return minNode->data;
    }
    
    int findMax() {
        Node* maxNode = findMaxHelper(root);
        if (maxNode == nullptr) {
            throw runtime_error("Tree is empty");
        }
        return maxNode->data;
    }
    
    void remove(int key) {
        root = deleteHelper(root, key);
    }
    
    void inorderTraversal() {
        inorderHelper(root);
        cout << endl;
    }
    
    bool isEmpty() {
        return root == nullptr;
    }
};

// Demo penggunaan
int main() {
    BST tree;
    
    // Insert
    cout << "Inserting: 50, 30, 70, 20, 40, 60, 80" << endl;
    tree.insert(50);
    tree.insert(30);
    tree.insert(70);
    tree.insert(20);
    tree.insert(40);
    tree.insert(60);
    tree.insert(80);
    
    // Inorder traversal
    cout << "Inorder traversal: ";
    tree.inorderTraversal();
    
    // Search
    cout << "Search 40: " << (tree.search(40) ? "Found" : "Not found") << endl;
    cout << "Search 45: " << (tree.search(45) ? "Found" : "Not found") << endl;
    
    // Min dan Max
    cout << "Minimum: " << tree.findMin() << endl;
    cout << "Maximum: " << tree.findMax() << endl;
    
    // Delete
    cout << "\nDeleting 20 (leaf)..." << endl;
    tree.remove(20);
    cout << "Inorder: ";
    tree.inorderTraversal();
    
    cout << "Deleting 30 (one child)..." << endl;
    tree.remove(30);
    cout << "Inorder: ";
    tree.inorderTraversal();
    
    cout << "Deleting 50 (two children, root)..." << endl;
    tree.remove(50);
    cout << "Inorder: ";
    tree.inorderTraversal();
    
    return 0;
}
```

**Output:**
```
Inserting: 50, 30, 70, 20, 40, 60, 80
Inorder traversal: 20 30 40 50 60 70 80 
Search 40: Found
Search 45: Not found
Minimum: 20
Maximum: 80

Deleting 20 (leaf)...
Inorder: 30 40 50 60 70 80 
Deleting 30 (one child)...
Inorder: 40 50 60 70 80 
Deleting 50 (two children, root)...
Inorder: 40 60 70 80 
```

---

## 8. Aplikasi BST dalam Konteks Pertahanan

### 8.1 Sistem Database Personel

BST dapat digunakan untuk menyimpan dan mencari data personel berdasarkan NIP (Nomor Induk Pegawai) dengan efisien.

```cpp
struct Personel {
    string nip;        // Key untuk BST
    string nama;
    string pangkat;
    string satuan;
    
    // Operator perbandingan berdasarkan NIP
    bool operator<(const Personel& other) const {
        return nip < other.nip;
    }
};
```

### 8.2 Sistem Tracking dengan Range Query

BST mendukung **range query** dengan efisien — mencari semua nilai dalam rentang tertentu.

```cpp
void rangeSearch(BSTNode* root, int low, int high, vector<int>& result) {
    if (root == nullptr) return;
    
    // Jika root->data > low, mungkin ada nilai di left subtree
    if (root->data > low) {
        rangeSearch(root->left, low, high, result);
    }
    
    // Jika root->data dalam range, masukkan ke result
    if (root->data >= low && root->data <= high) {
        result.push_back(root->data);
    }
    
    // Jika root->data < high, mungkin ada nilai di right subtree
    if (root->data < high) {
        rangeSearch(root->right, low, high, result);
    }
}
```

---

### SOLVED PROBLEM 19 ⭐⭐

**Soal:** Sistem radar mendeteksi objek pada jarak tertentu (dalam km). Implementasikan fungsi untuk mencari semua objek dalam jarak 100-200 km menggunakan BST!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

struct RadarContact {
    int id;
    int distance;  // dalam km
    string type;
    
    RadarContact(int i, int d, string t) : id(i), distance(d), type(t) {}
};

struct RadarNode {
    RadarContact* contact;
    RadarNode* left;
    RadarNode* right;
    
    RadarNode(RadarContact* c) : contact(c), left(nullptr), right(nullptr) {}
};

class RadarBST {
private:
    RadarNode* root;
    
    RadarNode* insert(RadarNode* node, RadarContact* contact) {
        if (node == nullptr) {
            return new RadarNode(contact);
        }
        
        if (contact->distance < node->contact->distance) {
            node->left = insert(node->left, contact);
        } else {
            node->right = insert(node->right, contact);
        }
        
        return node;
    }
    
    void rangeSearch(RadarNode* node, int minDist, int maxDist, 
                     vector<RadarContact*>& result) {
        if (node == nullptr) return;
        
        if (node->contact->distance > minDist) {
            rangeSearch(node->left, minDist, maxDist, result);
        }
        
        if (node->contact->distance >= minDist && 
            node->contact->distance <= maxDist) {
            result.push_back(node->contact);
        }
        
        if (node->contact->distance < maxDist) {
            rangeSearch(node->right, minDist, maxDist, result);
        }
    }
    
public:
    RadarBST() : root(nullptr) {}
    
    void addContact(RadarContact* contact) {
        root = insert(root, contact);
    }
    
    vector<RadarContact*> findInRange(int minDist, int maxDist) {
        vector<RadarContact*> result;
        rangeSearch(root, minDist, maxDist, result);
        return result;
    }
};

int main() {
    RadarBST radar;
    
    // Menambahkan kontak radar
    radar.addContact(new RadarContact(1, 50, "Aircraft"));
    radar.addContact(new RadarContact(2, 150, "Ship"));
    radar.addContact(new RadarContact(3, 75, "Aircraft"));
    radar.addContact(new RadarContact(4, 200, "Unknown"));
    radar.addContact(new RadarContact(5, 120, "Ship"));
    radar.addContact(new RadarContact(6, 180, "Aircraft"));
    radar.addContact(new RadarContact(7, 250, "Ship"));
    
    // Mencari objek dalam jarak 100-200 km
    cout << "Objek dalam jarak 100-200 km:" << endl;
    vector<RadarContact*> targets = radar.findInRange(100, 200);
    
    for (RadarContact* c : targets) {
        cout << "ID: " << c->id << ", Distance: " << c->distance 
             << " km, Type: " << c->type << endl;
    }
    
    return 0;
}
```

**Output:**
```
Objek dalam jarak 100-200 km:
ID: 5, Distance: 120 km, Type: Ship
ID: 2, Distance: 150 km, Type: Ship
ID: 6, Distance: 180 km, Type: Aircraft
ID: 4, Distance: 200 km, Type: Unknown
```

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Implementasikan fungsi `int countNodesInRange(BSTNode* root, int low, int high)` yang menghitung jumlah node dengan nilai dalam range [low, high]!

**Penyelesaian:**

```cpp
int countNodesInRange(BSTNode* root, int low, int high) {
    // Base case
    if (root == nullptr) {
        return 0;
    }
    
    // Jika nilai di luar range kiri, tidak perlu cek left subtree
    if (root->data < low) {
        return countNodesInRange(root->right, low, high);
    }
    
    // Jika nilai di luar range kanan, tidak perlu cek right subtree
    if (root->data > high) {
        return countNodesInRange(root->left, low, high);
    }
    
    // Nilai dalam range: hitung 1 + rekursi ke kedua subtree
    return 1 + countNodesInRange(root->left, low, high) +
               countNodesInRange(root->right, low, high);
}
```

**Contoh penggunaan:**
```cpp
// BST: 20, 30, 40, 50, 60, 70, 80
// countNodesInRange(root, 30, 60) = 4 (yaitu: 30, 40, 50, 60)
```

**Kompleksitas:** O(h + k) dimana h = tinggi tree dan k = jumlah node dalam range.

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Soal:** Implementasikan fungsi `BSTNode* lowestCommonAncestor(BSTNode* root, int p, int q)` yang mencari Lowest Common Ancestor (LCA) dari dua node dalam BST!

**Penyelesaian:**

> **Lowest Common Ancestor (LCA)** dari dua node p dan q adalah node terdalam yang memiliki baik p maupun q sebagai descendant.

Memanfaatkan properti BST untuk mencari LCA secara efisien:

```cpp
BSTNode* lowestCommonAncestor(BSTNode* root, int p, int q) {
    if (root == nullptr) {
        return nullptr;
    }
    
    // Jika kedua nilai lebih kecil dari root, LCA ada di left subtree
    if (p < root->data && q < root->data) {
        return lowestCommonAncestor(root->left, p, q);
    }
    
    // Jika kedua nilai lebih besar dari root, LCA ada di right subtree
    if (p > root->data && q > root->data) {
        return lowestCommonAncestor(root->right, p, q);
    }
    
    // Jika p dan q berada di sisi berbeda (atau salah satu sama dengan root)
    // maka root adalah LCA
    return root;
}
```

**Contoh:**
```
        50
       /  \
      30   70
     / \   / \
    20 40 60  80

LCA(20, 40) = 30  (keduanya di subtree 30)
LCA(20, 60) = 50  (20 di kiri, 60 di kanan dari 50)
LCA(40, 50) = 50  (50 adalah ancestor dari 40)
```

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Implementasikan fungsi yang mengkonversi BST menjadi Doubly Linked List (DLL) terurut tanpa menggunakan space tambahan (selain pointer)!

**Penyelesaian:**

Konversi BST ke DLL dilakukan dengan **inorder traversal**, menghubungkan `left` sebagai `prev` dan `right` sebagai `next`.

```cpp
class BSTtoDLL {
private:
    BSTNode* head;   // Kepala DLL
    BSTNode* prev;   // Pointer ke node sebelumnya dalam inorder
    
    void convert(BSTNode* root) {
        if (root == nullptr) return;
        
        // Rekursi ke left subtree
        convert(root->left);
        
        // Process current node
        if (prev == nullptr) {
            // Node pertama menjadi head
            head = root;
        } else {
            // Hubungkan prev dengan current
            prev->right = root;
            root->left = prev;
        }
        prev = root;
        
        // Rekursi ke right subtree
        convert(root->right);
    }
    
public:
    BSTNode* convertBSTtoDLL(BSTNode* root) {
        head = nullptr;
        prev = nullptr;
        convert(root);
        return head;
    }
    
    void printDLL(BSTNode* head) {
        cout << "DLL (forward): ";
        BSTNode* current = head;
        BSTNode* last = nullptr;
        
        while (current != nullptr) {
            cout << current->data << " ";
            last = current;
            current = current->right;
        }
        cout << endl;
        
        cout << "DLL (backward): ";
        while (last != nullptr) {
            cout << last->data << " ";
            last = last->left;
        }
        cout << endl;
    }
};
```

**Ilustrasi:**
```
BST:
        4
       / \
      2   5
     / \
    1   3

Setelah konversi:
DLL: 1 <-> 2 <-> 3 <-> 4 <-> 5

Dimana:
- node->left = prev pointer
- node->right = next pointer
```

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan. Jawaban singkat tersedia di bagian akhir.

### Problem S1 ⭐
Gambarkan BST yang dihasilkan dari menyisipkan nilai: 45, 25, 65, 15, 35, 55, 75

### Problem S2 ⭐⭐
Pada BST di S1, tunjukkan langkah-langkah menghapus node 45 (root)!

### Problem S3 ⭐⭐
Tuliskan fungsi `int height(BSTNode* root)` yang menghitung tinggi BST!

### Problem S4 ⭐⭐⭐
Implementasikan fungsi `BSTNode* buildBalancedBST(int arr[], int start, int end)` yang membangun BST seimbang dari array terurut!

### Problem S5 ⭐⭐⭐
Jelaskan bagaimana AVL Tree menjaga keseimbangan dengan menggunakan rotasi!

---

## Ringkasan

| Konsep | Deskripsi | Kompleksitas |
|--------|-----------|--------------|
| **BST Property** | Left < Parent < Right untuk setiap node | - |
| **Search** | Memanfaatkan properti untuk eliminasi setengah tree | O(log n) avg, O(n) worst |
| **Insert** | Cari posisi null yang tepat, sisipkan node baru | O(log n) avg, O(n) worst |
| **Delete Leaf** | Hapus langsung | O(log n) avg |
| **Delete 1 Child** | Ganti dengan child | O(log n) avg |
| **Delete 2 Children** | Ganti dengan inorder successor/predecessor | O(log n) avg |
| **findMin** | Traverse ke left-most node | O(log n) avg, O(n) worst |
| **findMax** | Traverse ke right-most node | O(log n) avg, O(n) worst |
| **Inorder Traversal** | Menghasilkan elemen terurut ascending | O(n) |
| **Balanced BST** | Self-balancing (AVL, Red-Black) menjamin O(log n) | O(log n) guaranteed |

---

## Jawaban Supplementary Problems

**SP-1:** 
```
        45
       /  \
      25   65
     / \   / \
    15 35 55  75
```

**SP-2:**
1. Cari inorder successor dari 45 = findMin(right subtree) = 55
2. Copy 55 ke posisi root
3. Hapus node 55 dari right subtree (leaf)
4. Hasil: root = 55

**SP-3:**
```cpp
int height(BSTNode* root) {
    if (root == nullptr) return -1;  // atau 0, tergantung definisi
    return 1 + max(height(root->left), height(root->right));
}
```

**SP-4:**
```cpp
BSTNode* buildBalancedBST(int arr[], int start, int end) {
    if (start > end) return nullptr;
    
    int mid = (start + end) / 2;
    BSTNode* root = new BSTNode(arr[mid]);
    
    root->left = buildBalancedBST(arr, start, mid - 1);
    root->right = buildBalancedBST(arr, mid + 1, end);
    
    return root;
}
```

**SP-5:**
AVL Tree menjaga keseimbangan dengan:
- Balance factor = height(left) - height(right)
- Harus selalu -1, 0, atau +1 untuk setiap node
- Jika melanggar, lakukan rotasi:
  - Single right rotation (LL case)
  - Single left rotation (RR case)
  - Left-Right rotation (LR case)
  - Right-Left rotation (RL case)

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 12.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 4.3.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 11.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
