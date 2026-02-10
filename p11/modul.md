# Modul 11: Tree dan Binary Tree

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 11  
**Topik:** Tree dan Binary Tree

> **Capaian Pembelajaran:** Sub-CPMK-5.1 — Mampu mengimplementasikan tree dan binary tree beserta algoritma traversal

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.12 (intro); Weiss Ch.4; Hubbard Ch.9-10

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** terminologi dan konsep dasar tree dengan tepat
2. **Mengidentifikasi** jenis-jenis binary tree (full, complete, perfect, skewed)
3. **Membandingkan** representasi binary tree menggunakan linked structure dan array
4. **Mengimplementasikan** struktur binary tree dalam C++
5. **Menerapkan** algoritma traversal: preorder, inorder, postorder (rekursif dan iteratif)
6. **Mengimplementasikan** level-order traversal menggunakan queue (BFS)
7. **Membangun** expression tree dan memahami aplikasi tree dalam sistem pertahanan

---

## 1. Pengantar Struktur Data Tree

### 1.1 Apa itu Tree?

> **Definisi:** Tree adalah struktur data non-linear yang terdiri dari node-node yang terhubung secara hierarkis. Setiap tree memiliki satu node khusus yang disebut **root** (akar), dan setiap node dapat memiliki nol atau lebih **child** (anak).

Berbeda dengan struktur data linear seperti array, linked list, stack, dan queue yang telah kita pelajari sebelumnya, tree memungkinkan hubungan hierarkis antar data. Struktur ini sangat natural untuk merepresentasikan data yang memiliki hubungan "parent-child" atau data yang bersifat hierarkis.

### 1.2 Mengapa Mempelajari Tree?

Tree memiliki banyak aplikasi penting dalam ilmu komputer dan sistem pertahanan:

| Aplikasi | Contoh Penggunaan |
|----------|-------------------|
| **File System** | Struktur folder dan file dalam komputer |
| **Database** | B-Tree dan B+Tree untuk indexing |
| **Struktur Organisasi** | Hierarki komando militer |
| **Parsing** | Syntax tree untuk compiler |
| **Decision Making** | Decision tree untuk analisis taktis |
| **Networking** | Spanning tree untuk routing |
| **AI/ML** | Decision tree classifier |

### 1.3 Tree vs Struktur Data Lainnya

| Aspek | Array/List | Tree |
|-------|------------|------|
| **Struktur** | Linear | Hierarkis (non-linear) |
| **Akses** | Sequential atau random | Traversal dari root |
| **Hubungan** | Predecessor-successor | Parent-child |
| **Searching** | O(n) untuk unsorted | O(log n) untuk BST seimbang |
| **Representasi** | Flat | Berlevel |

---

## 2. Terminologi Tree

### 2.1 Komponen Dasar Tree

![Terminologi Tree](images/gambar-11-1.png)

*Gambar 11.1: Terminologi dasar struktur data tree*

### 2.2 Definisi Terminologi

| Istilah | Definisi |
|---------|----------|
| **Node** | Elemen dasar tree yang menyimpan data |
| **Root** | Node paling atas tanpa parent |
| **Edge** | Garis penghubung antara dua node |
| **Parent** | Node yang memiliki child di bawahnya |
| **Child** | Node yang memiliki parent di atasnya |
| **Sibling** | Node-node yang memiliki parent yang sama |
| **Leaf** | Node tanpa child (node terminal) |
| **Internal Node** | Node yang bukan leaf (memiliki minimal satu child) |
| **Subtree** | Tree yang terdiri dari suatu node dan semua descendant-nya |
| **Ancestor** | Node pada path dari root ke suatu node |
| **Descendant** | Node yang berada di subtree suatu node |

### 2.3 Properti Ukuran Tree

| Properti | Definisi | Cara Menghitung |
|----------|----------|-----------------|
| **Depth (Kedalaman)** | Jumlah edge dari root ke suatu node | Depth root = 0 |
| **Height (Tinggi)** | Jumlah edge pada path terpanjang dari node ke leaf | Height leaf = 0 |
| **Level** | Semua node dengan depth yang sama | Level = Depth |
| **Degree** | Jumlah child dari suatu node | Hitung langsung |
| **Size** | Total jumlah node dalam tree | Hitung semua node |

> **Catatan Penting:** Dalam beberapa literatur, height dan depth dihitung berdasarkan jumlah node, bukan edge. Dalam modul ini, kita menggunakan konvensi edge-based yang lebih umum.

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Perhatikan tree berikut:

```
        A
       /|\
      B C D
     /|   |
    E F   G
        / \
       H   I
```

Tentukan: (a) root, (b) leaves, (c) internal nodes, (d) siblings dari F, (e) ancestors dari H, (f) descendants dari D!

**Penyelesaian:**

a) **Root**: A (node paling atas tanpa parent)

b) **Leaves**: E, F, H, I (node tanpa child)

c) **Internal nodes**: A, B, C, D, G (node yang memiliki minimal satu child)
   - A memiliki child B, C, D
   - B memiliki child E, F
   - D memiliki child G
   - G memiliki child H, I
   - C tidak memiliki child, jadi C adalah leaf, bukan internal node
   
   **Koreksi**: Internal nodes adalah A, B, D, G. C adalah leaf.

d) **Siblings dari F**: E (keduanya memiliki parent yang sama yaitu B)

e) **Ancestors dari H**: G, D, A (semua node pada path dari root ke H)

f) **Descendants dari D**: G, H, I (semua node di subtree D)

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Hitung depth dan height dari setiap node dalam tree berikut:

```
        1
       / \
      2   3
     /   / \
    4   5   6
           / \
          7   8
```

**Penyelesaian:**

| Node | Depth | Height |
|------|-------|--------|
| 1 (Root) | 0 | 3 |
| 2 | 1 | 1 |
| 3 | 1 | 2 |
| 4 | 2 | 0 |
| 5 | 2 | 0 |
| 6 | 2 | 1 |
| 7 | 3 | 0 |
| 8 | 3 | 0 |

**Penjelasan:**
- **Depth** dihitung dari root: depth(node) = jumlah edge dari root ke node
- **Height** dihitung dari leaf: height(node) = jumlah edge pada path terpanjang dari node ke leaf
- Height tree = height(root) = 3

---

## 3. Binary Tree

### 3.1 Definisi Binary Tree

> **Definisi:** Binary Tree adalah tree di mana setiap node memiliki **paling banyak dua child**, yang disebut **left child** dan **right child**.

Binary tree adalah struktur tree yang paling banyak dipelajari dan digunakan karena:
- Struktur sederhana dan mudah diimplementasikan
- Banyak algoritma efisien yang memanfaatkan sifat binary
- Menjadi dasar untuk struktur data lanjut (BST, AVL, Red-Black Tree, Heap)

### 3.2 Properti Matematis Binary Tree

Untuk binary tree dengan height `h`:

| Properti | Formula | Keterangan |
|----------|---------|------------|
| Minimum nodes | h + 1 | Skewed tree |
| Maximum nodes | 2^(h+1) - 1 | Perfect binary tree |
| Minimum height | ⌈log₂(n+1)⌉ - 1 | Perfect/complete tree |
| Maximum height | n - 1 | Skewed tree |
| Jumlah leaf (max) | 2^h | Di level terakhir |
| Total edge | n - 1 | Untuk n nodes |

### 3.3 Jenis-Jenis Binary Tree

![Jenis-Jenis Binary Tree](images/gambar-11-2.png)

*Gambar 11.2: Empat jenis binary tree — Full, Complete, Perfect, dan Skewed*

#### 3.3.1 Full Binary Tree

> **Definisi:** Binary tree di mana setiap node memiliki **0 atau 2 child** (tidak ada node dengan hanya 1 child).

Properti:
- Jika ada n nodes, maka jumlah leaf = (n + 1) / 2
- Jumlah internal nodes = (n - 1) / 2

#### 3.3.2 Complete Binary Tree

> **Definisi:** Binary tree di mana semua level terisi penuh kecuali mungkin level terakhir, dan node di level terakhir terisi dari **kiri ke kanan**.

Properti:
- Height minimum untuk n nodes
- Dapat direpresentasikan efisien dengan array
- Heap adalah complete binary tree

#### 3.3.3 Perfect Binary Tree

> **Definisi:** Binary tree di mana semua internal node memiliki **tepat 2 child** dan semua leaf berada pada **level yang sama**.

Properti:
- Jumlah nodes = 2^(h+1) - 1
- Jumlah leaf = 2^h
- Perfect binary tree adalah full dan complete

#### 3.3.4 Skewed Binary Tree

> **Definisi:** Binary tree di mana setiap node hanya memiliki **satu child** (left-skewed atau right-skewed).

Properti:
- Height = n - 1 (worst case)
- Mirip dengan linked list
- Tidak efisien untuk searching

---

### SOLVED PROBLEM 3 ⭐

**Soal:** Klasifikasikan tree berikut ke dalam jenis binary tree yang sesuai:

Tree A:
```
      1
     / \
    2   3
   / \
  4   5
```

Tree B:
```
      1
     / \
    2   3
   / \ / \
  4  5 6  7
```

Tree C:
```
      1
       \
        2
         \
          3
```

**Penyelesaian:**

**Tree A:**
- Full Binary Tree? Ya (setiap node memiliki 0 atau 2 child)
- Complete Binary Tree? Ya (semua level terisi, level terakhir dari kiri)
- Perfect Binary Tree? Tidak (leaf tidak pada level yang sama)
- **Klasifikasi:** Full dan Complete Binary Tree

**Tree B:**
- Full Binary Tree? Ya
- Complete Binary Tree? Ya
- Perfect Binary Tree? Ya (semua leaf di level yang sama, semua internal node punya 2 child)
- **Klasifikasi:** Perfect Binary Tree (juga full dan complete)

**Tree C:**
- Full Binary Tree? Tidak (setiap node hanya punya 1 child)
- Complete Binary Tree? Tidak
- Perfect Binary Tree? Tidak
- **Klasifikasi:** Right-Skewed Binary Tree

---

### SOLVED PROBLEM 4 ⭐⭐

**Soal:** Sebuah perfect binary tree memiliki 31 nodes. Tentukan: (a) height tree, (b) jumlah leaf, (c) jumlah internal nodes!

**Penyelesaian:**

Untuk perfect binary tree: n = 2^(h+1) - 1

**a) Height:**
```
31 = 2^(h+1) - 1
32 = 2^(h+1)
2^5 = 2^(h+1)
h + 1 = 5
h = 4
```
**Height = 4**

**b) Jumlah leaf:**
Pada perfect binary tree: leaf = 2^h = 2^4 = **16 leaves**

**c) Jumlah internal nodes:**
Internal nodes = total nodes - leaves = 31 - 16 = **15 internal nodes**

**Verifikasi:** 
- Jumlah internal nodes = 2^h - 1 = 2^4 - 1 = 15 ✓

---

## 4. Representasi Binary Tree

### 4.1 Representasi dengan Linked Structure

Setiap node menyimpan data dan pointer ke left child dan right child.

```cpp
#include <iostream>
using namespace std;

// Struktur Node untuk Binary Tree
struct Node {
    int data;
    Node* left;
    Node* right;
    
    // Constructor
    Node(int val) {
        data = val;
        left = nullptr;
        right = nullptr;
    }
};

// Class Binary Tree
class BinaryTree {
private:
    Node* root;
    
public:
    // Constructor
    BinaryTree() {
        root = nullptr;
    }
    
    // Getter root
    Node* getRoot() {
        return root;
    }
    
    // Set root
    void setRoot(Node* node) {
        root = node;
    }
    
    // Cek apakah tree kosong
    bool isEmpty() {
        return root == nullptr;
    }
};

int main() {
    BinaryTree tree;
    
    // Membuat tree secara manual
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    
    tree.setRoot(root);
    
    cout << "Root: " << tree.getRoot()->data << endl;
    cout << "Left child of root: " << tree.getRoot()->left->data << endl;
    cout << "Right child of root: " << tree.getRoot()->right->data << endl;
    
    return 0;
}
```

**Output:**
```
Root: 1
Left child of root: 2
Right child of root: 3
```

### 4.2 Representasi dengan Array

Untuk complete binary tree, kita dapat menggunakan array dengan aturan indexing:

![Representasi Array untuk Binary Tree](images/gambar-11-3.png)

*Gambar 11.3: Representasi binary tree menggunakan array dengan formula indexing*

**Formula Indexing (0-based):**

| Relasi | Formula |
|--------|---------|
| Parent dari node i | (i - 1) / 2 |
| Left child dari node i | 2 * i + 1 |
| Right child dari node i | 2 * i + 2 |

```cpp
#include <iostream>
#include <vector>
using namespace std;

class BinaryTreeArray {
private:
    vector<int> tree;
    
public:
    BinaryTreeArray(int size) {
        tree.resize(size, -1);  // -1 menandakan kosong
    }
    
    // Set root
    void setRoot(int data) {
        tree[0] = data;
    }
    
    // Set left child dari parent index
    void setLeftChild(int parentIdx, int data) {
        int leftIdx = 2 * parentIdx + 1;
        if (leftIdx < tree.size()) {
            tree[leftIdx] = data;
        }
    }
    
    // Set right child dari parent index
    void setRightChild(int parentIdx, int data) {
        int rightIdx = 2 * parentIdx + 2;
        if (rightIdx < tree.size()) {
            tree[rightIdx] = data;
        }
    }
    
    // Get parent
    int getParent(int childIdx) {
        if (childIdx == 0) return -1;  // Root tidak punya parent
        return tree[(childIdx - 1) / 2];
    }
    
    // Print tree as array
    void printArray() {
        cout << "Array: [";
        for (int i = 0; i < tree.size(); i++) {
            cout << tree[i];
            if (i < tree.size() - 1) cout << ", ";
        }
        cout << "]" << endl;
    }
};

int main() {
    BinaryTreeArray tree(7);
    
    tree.setRoot(10);
    tree.setLeftChild(0, 20);
    tree.setRightChild(0, 30);
    tree.setLeftChild(1, 40);
    tree.setRightChild(1, 50);
    tree.setLeftChild(2, 60);
    tree.setRightChild(2, 70);
    
    tree.printArray();
    
    return 0;
}
```

**Output:**
```
Array: [10, 20, 30, 40, 50, 60, 70]
```

### 4.3 Perbandingan Representasi

| Aspek | Linked Structure | Array |
|-------|------------------|-------|
| **Memory** | Fleksibel, sesuai kebutuhan | Fixed size atau perlu resize |
| **Akses parent** | Perlu pointer tambahan | O(1) dengan formula |
| **Akses child** | O(1) via pointer | O(1) dengan formula |
| **Insertion** | Mudah di mana saja | Sulit jika bukan complete |
| **Wasted space** | Tidak ada | Ada jika tree tidak complete |
| **Best for** | General binary tree | Complete binary tree, Heap |

---

### SOLVED PROBLEM 5 ⭐

**Soal:** Diberikan array representasi binary tree: `[15, 10, 20, 8, 12, 18, 25]`. Gambarkan tree-nya dan tentukan parent serta children dari node dengan nilai 20!

**Penyelesaian:**

**Tree Structure:**
```
          15 [0]
         /    \
      10 [1]   20 [2]
      /  \     /   \
   8[3] 12[4] 18[5] 25[6]
```

**Untuk node 20 (index 2):**

1. **Parent dari 20:**
   - Index parent = (2 - 1) / 2 = 0
   - Nilai parent = arr[0] = **15**

2. **Left child dari 20:**
   - Index left = 2 * 2 + 1 = 5
   - Nilai left child = arr[5] = **18**

3. **Right child dari 20:**
   - Index right = 2 * 2 + 2 = 6
   - Nilai right child = arr[6] = **25**

---

### SOLVED PROBLEM 6 ⭐⭐

**Soal:** Implementasikan fungsi untuk menghitung jumlah node dalam binary tree menggunakan linked structure!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Fungsi rekursif menghitung jumlah node
int countNodes(Node* root) {
    // Base case: tree kosong
    if (root == nullptr) {
        return 0;
    }
    
    // Rekursif: 1 (node ini) + nodes di subtree kiri + nodes di subtree kanan
    return 1 + countNodes(root->left) + countNodes(root->right);
}

// Fungsi menghitung jumlah leaf
int countLeaves(Node* root) {
    if (root == nullptr) {
        return 0;
    }
    
    // Jika node adalah leaf
    if (root->left == nullptr && root->right == nullptr) {
        return 1;
    }
    
    // Hitung leaf di subtree kiri dan kanan
    return countLeaves(root->left) + countLeaves(root->right);
}

// Fungsi menghitung height
int getHeight(Node* root) {
    if (root == nullptr) {
        return -1;  // Height tree kosong = -1
    }
    
    int leftHeight = getHeight(root->left);
    int rightHeight = getHeight(root->right);
    
    return 1 + max(leftHeight, rightHeight);
}

int main() {
    // Membuat tree
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);
    
    cout << "Jumlah node: " << countNodes(root) << endl;
    cout << "Jumlah leaf: " << countLeaves(root) << endl;
    cout << "Height tree: " << getHeight(root) << endl;
    
    return 0;
}
```

**Output:**
```
Jumlah node: 6
Jumlah leaf: 3
Height tree: 2
```

**Analisis Kompleksitas:**
- **Waktu:** O(n) — setiap node dikunjungi tepat sekali
- **Ruang:** O(h) — stack rekursi sebanyak height tree

---

## 5. Tree Traversal

### 5.1 Pengertian Traversal

> **Definisi:** Tree traversal adalah proses mengunjungi setiap node dalam tree tepat satu kali dengan urutan tertentu.

Ada empat metode traversal utama:

| Traversal | Urutan Kunjungan | Kegunaan |
|-----------|------------------|----------|
| **Preorder** | Root → Left → Right | Copy tree, prefix expression |
| **Inorder** | Left → Root → Right | Sorted order (untuk BST) |
| **Postorder** | Left → Right → Root | Delete tree, postfix expression |
| **Level-order** | Level demi level | BFS, print tree |

### 5.2 Preorder Traversal

![Preorder Traversal](images/gambar-11-4.png)

*Gambar 11.4: Preorder traversal — Root → Left → Right*

#### Implementasi Rekursif Preorder

```cpp
// Preorder: Root -> Left -> Right
void preorder(Node* root) {
    if (root == nullptr) return;
    
    cout << root->data << " ";   // Kunjungi root
    preorder(root->left);         // Traverse subtree kiri
    preorder(root->right);        // Traverse subtree kanan
}
```

#### Implementasi Iteratif Preorder (menggunakan Stack)

```cpp
#include <stack>

void preorderIterative(Node* root) {
    if (root == nullptr) return;
    
    stack<Node*> s;
    s.push(root);
    
    while (!s.empty()) {
        Node* current = s.top();
        s.pop();
        
        cout << current->data << " ";
        
        // Push right first, agar left diproses duluan (LIFO)
        if (current->right != nullptr) {
            s.push(current->right);
        }
        if (current->left != nullptr) {
            s.push(current->left);
        }
    }
}
```

### 5.3 Inorder Traversal

![Inorder Traversal](images/gambar-11-5.png)

*Gambar 11.5: Inorder traversal — Left → Root → Right*

#### Implementasi Rekursif Inorder

```cpp
// Inorder: Left -> Root -> Right
void inorder(Node* root) {
    if (root == nullptr) return;
    
    inorder(root->left);          // Traverse subtree kiri
    cout << root->data << " ";    // Kunjungi root
    inorder(root->right);         // Traverse subtree kanan
}
```

#### Implementasi Iteratif Inorder

```cpp
void inorderIterative(Node* root) {
    stack<Node*> s;
    Node* current = root;
    
    while (current != nullptr || !s.empty()) {
        // Pergi ke node paling kiri
        while (current != nullptr) {
            s.push(current);
            current = current->left;
        }
        
        // Current sekarang nullptr, pop dari stack
        current = s.top();
        s.pop();
        
        cout << current->data << " ";
        
        // Pindah ke subtree kanan
        current = current->right;
    }
}
```

### 5.4 Postorder Traversal

![Postorder Traversal](images/gambar-11-6.png)

*Gambar 11.6: Postorder traversal — Left → Right → Root*

#### Implementasi Rekursif Postorder

```cpp
// Postorder: Left -> Right -> Root
void postorder(Node* root) {
    if (root == nullptr) return;
    
    postorder(root->left);        // Traverse subtree kiri
    postorder(root->right);       // Traverse subtree kanan
    cout << root->data << " ";    // Kunjungi root
}
```

#### Implementasi Iteratif Postorder (Two Stacks)

```cpp
void postorderIterative(Node* root) {
    if (root == nullptr) return;
    
    stack<Node*> s1, s2;
    s1.push(root);
    
    while (!s1.empty()) {
        Node* current = s1.top();
        s1.pop();
        s2.push(current);
        
        if (current->left != nullptr) {
            s1.push(current->left);
        }
        if (current->right != nullptr) {
            s1.push(current->right);
        }
    }
    
    // Print dari s2
    while (!s2.empty()) {
        cout << s2.top()->data << " ";
        s2.pop();
    }
}
```

### 5.5 Level-Order Traversal (BFS)

Level-order traversal mengunjungi node level per level dari atas ke bawah, kiri ke kanan. Implementasi menggunakan **Queue**.

![Level-Order Traversal](images/gambar-11-7.png)

*Gambar 11.7: Level-order traversal menggunakan Queue (BFS)*

```cpp
#include <queue>

void levelOrder(Node* root) {
    if (root == nullptr) return;
    
    queue<Node*> q;
    q.push(root);
    
    while (!q.empty()) {
        Node* current = q.front();
        q.pop();
        
        cout << current->data << " ";
        
        // Enqueue children
        if (current->left != nullptr) {
            q.push(current->left);
        }
        if (current->right != nullptr) {
            q.push(current->right);
        }
    }
}
```

---

### SOLVED PROBLEM 7 ⭐

**Soal:** Diberikan binary tree berikut:

```
        A
       / \
      B   C
     / \   \
    D   E   F
```

Tuliskan hasil dari keempat jenis traversal!

**Penyelesaian:**

1. **Preorder (Root → Left → Right):**
   - Visit A → traverse left subtree → traverse right subtree
   - A → B → D → E → C → F
   - **Hasil: A B D E C F**

2. **Inorder (Left → Root → Right):**
   - Traverse left subtree → visit root → traverse right subtree
   - D → B → E → A → C → F
   - **Hasil: D B E A C F**

3. **Postorder (Left → Right → Root):**
   - Traverse left subtree → traverse right subtree → visit root
   - D → E → B → F → C → A
   - **Hasil: D E B F C A**

4. **Level-order:**
   - Level 0: A
   - Level 1: B, C
   - Level 2: D, E, F
   - **Hasil: A B C D E F**

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Implementasikan fungsi lengkap untuk semua traversal dalam satu program!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <stack>
using namespace std;

struct Node {
    char data;
    Node* left;
    Node* right;
    Node(char val) : data(val), left(nullptr), right(nullptr) {}
};

// Preorder Rekursif
void preorder(Node* root) {
    if (root == nullptr) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Inorder Rekursif
void inorder(Node* root) {
    if (root == nullptr) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Postorder Rekursif
void postorder(Node* root) {
    if (root == nullptr) return;
    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

// Level-order (BFS)
void levelOrder(Node* root) {
    if (root == nullptr) return;
    
    queue<Node*> q;
    q.push(root);
    
    while (!q.empty()) {
        Node* current = q.front();
        q.pop();
        cout << current->data << " ";
        
        if (current->left) q.push(current->left);
        if (current->right) q.push(current->right);
    }
}

int main() {
    // Membuat tree:
    //        A
    //       / \
    //      B   C
    //     / \   \
    //    D   E   F
    
    Node* root = new Node('A');
    root->left = new Node('B');
    root->right = new Node('C');
    root->left->left = new Node('D');
    root->left->right = new Node('E');
    root->right->right = new Node('F');
    
    cout << "=== Tree Traversal Demo ===" << endl;
    cout << "Preorder:    "; preorder(root); cout << endl;
    cout << "Inorder:     "; inorder(root); cout << endl;
    cout << "Postorder:   "; postorder(root); cout << endl;
    cout << "Level-order: "; levelOrder(root); cout << endl;
    
    return 0;
}
```

**Output:**
```
=== Tree Traversal Demo ===
Preorder:    A B D E C F 
Inorder:     D B E A C F 
Postorder:   D E B F C A 
Level-order: A B C D E F 
```

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Diberikan:
- Preorder: F, B, A, D, C, E, G, I, H
- Inorder: A, B, C, D, E, F, G, H, I

Konstruksi binary tree-nya!

**Penyelesaian:**

**Algoritma:**
1. Elemen pertama preorder adalah root
2. Cari posisi root di inorder untuk memisahkan subtree kiri dan kanan
3. Rekursif untuk subtree kiri dan kanan

**Langkah:**

1. **Root = F** (elemen pertama preorder)
   - Di inorder: A, B, C, D, E | F | G, H, I
   - Left subtree: A, B, C, D, E (5 nodes)
   - Right subtree: G, H, I (3 nodes)

2. **Left subtree dari F:**
   - Preorder: B, A, D, C, E
   - Inorder: A, B, C, D, E
   - Root = B
   - Di inorder: A | B | C, D, E

3. **Lanjutkan rekursif...**

**Hasil Tree:**
```
            F
           / \
          B   G
         / \   \
        A   D   I
           / \  /
          C   E H
```

**Implementasi:**

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

struct Node {
    char data;
    Node* left;
    Node* right;
    Node(char val) : data(val), left(nullptr), right(nullptr) {}
};

class TreeBuilder {
private:
    unordered_map<char, int> inorderIndex;
    int preIndex;
    
public:
    Node* buildTree(string preorder, string inorder) {
        // Buat map untuk index di inorder
        for (int i = 0; i < inorder.size(); i++) {
            inorderIndex[inorder[i]] = i;
        }
        
        preIndex = 0;
        return build(preorder, 0, inorder.size() - 1);
    }
    
private:
    Node* build(string& preorder, int inStart, int inEnd) {
        if (inStart > inEnd) return nullptr;
        
        // Ambil elemen dari preorder sebagai root
        char rootVal = preorder[preIndex++];
        Node* root = new Node(rootVal);
        
        // Cari posisi root di inorder
        int rootIndex = inorderIndex[rootVal];
        
        // Build subtree kiri dan kanan
        root->left = build(preorder, inStart, rootIndex - 1);
        root->right = build(preorder, rootIndex + 1, inEnd);
        
        return root;
    }
};

void printInorder(Node* root) {
    if (root == nullptr) return;
    printInorder(root->left);
    cout << root->data << " ";
    printInorder(root->right);
}

int main() {
    TreeBuilder builder;
    
    string preorder = "FBADCEGIH";
    string inorder = "ABCDEFGHI";
    
    Node* root = builder.buildTree(preorder, inorder);
    
    cout << "Inorder verification: ";
    printInorder(root);
    cout << endl;
    
    return 0;
}
```

---

### SOLVED PROBLEM 10 ⭐⭐

**Soal:** Implementasikan fungsi untuk menghapus seluruh binary tree dengan benar (mencegah memory leak)!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Menghapus tree menggunakan postorder traversal
void deleteTree(Node*& root) {
    if (root == nullptr) return;
    
    // Hapus subtree kiri dan kanan terlebih dahulu
    deleteTree(root->left);
    deleteTree(root->right);
    
    // Baru hapus root (postorder)
    cout << "Menghapus node: " << root->data << endl;
    delete root;
    root = nullptr;
}

int main() {
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    
    cout << "Menghapus tree..." << endl;
    deleteTree(root);
    
    if (root == nullptr) {
        cout << "Tree berhasil dihapus!" << endl;
    }
    
    return 0;
}
```

**Output:**
```
Menghapus tree...
Menghapus node: 4
Menghapus node: 5
Menghapus node: 2
Menghapus node: 3
Menghapus node: 1
Tree berhasil dihapus!
```

**Mengapa Postorder?**
- Postorder mengunjungi children sebelum parent
- Kita harus menghapus children dulu sebelum menghapus parent
- Jika menghapus parent dulu, kita kehilangan akses ke children → memory leak

---

### SOLVED PROBLEM 11 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk mencetak tree dalam format visual (tree printing)!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <cmath>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Menghitung height tree
int getHeight(Node* root) {
    if (root == nullptr) return 0;
    return 1 + max(getHeight(root->left), getHeight(root->right));
}

// Print tree secara horizontal dengan indentasi
void printTreeHorizontal(Node* root, string prefix = "", bool isLeft = true) {
    if (root == nullptr) return;
    
    cout << prefix;
    cout << (isLeft ? "├── " : "└── ");
    cout << root->data << endl;
    
    string newPrefix = prefix + (isLeft ? "│   " : "    ");
    
    if (root->left != nullptr || root->right != nullptr) {
        if (root->left) {
            printTreeHorizontal(root->left, newPrefix, true);
        } else {
            cout << newPrefix << "├── (null)" << endl;
        }
        if (root->right) {
            printTreeHorizontal(root->right, newPrefix, false);
        } else {
            cout << newPrefix << "└── (null)" << endl;
        }
    }
}

// Print tree level by level dengan spacing
void printTreeLevels(Node* root) {
    if (root == nullptr) return;
    
    queue<Node*> q;
    q.push(root);
    
    int level = 0;
    
    while (!q.empty()) {
        int size = q.size();
        cout << "Level " << level << ": ";
        
        for (int i = 0; i < size; i++) {
            Node* current = q.front();
            q.pop();
            
            if (current != nullptr) {
                cout << current->data << " ";
                q.push(current->left);
                q.push(current->right);
            } else {
                cout << "- ";
            }
        }
        cout << endl;
        level++;
        
        // Stop jika semua node di queue adalah null
        bool allNull = true;
        queue<Node*> temp = q;
        while (!temp.empty()) {
            if (temp.front() != nullptr) {
                allNull = false;
                break;
            }
            temp.pop();
        }
        if (allNull) break;
    }
}

int main() {
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);
    
    cout << "=== Tree Horizontal View ===" << endl;
    cout << root->data << endl;
    if (root->left) printTreeHorizontal(root->left, "", true);
    if (root->right) printTreeHorizontal(root->right, "", false);
    
    cout << "\n=== Tree Level View ===" << endl;
    printTreeLevels(root);
    
    return 0;
}
```

**Output:**
```
=== Tree Horizontal View ===
1
├── 2
│   ├── 4
│   └── 5
└── 3
    ├── (null)
    └── 6

=== Tree Level View ===
Level 0: 1 
Level 1: 2 3 
Level 2: 4 5 - 6 
```

---

## 6. Expression Tree

### 6.1 Pengertian Expression Tree

> **Definisi:** Expression tree adalah binary tree yang digunakan untuk merepresentasikan ekspresi matematika. Leaf nodes berisi operand, sedangkan internal nodes berisi operator.

![Expression Tree](images/gambar-11-8.png)

*Gambar 11.8: Expression tree untuk ekspresi (a + b) * (c - d)*

### 6.2 Notasi Ekspresi dan Traversal

| Traversal | Notasi | Contoh untuk (a + b) * (c - d) |
|-----------|--------|-------------------------------|
| **Inorder** | Infix | (a + b) * (c - d) |
| **Preorder** | Prefix (Polish) | * + a b - c d |
| **Postorder** | Postfix (Reverse Polish) | a b + c d - * |

### 6.3 Implementasi Expression Tree

```cpp
#include <iostream>
#include <stack>
#include <cctype>
#include <cmath>
using namespace std;

struct ExprNode {
    char data;
    ExprNode* left;
    ExprNode* right;
    
    ExprNode(char val) : data(val), left(nullptr), right(nullptr) {}
};

class ExpressionTree {
public:
    // Membangun expression tree dari postfix
    ExprNode* buildFromPostfix(string postfix) {
        stack<ExprNode*> s;
        
        for (char c : postfix) {
            ExprNode* node = new ExprNode(c);
            
            if (isOperator(c)) {
                // Operator: pop dua operand
                node->right = s.top(); s.pop();
                node->left = s.top(); s.pop();
            }
            // Operand atau operator, push ke stack
            s.push(node);
        }
        
        return s.top();
    }
    
    // Inorder traversal (infix dengan parentheses)
    void infix(ExprNode* root) {
        if (root == nullptr) return;
        
        if (isOperator(root->data)) cout << "(";
        infix(root->left);
        cout << root->data;
        infix(root->right);
        if (isOperator(root->data)) cout << ")";
    }
    
    // Preorder traversal (prefix)
    void prefix(ExprNode* root) {
        if (root == nullptr) return;
        cout << root->data;
        prefix(root->left);
        prefix(root->right);
    }
    
    // Postorder traversal (postfix)
    void postfix(ExprNode* root) {
        if (root == nullptr) return;
        postfix(root->left);
        postfix(root->right);
        cout << root->data;
    }
    
    // Evaluasi expression tree
    int evaluate(ExprNode* root) {
        if (root == nullptr) return 0;
        
        // Jika leaf (operand)
        if (!isOperator(root->data)) {
            return root->data - '0';  // Convert char ke int
        }
        
        // Evaluasi subtree
        int leftVal = evaluate(root->left);
        int rightVal = evaluate(root->right);
        
        // Apply operator
        switch (root->data) {
            case '+': return leftVal + rightVal;
            case '-': return leftVal - rightVal;
            case '*': return leftVal * rightVal;
            case '/': return leftVal / rightVal;
            default: return 0;
        }
    }
    
private:
    bool isOperator(char c) {
        return c == '+' || c == '-' || c == '*' || c == '/';
    }
};

int main() {
    ExpressionTree tree;
    
    // Postfix: ab+cd-* untuk (a+b)*(c-d)
    // Menggunakan angka: 23+45-* untuk (2+3)*(4-5)
    string postfix = "23+45-*";
    
    ExprNode* root = tree.buildFromPostfix(postfix);
    
    cout << "=== Expression Tree ===" << endl;
    cout << "Postfix input: " << postfix << endl;
    
    cout << "Infix:   "; tree.infix(root); cout << endl;
    cout << "Prefix:  "; tree.prefix(root); cout << endl;
    cout << "Postfix: "; tree.postfix(root); cout << endl;
    
    cout << "Result:  " << tree.evaluate(root) << endl;
    
    return 0;
}
```

**Output:**
```
=== Expression Tree ===
Postfix input: 23+45-*
Infix:   ((2+3)*(4-5))
Prefix:  *+23-45
Postfix: 23+45-*
Result:  -5
```

**Penjelasan:**
- (2 + 3) = 5
- (4 - 5) = -1
- 5 * (-1) = -5

---

### SOLVED PROBLEM 12 ⭐

**Soal:** Gambar expression tree untuk ekspresi: `a * b + c / d`

**Penyelesaian:**

Dengan memperhatikan precedence operator (* dan / lebih tinggi dari +):

```
        +
       / \
      *   /
     / \ / \
    a  b c  d
```

**Traversal:**
- Infix: ((a * b) + (c / d))
- Prefix: + * a b / c d
- Postfix: a b * c d / +

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Bangun expression tree dari ekspresi postfix: `5 3 + 8 2 - *` dan evaluasi hasilnya!

**Penyelesaian:**

**Langkah membangun tree dari postfix:**

1. Baca `5` → push node(5)
2. Baca `3` → push node(3)
3. Baca `+` → pop 3, pop 5, buat tree `+` dengan children 5 dan 3, push tree
4. Baca `8` → push node(8)
5. Baca `2` → push node(2)
6. Baca `-` → pop 2, pop 8, buat tree `-` dengan children 8 dan 2, push tree
7. Baca `*` → pop subtree(-), pop subtree(+), buat tree `*`

**Hasil Tree:**
```
        *
       / \
      +   -
     / \ / \
    5  3 8  2
```

**Evaluasi:**
- 5 + 3 = 8
- 8 - 2 = 6
- 8 * 6 = **48**

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Implementasikan fungsi untuk mencari node dalam binary tree!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Mencari node dengan nilai tertentu
Node* search(Node* root, int target) {
    // Base case: tree kosong atau node ditemukan
    if (root == nullptr || root->data == target) {
        return root;
    }
    
    // Cari di subtree kiri
    Node* found = search(root->left, target);
    if (found != nullptr) {
        return found;
    }
    
    // Jika tidak ditemukan di kiri, cari di kanan
    return search(root->right, target);
}

// Mencari path ke node
bool findPath(Node* root, int target, vector<int>& path) {
    if (root == nullptr) return false;
    
    // Tambahkan node ini ke path
    path.push_back(root->data);
    
    // Jika ini target, selesai
    if (root->data == target) return true;
    
    // Cari di subtree
    if (findPath(root->left, target, path) || 
        findPath(root->right, target, path)) {
        return true;
    }
    
    // Jika tidak ditemukan, hapus dari path
    path.pop_back();
    return false;
}

int main() {
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);
    
    int target = 5;
    
    Node* result = search(root, target);
    if (result) {
        cout << "Node " << target << " ditemukan!" << endl;
    } else {
        cout << "Node " << target << " tidak ditemukan!" << endl;
    }
    
    vector<int> path;
    if (findPath(root, target, path)) {
        cout << "Path ke " << target << ": ";
        for (int node : path) {
            cout << node << " ";
        }
        cout << endl;
    }
    
    return 0;
}
```

**Output:**
```
Node 5 ditemukan!
Path ke 5: 1 2 5 
```

---

### SOLVED PROBLEM 15 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk mencari Lowest Common Ancestor (LCA) dari dua node dalam binary tree!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Mencari LCA (Lowest Common Ancestor)
Node* findLCA(Node* root, int n1, int n2) {
    // Base case
    if (root == nullptr) return nullptr;
    
    // Jika root adalah salah satu dari n1 atau n2
    if (root->data == n1 || root->data == n2) {
        return root;
    }
    
    // Cari LCA di subtree kiri dan kanan
    Node* leftLCA = findLCA(root->left, n1, n2);
    Node* rightLCA = findLCA(root->right, n1, n2);
    
    // Jika kedua subtree mengembalikan non-null,
    // artinya satu node di kiri, satu di kanan
    // Maka root adalah LCA
    if (leftLCA != nullptr && rightLCA != nullptr) {
        return root;
    }
    
    // Jika hanya salah satu subtree yang mengembalikan non-null
    return (leftLCA != nullptr) ? leftLCA : rightLCA;
}

int main() {
    /*
            1
           / \
          2   3
         / \   \
        4   5   6
    */
    
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);
    
    // Test cases
    cout << "LCA(4, 5) = " << findLCA(root, 4, 5)->data << endl;  // 2
    cout << "LCA(4, 6) = " << findLCA(root, 4, 6)->data << endl;  // 1
    cout << "LCA(2, 5) = " << findLCA(root, 2, 5)->data << endl;  // 2
    cout << "LCA(3, 6) = " << findLCA(root, 3, 6)->data << endl;  // 3
    
    return 0;
}
```

**Output:**
```
LCA(4, 5) = 2
LCA(4, 6) = 1
LCA(2, 5) = 2
LCA(3, 6) = 3
```

**Kompleksitas:**
- **Waktu:** O(n) — mengunjungi setiap node paling banyak sekali
- **Ruang:** O(h) — stack rekursi

---

## 7. Aplikasi Tree dalam Sistem Pertahanan

### 7.1 Decision Tree untuk Analisis Ancaman

Decision tree dapat digunakan untuk klasifikasi ancaman berdasarkan berbagai parameter.

![Decision Tree Analisis Ancaman](images/gambar-11-9.png)

*Gambar 11.9: Decision tree untuk klasifikasi ancaman udara*

### 7.2 Hierarki Komando

Tree sangat cocok untuk merepresentasikan struktur organisasi dan rantai komando.

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct Unit {
    string nama;
    string pangkat;
    vector<Unit*> bawahan;
    
    Unit(string n, string p) : nama(n), pangkat(p) {}
    
    void tambahBawahan(Unit* u) {
        bawahan.push_back(u);
    }
};

void printHierarki(Unit* unit, int level = 0) {
    if (unit == nullptr) return;
    
    // Cetak dengan indentasi
    for (int i = 0; i < level; i++) cout << "  ";
    cout << "├─ " << unit->pangkat << " " << unit->nama << endl;
    
    for (Unit* bawahan : unit->bawahan) {
        printHierarki(bawahan, level + 1);
    }
}

int hitungPersonel(Unit* unit) {
    if (unit == nullptr) return 0;
    
    int total = 1;  // Hitung unit ini
    for (Unit* bawahan : unit->bawahan) {
        total += hitungPersonel(bawahan);
    }
    return total;
}

int main() {
    // Struktur komando
    Unit* komandan = new Unit("Ahmad", "Kolonel");
    
    Unit* kapten1 = new Unit("Budi", "Kapten");
    Unit* kapten2 = new Unit("Candra", "Kapten");
    
    Unit* letnan1 = new Unit("Deni", "Letnan");
    Unit* letnan2 = new Unit("Eko", "Letnan");
    Unit* letnan3 = new Unit("Fajar", "Letnan");
    
    komandan->tambahBawahan(kapten1);
    komandan->tambahBawahan(kapten2);
    
    kapten1->tambahBawahan(letnan1);
    kapten1->tambahBawahan(letnan2);
    kapten2->tambahBawahan(letnan3);
    
    cout << "=== Hierarki Komando ===" << endl;
    printHierarki(komandan);
    
    cout << "\nTotal personel: " << hitungPersonel(komandan) << endl;
    
    return 0;
}
```

**Output:**
```
=== Hierarki Komando ===
├─ Kolonel Ahmad
  ├─ Kapten Budi
    ├─ Letnan Deni
    ├─ Letnan Eko
  ├─ Kapten Candra
    ├─ Letnan Fajar

Total personel: 6
```

---

### SOLVED PROBLEM 16 ⭐⭐

**Soal:** Implementasikan fungsi untuk memeriksa apakah dua binary tree identik!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Mengecek apakah dua tree identik
bool isIdentical(Node* root1, Node* root2) {
    // Jika keduanya null, identik
    if (root1 == nullptr && root2 == nullptr) {
        return true;
    }
    
    // Jika salah satu null, tidak identik
    if (root1 == nullptr || root2 == nullptr) {
        return false;
    }
    
    // Cek data dan rekursif ke subtree
    return (root1->data == root2->data) &&
           isIdentical(root1->left, root2->left) &&
           isIdentical(root1->right, root2->right);
}

int main() {
    // Tree 1
    Node* root1 = new Node(1);
    root1->left = new Node(2);
    root1->right = new Node(3);
    
    // Tree 2 (identik)
    Node* root2 = new Node(1);
    root2->left = new Node(2);
    root2->right = new Node(3);
    
    // Tree 3 (berbeda)
    Node* root3 = new Node(1);
    root3->left = new Node(2);
    root3->right = new Node(4);  // Berbeda!
    
    cout << "Tree1 dan Tree2: " 
         << (isIdentical(root1, root2) ? "Identik" : "Berbeda") << endl;
    cout << "Tree1 dan Tree3: " 
         << (isIdentical(root1, root3) ? "Identik" : "Berbeda") << endl;
    
    return 0;
}
```

**Output:**
```
Tree1 dan Tree2: Identik
Tree1 dan Tree3: Berbeda
```

---

### SOLVED PROBLEM 17 ⭐⭐

**Soal:** Implementasikan fungsi untuk mencari kedalaman (depth) suatu node dalam binary tree!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Mencari depth node dengan nilai target
int findDepth(Node* root, int target, int depth = 0) {
    if (root == nullptr) return -1;  // Tidak ditemukan
    
    if (root->data == target) return depth;
    
    // Cari di subtree kiri
    int leftDepth = findDepth(root->left, target, depth + 1);
    if (leftDepth != -1) return leftDepth;
    
    // Cari di subtree kanan
    return findDepth(root->right, target, depth + 1);
}

int main() {
    /*
            1          depth 0
           / \
          2   3        depth 1
         / \
        4   5          depth 2
    */
    
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    
    cout << "Depth of 1: " << findDepth(root, 1) << endl;
    cout << "Depth of 2: " << findDepth(root, 2) << endl;
    cout << "Depth of 5: " << findDepth(root, 5) << endl;
    cout << "Depth of 9: " << findDepth(root, 9) << endl;  // Tidak ada
    
    return 0;
}
```

**Output:**
```
Depth of 1: 0
Depth of 2: 1
Depth of 5: 2
Depth of 9: -1
```

---

### SOLVED PROBLEM 18 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk mencetak semua path dari root ke leaf!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

void printPath(vector<int>& path) {
    for (int i = 0; i < path.size(); i++) {
        cout << path[i];
        if (i < path.size() - 1) cout << " -> ";
    }
    cout << endl;
}

void printAllPaths(Node* root, vector<int>& path) {
    if (root == nullptr) return;
    
    // Tambahkan node ke path
    path.push_back(root->data);
    
    // Jika leaf, cetak path
    if (root->left == nullptr && root->right == nullptr) {
        printPath(path);
    } else {
        // Rekursif ke subtree
        printAllPaths(root->left, path);
        printAllPaths(root->right, path);
    }
    
    // Backtrack: hapus node dari path
    path.pop_back();
}

int main() {
    /*
            1
           / \
          2   3
         / \   \
        4   5   6
    */
    
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->right->right = new Node(6);
    
    cout << "=== Semua Path dari Root ke Leaf ===" << endl;
    vector<int> path;
    printAllPaths(root, path);
    
    return 0;
}
```

**Output:**
```
=== Semua Path dari Root ke Leaf ===
1 -> 2 -> 4
1 -> 2 -> 5
1 -> 3 -> 6
```

---

### SOLVED PROBLEM 19 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk memeriksa apakah binary tree adalah mirror (symmetric)!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Helper function untuk cek apakah dua subtree adalah mirror
bool isMirror(Node* left, Node* right) {
    // Kedua subtree kosong
    if (left == nullptr && right == nullptr) return true;
    
    // Salah satu kosong
    if (left == nullptr || right == nullptr) return false;
    
    // Cek nilai dan rekursif dengan posisi yang di-mirror
    return (left->data == right->data) &&
           isMirror(left->left, right->right) &&
           isMirror(left->right, right->left);
}

// Fungsi utama untuk cek symmetric
bool isSymmetric(Node* root) {
    if (root == nullptr) return true;
    return isMirror(root->left, root->right);
}

int main() {
    // Symmetric tree
    /*
            1
           / \
          2   2
         / \ / \
        3  4 4  3
    */
    Node* symmetric = new Node(1);
    symmetric->left = new Node(2);
    symmetric->right = new Node(2);
    symmetric->left->left = new Node(3);
    symmetric->left->right = new Node(4);
    symmetric->right->left = new Node(4);
    symmetric->right->right = new Node(3);
    
    // Non-symmetric tree
    /*
            1
           / \
          2   2
           \   \
            3   3
    */
    Node* nonSymmetric = new Node(1);
    nonSymmetric->left = new Node(2);
    nonSymmetric->right = new Node(2);
    nonSymmetric->left->right = new Node(3);
    nonSymmetric->right->right = new Node(3);
    
    cout << "Symmetric tree: " 
         << (isSymmetric(symmetric) ? "Ya" : "Tidak") << endl;
    cout << "Non-symmetric tree: " 
         << (isSymmetric(nonSymmetric) ? "Ya" : "Tidak") << endl;
    
    return 0;
}
```

**Output:**
```
Symmetric tree: Ya
Non-symmetric tree: Tidak
```

---

### SOLVED PROBLEM 20 ⭐⭐

**Soal:** Implementasikan fungsi untuk mencari diameter binary tree (path terpanjang antara dua node)!

**Penyelesaian:**

```cpp
#include <iostream>
#include <algorithm>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Helper untuk menghitung height dan update diameter
int heightAndDiameter(Node* root, int& diameter) {
    if (root == nullptr) return 0;
    
    int leftHeight = heightAndDiameter(root->left, diameter);
    int rightHeight = heightAndDiameter(root->right, diameter);
    
    // Diameter melalui node ini = left height + right height
    diameter = max(diameter, leftHeight + rightHeight);
    
    // Return height subtree ini
    return 1 + max(leftHeight, rightHeight);
}

int findDiameter(Node* root) {
    int diameter = 0;
    heightAndDiameter(root, diameter);
    return diameter;
}

int main() {
    /*
            1
           / \
          2   3
         / \
        4   5
       /
      6
    */
    
    Node* root = new Node(1);
    root->left = new Node(2);
    root->right = new Node(3);
    root->left->left = new Node(4);
    root->left->right = new Node(5);
    root->left->left->left = new Node(6);
    
    cout << "Diameter tree: " << findDiameter(root) << endl;
    // Path terpanjang: 6 -> 4 -> 2 -> 5 atau 6 -> 4 -> 2 -> 1 -> 3
    // Panjang = 4 edges
    
    return 0;
}
```

**Output:**
```
Diameter tree: 4
```

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Soal:** Implementasikan sistem radar tracking menggunakan tree untuk mengorganisasi zona pemantauan!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

struct ZonaRadar {
    string kodeZona;
    string nama;
    int prioritas;  // 1 = tertinggi
    vector<ZonaRadar*> subZona;
    
    ZonaRadar(string kode, string n, int p) 
        : kodeZona(kode), nama(n), prioritas(p) {}
    
    void tambahSubZona(ZonaRadar* z) {
        subZona.push_back(z);
    }
};

class SistemRadar {
private:
    ZonaRadar* root;
    
public:
    SistemRadar(ZonaRadar* r) : root(r) {}
    
    // Traversal untuk menampilkan semua zona
    void tampilkanSemua(ZonaRadar* zona, int level = 0) {
        if (zona == nullptr) return;
        
        for (int i = 0; i < level; i++) cout << "  ";
        cout << "[" << zona->kodeZona << "] " << zona->nama 
             << " (Prioritas: " << zona->prioritas << ")" << endl;
        
        for (ZonaRadar* sub : zona->subZona) {
            tampilkanSemua(sub, level + 1);
        }
    }
    
    // Cari zona berdasarkan kode
    ZonaRadar* cariZona(ZonaRadar* zona, string kode) {
        if (zona == nullptr) return nullptr;
        if (zona->kodeZona == kode) return zona;
        
        for (ZonaRadar* sub : zona->subZona) {
            ZonaRadar* found = cariZona(sub, kode);
            if (found != nullptr) return found;
        }
        return nullptr;
    }
    
    // Hitung total zona
    int hitungZona(ZonaRadar* zona) {
        if (zona == nullptr) return 0;
        int total = 1;
        for (ZonaRadar* sub : zona->subZona) {
            total += hitungZona(sub);
        }
        return total;
    }
    
    // Zona dengan prioritas tertinggi
    void zonaKritis(ZonaRadar* zona, int maxPrioritas = 1) {
        if (zona == nullptr) return;
        
        if (zona->prioritas <= maxPrioritas) {
            cout << "[KRITIS] " << zona->kodeZona << " - " 
                 << zona->nama << endl;
        }
        
        for (ZonaRadar* sub : zona->subZona) {
            zonaKritis(sub, maxPrioritas);
        }
    }
    
    ZonaRadar* getRoot() { return root; }
};

int main() {
    // Buat hierarki zona radar
    ZonaRadar* indonesia = new ZonaRadar("ID", "Indonesia", 2);
    
    ZonaRadar* barat = new ZonaRadar("ID-W", "Wilayah Barat", 2);
    ZonaRadar* tengah = new ZonaRadar("ID-C", "Wilayah Tengah", 2);
    ZonaRadar* timur = new ZonaRadar("ID-E", "Wilayah Timur", 1);  // Kritis
    
    ZonaRadar* sumatra = new ZonaRadar("SUM", "Sumatra", 2);
    ZonaRadar* selat = new ZonaRadar("SM", "Selat Malaka", 1);  // Kritis
    ZonaRadar* kalimantan = new ZonaRadar("KAL", "Kalimantan", 2);
    ZonaRadar* natuna = new ZonaRadar("NAT", "Natuna", 1);  // Kritis
    
    indonesia->tambahSubZona(barat);
    indonesia->tambahSubZona(tengah);
    indonesia->tambahSubZona(timur);
    
    barat->tambahSubZona(sumatra);
    barat->tambahSubZona(selat);
    tengah->tambahSubZona(kalimantan);
    tengah->tambahSubZona(natuna);
    
    SistemRadar sistem(indonesia);
    
    cout << "=== SISTEM RADAR PERTAHANAN ===" << endl;
    cout << "\n--- Hierarki Zona ---" << endl;
    sistem.tampilkanSemua(sistem.getRoot());
    
    cout << "\n--- Zona Kritis (Prioritas 1) ---" << endl;
    sistem.zonaKritis(sistem.getRoot());
    
    cout << "\nTotal zona: " << sistem.hitungZona(sistem.getRoot()) << endl;
    
    return 0;
}
```

**Output:**
```
=== SISTEM RADAR PERTAHANAN ===

--- Hierarki Zona ---
[ID] Indonesia (Prioritas: 2)
  [ID-W] Wilayah Barat (Prioritas: 2)
    [SUM] Sumatra (Prioritas: 2)
    [SM] Selat Malaka (Prioritas: 1)
  [ID-C] Wilayah Tengah (Prioritas: 2)
    [KAL] Kalimantan (Prioritas: 2)
    [NAT] Natuna (Prioritas: 1)
  [ID-E] Wilayah Timur (Prioritas: 1)

--- Zona Kritis (Prioritas 1) ---
[KRITIS] SM - Selat Malaka
[KRITIS] NAT - Natuna
[KRITIS] ID-E - Wilayah Timur

Total zona: 7
```

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Implementasikan Binary Tree lengkap dengan semua operasi dan traversal dalam satu class!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <stack>
using namespace std;

class BinaryTree {
private:
    struct Node {
        int data;
        Node* left;
        Node* right;
        Node(int val) : data(val), left(nullptr), right(nullptr) {}
    };
    
    Node* root;
    
    // Helper functions
    void destroyTree(Node* node) {
        if (node == nullptr) return;
        destroyTree(node->left);
        destroyTree(node->right);
        delete node;
    }
    
    void preorderHelper(Node* node) {
        if (node == nullptr) return;
        cout << node->data << " ";
        preorderHelper(node->left);
        preorderHelper(node->right);
    }
    
    void inorderHelper(Node* node) {
        if (node == nullptr) return;
        inorderHelper(node->left);
        cout << node->data << " ";
        inorderHelper(node->right);
    }
    
    void postorderHelper(Node* node) {
        if (node == nullptr) return;
        postorderHelper(node->left);
        postorderHelper(node->right);
        cout << node->data << " ";
    }
    
    int heightHelper(Node* node) {
        if (node == nullptr) return -1;
        return 1 + max(heightHelper(node->left), heightHelper(node->right));
    }
    
    int countHelper(Node* node) {
        if (node == nullptr) return 0;
        return 1 + countHelper(node->left) + countHelper(node->right);
    }
    
    Node* searchHelper(Node* node, int val) {
        if (node == nullptr || node->data == val) return node;
        Node* found = searchHelper(node->left, val);
        if (found != nullptr) return found;
        return searchHelper(node->right, val);
    }
    
public:
    BinaryTree() : root(nullptr) {}
    
    ~BinaryTree() {
        destroyTree(root);
    }
    
    // Insert level order (untuk membuat complete binary tree)
    void insert(int data) {
        Node* newNode = new Node(data);
        
        if (root == nullptr) {
            root = newNode;
            return;
        }
        
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
    
    // Traversals
    void preorder() {
        cout << "Preorder: ";
        preorderHelper(root);
        cout << endl;
    }
    
    void inorder() {
        cout << "Inorder: ";
        inorderHelper(root);
        cout << endl;
    }
    
    void postorder() {
        cout << "Postorder: ";
        postorderHelper(root);
        cout << endl;
    }
    
    void levelOrder() {
        if (root == nullptr) return;
        
        cout << "Level-order: ";
        queue<Node*> q;
        q.push(root);
        
        while (!q.empty()) {
            Node* current = q.front();
            q.pop();
            cout << current->data << " ";
            
            if (current->left) q.push(current->left);
            if (current->right) q.push(current->right);
        }
        cout << endl;
    }
    
    // Properties
    int height() { return heightHelper(root); }
    int count() { return countHelper(root); }
    bool isEmpty() { return root == nullptr; }
    
    // Search
    bool search(int val) {
        return searchHelper(root, val) != nullptr;
    }
    
    // Print tree
    void printTree(Node* node = nullptr, string prefix = "", bool isLeft = true) {
        if (node == nullptr) {
            if (root == nullptr) {
                cout << "Tree is empty" << endl;
                return;
            }
            node = root;
            cout << node->data << endl;
            if (node->left || node->right) {
                if (node->left) printTree(node->left, "", true);
                if (node->right) printTree(node->right, "", false);
            }
            return;
        }
        
        cout << prefix << (isLeft ? "├── " : "└── ") << node->data << endl;
        
        string newPrefix = prefix + (isLeft ? "│   " : "    ");
        if (node->left || node->right) {
            if (node->left) printTree(node->left, newPrefix, node->right != nullptr);
            if (node->right) printTree(node->right, newPrefix, false);
        }
    }
};

int main() {
    BinaryTree tree;
    
    // Insert nodes
    for (int i = 1; i <= 7; i++) {
        tree.insert(i * 10);
    }
    
    cout << "=== Complete Binary Tree Demo ===" << endl;
    cout << "\n--- Tree Structure ---" << endl;
    tree.printTree();
    
    cout << "\n--- Traversals ---" << endl;
    tree.preorder();
    tree.inorder();
    tree.postorder();
    tree.levelOrder();
    
    cout << "\n--- Properties ---" << endl;
    cout << "Height: " << tree.height() << endl;
    cout << "Node count: " << tree.count() << endl;
    
    cout << "\n--- Search ---" << endl;
    cout << "Search 30: " << (tree.search(30) ? "Found" : "Not found") << endl;
    cout << "Search 100: " << (tree.search(100) ? "Found" : "Not found") << endl;
    
    return 0;
}
```

**Output:**
```
=== Complete Binary Tree Demo ===

--- Tree Structure ---
10
├── 20
│   ├── 40
│   └── 50
└── 30
    ├── 60
    └── 70

--- Traversals ---
Preorder: 10 20 40 50 30 60 70 
Inorder: 40 20 50 10 60 30 70 
Postorder: 40 50 20 60 70 30 10 
Level-order: 10 20 30 40 50 60 70 

--- Properties ---
Height: 2
Node count: 7

--- Search ---
Search 30: Found
Search 100: Not found
```

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan. Jawaban singkat tersedia di bagian akhir.

### Problem S1 ⭐
Sebuah complete binary tree memiliki 15 nodes. Berapakah height tree tersebut?

### Problem S2 ⭐⭐
Diberikan preorder: 1, 2, 4, 5, 3, 6 dan inorder: 4, 2, 5, 1, 3, 6. Gambarkan tree-nya dan tentukan hasil postorder!

### Problem S3 ⭐⭐
Implementasikan fungsi untuk menghitung jumlah leaf dalam binary tree!

### Problem S4 ⭐⭐⭐
Jelaskan mengapa postorder traversal digunakan untuk menghapus tree dan mengapa tidak bisa menggunakan preorder!

### Problem S5 ⭐⭐⭐
Implementasikan fungsi untuk mencari jarak antara dua node dalam binary tree!

---

## Ringkasan

| Konsep | Deskripsi | Kompleksitas |
|--------|-----------|--------------|
| **Tree** | Struktur data hierarkis non-linear dengan root dan children | - |
| **Binary Tree** | Tree di mana setiap node memiliki maksimal 2 children | - |
| **Full Binary Tree** | Setiap node memiliki 0 atau 2 children | n = 2^(h+1) - 1 (max) |
| **Complete Binary Tree** | Semua level penuh kecuali terakhir, diisi dari kiri | Cocok untuk array |
| **Perfect Binary Tree** | Semua leaf di level sama, internal punya 2 children | n = 2^(h+1) - 1 |
| **Preorder** | Root → Left → Right | O(n) time, O(h) space |
| **Inorder** | Left → Root → Right | O(n) time, O(h) space |
| **Postorder** | Left → Right → Root | O(n) time, O(h) space |
| **Level-order** | Level by level dengan Queue | O(n) time, O(w) space |
| **Height** | Edge terpanjang dari node ke leaf | O(n) |
| **Expression Tree** | Binary tree untuk ekspresi matematika | - |

---

## Jawaban Supplementary Problems

**S1:** Height = 3
- Untuk complete binary tree, h = ⌊log₂(n)⌋ = ⌊log₂(15)⌋ = 3

**S2:** 
Tree:
```
      1
     / \
    2   3
   / \   \
  4   5   6
```
Postorder: 4, 5, 2, 6, 3, 1

**S3:**
```cpp
int countLeaves(Node* root) {
    if (root == nullptr) return 0;
    if (root->left == nullptr && root->right == nullptr) return 1;
    return countLeaves(root->left) + countLeaves(root->right);
}
```

**S4:** 
- Postorder mengunjungi children sebelum parent
- Harus hapus children dulu sebelum parent untuk menghindari memory leak
- Jika preorder (hapus parent dulu), kita kehilangan akses ke children

**S5:**
```cpp
int findDistance(Node* root, int n1, int n2) {
    Node* lca = findLCA(root, n1, n2);
    int d1 = findDepth(lca, n1, 0);
    int d2 = findDepth(lca, n2, 0);
    return d1 + d2;
}
```

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 12.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 4.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapters 9-10.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
