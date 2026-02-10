# Modul 04: Linked List (Bagian 2) - Double dan Circular Linked List

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 04  
**Topik:** Double Linked List dan Circular Linked List

> **Capaian Pembelajaran:** Sub-CPMK-2.1 — Mampu mengimplementasikan single, double, dan circular linked list

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.10.2; Weiss Ch.3; Goodrich Ch.3

---

## Tujuan Pembelajaran

Setelah mempelajari modul ini, mahasiswa diharapkan mampu:

1. **Mengimplementasikan** struktur node dan operasi-operasi pada double linked list
2. **Menjelaskan** keuntungan double linked list dibandingkan single linked list
3. **Mengimplementasikan** single circular linked list beserta operasi-operasinya
4. **Mengimplementasikan** double circular linked list beserta operasi-operasinya
5. **Memahami** konsep dan penerapan sentinel node dalam linked list
6. **Menerapkan** iterator untuk traversal pada linked list
7. **Memilih** jenis linked list yang tepat untuk kasus penggunaan tertentu

---

## 1. Double Linked List

### 1.1 Konsep Dasar Double Linked List

> **Definisi:** Double Linked List (DLL) adalah struktur data linear di mana setiap node memiliki dua pointer: satu menunjuk ke node sebelumnya (prev) dan satu menunjuk ke node berikutnya (next). Struktur ini memungkinkan traversal dua arah (bidirectional).

Berbeda dengan Single Linked List yang hanya dapat melakukan traversal dari depan ke belakang, Double Linked List memungkinkan kita untuk bergerak ke kedua arah. Hal ini sangat berguna dalam berbagai aplikasi seperti:

- **Navigasi browser** (tombol back dan forward)
- **Playlist musik** (lagu sebelumnya dan berikutnya)
- **Undo/Redo** dalam aplikasi pengolah dokumen
- **Manajemen memori** pada sistem operasi

![Struktur Double Linked List](images/p04-01-double-linked-list-structure.png)

*Gambar 1.1: Struktur Double Linked List dengan pointer prev dan next*


### 1.2 Struktur Node Double Linked List

```cpp
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    // Constructor
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};
```

Setiap node pada DLL memiliki tiga komponen:
- **data**: Menyimpan nilai/informasi
- **prev**: Pointer ke node sebelumnya
- **next**: Pointer ke node berikutnya

### 1.3 Class Double Linked List

```cpp
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    int size;
    
public:
    DoublyLinkedList() : head(nullptr), tail(nullptr), size(0) {}
    ~DoublyLinkedList();
    
    // Operasi dasar
    void insertFront(int value);
    void insertBack(int value);
    void insertAt(int value, int position);
    void deleteFront();
    void deleteBack();
    void deleteAt(int position);
    void deleteValue(int value);
    
    // Traversal
    void displayForward();
    void displayBackward();
    
    // Utility
    int getSize() const { return size; }
    bool isEmpty() const { return size == 0; }
    Node* search(int value);
};
```

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Implementasikan fungsi `insertFront()` untuk menyisipkan node di awal double linked list.

**Penyelesaian:**

```cpp
void DoublyLinkedList::insertFront(int value) {
    // Langkah 1: Buat node baru
    Node* newNode = new Node(value);
    
    // Langkah 2: Jika list kosong
    if (head == nullptr) {
        head = tail = newNode;
    }
    // Langkah 3: Jika list tidak kosong
    else {
        newNode->next = head;    // Node baru menunjuk ke head lama
        head->prev = newNode;     // Head lama menunjuk balik ke node baru
        head = newNode;           // Update head ke node baru
    }
    
    size++;
}
```

**Analisis Kompleksitas:** O(1) - operasi konstan karena hanya melibatkan manipulasi pointer di awal list.

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Implementasikan fungsi `insertBack()` untuk menyisipkan node di akhir double linked list.

**Penyelesaian:**

```cpp
void DoublyLinkedList::insertBack(int value) {
    // Langkah 1: Buat node baru
    Node* newNode = new Node(value);
    
    // Langkah 2: Jika list kosong
    if (tail == nullptr) {
        head = tail = newNode;
    }
    // Langkah 3: Jika list tidak kosong
    else {
        newNode->prev = tail;    // Node baru menunjuk ke tail lama
        tail->next = newNode;     // Tail lama menunjuk ke node baru
        tail = newNode;           // Update tail ke node baru
    }
    
    size++;
}
```

**Analisis Kompleksitas:** O(1) - berbeda dengan Single Linked List tanpa tail pointer yang membutuhkan O(n), DLL dengan tail pointer dapat melakukan operasi ini dalam waktu konstan.

---

### 1.4 Operasi Insert pada Posisi Tertentu

![Insert pada Double Linked List](images/p04-02-dll-insert-middle.png)

*Gambar 1.2: Proses insert node di tengah Double Linked List*


### SOLVED PROBLEM 3 ⭐⭐

**Soal:** Implementasikan fungsi `insertAt()` untuk menyisipkan node pada posisi tertentu di double linked list.

**Penyelesaian:**

```cpp
void DoublyLinkedList::insertAt(int value, int position) {
    // Validasi posisi
    if (position < 0 || position > size) {
        cout << "Posisi tidak valid!" << endl;
        return;
    }
    
    // Kasus khusus: insert di awal
    if (position == 0) {
        insertFront(value);
        return;
    }
    
    // Kasus khusus: insert di akhir
    if (position == size) {
        insertBack(value);
        return;
    }
    
    // Langkah 1: Buat node baru
    Node* newNode = new Node(value);
    
    // Langkah 2: Tentukan arah traversal yang optimal
    Node* current;
    if (position <= size / 2) {
        // Traversal dari depan
        current = head;
        for (int i = 0; i < position; i++) {
            current = current->next;
        }
    } else {
        // Traversal dari belakang (keuntungan DLL!)
        current = tail;
        for (int i = size - 1; i > position; i--) {
            current = current->prev;
        }
    }
    
    // Langkah 3: Sisipkan node baru sebelum current
    newNode->next = current;
    newNode->prev = current->prev;
    current->prev->next = newNode;
    current->prev = newNode;
    
    size++;
}
```

**Analisis Kompleksitas:** O(n/2) ≈ O(n) dalam worst case, tetapi rata-rata lebih efisien karena dapat traversal dari kedua arah.

---

### 1.5 Operasi Delete pada Double Linked List

### SOLVED PROBLEM 4 ⭐

**Soal:** Implementasikan fungsi `deleteFront()` untuk menghapus node di awal double linked list.

**Penyelesaian:**

```cpp
void DoublyLinkedList::deleteFront() {
    // Kasus list kosong
    if (head == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    // Simpan node yang akan dihapus
    Node* temp = head;
    
    // Kasus hanya ada satu node
    if (head == tail) {
        head = tail = nullptr;
    }
    // Kasus lebih dari satu node
    else {
        head = head->next;
        head->prev = nullptr;
    }
    
    delete temp;
    size--;
}
```

---

### SOLVED PROBLEM 5 ⭐

**Soal:** Implementasikan fungsi `deleteBack()` untuk menghapus node di akhir double linked list.

**Penyelesaian:**

```cpp
void DoublyLinkedList::deleteBack() {
    // Kasus list kosong
    if (tail == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    // Simpan node yang akan dihapus
    Node* temp = tail;
    
    // Kasus hanya ada satu node
    if (head == tail) {
        head = tail = nullptr;
    }
    // Kasus lebih dari satu node
    else {
        tail = tail->prev;
        tail->next = nullptr;
    }
    
    delete temp;
    size--;
}
```

**Keuntungan DLL:** Operasi `deleteBack()` pada DLL memiliki kompleksitas O(1), sedangkan pada SLL tanpa tail pointer atau dengan tail pointer tapi tanpa prev, operasi ini membutuhkan O(n) untuk mencari node sebelum tail.

---

### 1.6 Perbandingan Single vs Double Linked List

| Aspek | Single Linked List | Double Linked List |
|-------|-------------------|-------------------|
| **Memori per node** | 2 field (data + next) | 3 field (data + prev + next) |
| **Traversal** | Satu arah (forward) | Dua arah (bidirectional) |
| **Insert di depan** | O(1) | O(1) |
| **Insert di belakang** | O(n) atau O(1)* | O(1) |
| **Delete di depan** | O(1) | O(1) |
| **Delete di belakang** | O(n) | O(1) |
| **Delete node tertentu** | O(n)** | O(1)*** |
| **Kompleksitas implementasi** | Sederhana | Lebih kompleks |

*dengan tail pointer  
**perlu mencari node sebelumnya  
***jika sudah memiliki pointer ke node tersebut

---

### SOLVED PROBLEM 6 ⭐⭐

**Soal:** Implementasikan fungsi `deleteAt()` untuk menghapus node pada posisi tertentu.

**Penyelesaian:**

```cpp
void DoublyLinkedList::deleteAt(int position) {
    // Validasi posisi
    if (position < 0 || position >= size) {
        cout << "Posisi tidak valid!" << endl;
        return;
    }
    
    // Kasus khusus
    if (position == 0) {
        deleteFront();
        return;
    }
    if (position == size - 1) {
        deleteBack();
        return;
    }
    
    // Tentukan arah traversal yang optimal
    Node* current;
    if (position <= size / 2) {
        current = head;
        for (int i = 0; i < position; i++) {
            current = current->next;
        }
    } else {
        current = tail;
        for (int i = size - 1; i > position; i--) {
            current = current->prev;
        }
    }
    
    // Hapus node
    current->prev->next = current->next;
    current->next->prev = current->prev;
    
    delete current;
    size--;
}
```

---

### SOLVED PROBLEM 7 ⭐⭐

**Soal:** Implementasikan fungsi untuk menampilkan isi double linked list dari depan ke belakang dan sebaliknya.

**Penyelesaian:**

```cpp
void DoublyLinkedList::displayForward() {
    if (head == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    cout << "Forward: NULL <- ";
    Node* current = head;
    while (current != nullptr) {
        cout << current->data;
        if (current->next != nullptr) {
            cout << " <-> ";
        }
        current = current->next;
    }
    cout << " -> NULL" << endl;
}

void DoublyLinkedList::displayBackward() {
    if (tail == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    cout << "Backward: NULL <- ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data;
        if (current->prev != nullptr) {
            cout << " <-> ";
        }
        current = current->prev;
    }
    cout << " -> NULL" << endl;
}
```

---

## 2. Circular Linked List

### 2.1 Konsep Circular Linked List

> **Definisi:** Circular Linked List adalah linked list di mana node terakhir tidak menunjuk ke NULL, melainkan menunjuk kembali ke node pertama, membentuk sebuah lingkaran (cycle).

Circular Linked List memiliki dua variasi:
1. **Single Circular Linked List** - Setiap node memiliki satu pointer next
2. **Double Circular Linked List** - Setiap node memiliki pointer prev dan next

![Circular Linked List](images/p04-03-circular-linked-list.png)

*Gambar 2.1: Single Circular Linked List dan Double Circular Linked List*


### 2.2 Aplikasi Circular Linked List

Circular Linked List sangat berguna untuk:

1. **Round-Robin Scheduling** - Sistem operasi menggunakan circular list untuk menjadwalkan proses secara bergantian
2. **Multiplayer Gaming** - Giliran pemain yang berputar
3. **Playlist Loop** - Musik yang berulang terus-menerus
4. **Buffer Circular** - Implementasi buffer untuk streaming data
5. **Token Ring Network** - Protokol jaringan di mana token beredar

**Konteks Pertahanan:**
- **Rotasi Penjagaan** - Jadwal personel yang bertugas secara bergilir 24/7
- **Sistem Radar Sweep** - Pemindaian radar yang berputar 360°
- **Convoy Circular Formation** - Formasi konvoi yang dapat berputar untuk proteksi

---

### 2.3 Struktur Single Circular Linked List

```cpp
struct Node {
    int data;
    Node* next;
    
    Node(int value) : data(value), next(nullptr) {}
};

class CircularLinkedList {
private:
    Node* tail;  // Menggunakan tail untuk efisiensi
    int size;
    
public:
    CircularLinkedList() : tail(nullptr), size(0) {}
    ~CircularLinkedList();
    
    void insertFront(int value);
    void insertBack(int value);
    void deleteFront();
    void deleteBack();
    void display();
    
    // Mendapatkan head dari tail
    Node* getHead() const {
        return (tail == nullptr) ? nullptr : tail->next;
    }
    
    int getSize() const { return size; }
    bool isEmpty() const { return size == 0; }
};
```

> **Catatan:** Pada Single Circular Linked List, kita lebih sering menyimpan pointer ke **tail** daripada **head**. Alasannya adalah dengan tail, kita dapat mengakses head dengan mudah (`tail->next`), sehingga operasi insert di depan dan belakang keduanya menjadi O(1).

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Implementasikan operasi `insertFront()` dan `insertBack()` pada Single Circular Linked List.

**Penyelesaian:**

```cpp
void CircularLinkedList::insertFront(int value) {
    Node* newNode = new Node(value);
    
    if (tail == nullptr) {
        // List kosong: node baru menjadi satu-satunya node
        tail = newNode;
        newNode->next = newNode;  // Menunjuk ke dirinya sendiri
    } else {
        // Insert di depan (antara tail dan head)
        newNode->next = tail->next;  // Node baru menunjuk ke head lama
        tail->next = newNode;         // Tail menunjuk ke node baru (head baru)
    }
    
    size++;
}

void CircularLinkedList::insertBack(int value) {
    // Insert di belakang adalah insert di depan lalu pindahkan tail
    insertFront(value);
    tail = tail->next;  // Geser tail ke node yang baru ditambahkan
}
```

**Analisis:** Dengan menyimpan tail, kedua operasi insert menjadi O(1).

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Implementasikan operasi `deleteFront()` pada Single Circular Linked List.

**Penyelesaian:**

```cpp
void CircularLinkedList::deleteFront() {
    if (tail == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    Node* head = tail->next;
    
    if (head == tail) {
        // Hanya ada satu node
        delete tail;
        tail = nullptr;
    } else {
        // Lebih dari satu node
        tail->next = head->next;  // Tail menunjuk ke node kedua
        delete head;
    }
    
    size--;
}
```

---

### SOLVED PROBLEM 10 ⭐⭐

**Soal:** Implementasikan fungsi `display()` untuk menampilkan seluruh elemen pada Single Circular Linked List.

**Penyelesaian:**

```cpp
void CircularLinkedList::display() {
    if (tail == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    Node* current = tail->next;  // Mulai dari head
    
    cout << "Circular List: ";
    do {
        cout << current->data;
        current = current->next;
        if (current != tail->next) {
            cout << " -> ";
        }
    } while (current != tail->next);  // Berhenti ketika kembali ke head
    
    cout << " -> (kembali ke " << tail->next->data << ")" << endl;
}
```

**Penting:** Pada circular list, kita tidak bisa menggunakan kondisi `current != nullptr` untuk berhenti karena tidak ada NULL. Kita harus menyimpan referensi ke node awal dan berhenti ketika kembali ke node tersebut.

---

### 2.4 Double Circular Linked List

Double Circular Linked List menggabungkan keuntungan dari Double Linked List dan Circular Linked List:
- Traversal dua arah
- Tidak ada NULL pointer (selalu terhubung)
- Operasi insert/delete di kedua ujung dalam O(1)

```cpp
struct Node {
    int data;
    Node* prev;
    Node* next;
    
    Node(int value) : data(value), prev(nullptr), next(nullptr) {}
};

class DoublyCircularLinkedList {
private:
    Node* head;
    int size;
    
public:
    DoublyCircularLinkedList() : head(nullptr), size(0) {}
    ~DoublyCircularLinkedList();
    
    void insertFront(int value);
    void insertBack(int value);
    void insertAfter(Node* node, int value);
    void deleteFront();
    void deleteBack();
    void deleteNode(Node* node);
    void displayForward();
    void displayBackward();
    
    Node* getHead() const { return head; }
    Node* getTail() const { 
        return (head == nullptr) ? nullptr : head->prev; 
    }
    int getSize() const { return size; }
    bool isEmpty() const { return size == 0; }
};
```

![Double Circular Linked List Operations](images/p04-04-dcll-operations.png)

*Gambar 2.2: Operasi pada Double Circular Linked List*


---

### SOLVED PROBLEM 11 ⭐⭐

**Soal:** Implementasikan operasi `insertFront()` dan `insertBack()` pada Double Circular Linked List.

**Penyelesaian:**

```cpp
void DoublyCircularLinkedList::insertFront(int value) {
    Node* newNode = new Node(value);
    
    if (head == nullptr) {
        // List kosong
        head = newNode;
        newNode->next = newNode;
        newNode->prev = newNode;
    } else {
        Node* tail = head->prev;
        
        // Hubungkan node baru
        newNode->next = head;
        newNode->prev = tail;
        head->prev = newNode;
        tail->next = newNode;
        
        // Update head
        head = newNode;
    }
    
    size++;
}

void DoublyCircularLinkedList::insertBack(int value) {
    if (head == nullptr) {
        insertFront(value);
        return;
    }
    
    Node* newNode = new Node(value);
    Node* tail = head->prev;
    
    // Hubungkan node baru di belakang (antara tail lama dan head)
    newNode->next = head;
    newNode->prev = tail;
    tail->next = newNode;
    head->prev = newNode;
    
    // Tidak perlu update head karena insert di belakang
    
    size++;
}
```

---

### SOLVED PROBLEM 12 ⭐⭐⭐

**Soal:** Implementasikan operasi `deleteNode()` untuk menghapus node tertentu yang sudah diketahui pointernya pada Double Circular Linked List.

**Penyelesaian:**

```cpp
void DoublyCircularLinkedList::deleteNode(Node* node) {
    if (node == nullptr || head == nullptr) {
        cout << "Node tidak valid atau list kosong!" << endl;
        return;
    }
    
    // Kasus hanya ada satu node
    if (node->next == node) {
        head = nullptr;
        delete node;
        size--;
        return;
    }
    
    // Hubungkan node sebelum dan sesudah
    node->prev->next = node->next;
    node->next->prev = node->prev;
    
    // Jika node yang dihapus adalah head, update head
    if (node == head) {
        head = node->next;
    }
    
    delete node;
    size--;
}
```

**Keunggulan:** Dengan Double Circular Linked List, jika kita sudah memiliki pointer ke node yang ingin dihapus, operasi delete dapat dilakukan dalam O(1) tanpa perlu traversal.

---

## 3. Sentinel Node

### 3.1 Konsep Sentinel Node

> **Definisi:** Sentinel Node (atau Dummy Node) adalah node khusus yang tidak menyimpan data aktual, tetapi digunakan untuk menyederhanakan penanganan kasus-kasus khusus (edge cases) dalam operasi linked list.

Manfaat menggunakan Sentinel Node:
1. Menghilangkan pengecekan khusus untuk list kosong
2. Menyederhanakan kode insert dan delete
3. Mengurangi kemungkinan bug pada edge cases

![Sentinel Node](images/p04-05-sentinel-node.png)

*Gambar 3.1: Double Linked List dengan Sentinel Node*


### 3.2 Implementasi dengan Sentinel Node

```cpp
class DoublyLinkedListWithSentinel {
private:
    Node* sentinelHead;  // Dummy node di awal
    Node* sentinelTail;  // Dummy node di akhir
    int size;
    
public:
    DoublyLinkedListWithSentinel() : size(0) {
        // Inisialisasi sentinel nodes
        sentinelHead = new Node(0);  // Data tidak digunakan
        sentinelTail = new Node(0);
        
        // Hubungkan kedua sentinel
        sentinelHead->next = sentinelTail;
        sentinelTail->prev = sentinelHead;
    }
    
    ~DoublyLinkedListWithSentinel() {
        // Hapus semua node termasuk sentinel
        Node* current = sentinelHead;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
    }
    
    // Insert setelah node tertentu (internal helper)
    void insertAfter(Node* node, int value) {
        Node* newNode = new Node(value);
        
        newNode->next = node->next;
        newNode->prev = node;
        node->next->prev = newNode;
        node->next = newNode;
        
        size++;
    }
    
    // Public methods
    void insertFront(int value) {
        insertAfter(sentinelHead, value);
    }
    
    void insertBack(int value) {
        insertAfter(sentinelTail->prev, value);
    }
};
```

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Implementasikan operasi delete dengan sentinel node yang tidak memerlukan pengecekan kasus khusus.

**Penyelesaian:**

```cpp
// Delete node tertentu (bukan sentinel)
void DoublyLinkedListWithSentinel::deleteNode(Node* node) {
    // Pastikan bukan sentinel yang dihapus
    if (node == sentinelHead || node == sentinelTail) {
        cout << "Tidak dapat menghapus sentinel node!" << endl;
        return;
    }
    
    // Dengan sentinel, kita tidak perlu cek apakah prev atau next adalah nullptr
    node->prev->next = node->next;
    node->next->prev = node->prev;
    
    delete node;
    size--;
}

void DoublyLinkedListWithSentinel::deleteFront() {
    if (size == 0) {
        cout << "List kosong!" << endl;
        return;
    }
    deleteNode(sentinelHead->next);
}

void DoublyLinkedListWithSentinel::deleteBack() {
    if (size == 0) {
        cout << "List kosong!" << endl;
        return;
    }
    deleteNode(sentinelTail->prev);
}
```

**Keuntungan:** Perhatikan bahwa fungsi `deleteNode()` tidak perlu menangani kasus node pertama atau terakhir secara khusus karena sentinel node menjamin `node->prev` dan `node->next` selalu valid.

---

## 4. Iterator pada Linked List

### 4.1 Konsep Iterator

> **Definisi:** Iterator adalah objek yang memungkinkan traversal melalui elemen-elemen container (seperti linked list) tanpa mengekspos struktur internal container tersebut.

Iterator menyediakan interface standar untuk:
- Mengakses elemen saat ini
- Berpindah ke elemen berikutnya/sebelumnya
- Mengecek apakah masih ada elemen tersisa

### 4.2 Implementasi Iterator untuk Double Linked List

```cpp
class DoublyLinkedList {
private:
    Node* head;
    Node* tail;
    int size;
    
public:
    // ... (operasi lainnya)
    
    // Inner class Iterator
    class Iterator {
    private:
        Node* current;
        
    public:
        Iterator(Node* node) : current(node) {}
        
        // Dereference operator
        int& operator*() {
            return current->data;
        }
        
        // Pre-increment (++it)
        Iterator& operator++() {
            current = current->next;
            return *this;
        }
        
        // Pre-decrement (--it)
        Iterator& operator--() {
            current = current->prev;
            return *this;
        }
        
        // Comparison operators
        bool operator==(const Iterator& other) const {
            return current == other.current;
        }
        
        bool operator!=(const Iterator& other) const {
            return current != other.current;
        }
        
        // Akses ke node internal (jika diperlukan)
        Node* getNode() const {
            return current;
        }
    };
    
    // Methods untuk mendapatkan iterator
    Iterator begin() { return Iterator(head); }
    Iterator end() { return Iterator(nullptr); }
    
    // Reverse iterator
    Iterator rbegin() { return Iterator(tail); }
    Iterator rend() { return Iterator(nullptr); }
};
```

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Demonstrasikan penggunaan iterator untuk traversal forward dan backward pada double linked list.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

int main() {
    DoublyLinkedList dll;
    
    // Insert beberapa nilai
    dll.insertBack(10);
    dll.insertBack(20);
    dll.insertBack(30);
    dll.insertBack(40);
    
    // Forward traversal menggunakan iterator
    cout << "Forward traversal: ";
    for (DoublyLinkedList::Iterator it = dll.begin(); it != dll.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;
    
    // Backward traversal menggunakan iterator
    cout << "Backward traversal: ";
    for (DoublyLinkedList::Iterator it = dll.rbegin(); it != dll.rend(); --it) {
        cout << *it << " ";
    }
    cout << endl;
    
    // Modifikasi nilai menggunakan iterator
    for (DoublyLinkedList::Iterator it = dll.begin(); it != dll.end(); ++it) {
        *it *= 2;  // Gandakan setiap nilai
    }
    
    cout << "Setelah digandakan: ";
    for (DoublyLinkedList::Iterator it = dll.begin(); it != dll.end(); ++it) {
        cout << *it << " ";
    }
    cout << endl;
    
    return 0;
}
```

**Output:**
```
Forward traversal: 10 20 30 40 
Backward traversal: 40 30 20 10 
Setelah digandakan: 20 40 60 80 
```

---

## 5. Studi Kasus: Playlist Musik dengan Circular Doubly Linked List

### 5.1 Deskripsi Masalah

Implementasikan sistem playlist musik yang mendukung:
- Menambah lagu ke playlist
- Menghapus lagu dari playlist
- Memutar lagu berikutnya/sebelumnya
- Mode loop (berputar terus)
- Mode shuffle (acak)

### SOLVED PROBLEM 15 ⭐⭐⭐

**Soal:** Implementasikan class `MusicPlaylist` menggunakan circular doubly linked list.

**Penyelesaian:**

```cpp
#include <iostream>
#include <string>
#include <cstdlib>
#include <ctime>
using namespace std;

struct Song {
    string title;
    string artist;
    int duration;  // dalam detik
    Song* prev;
    Song* next;
    
    Song(string t, string a, int d) 
        : title(t), artist(a), duration(d), prev(nullptr), next(nullptr) {}
};

class MusicPlaylist {
private:
    Song* current;  // Lagu yang sedang diputar
    int size;
    bool loopMode;
    
public:
    MusicPlaylist() : current(nullptr), size(0), loopMode(true) {
        srand(time(nullptr));  // Seed untuk shuffle
    }
    
    ~MusicPlaylist() {
        if (current == nullptr) return;
        
        Song* start = current;
        Song* temp;
        do {
            temp = current->next;
            delete current;
            current = temp;
        } while (current != start);
    }
    
    // Menambah lagu ke akhir playlist
    void addSong(string title, string artist, int duration) {
        Song* newSong = new Song(title, artist, duration);
        
        if (current == nullptr) {
            current = newSong;
            newSong->next = newSong;
            newSong->prev = newSong;
        } else {
            Song* tail = current->prev;
            
            newSong->next = current;
            newSong->prev = tail;
            tail->next = newSong;
            current->prev = newSong;
        }
        
        size++;
        cout << "Added: " << title << " by " << artist << endl;
    }
    
    // Menghapus lagu yang sedang diputar
    void removeCurrent() {
        if (current == nullptr) {
            cout << "Playlist kosong!" << endl;
            return;
        }
        
        cout << "Removing: " << current->title << endl;
        
        if (size == 1) {
            delete current;
            current = nullptr;
        } else {
            Song* toDelete = current;
            current->prev->next = current->next;
            current->next->prev = current->prev;
            current = current->next;
            delete toDelete;
        }
        
        size--;
    }
    
    // Lagu berikutnya
    void next() {
        if (current == nullptr) {
            cout << "Playlist kosong!" << endl;
            return;
        }
        current = current->next;
        displayCurrent();
    }
    
    // Lagu sebelumnya
    void previous() {
        if (current == nullptr) {
            cout << "Playlist kosong!" << endl;
            return;
        }
        current = current->prev;
        displayCurrent();
    }
    
    // Shuffle (pindah ke lagu acak)
    void shuffle() {
        if (size <= 1) {
            cout << "Tidak cukup lagu untuk shuffle!" << endl;
            return;
        }
        
        int steps = rand() % size;
        for (int i = 0; i < steps; i++) {
            current = current->next;
        }
        
        cout << "Shuffled to: ";
        displayCurrent();
    }
    
    // Menampilkan lagu saat ini
    void displayCurrent() {
        if (current == nullptr) {
            cout << "Tidak ada lagu yang diputar." << endl;
            return;
        }
        
        cout << "Now Playing: " << current->title 
             << " - " << current->artist 
             << " (" << current->duration << " sec)" << endl;
    }
    
    // Menampilkan seluruh playlist
    void displayPlaylist() {
        if (current == nullptr) {
            cout << "Playlist kosong!" << endl;
            return;
        }
        
        cout << "\n=== PLAYLIST (" << size << " songs) ===" << endl;
        Song* temp = current;
        int index = 1;
        
        do {
            cout << index++ << ". " << temp->title 
                 << " - " << temp->artist;
            if (temp == current) {
                cout << " [PLAYING]";
            }
            cout << endl;
            temp = temp->next;
        } while (temp != current);
        
        cout << "========================\n" << endl;
    }
    
    void toggleLoop() {
        loopMode = !loopMode;
        cout << "Loop mode: " << (loopMode ? "ON" : "OFF") << endl;
    }
};
```

---

### SOLVED PROBLEM 16 ⭐

**Soal:** Demonstrasikan penggunaan class `MusicPlaylist`.

**Penyelesaian:**

```cpp
int main() {
    MusicPlaylist playlist;
    
    // Menambah lagu
    playlist.addSong("Indonesia Raya", "W.R. Supratman", 180);
    playlist.addSong("Tanah Airku", "Ibu Sud", 210);
    playlist.addSong("Garuda Pancasila", "Sudharnoto", 195);
    playlist.addSong("Bagimu Negeri", "Kusbini", 240);
    
    // Tampilkan playlist
    playlist.displayPlaylist();
    
    // Navigasi
    cout << "--- Navigasi ---" << endl;
    playlist.displayCurrent();
    
    playlist.next();
    playlist.next();
    playlist.previous();
    
    // Shuffle
    cout << "\n--- Shuffle ---" << endl;
    playlist.shuffle();
    
    // Hapus lagu current
    cout << "\n--- Remove Current ---" << endl;
    playlist.removeCurrent();
    playlist.displayPlaylist();
    
    return 0;
}
```

---

## 6. Pemilihan Jenis Linked List

### 6.1 Kriteria Pemilihan

| Kebutuhan | Jenis Linked List yang Direkomendasikan |
|-----------|----------------------------------------|
| Traversal satu arah, hemat memori | Single Linked List |
| Traversal dua arah, delete cepat | Double Linked List |
| Data berputar/cyclic | Circular Linked List |
| Playlist, buffer, giliran | Circular Doubly Linked List |
| Implementasi sederhana | Single Linked List |
| Operasi di kedua ujung O(1) | Double Linked List dengan head & tail |

### 6.2 Trade-off

![Perbandingan Linked List](images/p04-06-linked-list-comparison.png)

*Gambar 6.1: Perbandingan berbagai jenis Linked List*


---

### SOLVED PROBLEM 17 ⭐

**Soal:** Untuk sistem rotasi penjagaan pos militer 24 jam dengan 4 shift, jenis linked list apa yang paling tepat? Jelaskan!

**Penyelesaian:**

**Jawaban:** Circular Doubly Linked List

**Alasan:**
1. **Circular** - Jadwal berputar terus-menerus tanpa henti (24/7), setelah shift terakhir langsung ke shift pertama
2. **Doubly** - Supervisor perlu melihat shift sebelumnya dan sesudahnya untuk koordinasi serah terima

```cpp
struct ShiftNode {
    string namaPersonel;
    int jamMulai;    // 0-23
    int jamSelesai;  // 0-23
    string pos;
    ShiftNode* prev;
    ShiftNode* next;
};

// Contoh penggunaan
// Shift: 00:00-06:00, 06:00-12:00, 12:00-18:00, 18:00-24:00
```

---

### SOLVED PROBLEM 18 ⭐⭐

**Soal:** Implementasikan fungsi untuk mencari node dalam circular linked list. Apa perbedaan dengan pencarian di non-circular list?

**Penyelesaian:**

```cpp
Node* CircularLinkedList::search(int value) {
    if (tail == nullptr) return nullptr;
    
    Node* current = tail->next;  // Mulai dari head
    
    // PERBEDAAN: Tidak bisa pakai (current != nullptr)
    do {
        if (current->data == value) {
            return current;
        }
        current = current->next;
    } while (current != tail->next);  // Berhenti saat kembali ke head
    
    return nullptr;  // Tidak ditemukan
}
```

**Perbedaan utama:**
1. **Non-circular:** Kondisi berhenti adalah `current != nullptr`
2. **Circular:** Kondisi berhenti adalah `current != startNode` (harus simpan referensi ke node awal)
3. **Circular:** Harus gunakan do-while agar node pertama dicek sebelum kondisi loop

---

### SOLVED PROBLEM 19 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk membalik (reverse) sebuah double linked list secara in-place.

**Penyelesaian:**

```cpp
void DoublyLinkedList::reverse() {
    if (head == nullptr || head == tail) {
        return;  // List kosong atau hanya 1 node
    }
    
    Node* current = head;
    Node* temp = nullptr;
    
    // Tukar prev dan next untuk setiap node
    while (current != nullptr) {
        // Tukar pointer
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        
        // Pindah ke node berikutnya (yang sekarang ada di prev)
        current = current->prev;
    }
    
    // Tukar head dan tail
    temp = head;
    head = tail;
    tail = temp;
}
```

**Analisis Kompleksitas:** O(n) waktu, O(1) ruang (in-place)

**Ilustrasi:**

![DLL Reversal](images/p04-07-dll-reversal.png)

*Gambar 4.8: Proses membalik Double Linked List secara in-place*


---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk mendeteksi apakah sebuah single linked list memiliki cycle (circular) menggunakan algoritma Floyd's Cycle Detection (Tortoise and Hare).

**Penyelesaian:**

```cpp
bool hasCycle(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return false;
    }
    
    Node* slow = head;        // Tortoise - bergerak 1 langkah
    Node* fast = head->next;  // Hare - bergerak 2 langkah
    
    while (fast != nullptr && fast->next != nullptr) {
        if (slow == fast) {
            return true;  // Cycle terdeteksi
        }
        
        slow = slow->next;        // 1 langkah
        fast = fast->next->next;  // 2 langkah
    }
    
    return false;  // Tidak ada cycle
}
```

**Penjelasan Algoritma:**
1. Gunakan dua pointer: slow (1 langkah) dan fast (2 langkah)
2. Jika ada cycle, fast akan "mengejar" slow dari belakang
3. Jika tidak ada cycle, fast akan mencapai NULL
4. **Kompleksitas:** O(n) waktu, O(1) ruang

![Floyd's Cycle Detection](images/p04-08-floyd-cycle-detection.png)

*Gambar 6.2: Algoritma Floyd's Cycle Detection*


---

### SOLVED PROBLEM 21 ⭐⭐

**Soal:** Implementasikan destructor untuk Double Circular Linked List yang benar agar tidak terjadi memory leak.

**Penyelesaian:**

```cpp
DoublyCircularLinkedList::~DoublyCircularLinkedList() {
    if (head == nullptr) return;
    
    // Putuskan circle terlebih dahulu untuk menghindari infinite loop
    Node* tail = head->prev;
    tail->next = nullptr;  // Putuskan koneksi circular
    
    // Hapus semua node seperti biasa
    Node* current = head;
    while (current != nullptr) {
        Node* next = current->next;
        delete current;
        current = next;
    }
    
    head = nullptr;
    size = 0;
}
```

**Alternatif dengan counter:**

```cpp
DoublyCircularLinkedList::~DoublyCircularLinkedList() {
    if (head == nullptr) return;
    
    Node* current = head;
    int count = size;  // Gunakan size untuk menghitung
    
    while (count > 0) {
        Node* next = current->next;
        delete current;
        current = next;
        count--;
    }
    
    head = nullptr;
    size = 0;
}
```

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk menggabungkan (merge) dua circular linked list menjadi satu.

**Penyelesaian:**

```cpp
void CircularLinkedList::merge(CircularLinkedList& other) {
    // Jika salah satu kosong
    if (other.tail == nullptr) return;
    if (this->tail == nullptr) {
        this->tail = other.tail;
        this->size = other.size;
        other.tail = nullptr;
        other.size = 0;
        return;
    }
    
    // Simpan pointer yang diperlukan
    Node* head1 = this->tail->next;   // Head list pertama
    Node* head2 = other.tail->next;   // Head list kedua
    
    // Hubungkan tail list pertama ke head list kedua
    this->tail->next = head2;
    
    // Hubungkan tail list kedua ke head list pertama
    other.tail->next = head1;
    
    // Update tail list pertama
    this->tail = other.tail;
    this->size += other.size;
    
    // Kosongkan list kedua
    other.tail = nullptr;
    other.size = 0;
}
```

**Ilustrasi:**
```
List 1: 1 -> 2 -> 3 -> (back to 1)
List 2: 4 -> 5 -> (back to 4)

Merged: 1 -> 2 -> 3 -> 4 -> 5 -> (back to 1)
```

---

## 7. Supplementary Problems

### Problem S1 ⭐
Implementasikan fungsi untuk menghitung jumlah node dalam circular linked list tanpa menggunakan variabel size. **Jawaban:** Gunakan do-while loop dan counter, berhenti ketika kembali ke node awal.

### Problem S2 ⭐⭐
Jelaskan mengapa pada circular linked list dengan tail pointer, operasi insert di depan dan di belakang keduanya O(1). **Jawaban:** Karena head dapat diakses via tail->next, sehingga insert di depan hanya perlu: newNode->next = tail->next; tail->next = newNode. Insert di belakang adalah insert di depan + geser tail.

### Problem S3 ⭐⭐
Apa yang terjadi jika kita memanggil reverse() pada circular doubly linked list? Apakah list tetap circular? **Jawaban:** Ya, list tetap circular. Setiap node hanya perlu swap prev dan next, dan koneksi circular tetap terjaga karena tidak ada NULL.

### Problem S4 ⭐⭐⭐
Bagaimana cara menemukan titik awal cycle dalam linked list setelah mendeteksi ada cycle menggunakan Floyd's algorithm? **Jawaban:** Setelah slow dan fast bertemu, pindahkan salah satu ke head. Gerakkan keduanya 1 langkah hingga bertemu lagi - titik pertemuan adalah awal cycle.

### Problem S5 ⭐⭐
Bandingkan penggunaan memori antara array dinamis dan double linked list untuk menyimpan n elemen integer. **Jawaban:** Array: n × sizeof(int) + overhead. DLL: n × (sizeof(int) + 2×sizeof(pointer)) = lebih besar karena setiap node menyimpan 2 pointer tambahan.

---

## 8. Ringkasan

| Konsep | Deskripsi | Kompleksitas Operasi Utama |
|--------|-----------|---------------------------|
| **Double Linked List** | Setiap node memiliki pointer prev dan next | Insert/Delete di ujung: O(1), Tengah: O(n) |
| **Single Circular LL** | Node terakhir menunjuk ke node pertama | Insert (dengan tail): O(1), Search: O(n) |
| **Double Circular LL** | Circular dengan pointer dua arah | Semua operasi di ujung: O(1) |
| **Sentinel Node** | Dummy node untuk menyederhanakan edge cases | Mengurangi pengecekan kondisi |
| **Iterator** | Objek untuk traversal standar | Traversal: O(n) |

### Kapan Menggunakan Masing-masing:

1. **Single Linked List**: Memori terbatas, hanya perlu traversal forward
2. **Double Linked List**: Perlu traversal dua arah, delete cepat jika punya pointer ke node
3. **Circular Linked List**: Data yang berputar (playlist, jadwal, buffer)
4. **Double Circular Linked List**: Kombinasi kebutuhan di atas

### Poin Penting untuk Diingat:

1. DLL menggunakan lebih banyak memori (3 field vs 2 field per node)
2. Pada circular list, selalu gunakan do-while untuk traversal
3. Sentinel node menghilangkan pengecekan khusus untuk edge cases
4. Floyd's algorithm mendeteksi cycle dalam O(n) waktu dan O(1) ruang
5. Pada Pertemuan 05 dan 06, kita akan mempelajari **Stack** dan **Queue** yang dapat diimplementasikan menggunakan linked list

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 10.2.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 3.
3. Goodrich, M.T., et al. (2011). *Data Structures and Algorithms in C++* (2nd Ed.). Wiley. Chapter 3.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
