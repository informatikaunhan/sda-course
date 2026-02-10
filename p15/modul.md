# Modul 15: Review dan Integrasi Struktur Data

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 15  
**Topik:** Review dan Integrasi Struktur Data

> **Capaian Pembelajaran:** Sub-CPMK-7.1, Sub-CPMK-7.2 — Mampu menganalisis trade-off dalam pemilihan struktur data dan mengintegrasikan berbagai struktur data untuk menyelesaikan masalah kompleks

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen (seluruh bab terkait); Weiss (seluruh bab terkait)

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Mengidentifikasi** karakteristik utama dari setiap struktur data yang telah dipelajari
2. **Menganalisis** kompleksitas waktu dan ruang dari berbagai operasi struktur data
3. **Membandingkan** trade-off antara berbagai struktur data
4. **Menentukan** struktur data yang optimal berdasarkan kriteria pemilihan
5. **Mengintegrasikan** beberapa struktur data untuk menyelesaikan masalah kompleks
6. **Mengimplementasikan** solusi untuk studi kasus nyata menggunakan kombinasi struktur data
7. **Mempersiapkan** diri untuk Ujian Akhir Semester dengan pemahaman komprehensif

---

## 1. Review Komprehensif Struktur Data

### 1.1 Peta Struktur Data dalam Mata Kuliah

Sepanjang semester ini, kita telah mempelajari berbagai struktur data yang dapat diklasifikasikan sebagai berikut:

![Peta Struktur Data SDA201](images/gambar-15-1.png)

*Gambar 15.1: Peta komprehensif struktur data yang dipelajari dalam SDA201*

### 1.2 Ringkasan Struktur Data Linear

| Struktur Data | Karakteristik Utama | Operasi Utama | Kompleksitas |
|---------------|---------------------|---------------|--------------|
| **Array Dinamis** | Akses random O(1), ukuran fleksibel | Access, Insert, Delete | Access: O(1), Insert/Delete: O(n) |
| **Single Linked List** | Node dengan satu pointer next | Insert/Delete di head | Insert/Delete head: O(1), Search: O(n) |
| **Double Linked List** | Node dengan pointer prev dan next | Traversal dua arah | Insert/Delete: O(1)*, Search: O(n) |
| **Circular Linked List** | Tail terhubung ke head | Round-robin traversal | Insert/Delete: O(1)*, Search: O(n) |
| **Stack** | LIFO (Last In First Out) | Push, Pop, Peek | Semua: O(1) |
| **Queue** | FIFO (First In First Out) | Enqueue, Dequeue, Front | Semua: O(1) |
| **Deque** | Double-ended queue | Insert/Delete di kedua ujung | Semua: O(1) |

*\* dengan asumsi pointer ke posisi sudah diketahui*

### 1.3 Ringkasan Struktur Data Non-Linear

| Struktur Data | Karakteristik Utama | Operasi Utama | Kompleksitas |
|---------------|---------------------|---------------|--------------|
| **Binary Tree** | Max 2 children per node | Traversal (Pre/In/Post/Level) | Traversal: O(n) |
| **BST** | Left < Root < Right | Search, Insert, Delete | Average: O(log n), Worst: O(n) |
| **Heap** | Complete binary tree + heap property | Insert, Extract | Insert/Extract: O(log n), Build: O(n) |
| **Priority Queue** | Elemen dengan prioritas | Insert, ExtractMax/Min | Insert/Extract: O(log n) |
| **Hash Table** | Key-value mapping | Insert, Search, Delete | Average: O(1), Worst: O(n) |

### 1.4 Ringkasan Algoritma

| Algoritma | Paradigma | Kompleksitas Waktu | Kompleksitas Ruang | Stable |
|-----------|-----------|-------------------|-------------------|--------|
| **Bubble Sort** | Comparison | O(n²) | O(1) | Ya |
| **Selection Sort** | Comparison | O(n²) | O(1) | Tidak |
| **Insertion Sort** | Comparison | O(n²), Best: O(n) | O(1) | Ya |
| **Merge Sort** | Divide & Conquer | O(n log n) | O(n) | Ya |
| **Quick Sort** | Divide & Conquer | Avg: O(n log n), Worst: O(n²) | O(log n) | Tidak |
| **Heap Sort** | Selection + Heap | O(n log n) | O(1) | Tidak |

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Sebutkan struktur data yang paling cocok untuk masing-masing situasi berikut:
1. Menyimpan history browser
2. Mengelola antrian print job
3. Mencari kontak berdasarkan nama dengan cepat
4. Menyimpan hierarki folder

**Penyelesaian:**

| Situasi | Struktur Data | Alasan |
|---------|---------------|--------|
| History browser | **Stack** | LIFO - halaman terakhir dikunjungi harus bisa di-back pertama |
| Antrian print job | **Queue** | FIFO - dokumen pertama masuk harus diprint pertama |
| Pencarian kontak | **Hash Table** atau **BST** | Hash Table: O(1) average, BST: O(log n) dengan sorted traversal |
| Hierarki folder | **Tree** (N-ary Tree) | Struktur parent-child alami untuk folder dan subfolder |

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Lengkapi tabel berikut dengan kompleksitas waktu yang tepat!

| Operasi | Array | Linked List | Stack | Queue | BST (Balanced) | Hash Table |
|---------|-------|-------------|-------|-------|----------------|------------|
| Access by index | ? | ? | ? | ? | ? | ? |
| Search | ? | ? | ? | ? | ? | ? |
| Insert at beginning | ? | ? | ? | ? | ? | ? |
| Insert at end | ? | ? | ? | ? | ? | ? |

**Penyelesaian:**

| Operasi | Array | Linked List | Stack | Queue | BST (Balanced) | Hash Table |
|---------|:-----:|:-----------:|:-----:|:-----:|:--------------:|:----------:|
| Access by index | O(1) | O(n) | O(n) | O(n) | O(n) | O(1)* |
| Search | O(n) | O(n) | O(n) | O(n) | O(log n) | O(1) avg |
| Insert at beginning | O(n) | O(1) | N/A | N/A | O(log n) | O(1) avg |
| Insert at end | O(1)** | O(n)*** | O(1) | O(1) | O(log n) | O(1) avg |

*\* jika key diketahui*  
*\*\* amortized, jika kapasitas cukup*  
*\*\*\* O(1) jika ada tail pointer*

---

## 2. Perbandingan dan Trade-off

### 2.1 Array vs Linked List

> **Trade-off Fundamental:** Array unggul dalam akses random, Linked List unggul dalam insert/delete dinamis.

![Array vs Linked List Comparison](images/gambar-15-2.png)

*Gambar 15.2: Perbandingan visual Array dan Linked List*

**Kapan menggunakan Array:**
- Membutuhkan akses random yang cepat
- Ukuran data relatif tetap atau dapat diprediksi
- Iterasi berurutan yang sering
- Memory locality penting (cache-friendly)

**Kapan menggunakan Linked List:**
- Insert/delete sering terjadi di berbagai posisi
- Ukuran data sangat dinamis dan tidak dapat diprediksi
- Tidak memerlukan akses random
- Implementasi struktur data lain (Stack, Queue)

### 2.2 Stack vs Queue vs Deque

| Aspek | Stack | Queue | Deque |
|-------|-------|-------|-------|
| **Prinsip** | LIFO | FIFO | Double-ended |
| **Insert** | Push (top) | Enqueue (rear) | Push front/back |
| **Remove** | Pop (top) | Dequeue (front) | Pop front/back |
| **Akses** | Top only | Front only | Front dan back |
| **Use Case** | Undo, recursion | BFS, scheduling | Sliding window |

### 2.3 BST vs Hash Table

> **Pilihan Kritis:** BST mempertahankan urutan data, Hash Table memberikan O(1) average lookup.

| Kriteria | BST | Hash Table |
|----------|-----|------------|
| **Search** | O(log n) - guaranteed | O(1) avg, O(n) worst |
| **Insert** | O(log n) | O(1) avg |
| **Delete** | O(log n) | O(1) avg |
| **Ordered traversal** | Ya (inorder) | Tidak |
| **Range queries** | Efisien | Tidak efisien |
| **Memory overhead** | Pointer per node | Load factor dependent |
| **Worst case** | O(n) jika tidak balanced | O(n) jika banyak collision |

---

### SOLVED PROBLEM 3 ⭐⭐

**Soal:** Sebuah aplikasi memerlukan operasi berikut dengan frekuensi yang berbeda:
- Search by key: 1000 kali/detik
- Insert: 10 kali/detik
- Range query (find all values between min and max): 5 kali/detik

Struktur data mana yang paling cocok? Jelaskan alasannya!

**Penyelesaian:**

**Analisis kebutuhan:**
1. Search sangat frequent → perlu O(1) atau O(log n)
2. Insert jarang → tidak kritis
3. Range query ada → perlu ordered structure

**Perbandingan kandidat:**

| Struktur Data | Search | Insert | Range Query |
|---------------|--------|--------|-------------|
| Hash Table | O(1) ✓ | O(1) ✓ | O(n) ✗ |
| BST (Balanced) | O(log n) | O(log n) | O(k + log n) ✓ |
| Array Sorted | O(log n) | O(n) | O(k + log n) ✓ |

**Rekomendasi: Balanced BST (seperti AVL atau Red-Black Tree)**

**Alasan:**
1. Search O(log n) cukup cepat untuk 1000 ops/detik
2. Insert O(log n) tidak masalah karena hanya 10/detik
3. **Range query efisien**: Cukup find start point, lalu inorder traversal

Jika range query tidak diperlukan, Hash Table akan lebih baik karena O(1) search.

---

### SOLVED PROBLEM 4 ⭐⭐

**Soal:** Jelaskan mengapa Heap lebih cocok untuk Priority Queue dibandingkan dengan:
a) Array terurut
b) Linked List terurut
c) BST

**Penyelesaian:**

**a) Heap vs Array Terurut:**

| Operasi | Heap | Array Terurut |
|---------|------|---------------|
| Insert | O(log n) | O(n) - perlu geser elemen |
| ExtractMax | O(log n) | O(1) - ambil dari ujung |
| FindMax | O(1) | O(1) |

**Kesimpulan:** Heap lebih baik karena insert O(log n) vs O(n)

**b) Heap vs Linked List Terurut:**

| Operasi | Heap | Linked List Terurut |
|---------|------|---------------------|
| Insert | O(log n) | O(n) - perlu traverse |
| ExtractMax | O(log n) | O(1) - dari head |
| FindMax | O(1) | O(1) |

**Kesimpulan:** Heap lebih baik karena insert O(log n) vs O(n)

**c) Heap vs BST:**

| Operasi | Heap | BST (Balanced) |
|---------|------|----------------|
| Insert | O(log n) | O(log n) |
| ExtractMax | O(log n) | O(log n) |
| FindMax | O(1) | O(log n) - traverse ke kanan |

**Kesimpulan:** Heap lebih baik karena:
- FindMax O(1) karena max selalu di root
- Implementasi lebih sederhana dengan array
- Memory overhead lebih kecil (tidak perlu pointer)

---

## 3. Kriteria Pemilihan Struktur Data

### 3.1 Framework Pemilihan

Saat memilih struktur data, pertimbangkan kriteria berikut:

![Decision Framework](images/gambar-15-3.png)

*Gambar 15.3: Framework pemilihan struktur data*

### 3.2 Faktor-faktor Pertimbangan

**1. Jenis Operasi yang Dominan:**
- Read-heavy → Hash Table, Array
- Write-heavy → Linked List, Hash Table
- Mixed → BST, Skip List

**2. Frekuensi Operasi:**
- Operasi yang sering dilakukan harus memiliki kompleksitas rendah
- Operasi jarang dapat memiliki kompleksitas lebih tinggi

**3. Ukuran Data:**
- Data kecil (< 100 elemen): Kompleksitas tidak terlalu signifikan
- Data besar (> 10000 elemen): Perbedaan O(n) vs O(log n) sangat signifikan

**4. Memory Constraint:**
- Terbatas → Array, in-place algorithms
- Cukup → Linked List, Tree dengan pointer

**5. Ordered Requirement:**
- Perlu sorted output → BST, Sorted Array
- Tidak perlu order → Hash Table

### 3.3 Tabel Keputusan Cepat

| Kebutuhan | Struktur Data Terbaik | Alternatif |
|-----------|----------------------|------------|
| Search by key cepat | Hash Table | BST |
| Search by value | BST | Sorted Array |
| Insert/Delete cepat | Linked List | Hash Table |
| LIFO access | Stack | Array |
| FIFO access | Queue | Circular Array |
| Prioritas | Heap | BST |
| Sorted output | BST | Sorted Array |
| Range query | BST | Sorted Array |
| Frequency count | Hash Table | BST |
| Graph adjacency | Adjacency List/Matrix | Hash Table |

---

### SOLVED PROBLEM 5 ⭐

**Soal:** Tentukan struktur data yang tepat untuk implementasi berikut:
1. Autocomplete search (prefix matching)
2. Undo/Redo di text editor
3. Task scheduler dengan prioritas
4. Deteksi duplicate dalam dataset besar

**Penyelesaian:**

| Implementasi | Struktur Data | Alasan |
|--------------|---------------|--------|
| Autocomplete | **Trie** (atau Hash Map dengan prefix keys) | Efisien untuk prefix matching, O(m) dimana m = panjang prefix |
| Undo/Redo | **Dua Stack** (undo stack + redo stack) | LIFO natural untuk operasi undo, push ke redo saat undo |
| Task scheduler | **Heap (Priority Queue)** | ExtractMax/Min untuk task dengan prioritas tertinggi |
| Deteksi duplicate | **Hash Set** | Insert dan check existence O(1) average |

**Catatan:** Trie (prefix tree) adalah struktur data khusus yang akan dipelajari di mata kuliah lanjutan. Untuk saat ini, Hash Table dengan prefix sebagai key dapat menjadi alternatif sederhana.

---

### SOLVED PROBLEM 6 ⭐⭐

**Soal:** Sebuah sistem perlu menyimpan 1 juta record dengan atribut:
- ID (unique integer)
- Nama (string)
- Timestamp (untuk sorting)

Operasi yang dibutuhkan:
- Lookup by ID: sangat sering
- Insert: moderately frequent
- Get records in time range: occasional

Desain struktur data yang optimal!

**Penyelesaian:**

**Desain: Kombinasi Hash Table + BST**

```cpp
#include <unordered_map>
#include <map>
#include <string>

struct Record {
    int id;
    string nama;
    long timestamp;
};

class SystemData {
private:
    // Hash Table untuk lookup by ID - O(1)
    unordered_map<int, Record*> byId;
    
    // BST (std::map) untuk range query by timestamp - O(log n)
    map<long, Record*> byTimestamp;
    
public:
    // Insert: O(1) + O(log n) = O(log n)
    void insert(Record* r) {
        byId[r->id] = r;
        byTimestamp[r->timestamp] = r;
    }
    
    // Lookup by ID: O(1)
    Record* findById(int id) {
        if (byId.find(id) != byId.end())
            return byId[id];
        return nullptr;
    }
    
    // Range query by timestamp: O(log n + k)
    vector<Record*> getInRange(long start, long end) {
        vector<Record*> result;
        auto it = byTimestamp.lower_bound(start);
        while (it != byTimestamp.end() && it->first <= end) {
            result.push_back(it->second);
            ++it;
        }
        return result;
    }
};
```

**Trade-off:**
- Memory: 2x pointer overhead
- Insert: O(log n) bukan O(1)
- Lookup by ID: O(1) - optimal
- Range query: O(log n + k) - optimal

---

## 4. Studi Kasus: LRU Cache

### 4.1 Definisi dan Kebutuhan

> **LRU Cache** (Least Recently Used Cache) adalah struktur data yang menyimpan sejumlah terbatas item dan menghapus item yang paling lama tidak digunakan ketika kapasitas penuh.

**Operasi yang diperlukan:**
1. `get(key)`: Mengembalikan value jika ada, -1 jika tidak ada. **Harus O(1)**
2. `put(key, value)`: Insert atau update. Jika kapasitas penuh, hapus LRU. **Harus O(1)**

### 4.2 Analisis Struktur Data

**Pendekatan 1: Hanya Hash Table**
- get: O(1) ✓
- put: O(1) ✓
- Track LRU: ✗ Tidak bisa menentukan mana yang paling lama

**Pendekatan 2: Hanya Linked List (ordered by recency)**
- get: O(n) ✗ Harus traverse untuk mencari
- put: O(n) ✗ Harus traverse
- Track LRU: ✓ Tail adalah LRU

**Pendekatan 3: Hash Table + Doubly Linked List ✓**
- get: O(1) via hash + O(1) move to front
- put: O(1) via hash + O(1) insert at front + O(1) remove LRU
- Track LRU: ✓ Tail adalah LRU

### 4.3 Implementasi

![LRU Cache Structure](images/gambar-15-4.png)

*Gambar 15.4: Struktur LRU Cache menggunakan Hash Table + Doubly Linked List*

```cpp
#include <unordered_map>
using namespace std;

class LRUCache {
private:
    struct Node {
        int key, value;
        Node* prev;
        Node* next;
        Node(int k, int v) : key(k), value(v), prev(nullptr), next(nullptr) {}
    };
    
    int capacity;
    unordered_map<int, Node*> cache;  // Hash Table
    Node* head;  // Dummy head (MRU side)
    Node* tail;  // Dummy tail (LRU side)
    
    // Helper: Remove node from list
    void removeNode(Node* node) {
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }
    
    // Helper: Add node right after head (MRU position)
    void addToFront(Node* node) {
        node->next = head->next;
        node->prev = head;
        head->next->prev = node;
        head->next = node;
    }
    
    // Helper: Move existing node to front
    void moveToFront(Node* node) {
        removeNode(node);
        addToFront(node);
    }

public:
    LRUCache(int cap) : capacity(cap) {
        // Initialize dummy head and tail
        head = new Node(0, 0);
        tail = new Node(0, 0);
        head->next = tail;
        tail->prev = head;
    }
    
    int get(int key) {
        if (cache.find(key) == cache.end()) {
            return -1;  // Not found
        }
        
        Node* node = cache[key];
        moveToFront(node);  // Update to most recently used
        return node->value;
    }
    
    void put(int key, int value) {
        // If key exists, update value and move to front
        if (cache.find(key) != cache.end()) {
            Node* node = cache[key];
            node->value = value;
            moveToFront(node);
            return;
        }
        
        // If at capacity, remove LRU (node before tail)
        if (cache.size() == capacity) {
            Node* lru = tail->prev;
            removeNode(lru);
            cache.erase(lru->key);
            delete lru;
        }
        
        // Insert new node at front
        Node* newNode = new Node(key, value);
        cache[key] = newNode;
        addToFront(newNode);
    }
    
    ~LRUCache() {
        // Clean up all nodes
        Node* curr = head;
        while (curr != nullptr) {
            Node* next = curr->next;
            delete curr;
            curr = next;
        }
    }
};
```

---

### SOLVED PROBLEM 7 ⭐⭐⭐

**Soal:** Trace eksekusi LRU Cache dengan kapasitas 3 untuk operasi berikut:
```
put(1, 10), put(2, 20), put(3, 30), get(1), put(4, 40), get(2), put(5, 50)
```
Tunjukkan state cache setelah setiap operasi!

**Penyelesaian:**

| Operasi | Cache State (MRU → LRU) | Return | Catatan |
|---------|-------------------------|--------|---------|
| Initial | [] | - | Empty cache |
| put(1, 10) | [1:10] | - | Insert 1 |
| put(2, 20) | [2:20 ↔ 1:10] | - | Insert 2, 2 is MRU |
| put(3, 30) | [3:30 ↔ 2:20 ↔ 1:10] | - | Insert 3, 3 is MRU |
| get(1) | [1:10 ↔ 3:30 ↔ 2:20] | 10 | Access 1, move to MRU |
| put(4, 40) | [4:40 ↔ 1:10 ↔ 3:30] | - | Capacity full, evict 2 (LRU), insert 4 |
| get(2) | [4:40 ↔ 1:10 ↔ 3:30] | -1 | 2 was evicted, not found |
| put(5, 50) | [5:50 ↔ 4:40 ↔ 1:10] | - | Evict 3 (LRU), insert 5 |

**Final State:** Hash Table berisi {5, 4, 1}, Linked List: 5 ↔ 4 ↔ 1

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Mengapa LRU Cache menggunakan Doubly Linked List, bukan Single Linked List?

**Penyelesaian:**

**Alasan Utama: Operasi delete memerlukan O(1)**

Ketika `get(key)` dipanggil, node harus dipindahkan ke front (MRU position). Ini memerlukan:
1. Remove node dari posisi saat ini
2. Insert node di front

**Dengan Single Linked List:**
- Untuk remove node, perlu pointer ke node sebelumnya
- Harus traverse dari head untuk mencari prev: **O(n)**

**Dengan Doubly Linked List:**
- Setiap node memiliki pointer `prev`
- Remove: `node->prev->next = node->next` dan `node->next->prev = node->prev`: **O(1)**

```
Single Linked List Remove:
  head → A → B → C → tail
  Untuk remove B, perlu find A dulu (traverse dari head)
  
Doubly Linked List Remove:
  head ↔ A ↔ B ↔ C ↔ tail
  B->prev = A, B->next = C
  Langsung: A->next = C, C->prev = A (O(1))
```

**Kesimpulan:** Doubly Linked List memungkinkan semua operasi LRU Cache menjadi O(1).

---

## 5. Studi Kasus: Text Editor dengan Undo/Redo

### 5.1 Analisis Kebutuhan

Text editor memerlukan fitur:
1. **Insert** text di posisi kursor
2. **Delete** text
3. **Undo** membatalkan operasi terakhir
4. **Redo** mengulangi operasi yang di-undo

### 5.2 Desain dengan Dua Stack

> **Pattern:** Gunakan dua stack — undo stack untuk operasi yang dilakukan, redo stack untuk operasi yang di-undo.

![Text Editor Undo Redo](images/gambar-15-5.png)

*Gambar 15.5: Mekanisme Undo/Redo dengan dua Stack*

### 5.3 Implementasi

```cpp
#include <stack>
#include <string>
using namespace std;

// Struktur untuk menyimpan operasi
struct Operation {
    enum Type { INSERT, DELETE };
    Type type;
    int position;
    string text;
    
    Operation(Type t, int pos, const string& txt) 
        : type(t), position(pos), text(txt) {}
    
    // Inverse operation untuk undo
    Operation inverse() const {
        if (type == INSERT) {
            return Operation(DELETE, position, text);
        } else {
            return Operation(INSERT, position, text);
        }
    }
};

class TextEditor {
private:
    string document;
    stack<Operation> undoStack;
    stack<Operation> redoStack;
    
    void applyOperation(const Operation& op) {
        if (op.type == Operation::INSERT) {
            document.insert(op.position, op.text);
        } else {  // DELETE
            document.erase(op.position, op.text.length());
        }
    }
    
public:
    TextEditor() : document("") {}
    
    // Insert text at position
    void insert(int position, const string& text) {
        Operation op(Operation::INSERT, position, text);
        applyOperation(op);
        undoStack.push(op);
        
        // Clear redo stack - new operation invalidates redo history
        while (!redoStack.empty()) redoStack.pop();
    }
    
    // Delete text at position with given length
    void deleteText(int position, int length) {
        string deletedText = document.substr(position, length);
        Operation op(Operation::DELETE, position, deletedText);
        applyOperation(op);
        undoStack.push(op);
        
        // Clear redo stack
        while (!redoStack.empty()) redoStack.pop();
    }
    
    // Undo last operation
    bool undo() {
        if (undoStack.empty()) return false;
        
        Operation lastOp = undoStack.top();
        undoStack.pop();
        
        // Apply inverse operation
        Operation inverseOp = lastOp.inverse();
        applyOperation(inverseOp);
        
        // Push original operation to redo stack
        redoStack.push(lastOp);
        
        return true;
    }
    
    // Redo last undone operation
    bool redo() {
        if (redoStack.empty()) return false;
        
        Operation redoOp = redoStack.top();
        redoStack.pop();
        
        // Apply the operation again
        applyOperation(redoOp);
        
        // Push back to undo stack
        undoStack.push(redoOp);
        
        return true;
    }
    
    string getDocument() const { return document; }
};
```

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Trace text editor berikut dan tunjukkan state setelah setiap operasi:
```cpp
TextEditor editor;
editor.insert(0, "Hello");
editor.insert(5, " World");
editor.deleteText(5, 6);
editor.undo();
editor.undo();
editor.redo();
```

**Penyelesaian:**

| # | Operasi | Document | Undo Stack | Redo Stack |
|---|---------|----------|------------|------------|
| 0 | Initial | "" | [] | [] |
| 1 | insert(0, "Hello") | "Hello" | [INS(0,"Hello")] | [] |
| 2 | insert(5, " World") | "Hello World" | [INS(0,"Hello"), INS(5," World")] | [] |
| 3 | delete(5, 6) | "Hello" | [..., DEL(5," World")] | [] |
| 4 | undo() | "Hello World" | [INS(0,"Hello"), INS(5," World")] | [DEL(5," World")] |
| 5 | undo() | "Hello" | [INS(0,"Hello")] | [DEL(...), INS(5," World")] |
| 6 | redo() | "Hello World" | [INS(0,"Hello"), INS(5," World")] | [DEL(5," World")] |

**Final State:** Document = "Hello World"

---

### SOLVED PROBLEM 10 ⭐⭐⭐

**Soal:** Bagaimana mengimplementasikan batasan jumlah undo (misalnya maksimal 50 operasi)? Modifikasi desain untuk mendukung ini!

**Penyelesaian:**

**Pendekatan: Gunakan Deque atau Circular Buffer sebagai pengganti Stack**

```cpp
#include <deque>

class TextEditorWithLimit {
private:
    string document;
    deque<Operation> undoDeque;  // Gunakan deque bukan stack
    stack<Operation> redoStack;
    int maxUndoCount;
    
public:
    TextEditorWithLimit(int maxUndo = 50) : maxUndoCount(maxUndo) {}
    
    void insert(int position, const string& text) {
        Operation op(Operation::INSERT, position, text);
        applyOperation(op);
        
        // Add to back of deque
        undoDeque.push_back(op);
        
        // If exceed limit, remove oldest (front)
        if (undoDeque.size() > maxUndoCount) {
            undoDeque.pop_front();
        }
        
        // Clear redo
        while (!redoStack.empty()) redoStack.pop();
    }
    
    bool undo() {
        if (undoDeque.empty()) return false;
        
        // Get from back (most recent)
        Operation lastOp = undoDeque.back();
        undoDeque.pop_back();
        
        Operation inverseOp = lastOp.inverse();
        applyOperation(inverseOp);
        
        redoStack.push(lastOp);
        return true;
    }
    
    // ... rest of methods similar
};
```

**Perubahan kunci:**
1. Gunakan `deque` yang memungkinkan akses di kedua ujung
2. `push_back()` untuk operasi baru (seperti stack push)
3. `pop_back()` untuk undo (seperti stack pop)
4. `pop_front()` untuk menghapus operasi terlama saat limit tercapai

**Kompleksitas tetap O(1)** untuk semua operasi karena deque mendukung O(1) operation di kedua ujung.

---

## 6. Studi Kasus: Sistem Manajemen Data Pertahanan

### 6.1 Skenario

> **Skenario:** Komando pusat memerlukan sistem manajemen data untuk tracking aset pertahanan. Sistem harus mendukung berbagai operasi dengan performa tinggi.

**Kebutuhan:**
1. Lookup aset by ID: sangat sering
2. Lookup aset by lokasi (koordinat region): sering
3. Mendapatkan aset dengan prioritas tertinggi: sering
4. Insert aset baru: moderate
5. Update posisi aset: sering
6. History pergerakan: tersedia

### 6.2 Desain Multi-Index

Untuk memenuhi kebutuhan di atas, kita perlu kombinasi beberapa struktur data:

![Multi-Index System](images/gambar-15-6.png)

*Gambar 15.6: Arsitektur sistem multi-index untuk manajemen aset pertahanan*

### 6.3 Implementasi

```cpp
#include <unordered_map>
#include <map>
#include <queue>
#include <stack>
#include <vector>
#include <string>
using namespace std;

struct Koordinat {
    double latitude;
    double longitude;
    
    // Untuk BST ordering berdasarkan region
    bool operator<(const Koordinat& other) const {
        if (latitude != other.latitude) return latitude < other.latitude;
        return longitude < other.longitude;
    }
};

struct Aset {
    int id;
    string nama;
    string tipe;  // pesawat, kapal, kendaraan, dll
    Koordinat lokasi;
    int prioritas;  // 1-10, semakin tinggi semakin penting
    string status;
    
    // Untuk priority queue (max heap by priority)
    bool operator<(const Aset& other) const {
        return prioritas < other.prioritas;  // Max heap
    }
};

struct MovementRecord {
    Koordinat lokasi;
    long timestamp;
};

class SistemManajemenAset {
private:
    // Primary storage
    vector<Aset> asetStorage;
    
    // Index 1: Hash Table untuk lookup by ID - O(1)
    unordered_map<int, int> indexById;  // id -> index in storage
    
    // Index 2: BST untuk lookup by region - O(log n)
    map<Koordinat, vector<int>> indexByRegion;  // koordinat -> list of asset indices
    
    // Index 3: Max Heap untuk prioritas - O(1) get max
    priority_queue<pair<int, int>> priorityHeap;  // (priority, id)
    
    // History: Stack per aset untuk movement history
    unordered_map<int, stack<MovementRecord>> movementHistory;

public:
    // Insert aset baru: O(log n) karena BST dan Heap
    void insertAset(const Aset& aset) {
        int idx = asetStorage.size();
        asetStorage.push_back(aset);
        
        // Update all indexes
        indexById[aset.id] = idx;
        indexByRegion[aset.lokasi].push_back(idx);
        priorityHeap.push({aset.prioritas, aset.id});
        
        // Initialize movement history
        MovementRecord initial = {aset.lokasi, time(nullptr)};
        movementHistory[aset.id].push(initial);
    }
    
    // Lookup by ID: O(1)
    Aset* getById(int id) {
        if (indexById.find(id) == indexById.end()) return nullptr;
        return &asetStorage[indexById[id]];
    }
    
    // Get aset dengan prioritas tertinggi: O(log n) amortized
    Aset* getHighestPriority() {
        while (!priorityHeap.empty()) {
            auto [priority, id] = priorityHeap.top();
            priorityHeap.pop();
            
            // Validate - priority might have changed
            Aset* aset = getById(id);
            if (aset && aset->prioritas == priority) {
                priorityHeap.push({priority, id});  // Put back
                return aset;
            }
        }
        return nullptr;
    }
    
    // Get aset dalam region: O(log n + k)
    vector<Aset*> getByRegion(Koordinat min, Koordinat max) {
        vector<Aset*> result;
        auto start = indexByRegion.lower_bound(min);
        auto end = indexByRegion.upper_bound(max);
        
        for (auto it = start; it != end; ++it) {
            for (int idx : it->second) {
                result.push_back(&asetStorage[idx]);
            }
        }
        return result;
    }
    
    // Update posisi aset: O(log n)
    void updatePosisi(int id, Koordinat newLokasi) {
        Aset* aset = getById(id);
        if (!aset) return;
        
        // Record to history
        MovementRecord record = {newLokasi, time(nullptr)};
        movementHistory[id].push(record);
        
        // Update region index (simplified - should remove from old region)
        Koordinat oldLokasi = aset->lokasi;
        // ... remove from indexByRegion[oldLokasi]
        
        // Update location
        aset->lokasi = newLokasi;
        indexByRegion[newLokasi].push_back(indexById[id]);
    }
    
    // Get movement history: O(1) per access
    stack<MovementRecord>& getHistory(int id) {
        return movementHistory[id];
    }
};
```

---

### SOLVED PROBLEM 11 ⭐⭐⭐

**Soal:** Untuk sistem di atas, analisis trade-off dari desain multi-index:
1. Memory overhead
2. Insert performance
3. Update performance
4. Query performance

**Penyelesaian:**

**1. Memory Overhead:**
- Primary storage: O(n) untuk n aset
- Hash Table index: O(n) entries
- BST index: O(n) entries (bisa less jika banyak aset di lokasi sama)
- Priority Heap: O(n) entries
- Movement history: O(n × m) dimana m = avg movement per aset

**Total: ~4n + nm = O(n × m)**

Trade-off: Memory lebih besar, tapi query lebih cepat.

**2. Insert Performance:**
- Storage: O(1) amortized (vector push_back)
- Hash Table: O(1)
- BST: O(log n)
- Heap: O(log n)

**Total: O(log n)**

**3. Update Performance (posisi):**
- Find: O(1) via hash
- Remove from old BST entry: O(log n)
- Insert to new BST entry: O(log n)
- Push history: O(1)

**Total: O(log n)**

**4. Query Performance:**
| Query Type | Complexity | Structure Used |
|------------|------------|----------------|
| By ID | O(1) | Hash Table |
| By Region | O(log n + k) | BST |
| Highest Priority | O(log n)* | Heap |
| Movement History | O(1) | Stack |

*O(log n) amortized karena lazy deletion of stale entries

**Kesimpulan:** Desain ini optimal untuk read-heavy workload dengan berbagai jenis query.

---

### SOLVED PROBLEM 12 ⭐⭐

**Soal:** Apa kelemahan dari desain di atas dan bagaimana mengatasinya?

**Penyelesaian:**

**Kelemahan 1: Priority Heap tidak mendukung update priority**

**Masalah:** Jika prioritas aset berubah, heap entry lama masih ada (stale).

**Solusi:** 
1. Lazy deletion seperti yang diimplementasikan
2. Atau gunakan indexed priority queue (Fibonacci Heap)

**Kelemahan 2: Delete operation kompleks**

**Masalah:** Harus update semua index saat delete.

**Solusi:** 
1. Soft delete dengan flag `isDeleted`
2. Periodic cleanup (garbage collection)

```cpp
struct Aset {
    // ... fields
    bool isDeleted = false;
};

void deleteAset(int id) {
    Aset* aset = getById(id);
    if (aset) {
        aset->isDeleted = true;  // Soft delete
    }
}
```

**Kelemahan 3: Tidak thread-safe**

**Masalah:** Multiple threads accessing dapat menyebabkan race condition.

**Solusi:** 
1. Mutex locks pada setiap operasi
2. Read-write locks untuk concurrent reads
3. Lock-free data structures untuk high concurrency

**Kelemahan 4: Region index tidak efisien untuk exact coordinate removal**

**Masalah:** Saat update posisi, harus search dalam vector.

**Solusi:**
1. Gunakan `map<Koordinat, set<int>>` untuk O(log n) removal
2. Atau simpan pointer ke parent region di setiap aset

---

## 7. Strategi Integrasi Struktur Data

### 7.1 Pola Umum Integrasi

**Pola 1: Multi-Index (seperti studi kasus di atas)**
- Satu primary storage
- Multiple index structures untuk berbagai jenis query
- Trade-off: Memory vs Query Speed

**Pola 2: Composite Structure**
- Menggabungkan dua struktur menjadi satu
- Contoh: LRU Cache = Hash Table + Doubly Linked List

**Pola 3: Auxiliary Structure**
- Struktur utama untuk data
- Struktur tambahan untuk tracking metadata
- Contoh: Text Editor = String + Undo Stack + Redo Stack

**Pola 4: Layered Structure**
- Struktur bertingkat untuk hierarki
- Contoh: Tree dengan Hash Table di setiap node

### 7.2 Checklist Desain

Saat mendesain sistem dengan multiple struktur data:

1. **Identifikasi operasi dan frekuensinya**
2. **Tentukan kompleksitas target untuk setiap operasi**
3. **Pilih struktur data untuk operasi paling kritis**
4. **Tambahkan index untuk operasi sekunder**
5. **Analisis memory overhead**
6. **Pertimbangkan konsistensi antar struktur**
7. **Implementasikan dengan perhatian pada edge cases**

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Desain struktur data untuk sistem rekomendasi film dengan kebutuhan:
- Search film by title: frequent
- Get films by genre: frequent
- Get top-rated films: frequent
- Add new film: rare
- User rating update: moderate

**Penyelesaian:**

```cpp
struct Film {
    int id;
    string title;
    string genre;
    double avgRating;
    int ratingCount;
};

class FilmRecommendationSystem {
private:
    // Primary: ID → Film
    unordered_map<int, Film> films;
    
    // Index 1: Title → ID (untuk search by title)
    unordered_map<string, int> titleIndex;
    
    // Index 2: Genre → Set of IDs (untuk films by genre)
    unordered_map<string, set<int>> genreIndex;
    
    // Index 3: (Rating, ID) ordered set (untuk top-rated)
    set<pair<double, int>, greater<>> ratingIndex;  // Descending order
    
public:
    // Search by title: O(1)
    Film* searchByTitle(const string& title) {
        if (titleIndex.find(title) == titleIndex.end()) return nullptr;
        return &films[titleIndex[title]];
    }
    
    // Get by genre: O(1) untuk akses, O(k) untuk iterasi
    vector<Film*> getByGenre(const string& genre) {
        vector<Film*> result;
        if (genreIndex.find(genre) != genreIndex.end()) {
            for (int id : genreIndex[genre]) {
                result.push_back(&films[id]);
            }
        }
        return result;
    }
    
    // Get top N rated: O(N)
    vector<Film*> getTopRated(int n) {
        vector<Film*> result;
        int count = 0;
        for (auto& [rating, id] : ratingIndex) {
            if (count >= n) break;
            result.push_back(&films[id]);
            count++;
        }
        return result;
    }
    
    // Update rating: O(log n) karena set operations
    void updateRating(int filmId, double newUserRating) {
        Film& film = films[filmId];
        
        // Remove old entry from rating index
        ratingIndex.erase({film.avgRating, filmId});
        
        // Update average
        double total = film.avgRating * film.ratingCount + newUserRating;
        film.ratingCount++;
        film.avgRating = total / film.ratingCount;
        
        // Insert new entry
        ratingIndex.insert({film.avgRating, filmId});
    }
};
```

---

### SOLVED PROBLEM 14 ⭐⭐⭐

**Soal:** Implementasikan sliding window maximum yang efisien menggunakan kombinasi struktur data yang tepat!

**Problem:** Diberikan array dan window size k, untuk setiap window, kembalikan nilai maksimum.

**Contoh:**
- Input: arr = [1, 3, -1, -3, 5, 3, 6, 7], k = 3
- Output: [3, 3, 5, 5, 6, 7]

**Penyelesaian:**

**Pendekatan: Deque untuk menyimpan kandidat maximum**

```cpp
#include <deque>
#include <vector>
using namespace std;

vector<int> slidingWindowMaximum(vector<int>& arr, int k) {
    vector<int> result;
    deque<int> dq;  // Stores indices, not values
    
    for (int i = 0; i < arr.size(); i++) {
        // Remove indices outside current window
        while (!dq.empty() && dq.front() <= i - k) {
            dq.pop_front();
        }
        
        // Remove smaller elements from back
        // (they can never be maximum while current element exists)
        while (!dq.empty() && arr[dq.back()] < arr[i]) {
            dq.pop_back();
        }
        
        // Add current index
        dq.push_back(i);
        
        // Record result when window is complete
        if (i >= k - 1) {
            result.push_back(arr[dq.front()]);
        }
    }
    
    return result;
}
```

**Trace untuk contoh:**

| i | arr[i] | Window | Deque (indices) | Deque (values) | Max |
|---|--------|--------|-----------------|----------------|-----|
| 0 | 1 | [1] | [0] | [1] | - |
| 1 | 3 | [1,3] | [1] | [3] | - |
| 2 | -1 | [1,3,-1] | [1,2] | [3,-1] | 3 |
| 3 | -3 | [3,-1,-3] | [1,2,3] | [3,-1,-3] | 3 |
| 4 | 5 | [-1,-3,5] | [4] | [5] | 5 |
| 5 | 3 | [-3,5,3] | [4,5] | [5,3] | 5 |
| 6 | 6 | [5,3,6] | [6] | [6] | 6 |
| 7 | 7 | [3,6,7] | [7] | [7] | 7 |

**Kompleksitas:**
- Waktu: O(n) - setiap elemen di-push dan di-pop paling banyak sekali
- Ruang: O(k) - deque menyimpan maksimal k elemen

**Mengapa Deque?**
- Perlu akses di kedua ujung: front untuk maximum, back untuk maintenance
- pop_front O(1) untuk remove expired
- pop_back O(1) untuk remove smaller elements
- push_back O(1) untuk add new element

---

## 8. Persiapan UAS

### 8.1 Topik-topik Penting

Berdasarkan materi Pertemuan 1-15, topik yang perlu dikuasai:

| Pertemuan | Topik | Tingkat Kepentingan |
|-----------|-------|---------------------|
| 1 | ADT, Pointer, Dynamic Memory | ⭐⭐⭐ |
| 2 | Analisis Kompleksitas, Big-O | ⭐⭐⭐ |
| 3-4 | Linked List (Single, Double, Circular) | ⭐⭐⭐ |
| 5 | Stack dan Aplikasi | ⭐⭐⭐ |
| 6 | Queue, Deque | ⭐⭐ |
| 7 | Rekursi, Divide & Conquer | ⭐⭐⭐ |
| 9-10 | Sorting Algorithms | ⭐⭐⭐ |
| 11 | Tree, Binary Tree, Traversal | ⭐⭐ |
| 12 | BST | ⭐⭐⭐ |
| 13 | Heap, Priority Queue | ⭐⭐⭐ |
| 14 | Hash Table | ⭐⭐⭐ |
| 15 | Integrasi & Trade-off | ⭐⭐⭐ |

### 8.2 Jenis Soal yang Mungkin

1. **Trace algoritma:** Tunjukkan step-by-step eksekusi
2. **Implementasi:** Tulis kode untuk operasi tertentu
3. **Analisis kompleksitas:** Tentukan Big-O dari kode
4. **Pemilihan struktur data:** Pilih struktur data optimal untuk skenario
5. **Desain sistem:** Gabungkan beberapa struktur data
6. **Studi kasus:** Aplikasi dalam konteks nyata

### 8.3 Tips Persiapan

1. **Review semua SOLVED PROBLEM** dari setiap modul
2. **Latih tracing** untuk setiap algoritma
3. **Hafalkan kompleksitas** untuk operasi umum
4. **Pahami trade-off** antar struktur data
5. **Praktik coding** tanpa IDE (tulis tangan)
6. **Review studi kasus** pertahanan dari setiap pertemuan

---

### SOLVED PROBLEM 15 ⭐

**Soal:** Untuk setiap operasi berikut, tentukan kompleksitas waktu best case dan worst case!

| Operasi | Best Case | Worst Case |
|---------|-----------|------------|
| Binary Search pada array terurut | ? | ? |
| Insert di BST | ? | ? |
| Quick Sort | ? | ? |
| Hash Table search | ? | ? |

**Penyelesaian:**

| Operasi | Best Case | Worst Case | Penjelasan |
|---------|-----------|------------|------------|
| Binary Search | O(1) | O(log n) | Best: target di tengah; Worst: target di ujung |
| Insert di BST | O(1)* | O(n) | *Akar kosong; Worst: tree menjadi linear |
| Quick Sort | O(n log n) | O(n²) | Best: pivot selalu median; Worst: pivot selalu min/max |
| Hash Table search | O(1) | O(n) | Best: no collision; Worst: all keys collision |

---

### SOLVED PROBLEM 16 ⭐⭐

**Soal:** Berikan contoh skenario nyata dimana:
a) Array lebih baik dari Linked List
b) BST lebih baik dari Hash Table
c) Queue lebih baik dari Stack

**Penyelesaian:**

**a) Array lebih baik dari Linked List:**

**Skenario:** Sistem streaming video yang membaca frame secara berurutan.

**Alasan:**
- Frame dibaca secara sequential → cache-friendly
- Akses random ke frame tertentu (seek) perlu O(1)
- Ukuran frame buffer biasanya tetap
- Memory locality penting untuk performa

**b) BST lebih baik dari Hash Table:**

**Skenario:** Database index yang perlu mendukung range query (misal: "SELECT * WHERE price BETWEEN 100 AND 500").

**Alasan:**
- Range query pada hash table memerlukan scan seluruh data O(n)
- BST dapat range query dalam O(log n + k)
- BST juga mendukung operasi min, max, predecessor, successor

**c) Queue lebih baik dari Stack:**

**Skenario:** Print spooler yang memproses dokumen dalam urutan pengiriman.

**Alasan:**
- Fairness: dokumen yang dikirim duluan harus diprint duluan (FIFO)
- Dengan Stack (LIFO), dokumen terakhir diprint duluan → tidak adil
- User yang mengirim duluan menunggu lebih lama

---

### SOLVED PROBLEM 17 ⭐⭐

**Soal:** Jelaskan apa yang terjadi pada setiap struktur data saat terjadi memory fragmentation, dan bagaimana mengatasinya!

**Penyelesaian:**

| Struktur Data | Dampak Fragmentation | Solusi |
|---------------|---------------------|--------|
| **Array Dinamis** | Tidak bisa expand meski total free memory cukup | Realokasi ke blok kontinu baru; Gunakan memory pool |
| **Linked List** | Minimal dampak - node dapat tersebar | Tidak perlu solusi khusus |
| **Tree/BST** | Minimal - node independen | Tidak perlu solusi khusus |
| **Hash Table (Chaining)** | Minimal - chain nodes tersebar | Tidak perlu solusi khusus |
| **Hash Table (Open Addressing)** | Array harus kontinu | Sama seperti array dinamis |

**Kesimpulan:** 
- Struktur berbasis pointer (linked list, tree) lebih tahan terhadap fragmentation
- Struktur berbasis array perlu memori kontinu

---

### SOLVED PROBLEM 18 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk mendeteksi cycle dalam linked list menggunakan minimum memory!

**Penyelesaian:**

**Algoritma: Floyd's Cycle Detection (Tortoise and Hare)**

```cpp
struct Node {
    int data;
    Node* next;
};

// O(n) time, O(1) space
bool hasCycle(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return false;
    }
    
    Node* slow = head;       // Tortoise - moves 1 step
    Node* fast = head->next; // Hare - moves 2 steps
    
    while (fast != nullptr && fast->next != nullptr) {
        if (slow == fast) {
            return true;  // Cycle detected
        }
        slow = slow->next;
        fast = fast->next->next;
    }
    
    return false;  // No cycle
}

// Bonus: Find cycle start point
Node* findCycleStart(Node* head) {
    if (head == nullptr) return nullptr;
    
    Node* slow = head;
    Node* fast = head;
    
    // Phase 1: Detect cycle
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
        
        if (slow == fast) {
            // Phase 2: Find start of cycle
            slow = head;
            while (slow != fast) {
                slow = slow->next;
                fast = fast->next;
            }
            return slow;  // Start of cycle
        }
    }
    
    return nullptr;  // No cycle
}
```

**Mengapa ini bekerja:**
1. Jika ada cycle, fast pasti akan "menyusul" slow di dalam cycle
2. Untuk menemukan start: jarak dari head ke start = jarak dari meeting point ke start

**Kompleksitas:**
- Waktu: O(n)
- Ruang: O(1) - hanya 2 pointer

---

### SOLVED PROBLEM 19 ⭐

**Soal:** Bandingkan implementasi Queue menggunakan Array vs Linked List!

**Penyelesaian:**

**1. Array-based Queue (Circular Array):**

```cpp
class ArrayQueue {
private:
    int* arr;
    int front, rear, size, capacity;
    
public:
    ArrayQueue(int cap) : capacity(cap), front(0), rear(-1), size(0) {
        arr = new int[capacity];
    }
    
    void enqueue(int x) {
        if (size == capacity) throw overflow_error("Full");
        rear = (rear + 1) % capacity;
        arr[rear] = x;
        size++;
    }
    
    int dequeue() {
        if (size == 0) throw underflow_error("Empty");
        int val = arr[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }
};
```

**2. Linked List-based Queue:**

```cpp
class LinkedQueue {
private:
    struct Node {
        int data;
        Node* next;
    };
    Node* front;
    Node* rear;
    
public:
    LinkedQueue() : front(nullptr), rear(nullptr) {}
    
    void enqueue(int x) {
        Node* newNode = new Node{x, nullptr};
        if (rear == nullptr) {
            front = rear = newNode;
        } else {
            rear->next = newNode;
            rear = newNode;
        }
    }
    
    int dequeue() {
        if (front == nullptr) throw underflow_error("Empty");
        int val = front->data;
        Node* temp = front;
        front = front->next;
        if (front == nullptr) rear = nullptr;
        delete temp;
        return val;
    }
};
```

**Perbandingan:**

| Aspek | Array Queue | Linked Queue |
|-------|-------------|--------------|
| Enqueue | O(1) | O(1) |
| Dequeue | O(1) | O(1) |
| Memory per element | sizeof(int) | sizeof(Node) = int + pointer |
| Max size | Fixed (atau perlu resize) | Unlimited |
| Cache performance | Baik | Kurang baik |
| Memory allocation | Sekali di awal | Setiap enqueue |

---

### SOLVED PROBLEM 20 ⭐⭐

**Soal:** Desain struktur data untuk browser tab manager dengan fitur:
- Open new tab: tambah di posisi setelah tab aktif
- Close tab: tutup tab aktif, pindah ke tab sebelahnya
- Switch tab: pindah ke tab tertentu
- View recent tabs: lihat N tab terakhir dibuka

**Penyelesaian:**

```cpp
#include <list>
#include <stack>
#include <string>
using namespace std;

class TabManager {
private:
    // Doubly linked list untuk tabs - efficient insert/delete di tengah
    list<string> tabs;
    list<string>::iterator activeTab;
    
    // Stack untuk recent tabs history
    stack<string> recentHistory;
    int maxHistory;
    
public:
    TabManager(int maxRecent = 10) : maxHistory(maxRecent) {
        activeTab = tabs.end();
    }
    
    // Open tab setelah tab aktif: O(1)
    void openTab(const string& url) {
        if (activeTab != tabs.end()) {
            ++activeTab;  // Move past current active
            activeTab = tabs.insert(activeTab, url);
        } else {
            tabs.push_back(url);
            activeTab = --tabs.end();
        }
        
        addToHistory(url);
    }
    
    // Close active tab: O(1)
    void closeTab() {
        if (activeTab == tabs.end()) return;
        
        auto toDelete = activeTab;
        
        // Move to previous tab (or next if no previous)
        if (activeTab != tabs.begin()) {
            --activeTab;
        } else {
            ++activeTab;
        }
        
        tabs.erase(toDelete);
        
        if (tabs.empty()) {
            activeTab = tabs.end();
        }
    }
    
    // Switch to specific tab: O(n) worst case
    void switchToTab(const string& url) {
        for (auto it = tabs.begin(); it != tabs.end(); ++it) {
            if (*it == url) {
                activeTab = it;
                addToHistory(url);
                return;
            }
        }
    }
    
    // Get current tab: O(1)
    string getCurrentTab() {
        if (activeTab == tabs.end()) return "";
        return *activeTab;
    }
    
    // Get recent N tabs: O(n)
    vector<string> getRecentTabs(int n) {
        vector<string> result;
        stack<string> temp = recentHistory;
        
        while (!temp.empty() && result.size() < n) {
            result.push_back(temp.top());
            temp.pop();
        }
        
        return result;
    }
    
private:
    void addToHistory(const string& url) {
        recentHistory.push(url);
        // Note: Proper implementation would limit stack size
    }
};
```

**Struktur data yang digunakan:**
1. **Doubly Linked List (std::list)** untuk tabs
   - Insert/delete di posisi manapun: O(1)
   - Navigation antar tab: O(1)
   
2. **Stack** untuk recent history
   - Push pada setiap open/switch: O(1)
   - LIFO cocok untuk "recent" concept

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Soal:** Implementasikan MinStack yang mendukung operasi push, pop, top, dan getMin semuanya dalam O(1)!

**Penyelesaian:**

**Pendekatan: Gunakan dua stack - satu untuk data, satu untuk tracking minimum**

```cpp
#include <stack>
using namespace std;

class MinStack {
private:
    stack<int> dataStack;
    stack<int> minStack;  // Stores minimum at each level
    
public:
    MinStack() {}
    
    // Push: O(1)
    void push(int val) {
        dataStack.push(val);
        
        // Update min stack
        if (minStack.empty() || val <= minStack.top()) {
            minStack.push(val);
        } else {
            minStack.push(minStack.top());  // Carry forward current min
        }
    }
    
    // Pop: O(1)
    void pop() {
        if (!dataStack.empty()) {
            dataStack.pop();
            minStack.pop();
        }
    }
    
    // Top: O(1)
    int top() {
        return dataStack.top();
    }
    
    // GetMin: O(1)
    int getMin() {
        return minStack.top();
    }
};

// Optimized version - minStack only stores when min changes
class MinStackOptimized {
private:
    stack<int> dataStack;
    stack<pair<int, int>> minStack;  // (minValue, count)
    
public:
    void push(int val) {
        dataStack.push(val);
        
        if (minStack.empty() || val < minStack.top().first) {
            minStack.push({val, 1});
        } else if (val == minStack.top().first) {
            minStack.top().second++;
        }
    }
    
    void pop() {
        if (dataStack.top() == minStack.top().first) {
            minStack.top().second--;
            if (minStack.top().second == 0) {
                minStack.pop();
            }
        }
        dataStack.pop();
    }
    
    int top() { return dataStack.top(); }
    int getMin() { return minStack.top().first; }
};
```

**Trace contoh:**

| Operation | Data Stack | Min Stack | getMin |
|-----------|------------|-----------|--------|
| push(5) | [5] | [5] | 5 |
| push(3) | [5,3] | [5,3] | 3 |
| push(7) | [5,3,7] | [5,3,3] | 3 |
| push(3) | [5,3,7,3] | [5,3,3,3] | 3 |
| pop() | [5,3,7] | [5,3,3] | 3 |
| pop() | [5,3] | [5,3] | 3 |
| pop() | [5] | [5] | 5 |

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Desain struktur data untuk Leaderboard game online yang mendukung:
- addScore(playerId, score): tambah score ke player
- top(K): return top K players dengan score tertinggi
- reset(playerId): reset score player ke 0

Semua operasi harus efisien untuk skala besar (jutaan pemain).

**Penyelesaian:**

```cpp
#include <unordered_map>
#include <set>
#include <vector>
using namespace std;

class Leaderboard {
private:
    // Player ID → Score
    unordered_map<int, int> scores;
    
    // Ordered set of (score, playerId) for ranking
    // Using set with custom comparator for descending score order
    set<pair<int, int>, greater<pair<int, int>>> ranking;
    
public:
    // Add score: O(log n)
    void addScore(int playerId, int score) {
        // Remove old entry if exists
        if (scores.find(playerId) != scores.end()) {
            int oldScore = scores[playerId];
            ranking.erase({oldScore, playerId});
        }
        
        // Update score
        scores[playerId] = scores[playerId] + score;
        int newScore = scores[playerId];
        
        // Insert new entry to ranking
        ranking.insert({newScore, playerId});
    }
    
    // Get top K: O(K)
    vector<int> top(int K) {
        vector<int> result;
        int count = 0;
        
        for (auto& [score, playerId] : ranking) {
            if (count >= K) break;
            result.push_back(score);
            count++;
        }
        
        return result;
    }
    
    // Reset player: O(log n)
    void reset(int playerId) {
        if (scores.find(playerId) != scores.end()) {
            int oldScore = scores[playerId];
            ranking.erase({oldScore, playerId});
            scores.erase(playerId);
        }
    }
    
    // Bonus: Get player rank: O(n) atau O(log n) dengan augmented BST
    int getRank(int playerId) {
        if (scores.find(playerId) == scores.end()) return -1;
        
        int playerScore = scores[playerId];
        int rank = 1;
        
        for (auto& [score, id] : ranking) {
            if (id == playerId) return rank;
            rank++;
        }
        
        return -1;
    }
};
```

**Analisis Kompleksitas:**

| Operasi | Kompleksitas | Struktur yang Digunakan |
|---------|-------------|-------------------------|
| addScore | O(log n) | Hash map lookup + Set insert/delete |
| top(K) | O(K) | Set iteration |
| reset | O(log n) | Hash map delete + Set delete |

**Optimasi untuk scale:**
1. Untuk top(K) yang sangat frequent, cache hasil
2. Untuk jutaan pemain, partition berdasarkan score range
3. Gunakan Redis Sorted Set untuk distributed system

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan. Jawaban singkat tersedia di bagian akhir.

### Problem S1 ⭐
Struktur data apa yang paling cocok untuk implementasi autocomplete yang mendukung prefix matching?

### Problem S2 ⭐⭐
Jelaskan perbedaan antara in-place sorting dan out-of-place sorting. Berikan contoh masing-masing!

### Problem S3 ⭐⭐
Desain struktur data untuk menyimpan sparse matrix (matrix dengan banyak elemen 0) secara efisien!

### Problem S4 ⭐⭐⭐
Bagaimana mengimplementasikan LFU (Least Frequently Used) Cache? Struktur data apa yang diperlukan?

### Problem S5 ⭐⭐⭐
Desain sistem yang mendukung operasi: insert, delete, getRandom (return random element) semua dalam O(1)!

---

## Ringkasan

| Topik | Poin Kunci |
|-------|------------|
| **Struktur Data Linear** | Array (akses O(1)), Linked List (insert O(1)), Stack (LIFO), Queue (FIFO), Deque (double-ended) |
| **Struktur Data Non-Linear** | Tree (hierarki), BST (ordered search O(log n)), Heap (priority O(log n)), Hash Table (lookup O(1)) |
| **Sorting** | Simple: O(n²), Advanced: O(n log n), Lower bound comparison: Ω(n log n) |
| **Trade-off Array vs Linked List** | Array: akses random; Linked List: insert/delete dinamis |
| **Trade-off BST vs Hash Table** | BST: ordered + range query; Hash Table: O(1) lookup |
| **LRU Cache** | Hash Table + Doubly Linked List = O(1) semua operasi |
| **Undo/Redo** | Dua Stack: undo stack + redo stack |
| **Multi-Index** | Satu storage + multiple index untuk berbagai query pattern |
| **Kriteria Pemilihan** | Jenis operasi, frekuensi, ukuran data, memory constraint, ordering requirement |

---

## Jawaban Supplementary Problems

**S1:** **Trie (Prefix Tree)** - memungkinkan pencarian prefix dalam O(m) dimana m adalah panjang prefix, dan mengembalikan semua kata dengan prefix tersebut secara efisien.

**S2:**
- **In-place sorting:** Tidak memerlukan memory tambahan O(1). Contoh: Quick Sort, Heap Sort, Insertion Sort
- **Out-of-place sorting:** Memerlukan memory tambahan O(n). Contoh: Merge Sort

**S3:** **Compressed Sparse Row (CSR)** atau **Hash Map dengan key (row, col)**

```cpp
// Pendekatan Hash Map
unordered_map<pair<int,int>, double> sparseMatrix;

// Hanya simpan elemen non-zero
void set(int row, int col, double val) {
    if (val != 0) sparseMatrix[{row, col}] = val;
    else sparseMatrix.erase({row, col});
}

double get(int row, int col) {
    if (sparseMatrix.count({row, col})) 
        return sparseMatrix[{row, col}];
    return 0;
}
```

**S4:** **LFU Cache** memerlukan:
1. Hash Map: key → (value, frequency)
2. Hash Map: frequency → Doubly Linked List of keys dengan frequency tersebut
3. Variable: minFrequency

**S5:** **Array + Hash Map**
```cpp
class RandomizedSet {
    vector<int> arr;
    unordered_map<int, int> valToIndex;
    
    // Insert: push_back, update map - O(1)
    // Delete: swap with last, pop_back, update map - O(1)
    // GetRandom: return arr[rand() % size] - O(1)
};
```

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. (Seluruh bab terkait)
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. (Seluruh bab terkait)
3. Skiena, S.S. (2020). *The Algorithm Design Manual* (3rd Ed.). Springer.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
