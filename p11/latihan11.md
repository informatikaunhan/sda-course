# Latihan Mandiri 11: Tree dan Binary Tree

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 11  
**Topik:** Tree dan Binary Tree  
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
Manakah pernyataan yang **BENAR** tentang struktur data Tree?

A. Tree adalah struktur data linear seperti array dan linked list  
B. Setiap node dalam tree dapat memiliki maksimal satu child  
C. Tree adalah struktur data non-linear hierarkis dengan satu root  
D. Tree harus selalu memiliki minimal dua level  
E. Semua node dalam tree harus memiliki jumlah child yang sama  

### Soal 2
Perhatikan tree berikut:
```
        A
       /|\
      B C D
     /|   |
    E F   G
```
Berapakah **height** dari tree di atas?

A. 1  
B. 2  
C. 3  
D. 4  
E. 7  

### Soal 3
Pada tree di Soal 2, node manakah yang merupakan **sibling** dari node C?

A. A dan D  
B. B dan D  
C. E dan F  
D. E, F, dan G  
E. Hanya G  

### Soal 4
Manakah yang **BUKAN** merupakan properti dari Binary Tree?

A. Setiap node memiliki maksimal 2 child  
B. Child dibedakan menjadi left child dan right child  
C. Setiap node harus memiliki tepat 2 child  
D. Dapat direpresentasikan dengan linked structure atau array  
E. Subtree kiri dan kanan juga merupakan binary tree  

### Soal 5
Pada **Full Binary Tree**, pernyataan manakah yang BENAR?

A. Semua level terisi penuh  
B. Setiap node memiliki 0 atau 2 child  
C. Semua leaf berada di level yang sama  
D. Jumlah node harus ganjil  
E. Tidak boleh memiliki leaf node  

### Soal 6
Sebuah **Perfect Binary Tree** dengan height h = 3 memiliki berapa node?

A. 7  
B. 8  
C. 15  
D. 16  
E. 31  

### Soal 7
Perhatikan binary tree berikut:
```
        10
       /  \
      5    15
     / \     \
    3   7    20
```
Hasil traversal **Inorder** dari tree di atas adalah:

A. 10, 5, 3, 7, 15, 20  
B. 3, 5, 7, 10, 15, 20  
C. 3, 7, 5, 20, 15, 10  
D. 10, 5, 15, 3, 7, 20  
E. 20, 15, 7, 3, 5, 10  

### Soal 8
Pada binary tree di Soal 7, hasil traversal **Preorder** adalah:

A. 10, 5, 3, 7, 15, 20  
B. 3, 5, 7, 10, 15, 20  
C. 3, 7, 5, 20, 15, 10  
D. 10, 5, 15, 3, 7, 20  
E. 20, 15, 10, 7, 5, 3  

### Soal 9
Pada binary tree di Soal 7, hasil traversal **Postorder** adalah:

A. 10, 5, 3, 7, 15, 20  
B. 3, 5, 7, 10, 15, 20  
C. 3, 7, 5, 20, 15, 10  
D. 10, 5, 15, 3, 7, 20  
E. 20, 7, 3, 15, 5, 10  

### Soal 10
Traversal manakah yang menggunakan **Queue** sebagai struktur data bantu?

A. Preorder  
B. Inorder  
C. Postorder  
D. Level-order  
E. Semua traversal di atas  

### Soal 11
Perhatikan kode berikut:
```cpp
void mystery(Node* node) {
    if (node == nullptr) return;
    mystery(node->left);
    cout << node->data << " ";
    mystery(node->right);
}
```
Kode di atas merupakan implementasi traversal:

A. Preorder  
B. Inorder  
C. Postorder  
D. Level-order  
E. Reverse order  

### Soal 12
Jika sebuah binary tree direpresentasikan dalam array dengan root di index 0, maka untuk node di index `i`, di manakah **left child** berada?

A. `i + 1`  
B. `i * 2`  
C. `2 * i + 1`  
D. `2 * i + 2`  
E. `(i - 1) / 2`  

### Soal 13
Pada representasi array binary tree, jika node berada di index `i`, di manakah **parent** node tersebut?

A. `i - 1`  
B. `i / 2`  
C. `(i - 1) / 2`  
D. `2 * i`  
E. `i + 1`  

### Soal 14
Manakah pernyataan yang BENAR tentang **Expression Tree**?

A. Leaf node berisi operator  
B. Internal node berisi operand  
C. Inorder traversal menghasilkan notasi prefix  
D. Postorder traversal menghasilkan notasi postfix  
E. Expression tree hanya untuk operasi aritmatika sederhana  

### Soal 15
Untuk expression tree dari ekspresi `(3 + 5) * 2`, hasil traversal **Preorder** adalah:

A. 3 5 + 2 *  
B. * + 3 5 2  
C. 3 + 5 * 2  
D. 2 * 3 + 5  
E. + 3 5 * 2  

### Soal 16
Perhatikan binary tree berikut:
```
        1
       / \
      2   3
     /   / \
    4   5   6
```
Hasil traversal **Level-order** adalah:

A. 1, 2, 3, 4, 5, 6  
B. 4, 2, 1, 5, 3, 6  
C. 4, 2, 5, 6, 3, 1  
D. 1, 2, 4, 3, 5, 6  
E. 6, 5, 3, 4, 2, 1  

### Soal 17
Apa kompleksitas waktu untuk traversal pada binary tree dengan n node?

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

### Soal 18
Manakah jenis binary tree yang paling cocok untuk representasi array tanpa pemborosan memori?

A. Skewed Tree  
B. Full Binary Tree  
C. Complete Binary Tree  
D. Binary Search Tree  
E. Expression Tree  

### Soal 19
Pada iterative preorder traversal, struktur data apa yang digunakan?

A. Queue  
B. Stack  
C. Linked List  
D. Array  
E. Hash Table  

### Soal 20
Sebuah binary tree memiliki 7 leaf node. Jika tree tersebut adalah **Full Binary Tree**, berapa jumlah internal node?

A. 5  
B. 6  
C. 7  
D. 8  
E. 14  

---

## Bagian B: Soal Uraian (8 Soal)

### Soal 1 (5 poin) — Mudah
Jelaskan perbedaan antara terminologi berikut dalam konteks Tree:
a. Root dan Leaf
b. Parent dan Child
c. Depth dan Height
d. Sibling dan Ancestor

### Soal 2 (5 poin) — Mudah
Perhatikan binary tree berikut:
```
          A
         / \
        B   C
       / \   \
      D   E   F
         / \
        G   H
```
Tentukan:
a. Root node
b. Semua leaf node
c. Height dari tree
d. Depth dari node E
e. Sibling dari node B

### Soal 3 (5 poin) — Mudah
Jelaskan perbedaan antara empat jenis binary tree berikut dan berikan contoh sederhana untuk masing-masing:
a. Full Binary Tree
b. Complete Binary Tree
c. Perfect Binary Tree
d. Skewed Binary Tree

### Soal 4 (6 poin) — Sedang
Perhatikan binary tree berikut:
```
          50
         /  \
       30    70
      /  \   /  \
    20   40 60   80
```
Tuliskan hasil dari keempat jenis traversal:
a. Preorder
b. Inorder
c. Postorder
d. Level-order

Sertakan juga urutan kunjungan dengan penjelasan singkat untuk masing-masing traversal.

### Soal 5 (6 poin) — Sedang
Implementasikan fungsi C++ untuk **Postorder Traversal** secara:
a. Rekursif
b. Iteratif (menggunakan dua stack atau satu stack)

Sertakan penjelasan algoritma untuk masing-masing implementasi.

### Soal 6 (6 poin) — Sedang
Diberikan representasi binary tree dalam array berikut:
```
Index:   0   1   2   3   4   5   6
Array: [10, 20, 30, 40, 50, 60, 70]
```
a. Gambarkan binary tree yang direpresentasikan
b. Tentukan parent dari node di index 5
c. Tentukan left child dan right child dari node di index 2
d. Tuliskan hasil inorder traversal

### Soal 7 (6 poin) — Sedang
Buatlah Expression Tree untuk ekspresi matematika berikut:
`(a + b) * (c - d) / e`

Kemudian tentukan:
a. Gambar expression tree-nya
b. Hasil Preorder traversal (notasi prefix)
c. Hasil Postorder traversal (notasi postfix)

### Soal 8 (6 poin) — Sulit
Implementasikan class `BinaryTree` dalam C++ yang memiliki:
a. Struct Node dengan data, left pointer, dan right pointer
b. Constructor dan Destructor (dengan proper memory management)
c. Method `void insert(int data)` untuk menambah node secara level-order
d. Method `int countNodes()` untuk menghitung jumlah node
e. Method `int height()` untuk menghitung height tree

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Klasifikasi Ancaman Udara (7 poin)

**Latar Belakang:**
Komando Pertahanan Udara memerlukan sistem klasifikasi cepat untuk mengidentifikasi objek yang terdeteksi radar. Sistem menggunakan Decision Tree dengan kriteria bertingkat untuk mengklasifikasikan objek menjadi: Pesawat Tempur Musuh, Pesawat Komersial, Drone, Rudal, atau Unknown.

**Kriteria Klasifikasi:**
- Kecepatan: < 200 km/jam (Lambat), 200-800 km/jam (Sedang), > 800 km/jam (Cepat)
- Ketinggian: < 1000m (Rendah), 1000-10000m (Sedang), > 10000m (Tinggi)
- Ukuran radar cross-section: Kecil, Sedang, Besar
- Pola terbang: Linear, Manuver

**Tugas:**
a. **(2 poin)** Rancang Decision Tree untuk klasifikasi objek udara berdasarkan kriteria di atas. Gambarkan tree-nya dengan jelas.

b. **(2 poin)** Implementasikan struct `ObjekUdara` dan struct `DecisionNode` yang sesuai untuk sistem ini.

c. **(3 poin)** Implementasikan fungsi `string klasifikasi(DecisionNode* root, ObjekUdara obj)` yang melakukan traversal pada decision tree untuk mengklasifikasikan objek.

---

### Studi Kasus 2: Struktur Komando Militer (8 poin)

**Latar Belakang:**
Sistem informasi pertahanan memerlukan representasi hierarki komando militer yang efisien. Struktur dimulai dari Panglima TNI, kemudian Kepala Staf Angkatan (AD, AL, AU), dan seterusnya hingga level satuan terkecil. Sistem harus dapat:
- Menampilkan seluruh rantai komando dari atas ke bawah
- Mencari unit berdasarkan nama
- Menghitung jumlah personel di bawah suatu komando

**Tugas:**
a. **(2 poin)** Jelaskan mengapa struktur Tree lebih cocok daripada struktur linear untuk merepresentasikan hierarki komando militer.

b. **(3 poin)** Rancang ADT `HierarkiKomando` lengkap dengan:
   - Struktur Node yang menyimpan: nama unit, pangkat komandan, jumlah personel, dan pointer ke bawahan
   - Operasi-operasi yang diperlukan
   - Batasan/aturan

c. **(3 poin)** Implementasikan fungsi-fungsi berikut:
   - `void tampilkanStruktur(KomandoNode* root, int level)` — menampilkan hierarki dengan indentasi
   - `int totalPersonel(KomandoNode* root)` — menghitung total personel di bawah suatu komando (termasuk bawahan)

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | C | Tree adalah struktur non-linear hierarkis dengan satu root |
| 2 | B | Height = 2 (dari root A ke level terbawah E/F/G) |
| 3 | B | Sibling C adalah B dan D (sama-sama child dari A) |
| 4 | C | Binary tree MAKSIMAL 2 child, tidak harus tepat 2 |
| 5 | B | Full binary tree: setiap node punya 0 atau 2 child |
| 6 | C | Perfect binary tree h=3: 2^(h+1) - 1 = 2^4 - 1 = 15 |
| 7 | B | Inorder (LNR): 3, 5, 7, 10, 15, 20 |
| 8 | A | Preorder (NLR): 10, 5, 3, 7, 15, 20 |
| 9 | C | Postorder (LRN): 3, 7, 5, 20, 15, 10 |
| 10 | D | Level-order menggunakan Queue (BFS) |
| 11 | B | Pola Left-Node-Right adalah Inorder |
| 12 | C | Left child di index 2*i + 1 |
| 13 | C | Parent di index (i-1)/2 |
| 14 | D | Postorder traversal = notasi postfix |
| 15 | B | Preorder (prefix): * + 3 5 2 |
| 16 | A | Level-order: 1, 2, 3, 4, 5, 6 |
| 17 | C | Traversal mengunjungi setiap node sekali = O(n) |
| 18 | C | Complete binary tree optimal untuk array |
| 19 | B | Iterative preorder menggunakan Stack |
| 20 | B | Full binary tree: internal = leaf - 1 = 7 - 1 = 6 |

---

### Bagian B: Soal Uraian

#### Jawaban Soal 1

**a. Root dan Leaf:**
- **Root**: Node paling atas dalam tree, tidak memiliki parent. Hanya ada satu root dalam setiap tree.
- **Leaf**: Node yang tidak memiliki child (node terminal). Bisa ada banyak leaf dalam satu tree.

**b. Parent dan Child:**
- **Parent**: Node yang memiliki satu atau lebih node di bawahnya (child).
- **Child**: Node yang terhubung langsung di bawah node lain (parent-nya).

**c. Depth dan Height:**
- **Depth**: Jarak dari root ke node tertentu (jumlah edge). Root memiliki depth 0.
- **Height**: Jarak terpanjang dari node ke leaf terjauh di bawahnya. Height tree = height root.

**d. Sibling dan Ancestor:**
- **Sibling**: Node-node yang memiliki parent yang sama.
- **Ancestor**: Semua node pada path dari root ke node tertentu (tidak termasuk node itu sendiri).

---

#### Jawaban Soal 2

```
          A          (depth 0)
         / \
        B   C        (depth 1)
       / \   \
      D   E   F      (depth 2)
         / \
        G   H        (depth 3)
```

**a. Root node:** A

**b. Semua leaf node:** D, G, H, F

**c. Height dari tree:** 3 (path terpanjang A → B → E → G atau A → B → E → H)

**d. Depth dari node E:** 2 (path A → B → E = 2 edge)

**e. Sibling dari node B:** C (keduanya adalah child dari A)

---

#### Jawaban Soal 3

**a. Full Binary Tree:**
- Setiap node memiliki **0 atau 2** child
- Tidak ada node dengan hanya 1 child
```
      1
     / \
    2   3
   / \
  4   5
```

**b. Complete Binary Tree:**
- Semua level terisi penuh **kecuali level terakhir**
- Level terakhir terisi dari **kiri ke kanan**
```
      1
     / \
    2   3
   / \  /
  4   5 6
```

**c. Perfect Binary Tree:**
- Semua internal node memiliki **tepat 2** child
- Semua leaf berada di **level yang sama**
```
      1
     / \
    2   3
   / \ / \
  4  5 6  7
```

**d. Skewed Binary Tree:**
- Semua node hanya memiliki **satu child** (kiri semua atau kanan semua)
- Mirip linked list
```
  1
   \
    2
     \
      3
       \
        4
```

---

#### Jawaban Soal 4

```
          50
         /  \
       30    70
      /  \   /  \
    20   40 60   80
```

**a. Preorder (Node-Left-Right):**
```
50 → 30 → 20 → 40 → 70 → 60 → 80
```
Urutan: Kunjungi node, lalu subtree kiri, lalu subtree kanan.

**b. Inorder (Left-Node-Right):**
```
20 → 30 → 40 → 50 → 60 → 70 → 80
```
Urutan: Subtree kiri, kunjungi node, lalu subtree kanan. Hasilnya terurut ascending untuk BST.

**c. Postorder (Left-Right-Node):**
```
20 → 40 → 30 → 60 → 80 → 70 → 50
```
Urutan: Subtree kiri, subtree kanan, baru kunjungi node. Cocok untuk delete tree.

**d. Level-order (BFS):**
```
50 → 30 → 70 → 20 → 40 → 60 → 80
```
Urutan: Kunjungi per level dari atas ke bawah, kiri ke kanan.

---

#### Jawaban Soal 5

**a. Postorder Rekursif:**
```cpp
void postorderRekursif(Node* node) {
    if (node == nullptr) return;
    
    postorderRekursif(node->left);   // Traverse left subtree
    postorderRekursif(node->right);  // Traverse right subtree
    cout << node->data << " ";       // Visit node
}
```
**Penjelasan:** Rekursi mengikuti pola LRN (Left-Right-Node). Base case adalah node null.

**b. Postorder Iteratif (menggunakan dua stack):**
```cpp
void postorderIteratif(Node* root) {
    if (root == nullptr) return;
    
    stack<Node*> s1, s2;
    s1.push(root);
    
    // Traverse dalam urutan Node-Right-Left (kebalikan preorder mirror)
    while (!s1.empty()) {
        Node* node = s1.top();
        s1.pop();
        s2.push(node);  // Simpan di stack kedua
        
        if (node->left) s1.push(node->left);
        if (node->right) s1.push(node->right);
    }
    
    // Pop dari s2 menghasilkan urutan Left-Right-Node
    while (!s2.empty()) {
        cout << s2.top()->data << " ";
        s2.pop();
    }
}
```
**Penjelasan:** Stack pertama untuk traversal Node-Right-Left, stack kedua membalik urutan menjadi Left-Right-Node (postorder).

---

#### Jawaban Soal 6

**a. Gambar Binary Tree:**
```
Index:   0   1   2   3   4   5   6
Array: [10, 20, 30, 40, 50, 60, 70]

           10 (0)
          /     \
       20 (1)   30 (2)
       /  \     /  \
    40(3) 50(4) 60(5) 70(6)
```

**b. Parent dari node di index 5 (nilai 60):**
- Formula: parent(i) = (i - 1) / 2
- parent(5) = (5 - 1) / 2 = 4 / 2 = 2
- **Parent adalah node di index 2, yaitu nilai 30**

**c. Left child dan Right child dari node di index 2 (nilai 30):**
- Left child: 2 * i + 1 = 2 * 2 + 1 = 5 → **nilai 60**
- Right child: 2 * i + 2 = 2 * 2 + 2 = 6 → **nilai 70**

**d. Hasil Inorder Traversal (Left-Node-Right):**
```
40, 20, 50, 10, 60, 30, 70
```

---

#### Jawaban Soal 7

**Ekspresi:** `(a + b) * (c - d) / e`

**a. Expression Tree:**
```
           /
          / \
         *   e
        / \
       +   -
      / \ / \
     a  b c  d
```

**b. Preorder Traversal (Notasi Prefix):**
```
/ * + a b - c d e
```
Dibaca: Divide hasil dari (multiply hasil dari (add a b) dengan (subtract c d)) dengan e

**c. Postorder Traversal (Notasi Postfix):**
```
a b + c d - * e /
```
Dibaca: Push a, push b, add; push c, push d, subtract; multiply; push e, divide

---

#### Jawaban Soal 8

```cpp
#include <iostream>
#include <queue>
using namespace std;

// a. Struct Node
struct Node {
    int data;
    Node* left;
    Node* right;
    
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

class BinaryTree {
private:
    Node* root;
    
    // Helper untuk destructor
    void deleteTree(Node* node) {
        if (node == nullptr) return;
        deleteTree(node->left);
        deleteTree(node->right);
        delete node;
    }
    
    // Helper untuk countNodes
    int countNodesHelper(Node* node) {
        if (node == nullptr) return 0;
        return 1 + countNodesHelper(node->left) + countNodesHelper(node->right);
    }
    
    // Helper untuk height
    int heightHelper(Node* node) {
        if (node == nullptr) return -1;  // Empty tree height = -1
        int leftHeight = heightHelper(node->left);
        int rightHeight = heightHelper(node->right);
        return 1 + max(leftHeight, rightHeight);
    }

public:
    // b. Constructor
    BinaryTree() : root(nullptr) {}
    
    // b. Destructor dengan proper memory management
    ~BinaryTree() {
        deleteTree(root);
    }
    
    // c. Insert secara level-order
    void insert(int data) {
        Node* newNode = new Node(data);
        
        if (root == nullptr) {
            root = newNode;
            return;
        }
        
        // BFS untuk menemukan posisi kosong pertama
        queue<Node*> q;
        q.push(root);
        
        while (!q.empty()) {
            Node* current = q.front();
            q.pop();
            
            if (current->left == nullptr) {
                current->left = newNode;
                return;
            } else {
                q.push(current->left);
            }
            
            if (current->right == nullptr) {
                current->right = newNode;
                return;
            } else {
                q.push(current->right);
            }
        }
    }
    
    // d. Count nodes
    int countNodes() {
        return countNodesHelper(root);
    }
    
    // e. Height
    int height() {
        return heightHelper(root);
    }
    
    // Getter untuk root (opsional)
    Node* getRoot() { return root; }
};

// Contoh penggunaan
int main() {
    BinaryTree tree;
    
    tree.insert(10);
    tree.insert(20);
    tree.insert(30);
    tree.insert(40);
    tree.insert(50);
    
    cout << "Jumlah node: " << tree.countNodes() << endl;  // Output: 5
    cout << "Height tree: " << tree.height() << endl;      // Output: 2
    
    return 0;
}
```

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Klasifikasi Ancaman Udara

**a. Decision Tree untuk Klasifikasi Objek Udara:**

```
                         [Kecepatan?]
                        /     |      \
                    <200   200-800   >800
                      |       |        |
               [Ketinggian?] [Ukuran?] [Pola?]
                /    \       /    \     /    \
            <1000   >1000  Kecil Besar Linear Manuver
              |       |      |     |     |      |
           [Ukuran?] [Pola?] Drone Pesawat RUDAL Pesawat
            /    \    |              Komersial    Tempur
         Kecil  Besar |                           Musuh
           |      |   |
         Drone  Unknown Pesawat
                        Komersial
```

**Logika Keputusan:**
1. Cepat (>800 km/jam) + Linear → Rudal
2. Cepat (>800 km/jam) + Manuver → Pesawat Tempur Musuh
3. Sedang (200-800 km/jam) + Ukuran Besar → Pesawat Komersial
4. Sedang + Ukuran Kecil → Drone
5. Lambat (<200 km/jam) + Rendah + Kecil → Drone
6. Lainnya → Unknown (perlu investigasi lebih lanjut)

**b. Implementasi Struct:**

```cpp
// Struct untuk objek yang terdeteksi radar
struct ObjekUdara {
    double kecepatan;       // km/jam
    double ketinggian;      // meter
    string ukuran;          // "Kecil", "Sedang", "Besar"
    string polaTerbang;     // "Linear", "Manuver"
    
    ObjekUdara(double kec, double ting, string uk, string pola)
        : kecepatan(kec), ketinggian(ting), ukuran(uk), polaTerbang(pola) {}
};

// Struct untuk node Decision Tree
struct DecisionNode {
    string kriteria;        // Nama kriteria: "kecepatan", "ketinggian", dll
    string klasifikasi;     // Jika leaf node, berisi hasil klasifikasi
    bool isLeaf;
    
    // Pointer ke child berdasarkan kondisi
    DecisionNode* kondisiRendah;   // < threshold
    DecisionNode* kondisiSedang;   // dalam range
    DecisionNode* kondisiTinggi;   // > threshold
    
    // Untuk kondisi non-numerik
    DecisionNode* kondisiKecil;
    DecisionNode* kondisiBesar;
    DecisionNode* kondisiLinear;
    DecisionNode* kondisiManuver;
    
    // Threshold untuk kondisi numerik
    double thresholdLow;
    double thresholdHigh;
    
    DecisionNode(string krit, bool leaf = false) 
        : kriteria(krit), isLeaf(leaf), 
          kondisiRendah(nullptr), kondisiSedang(nullptr), kondisiTinggi(nullptr),
          kondisiKecil(nullptr), kondisiBesar(nullptr),
          kondisiLinear(nullptr), kondisiManuver(nullptr) {}
};
```

**c. Fungsi Klasifikasi:**

```cpp
string klasifikasi(DecisionNode* node, ObjekUdara obj) {
    // Base case: leaf node
    if (node == nullptr) return "UNKNOWN";
    if (node->isLeaf) return node->klasifikasi;
    
    // Evaluasi berdasarkan kriteria
    if (node->kriteria == "kecepatan") {
        if (obj.kecepatan < 200) {
            return klasifikasi(node->kondisiRendah, obj);
        } else if (obj.kecepatan <= 800) {
            return klasifikasi(node->kondisiSedang, obj);
        } else {
            return klasifikasi(node->kondisiTinggi, obj);
        }
    }
    else if (node->kriteria == "ketinggian") {
        if (obj.ketinggian < 1000) {
            return klasifikasi(node->kondisiRendah, obj);
        } else if (obj.ketinggian <= 10000) {
            return klasifikasi(node->kondisiSedang, obj);
        } else {
            return klasifikasi(node->kondisiTinggi, obj);
        }
    }
    else if (node->kriteria == "ukuran") {
        if (obj.ukuran == "Kecil") {
            return klasifikasi(node->kondisiKecil, obj);
        } else {
            return klasifikasi(node->kondisiBesar, obj);
        }
    }
    else if (node->kriteria == "pola") {
        if (obj.polaTerbang == "Linear") {
            return klasifikasi(node->kondisiLinear, obj);
        } else {
            return klasifikasi(node->kondisiManuver, obj);
        }
    }
    
    return "UNKNOWN";
}

// Contoh penggunaan
int main() {
    // Build decision tree (simplified)
    DecisionNode* root = new DecisionNode("kecepatan");
    
    // ... (build tree structure) ...
    
    // Test klasifikasi
    ObjekUdara obj1(900, 5000, "Kecil", "Linear");
    cout << "Klasifikasi: " << klasifikasi(root, obj1) << endl;
    // Expected: RUDAL
    
    return 0;
}
```

---

#### Studi Kasus 2: Struktur Komando Militer

**a. Alasan Tree lebih cocok dari struktur linear:**

1. **Hierarki Alami**: Struktur komando militer bersifat hierarkis — satu atasan membawahi beberapa bawahan, yang masing-masing juga membawahi bawahan. Tree merepresentasikan hubungan parent-child ini secara natural.

2. **Multiple Children**: Satu komandan dapat memiliki banyak unit bawahan. Array/Linked List hanya merepresentasikan hubungan sekuensial, tidak cocok untuk one-to-many relationship.

3. **Efisiensi Operasi**: 
   - Mencari rantai komando (ancestor) = O(height)
   - Mencari semua bawahan = O(subtree size)
   - Jika linear, mencari hubungan hierarki memerlukan O(n) dengan logika kompleks

4. **Representasi Visual**: Tree langsung menggambarkan struktur organisasi yang mudah dipahami.

**b. ADT HierarkiKomando:**

```
ADT HierarkiKomando:

  Data:
    - Struktur Node:
      * namaUnit: string (contoh: "Kodam Jaya")
      * pangkatKomandan: string (contoh: "Mayor Jenderal")
      * jumlahPersonel: integer (personel langsung di unit ini)
      * children: list of KomandoNode* (unit-unit bawahan)
    
    - root: pointer ke Panglima TNI
    - totalUnit: integer
    
  Operasi:
    - insertUnit(parentName, unitData): Menambah unit bawahan
    - removeUnit(unitName): Menghapus unit beserta semua bawahan
    - findUnit(unitName): Mencari unit berdasarkan nama
    - getRantaiKomando(unitName): Mendapatkan path dari root ke unit
    - totalPersonel(unitName): Menghitung total personel (termasuk bawahan)
    - tampilkanStruktur(): Menampilkan seluruh hierarki
    - hitungKedalaman(unitName): Menghitung level unit dari root
    
  Batasan/Aturan:
    - Harus ada tepat satu root (Panglima TNI)
    - Setiap unit hanya memiliki satu parent (satu atasan langsung)
    - Nama unit harus unik
    - Jumlah personel tidak boleh negatif
    - Penghapusan unit juga menghapus seluruh unit bawahan
```

**c. Implementasi Fungsi:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct KomandoNode {
    string namaUnit;
    string pangkatKomandan;
    int jumlahPersonel;
    vector<KomandoNode*> bawahan;
    
    KomandoNode(string nama, string pangkat, int personel)
        : namaUnit(nama), pangkatKomandan(pangkat), jumlahPersonel(personel) {}
};

// Fungsi 1: Menampilkan struktur dengan indentasi
void tampilkanStruktur(KomandoNode* node, int level) {
    if (node == nullptr) return;
    
    // Buat indentasi sesuai level
    string indent = "";
    for (int i = 0; i < level; i++) {
        indent += "    ";  // 4 spasi per level
    }
    
    // Tambahkan connector untuk visualisasi
    string connector = (level > 0) ? "|-- " : "";
    
    // Tampilkan node saat ini
    cout << indent << connector << node->namaUnit 
         << " (" << node->pangkatKomandan << ")"
         << " [" << node->jumlahPersonel << " personel]" << endl;
    
    // Rekursif untuk semua bawahan
    for (KomandoNode* child : node->bawahan) {
        tampilkanStruktur(child, level + 1);
    }
}

// Fungsi 2: Menghitung total personel (termasuk bawahan rekursif)
int totalPersonel(KomandoNode* node) {
    if (node == nullptr) return 0;
    
    // Mulai dari personel di unit ini
    int total = node->jumlahPersonel;
    
    // Tambahkan personel dari semua bawahan secara rekursif
    for (KomandoNode* child : node->bawahan) {
        total += totalPersonel(child);
    }
    
    return total;
}

// Contoh penggunaan
int main() {
    // Buat struktur komando sederhana
    KomandoNode* panglima = new KomandoNode("Mabes TNI", "Jenderal", 500);
    
    KomandoNode* tniAD = new KomandoNode("TNI AD", "Jenderal", 300);
    KomandoNode* tniAL = new KomandoNode("TNI AL", "Laksamana", 200);
    KomandoNode* tniAU = new KomandoNode("TNI AU", "Marsekal", 150);
    
    panglima->bawahan.push_back(tniAD);
    panglima->bawahan.push_back(tniAL);
    panglima->bawahan.push_back(tniAU);
    
    KomandoNode* kodam = new KomandoNode("Kodam Jaya", "Mayjen", 5000);
    KomandoNode* kopassus = new KomandoNode("Kopassus", "Mayjen", 3000);
    tniAD->bawahan.push_back(kodam);
    tniAD->bawahan.push_back(kopassus);
    
    KomandoNode* brigif = new KomandoNode("Brigif 1", "Brigjen", 2000);
    kodam->bawahan.push_back(brigif);
    
    // Tampilkan struktur
    cout << "=== STRUKTUR KOMANDO TNI ===" << endl;
    tampilkanStruktur(panglima, 0);
    
    cout << "\n=== TOTAL PERSONEL ===" << endl;
    cout << "Total personel Mabes TNI: " << totalPersonel(panglima) << endl;
    cout << "Total personel TNI AD: " << totalPersonel(tniAD) << endl;
    cout << "Total personel Kodam Jaya: " << totalPersonel(kodam) << endl;
    
    return 0;
}
```

**Output:**
```
=== STRUKTUR KOMANDO TNI ===
Mabes TNI (Jenderal) [500 personel]
    |-- TNI AD (Jenderal) [300 personel]
        |-- Kodam Jaya (Mayjen) [5000 personel]
            |-- Brigif 1 (Brigjen) [2000 personel]
        |-- Kopassus (Mayjen) [3000 personel]
    |-- TNI AL (Laksamana) [200 personel]
    |-- TNI AU (Marsekal) [150 personel]

=== TOTAL PERSONEL ===
Total personel Mabes TNI: 11150
Total personel TNI AD: 10300
Total personel Kodam Jaya: 7000
```

---

## Kriteria Penilaian

| Bagian | Jumlah Soal | Poin per Soal | Total |
|--------|-------------|---------------|-------|
| Pilihan Ganda | 20 | 2 | 40 |
| Uraian | 8 | Bervariasi (5-6) | 45 |
| Studi Kasus | 2 | Bervariasi (7-8) | 15 |
| **Total** | | | **100** |

---

## Catatan untuk Pengajar

- Soal-soal mencakup semua Sub-CPMK untuk Pertemuan 11 (Sub-CPMK-5.1)
- Materi yang diuji meliputi:
  - Terminologi tree (root, node, parent, child, sibling, leaf, height, depth, level)
  - Jenis-jenis binary tree (full, complete, perfect, skewed)
  - Representasi binary tree (linked structure dan array)
  - Empat jenis traversal (preorder, inorder, postorder, level-order)
  - Expression tree
  - Aplikasi tree dalam konteks pertahanan
- Studi kasus dirancang dengan konteks pertahanan Indonesia yang relevan
- Tingkat kesulitan bervariasi: Mudah (30%), Sedang (50%), Sulit (20%)

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
