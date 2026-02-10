# Modul 03: Linked List (Bagian 1) - Single Linked List

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 03  
**Topik:** Single Linked List

> **Capaian Pembelajaran:** Sub-CPMK-2.1 — Mampu mengimplementasikan single, double, dan circular linked list

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.10.2; Weiss Ch.3; Hubbard Ch.7

---

## Tujuan Pembelajaran

Setelah mempelajari modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** konsep dasar linked list dan komponen penyusunnya (node dan pointer)
2. **Membandingkan** karakteristik array dan linked list serta menentukan kapan menggunakan masing-masing
3. **Mengimplementasikan** struktur node untuk single linked list dalam C++
4. **Mengimplementasikan** operasi **insert** (di awal, di akhir, dan di tengah) pada single linked list
5. **Mengimplementasikan** operasi **delete** pada single linked list
6. **Mengimplementasikan** operasi **search** dan **traversal** pada single linked list
7. **Menganalisis** kompleksitas waktu dan ruang dari setiap operasi single linked list

---

## 1. Pendahuluan Linked List

### 1.1 Motivasi: Keterbatasan Array

Pada Pertemuan 01, kita telah mempelajari array sebagai struktur data fundamental. Meskipun array sangat berguna, array memiliki beberapa keterbatasan:

> **Keterbatasan Array:**
> 1. **Ukuran tetap (static)**: Ukuran array harus ditentukan saat kompilasi atau alokasi, dan tidak dapat diubah secara dinamis
> 2. **Operasi insert/delete tidak efisien**: Menyisipkan atau menghapus elemen di tengah array memerlukan pergeseran elemen-elemen lain dengan kompleksitas O(n)
> 3. **Pemborosan memori**: Jika kita mengalokasikan array lebih besar dari yang dibutuhkan, memori akan terbuang; jika terlalu kecil, perlu realokasi

### 1.2 Definisi Linked List

> **Linked List** adalah struktur data linear yang terdiri dari sekumpulan **node** yang saling terhubung melalui **pointer**. Berbeda dengan array yang menyimpan elemen secara berurutan dalam memori, linked list menyimpan elemen secara tersebar di memori dan menggunakan pointer untuk menghubungkan satu elemen dengan elemen berikutnya.

![Perbandingan Array vs Linked List](images/p03-01-array-vs-linkedlist-memory.png)

*Gambar 1.1: Perbandingan penyimpanan Array dan Linked List di memori*


### 1.3 Komponen Linked List

#### 1.3.1 Node

> **Node** adalah unit dasar penyusun linked list yang terdiri dari dua komponen:
> 1. **Data field**: Menyimpan nilai atau informasi
> 2. **Pointer field (next)**: Menyimpan alamat node berikutnya

![Struktur Node](images/p03-02-node-structure.png)

*Gambar 1.2: Struktur Node dalam Single Linked List*


#### 1.3.2 Head Pointer

> **Head** adalah pointer yang menunjuk ke node pertama dalam linked list. Head sangat penting karena merupakan satu-satunya akses masuk ke seluruh linked list.

#### 1.3.3 Tail (Opsional)

> **Tail** adalah pointer yang menunjuk ke node terakhir dalam linked list. Menyimpan tail bersifat opsional tetapi dapat mempercepat operasi insert di akhir dari O(n) menjadi O(1).

---

## 2. Perbandingan Array vs Linked List

| Aspek | Array | Linked List |
|-------|-------|-------------|
| **Ukuran** | Tetap (static) | Dinamis |
| **Alokasi Memori** | Berurutan (contiguous) | Tersebar (non-contiguous) |
| **Akses Elemen** | Random access O(1) | Sequential access O(n) |
| **Insert di Awal** | O(n) - perlu geser | O(1) |
| **Insert di Akhir** | O(1) jika ada ruang | O(n) tanpa tail, O(1) dengan tail |
| **Insert di Tengah** | O(n) | O(n) untuk cari + O(1) untuk insert |
| **Delete di Awal** | O(n) - perlu geser | O(1) |
| **Delete di Tengah** | O(n) | O(n) untuk cari + O(1) untuk delete |
| **Memory Overhead** | Tidak ada | Ada (pointer tambahan) |
| **Cache Performance** | Baik (locality) | Kurang baik (scattered) |

### SOLVED PROBLEM 1 ⭐

**Soal:** Sebuah sistem radar militer perlu menyimpan data 100 pesawat yang terdeteksi. Data pesawat sering ditambah dan dihapus secara dinamis. Struktur data mana yang lebih tepat digunakan, array atau linked list? Jelaskan alasannya.

**Penyelesaian:**

**Analisis:**
1. Jumlah pesawat terdeteksi bersifat dinamis (bisa bertambah/berkurang)
2. Operasi utama: insert (pesawat baru terdeteksi) dan delete (pesawat keluar area)
3. Tidak memerlukan akses random (tidak perlu langsung ke pesawat ke-50)

**Jawaban:** **Linked List** lebih tepat digunakan karena:
- Ukuran dinamis sesuai jumlah pesawat yang terdeteksi
- Insert dan delete yang sering akan lebih efisien
- Tidak ada pemborosan memori untuk slot yang kosong

Namun, jika sistem memerlukan akses cepat ke pesawat tertentu berdasarkan index, array dengan dynamic resizing (seperti `std::vector`) bisa menjadi alternatif yang baik.

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Mengapa linked list memiliki cache performance yang lebih buruk dibandingkan array?

**Penyelesaian:**

**Konsep Cache:**
- CPU cache menyimpan data yang berdekatan dalam memori untuk akses cepat
- Ketika satu elemen diakses, elemen-elemen di sekitarnya juga di-load ke cache (spatial locality)

**Array:**
- Elemen tersimpan berurutan di memori
- Akses elemen[0] akan membawa elemen[1], elemen[2], dst ke cache
- Cache hit rate tinggi

**Linked List:**
- Node tersebar di berbagai lokasi memori
- Akses satu node tidak menjamin node berikutnya ada di cache
- Cache miss rate tinggi → perlu akses ke main memory yang lebih lambat

---

## 3. Implementasi Node dalam C++

### 3.1 Definisi Struct Node

```cpp
struct Node {
    int data;       // Data yang disimpan (bisa tipe data lain)
    Node* next;     // Pointer ke node berikutnya
    
    // Constructor
    Node(int value) : data(value), next(nullptr) {}
};
```

### 3.2 Membuat Node Baru

```cpp
// Menggunakan constructor
Node* newNode = new Node(10);

// Atau secara manual
Node* anotherNode = new Node;
anotherNode->data = 20;
anotherNode->next = nullptr;
```

### SOLVED PROBLEM 3 ⭐

**Soal:** Tuliskan kode untuk membuat tiga node dengan nilai 5, 10, dan 15, kemudian hubungkan ketiganya menjadi sebuah linked list.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

int main() {
    // Buat tiga node
    Node* node1 = new Node(5);
    Node* node2 = new Node(10);
    Node* node3 = new Node(15);
    
    // Hubungkan node-node
    node1->next = node2;  // node1 -> node2
    node2->next = node3;  // node2 -> node3
    // node3->next sudah nullptr dari constructor
    
    // Set head
    Node* head = node1;
    
    // Verifikasi dengan traversal
    Node* current = head;
    while (current != nullptr) {
        cout << current->data << " -> ";
        current = current->next;
    }
    cout << "NULL" << endl;
    
    // Output: 5 -> 10 -> 15 -> NULL
    
    return 0;
}
```

---

## 4. Single Linked List

### 4.1 Definisi

> **Single Linked List** adalah jenis linked list di mana setiap node hanya memiliki satu pointer yang menunjuk ke node berikutnya. Traversal hanya dapat dilakukan dalam satu arah: dari head ke tail.

![Single Linked List](images/p03-03-single-linked-list.png)

*Gambar 4.1: Struktur Single Linked List*


### 4.2 Kelas Single Linked List

```cpp
class SingleLinkedList {
private:
    Node* head;
    int size;

public:
    // Constructor
    SingleLinkedList() : head(nullptr), size(0) {}
    
    // Destructor
    ~SingleLinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
    }
    
    // Method declarations
    void insertAtBeginning(int value);
    void insertAtEnd(int value);
    void insertAtPosition(int value, int position);
    void deleteAtBeginning();
    void deleteAtEnd();
    void deleteAtPosition(int position);
    bool search(int value);
    void display();
    int getSize();
    bool isEmpty();
};
```

---

## 5. Operasi pada Single Linked List

### 5.1 Traversal (Penelusuran)

> **Traversal** adalah operasi mengunjungi setiap node dalam linked list dari head hingga node terakhir (NULL).

**Algoritma:**
1. Mulai dari head
2. Kunjungi node saat ini
3. Pindah ke node berikutnya (current = current->next)
4. Ulangi langkah 2-3 sampai current == NULL

```cpp
void SingleLinkedList::display() {
    Node* current = head;
    while (current != nullptr) {
        cout << current->data;
        if (current->next != nullptr) {
            cout << " -> ";
        }
        current = current->next;
    }
    cout << " -> NULL" << endl;
}
```

**Kompleksitas:** O(n) - harus mengunjungi semua node

### SOLVED PROBLEM 4 ⭐

**Soal:** Implementasikan fungsi untuk menghitung jumlah total elemen dalam single linked list.

**Penyelesaian:**

```cpp
int SingleLinkedList::getSize() {
    // Opsi 1: Gunakan variabel size yang sudah disimpan
    return size;  // O(1)
    
    // Opsi 2: Hitung dengan traversal (jika tidak menyimpan size)
    /*
    int count = 0;
    Node* current = head;
    while (current != nullptr) {
        count++;
        current = current->next;
    }
    return count;  // O(n)
    */
}
```

### SOLVED PROBLEM 5 ⭐

**Soal:** Implementasikan fungsi untuk mencari nilai maksimum dalam single linked list.

**Penyelesaian:**

```cpp
int findMax(Node* head) {
    if (head == nullptr) {
        throw runtime_error("List kosong!");
    }
    
    int maxVal = head->data;  // Asumsi nilai pertama sebagai max
    Node* current = head->next;
    
    while (current != nullptr) {
        if (current->data > maxVal) {
            maxVal = current->data;
        }
        current = current->next;
    }
    
    return maxVal;
}
```

**Kompleksitas:** O(n) - harus memeriksa semua node

---

### 5.2 Insert di Awal (Insert at Beginning)

**Langkah-langkah:**
1. Buat node baru
2. Set next dari node baru ke head saat ini
3. Update head ke node baru

![Insert di Awal](images/p03-04-insert-at-beginning.png)

*Gambar 5.1: Operasi Insert di Awal Single Linked List*


```cpp
void SingleLinkedList::insertAtBeginning(int value) {
    Node* newNode = new Node(value);  // Step 1
    newNode->next = head;              // Step 2
    head = newNode;                    // Step 3
    size++;
}
```

**Kompleksitas:** O(1) - operasi konstan

### SOLVED PROBLEM 6 ⭐

**Soal:** Diberikan linked list: 10 -> 20 -> 30 -> NULL. Gambarkan kondisi linked list setelah operasi `insertAtBeginning(5)`.

**Penyelesaian:**

**Sebelum:**
```
head -> [10] -> [20] -> [30] -> NULL
```

**Proses:**
1. Buat node baru dengan data = 5
2. newNode->next = head (newNode->next menunjuk ke node 10)
3. head = newNode (head sekarang menunjuk ke node 5)

**Sesudah:**
```
head -> [5] -> [10] -> [20] -> [30] -> NULL
```

---

### 5.3 Insert di Akhir (Insert at End)

**Langkah-langkah:**
1. Buat node baru
2. Jika list kosong, jadikan node baru sebagai head
3. Jika tidak, traversal sampai node terakhir
4. Set next dari node terakhir ke node baru

![Insert di Akhir](images/p03-05-insert-at-end.png)

*Gambar 5.2: Operasi Insert di Akhir Single Linked List*


```cpp
void SingleLinkedList::insertAtEnd(int value) {
    Node* newNode = new Node(value);
    
    // Kasus list kosong
    if (head == nullptr) {
        head = newNode;
        size++;
        return;
    }
    
    // Traversal ke node terakhir
    Node* current = head;
    while (current->next != nullptr) {
        current = current->next;
    }
    
    // Hubungkan node terakhir ke node baru
    current->next = newNode;
    size++;
}
```

**Kompleksitas:** O(n) - perlu traversal ke akhir

### SOLVED PROBLEM 7 ⭐⭐

**Soal:** Modifikasi kelas SingleLinkedList agar memiliki pointer tail sehingga operasi insertAtEnd menjadi O(1).

**Penyelesaian:**

```cpp
class SingleLinkedListWithTail {
private:
    Node* head;
    Node* tail;  // Tambahan pointer tail
    int size;

public:
    SingleLinkedListWithTail() : head(nullptr), tail(nullptr), size(0) {}
    
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        
        if (head == nullptr) {
            // List kosong
            head = newNode;
            tail = newNode;
        } else {
            // List tidak kosong
            tail->next = newNode;  // O(1) - langsung akses tail
            tail = newNode;        // Update tail
        }
        size++;
    }
    
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
        
        if (tail == nullptr) {
            tail = newNode;  // Jika list sebelumnya kosong
        }
        size++;
    }
};
```

---

### 5.4 Insert di Posisi Tertentu

**Langkah-langkah:**
1. Validasi posisi (0 <= posisi <= size)
2. Jika posisi == 0, panggil insertAtBeginning
3. Traversal sampai node di posisi (posisi - 1)
4. Sisipkan node baru

![Insert di Tengah](images/p03-06-insert-at-position.png)

*Gambar 5.3: Operasi Insert di Posisi Tertentu*


```cpp
void SingleLinkedList::insertAtPosition(int value, int position) {
    // Validasi posisi
    if (position < 0 || position > size) {
        throw out_of_range("Posisi tidak valid!");
    }
    
    // Insert di awal
    if (position == 0) {
        insertAtBeginning(value);
        return;
    }
    
    // Traversal ke posisi (position - 1)
    Node* prev = head;
    for (int i = 0; i < position - 1; i++) {
        prev = prev->next;
    }
    
    // Sisipkan node baru
    Node* newNode = new Node(value);
    newNode->next = prev->next;
    prev->next = newNode;
    size++;
}
```

**Kompleksitas:** O(n) - perlu traversal ke posisi tertentu

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Diberikan linked list: 10 -> 30 -> 40 -> NULL. Sisipkan nilai 20 di posisi 1 (index berbasis 0). Tunjukkan langkah-langkahnya.

**Penyelesaian:**

**Kondisi Awal:**
```
Position:  0     1     2
          [10] -> [30] -> [40] -> NULL
          head
```

**Langkah 1:** Validasi posisi (1 valid karena 0 <= 1 <= 3)

**Langkah 2:** Traversal ke posisi 0 (posisi - 1 = 0)
```cpp
prev = head;  // prev menunjuk ke [10]
```

**Langkah 3:** Buat node baru dengan nilai 20

**Langkah 4:** Hubungkan
```cpp
newNode->next = prev->next;  // newNode->next = [30]
prev->next = newNode;        // [10]->next = newNode
```

**Kondisi Akhir:**
```
Position:  0     1     2     3
          [10] -> [20] -> [30] -> [40] -> NULL
          head
```

---

### 5.5 Delete di Awal (Delete at Beginning)

**Langkah-langkah:**
1. Jika list kosong, return atau throw exception
2. Simpan pointer ke head
3. Update head ke node berikutnya
4. Delete node yang disimpan

![Delete di Awal](images/p03-07-delete-at-beginning.png)

*Gambar 5.4: Operasi Delete di Awal Single Linked List*


```cpp
void SingleLinkedList::deleteAtBeginning() {
    if (head == nullptr) {
        throw runtime_error("List kosong!");
    }
    
    Node* temp = head;      // Simpan node yang akan dihapus
    head = head->next;      // Update head
    delete temp;            // Hapus node
    size--;
}
```

**Kompleksitas:** O(1) - operasi konstan

### SOLVED PROBLEM 9 ⭐

**Soal:** Apa yang terjadi jika kita langsung melakukan `delete head` tanpa menyimpan `head->next` terlebih dahulu?

**Penyelesaian:**

Jika kita langsung melakukan `delete head` tanpa menyimpan referensi ke node berikutnya:

```cpp
// SALAH!
delete head;
head = head->next;  // ERROR! head sudah dihapus, akses ke head->next undefined behavior
```

**Masalah:**
1. Setelah `delete head`, memori yang ditunjuk `head` sudah dibebaskan
2. Mengakses `head->next` adalah **undefined behavior** (dangling pointer)
3. Bisa menyebabkan crash atau data corruption

**Solusi yang Benar:**
```cpp
Node* temp = head;     // Simpan dulu
head = head->next;     // Update head sebelum delete
delete temp;           // Baru hapus
```

---

### 5.6 Delete di Akhir (Delete at End)

**Langkah-langkah:**
1. Jika list kosong, return atau throw exception
2. Jika hanya ada satu node, hapus dan set head = nullptr
3. Traversal sampai node kedua terakhir
4. Delete node terakhir dan set next node kedua terakhir = nullptr

```cpp
void SingleLinkedList::deleteAtEnd() {
    if (head == nullptr) {
        throw runtime_error("List kosong!");
    }
    
    // Kasus hanya satu node
    if (head->next == nullptr) {
        delete head;
        head = nullptr;
        size--;
        return;
    }
    
    // Traversal ke node kedua terakhir
    Node* current = head;
    while (current->next->next != nullptr) {
        current = current->next;
    }
    
    // Hapus node terakhir
    delete current->next;
    current->next = nullptr;
    size--;
}
```

**Kompleksitas:** O(n) - perlu traversal ke akhir

### SOLVED PROBLEM 10 ⭐⭐

**Soal:** Mengapa kondisi loop untuk delete di akhir adalah `current->next->next != nullptr` bukan `current->next != nullptr`?

**Penyelesaian:**

**Jika menggunakan `current->next != nullptr`:**
```
head -> [10] -> [20] -> [30] -> NULL
                         ^
                      current (berhenti di node terakhir)
```
- Loop berhenti ketika current menunjuk ke node terakhir [30]
- Kita tidak punya akses ke node sebelumnya untuk mengubah next-nya
- Tidak bisa melakukan `sebelumnya->next = nullptr`

**Jika menggunakan `current->next->next != nullptr`:**
```
head -> [10] -> [20] -> [30] -> NULL
                 ^
              current (berhenti di node kedua terakhir)
```
- Loop berhenti ketika current menunjuk ke [20]
- `current->next` adalah [30] (node yang akan dihapus)
- Kita bisa melakukan `delete current->next` dan `current->next = nullptr`

**Kesimpulan:** Untuk menghapus node terakhir, kita perlu akses ke node **kedua terakhir** agar bisa mengubah pointer next-nya menjadi nullptr.

---

### 5.7 Delete di Posisi Tertentu

```cpp
void SingleLinkedList::deleteAtPosition(int position) {
    if (head == nullptr) {
        throw runtime_error("List kosong!");
    }
    
    if (position < 0 || position >= size) {
        throw out_of_range("Posisi tidak valid!");
    }
    
    // Delete di awal
    if (position == 0) {
        deleteAtBeginning();
        return;
    }
    
    // Traversal ke posisi (position - 1)
    Node* prev = head;
    for (int i = 0; i < position - 1; i++) {
        prev = prev->next;
    }
    
    // Hapus node
    Node* toDelete = prev->next;
    prev->next = toDelete->next;
    delete toDelete;
    size--;
}
```

**Kompleksitas:** O(n) - perlu traversal ke posisi tertentu

### SOLVED PROBLEM 11 ⭐⭐

**Soal:** Implementasikan fungsi untuk menghapus node dengan nilai tertentu (bukan berdasarkan posisi).

**Penyelesaian:**

```cpp
bool deleteByValue(Node*& head, int value) {
    if (head == nullptr) {
        return false;  // List kosong
    }
    
    // Kasus node pertama memiliki nilai yang dicari
    if (head->data == value) {
        Node* temp = head;
        head = head->next;
        delete temp;
        return true;
    }
    
    // Cari node dengan nilai yang dicari
    Node* current = head;
    while (current->next != nullptr && current->next->data != value) {
        current = current->next;
    }
    
    // Node tidak ditemukan
    if (current->next == nullptr) {
        return false;
    }
    
    // Hapus node
    Node* toDelete = current->next;
    current->next = toDelete->next;
    delete toDelete;
    return true;
}
```

---

### 5.8 Search (Pencarian)

> **Search** adalah operasi untuk mencari apakah suatu nilai ada dalam linked list.

```cpp
bool SingleLinkedList::search(int value) {
    Node* current = head;
    while (current != nullptr) {
        if (current->data == value) {
            return true;  // Ditemukan
        }
        current = current->next;
    }
    return false;  // Tidak ditemukan
}
```

**Kompleksitas:** O(n) - worst case harus memeriksa semua node

### SOLVED PROBLEM 12 ⭐

**Soal:** Modifikasi fungsi search agar mengembalikan posisi (index) elemen yang ditemukan, atau -1 jika tidak ditemukan.

**Penyelesaian:**

```cpp
int searchPosition(Node* head, int value) {
    Node* current = head;
    int position = 0;
    
    while (current != nullptr) {
        if (current->data == value) {
            return position;  // Return posisi
        }
        current = current->next;
        position++;
    }
    
    return -1;  // Tidak ditemukan
}
```

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Implementasikan fungsi untuk mencari elemen ke-k dari belakang dalam single linked list dengan satu kali traversal.

**Penyelesaian:**

**Strategi:** Gunakan dua pointer dengan jarak k node.

```cpp
int findKthFromEnd(Node* head, int k) {
    if (head == nullptr || k <= 0) {
        throw invalid_argument("Parameter tidak valid!");
    }
    
    Node* fast = head;
    Node* slow = head;
    
    // Majukan fast k langkah
    for (int i = 0; i < k; i++) {
        if (fast == nullptr) {
            throw out_of_range("k lebih besar dari panjang list!");
        }
        fast = fast->next;
    }
    
    // Majukan kedua pointer bersamaan sampai fast mencapai akhir
    while (fast != nullptr) {
        fast = fast->next;
        slow = slow->next;
    }
    
    return slow->data;  // slow sekarang di posisi ke-k dari belakang
}
```

**Penjelasan:**
- Jarak antara fast dan slow adalah k node
- Ketika fast mencapai nullptr (akhir), slow berada di posisi ke-k dari belakang
- Kompleksitas: O(n) waktu, O(1) ruang

**Contoh:** List: 10 -> 20 -> 30 -> 40 -> 50, k = 2

![Finding K-th Element from End](images/p03-08-kth-from-end-two-pointers.png)

*Gambar 3.8: Visualisasi two-pointer technique untuk menemukan elemen ke-k dari belakang*


**Hasil:** fast = NULL, slow->data = 40 (elemen ke-2 dari belakang)

---

## 6. Kompleksitas Operasi Single Linked List

| Operasi | Kompleksitas Waktu | Kompleksitas Ruang |
|---------|-------------------|-------------------|
| Traversal | O(n) | O(1) |
| Search | O(n) | O(1) |
| Insert at Beginning | O(1) | O(1) |
| Insert at End | O(n) tanpa tail, O(1) dengan tail | O(1) |
| Insert at Position | O(n) | O(1) |
| Delete at Beginning | O(1) | O(1) |
| Delete at End | O(n) | O(1) |
| Delete at Position | O(n) | O(1) |
| Access by Index | O(n) | O(1) |

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Mengapa delete di akhir single linked list tetap O(n) meskipun kita memiliki pointer tail?

**Penyelesaian:**

Meskipun memiliki pointer tail yang menunjuk ke node terakhir, kita tidak bisa langsung menghapus node terakhir karena:

1. **Single linked list hanya memiliki pointer ke node berikutnya (next)**
2. **Untuk menghapus node terakhir, kita perlu mengubah `next` dari node kedua terakhir menjadi `nullptr`**
3. **Dari tail, kita tidak bisa mundur ke node sebelumnya**

```cpp
// Meskipun punya tail, tetap harus traversal
void deleteAtEnd() {
    // ...
    Node* current = head;
    while (current->next != tail) {  // Tetap O(n)
        current = current->next;
    }
    delete tail;
    tail = current;
    current->next = nullptr;
}
```

**Solusi untuk O(1) delete di akhir:**
- Gunakan **Double Linked List** (akan dipelajari di Pertemuan 04)
- Setiap node memiliki pointer ke node sebelumnya (prev) dan berikutnya (next)

---

## 7. Implementasi Lengkap Single Linked List

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int value) : data(value), next(nullptr) {}
};

class SingleLinkedList {
private:
    Node* head;
    int size;

public:
    // Constructor
    SingleLinkedList() : head(nullptr), size(0) {}
    
    // Destructor - penting untuk menghindari memory leak
    ~SingleLinkedList() {
        Node* current = head;
        while (current != nullptr) {
            Node* next = current->next;
            delete current;
            current = next;
        }
    }
    
    // Cek apakah list kosong
    bool isEmpty() {
        return head == nullptr;
    }
    
    // Dapatkan ukuran list
    int getSize() {
        return size;
    }
    
    // Insert di awal - O(1)
    void insertAtBeginning(int value) {
        Node* newNode = new Node(value);
        newNode->next = head;
        head = newNode;
        size++;
    }
    
    // Insert di akhir - O(n)
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* current = head;
            while (current->next != nullptr) {
                current = current->next;
            }
            current->next = newNode;
        }
        size++;
    }
    
    // Insert di posisi tertentu - O(n)
    void insertAtPosition(int value, int position) {
        if (position < 0 || position > size) {
            throw out_of_range("Posisi tidak valid!");
        }
        
        if (position == 0) {
            insertAtBeginning(value);
            return;
        }
        
        Node* prev = head;
        for (int i = 0; i < position - 1; i++) {
            prev = prev->next;
        }
        
        Node* newNode = new Node(value);
        newNode->next = prev->next;
        prev->next = newNode;
        size++;
    }
    
    // Delete di awal - O(1)
    void deleteAtBeginning() {
        if (head == nullptr) {
            throw runtime_error("List kosong!");
        }
        Node* temp = head;
        head = head->next;
        delete temp;
        size--;
    }
    
    // Delete di akhir - O(n)
    void deleteAtEnd() {
        if (head == nullptr) {
            throw runtime_error("List kosong!");
        }
        
        if (head->next == nullptr) {
            delete head;
            head = nullptr;
            size--;
            return;
        }
        
        Node* current = head;
        while (current->next->next != nullptr) {
            current = current->next;
        }
        
        delete current->next;
        current->next = nullptr;
        size--;
    }
    
    // Delete di posisi tertentu - O(n)
    void deleteAtPosition(int position) {
        if (head == nullptr) {
            throw runtime_error("List kosong!");
        }
        if (position < 0 || position >= size) {
            throw out_of_range("Posisi tidak valid!");
        }
        
        if (position == 0) {
            deleteAtBeginning();
            return;
        }
        
        Node* prev = head;
        for (int i = 0; i < position - 1; i++) {
            prev = prev->next;
        }
        
        Node* toDelete = prev->next;
        prev->next = toDelete->next;
        delete toDelete;
        size--;
    }
    
    // Search - O(n)
    bool search(int value) {
        Node* current = head;
        while (current != nullptr) {
            if (current->data == value) {
                return true;
            }
            current = current->next;
        }
        return false;
    }
    
    // Display
    void display() {
        Node* current = head;
        while (current != nullptr) {
            cout << current->data;
            if (current->next != nullptr) {
                cout << " -> ";
            }
            current = current->next;
        }
        cout << " -> NULL" << endl;
    }
};

int main() {
    SingleLinkedList list;
    
    // Insert
    list.insertAtEnd(10);
    list.insertAtEnd(20);
    list.insertAtEnd(30);
    cout << "Setelah insert 10, 20, 30: ";
    list.display();  // 10 -> 20 -> 30 -> NULL
    
    list.insertAtBeginning(5);
    cout << "Setelah insertAtBeginning(5): ";
    list.display();  // 5 -> 10 -> 20 -> 30 -> NULL
    
    list.insertAtPosition(15, 2);
    cout << "Setelah insertAtPosition(15, 2): ";
    list.display();  // 5 -> 10 -> 15 -> 20 -> 30 -> NULL
    
    // Search
    cout << "Search 15: " << (list.search(15) ? "Ditemukan" : "Tidak ditemukan") << endl;
    cout << "Search 100: " << (list.search(100) ? "Ditemukan" : "Tidak ditemukan") << endl;
    
    // Delete
    list.deleteAtBeginning();
    cout << "Setelah deleteAtBeginning(): ";
    list.display();  // 10 -> 15 -> 20 -> 30 -> NULL
    
    list.deleteAtEnd();
    cout << "Setelah deleteAtEnd(): ";
    list.display();  // 10 -> 15 -> 20 -> NULL
    
    list.deleteAtPosition(1);
    cout << "Setelah deleteAtPosition(1): ";
    list.display();  // 10 -> 20 -> NULL
    
    cout << "Size: " << list.getSize() << endl;  // 2
    
    return 0;
}
```

---

## 8. Aplikasi Single Linked List

### 8.1 Implementasi Stack

Stack (yang akan dipelajari di Pertemuan 05) dapat diimplementasikan dengan linked list:
- Push = insertAtBeginning() - O(1)
- Pop = deleteAtBeginning() - O(1)

### 8.2 Implementasi Queue

Queue (yang akan dipelajari di Pertemuan 06) dapat diimplementasikan dengan linked list:
- Enqueue = insertAtEnd() - O(n) atau O(1) dengan tail
- Dequeue = deleteAtBeginning() - O(1)

### 8.3 Konteks Pertahanan: Sistem Antrian Komunikasi

Dalam sistem komunikasi militer, pesan-pesan yang masuk dapat disimpan dalam linked list:
- Pesan baru ditambahkan di akhir (insertAtEnd)
- Pesan diproses dari awal (deleteAtBeginning)
- Pesan prioritas tinggi dapat disisipkan di posisi tertentu

### SOLVED PROBLEM 15 ⭐⭐

**Soal:** Implementasikan sistem antrian pesan sederhana untuk komando pertahanan menggunakan single linked list.

**Penyelesaian:**

```cpp
#include <iostream>
#include <string>
using namespace std;

// Node untuk menyimpan pesan
struct MessageNode {
    string sender;
    string message;
    int priority;  // 1 = tinggi, 2 = sedang, 3 = rendah
    MessageNode* next;
    
    MessageNode(string s, string m, int p) 
        : sender(s), message(m), priority(p), next(nullptr) {}
};

class MessageQueue {
private:
    MessageNode* head;
    MessageNode* tail;

public:
    MessageQueue() : head(nullptr), tail(nullptr) {}
    
    // Tambah pesan (di akhir untuk FIFO normal)
    void addMessage(string sender, string message, int priority) {
        MessageNode* newNode = new MessageNode(sender, message, priority);
        
        if (head == nullptr) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
        cout << "[PESAN MASUK] Dari: " << sender << endl;
    }
    
    // Tambah pesan prioritas tinggi (di awal)
    void addUrgentMessage(string sender, string message) {
        MessageNode* newNode = new MessageNode(sender, message, 1);
        newNode->next = head;
        head = newNode;
        if (tail == nullptr) {
            tail = newNode;
        }
        cout << "[PESAN URGENT] Dari: " << sender << endl;
    }
    
    // Proses pesan (ambil dari awal)
    void processMessage() {
        if (head == nullptr) {
            cout << "[KOSONG] Tidak ada pesan untuk diproses" << endl;
            return;
        }
        
        cout << "=== MEMPROSES PESAN ===" << endl;
        cout << "Dari    : " << head->sender << endl;
        cout << "Pesan   : " << head->message << endl;
        cout << "Prioritas: " << head->priority << endl;
        
        MessageNode* temp = head;
        head = head->next;
        if (head == nullptr) {
            tail = nullptr;
        }
        delete temp;
    }
    
    // Tampilkan semua pesan
    void displayAll() {
        if (head == nullptr) {
            cout << "[KOSONG] Tidak ada pesan" << endl;
            return;
        }
        
        cout << "\n=== DAFTAR PESAN ===" << endl;
        MessageNode* current = head;
        int no = 1;
        while (current != nullptr) {
            cout << no++ << ". [P" << current->priority << "] " 
                 << current->sender << ": " << current->message << endl;
            current = current->next;
        }
        cout << endl;
    }
};

int main() {
    MessageQueue mq;
    
    mq.addMessage("Komandan A", "Laporan posisi sektor utara aman", 2);
    mq.addMessage("Komandan B", "Request supply amunisi", 2);
    mq.addUrgentMessage("Komandan C", "KONTAK! Terdeteksi pergerakan musuh!");
    mq.addMessage("Komandan D", "Laporan rutin sektor timur", 3);
    
    mq.displayAll();
    
    cout << "\nMemproses pesan...\n" << endl;
    mq.processMessage();  // Akan memproses pesan urgent dulu
    mq.processMessage();
    
    mq.displayAll();
    
    return 0;
}
```

---

## 9. Solved Problems Lanjutan

### SOLVED PROBLEM 16 ⭐⭐

**Soal:** Implementasikan fungsi untuk membalik (reverse) single linked list secara in-place.

**Penyelesaian:**

```cpp
void reverseList(Node*& head) {
    Node* prev = nullptr;
    Node* current = head;
    Node* next = nullptr;
    
    while (current != nullptr) {
        // Simpan next
        next = current->next;
        // Balik pointer
        current->next = prev;
        // Pindah prev dan current
        prev = current;
        current = next;
    }
    
    head = prev;
}
```

**Visualisasi:**

![Reverse Single Linked List](images/p03-09-reverse-linked-list-steps.png)

*Gambar 3.9: Step-by-step proses membalik single linked list*


**Kompleksitas:** O(n) waktu, O(1) ruang

### SOLVED PROBLEM 17 ⭐⭐⭐

**Soal:** Deteksi apakah single linked list memiliki cycle (loop) menggunakan Floyd's Cycle Detection Algorithm.

**Penyelesaian:**

```cpp
bool hasCycle(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return false;
    }
    
    Node* slow = head;      // Bergerak 1 langkah
    Node* fast = head;      // Bergerak 2 langkah
    
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
        
        if (slow == fast) {
            return true;  // Cycle terdeteksi
        }
    }
    
    return false;  // Tidak ada cycle
}
```

**Penjelasan:**
- Slow pointer bergerak 1 node per iterasi
- Fast pointer bergerak 2 node per iterasi
- Jika ada cycle, fast akan "mengejar" slow dan mereka akan bertemu
- Jika tidak ada cycle, fast akan mencapai nullptr

**Kompleksitas:** O(n) waktu, O(1) ruang

### SOLVED PROBLEM 18 ⭐⭐⭐

**Soal:** Gabungkan dua sorted linked list menjadi satu sorted linked list.

**Penyelesaian:**

```cpp
Node* mergeSortedLists(Node* l1, Node* l2) {
    // Dummy node untuk mempermudah
    Node dummy(0);
    Node* tail = &dummy;
    
    while (l1 != nullptr && l2 != nullptr) {
        if (l1->data <= l2->data) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    
    // Sisakan yang tersisa
    if (l1 != nullptr) {
        tail->next = l1;
    } else {
        tail->next = l2;
    }
    
    return dummy.next;
}
```

**Contoh:**
```
l1: 1 -> 3 -> 5 -> NULL
l2: 2 -> 4 -> 6 -> NULL

Hasil: 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> NULL
```

**Kompleksitas:** O(n + m) waktu, O(1) ruang

### SOLVED PROBLEM 19 ⭐⭐

**Soal:** Implementasikan fungsi untuk menghapus semua duplikat dari sorted linked list.

**Penyelesaian:**

```cpp
void removeDuplicates(Node* head) {
    if (head == nullptr) return;
    
    Node* current = head;
    
    while (current->next != nullptr) {
        if (current->data == current->next->data) {
            // Hapus duplikat
            Node* duplicate = current->next;
            current->next = current->next->next;
            delete duplicate;
        } else {
            current = current->next;
        }
    }
}
```

**Contoh:**
```
Sebelum: 1 -> 1 -> 2 -> 3 -> 3 -> 3 -> NULL
Sesudah: 1 -> 2 -> 3 -> NULL
```

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Temukan node di mana dua single linked list bertemu (intersection point).

**Penyelesaian:**

```cpp
Node* findIntersection(Node* headA, Node* headB) {
    if (headA == nullptr || headB == nullptr) {
        return nullptr;
    }
    
    // Hitung panjang kedua list
    int lenA = 0, lenB = 0;
    Node* currA = headA;
    Node* currB = headB;
    
    while (currA != nullptr) {
        lenA++;
        currA = currA->next;
    }
    while (currB != nullptr) {
        lenB++;
        currB = currB->next;
    }
    
    // Reset pointer
    currA = headA;
    currB = headB;
    
    // Majukan pointer yang lebih panjang
    int diff = abs(lenA - lenB);
    if (lenA > lenB) {
        for (int i = 0; i < diff; i++) currA = currA->next;
    } else {
        for (int i = 0; i < diff; i++) currB = currB->next;
    }
    
    // Cari titik temu
    while (currA != currB) {
        currA = currA->next;
        currB = currB->next;
    }
    
    return currA;  // nullptr jika tidak ada intersection
}
```

**Kompleksitas:** O(n + m) waktu, O(1) ruang

### SOLVED PROBLEM 21 ⭐

**Soal:** Implementasikan fungsi untuk mengecek apakah linked list adalah palindrome.

**Penyelesaian:**

```cpp
bool isPalindrome(Node* head) {
    if (head == nullptr || head->next == nullptr) {
        return true;
    }
    
    // 1. Cari tengah list
    Node* slow = head;
    Node* fast = head;
    while (fast->next != nullptr && fast->next->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    // 2. Reverse setengah kedua
    Node* secondHalf = reverseListHelper(slow->next);
    
    // 3. Bandingkan
    Node* firstHalf = head;
    Node* secondHalfCopy = secondHalf;
    bool result = true;
    
    while (secondHalf != nullptr) {
        if (firstHalf->data != secondHalf->data) {
            result = false;
            break;
        }
        firstHalf = firstHalf->next;
        secondHalf = secondHalf->next;
    }
    
    // 4. Restore list (opsional)
    slow->next = reverseListHelper(secondHalfCopy);
    
    return result;
}

Node* reverseListHelper(Node* head) {
    Node* prev = nullptr;
    Node* curr = head;
    while (curr != nullptr) {
        Node* next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

**Contoh:**
```
1 -> 2 -> 3 -> 2 -> 1 -> NULL  =>  true (palindrome)
1 -> 2 -> 3 -> 4 -> 5 -> NULL  =>  false
```

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Dalam konteks sistem pertahanan, implementasikan linked list untuk menyimpan log aktivitas radar dengan fitur circular buffer (ketika penuh, data lama tertimpa).

**Penyelesaian:**

```cpp
#include <iostream>
#include <string>
#include <ctime>
using namespace std;

struct RadarLog {
    time_t timestamp;
    string activity;
    RadarLog* next;
    
    RadarLog(string act) : activity(act), next(nullptr) {
        timestamp = time(nullptr);
    }
};

class RadarLogBuffer {
private:
    RadarLog* head;
    RadarLog* tail;
    int maxSize;
    int currentSize;

public:
    RadarLogBuffer(int size) : head(nullptr), tail(nullptr), 
                                maxSize(size), currentSize(0) {}
    
    void addLog(string activity) {
        RadarLog* newLog = new RadarLog(activity);
        
        if (currentSize == 0) {
            head = tail = newLog;
            currentSize = 1;
        } else if (currentSize < maxSize) {
            // Masih ada ruang
            tail->next = newLog;
            tail = newLog;
            currentSize++;
        } else {
            // Buffer penuh, hapus yang paling lama (head)
            RadarLog* oldHead = head;
            head = head->next;
            delete oldHead;
            
            // Tambah yang baru di akhir
            tail->next = newLog;
            tail = newLog;
        }
        
        cout << "[LOG ADDED] " << activity << endl;
    }
    
    void displayLogs() {
        cout << "\n=== RADAR LOG BUFFER (" << currentSize 
             << "/" << maxSize << ") ===" << endl;
        
        RadarLog* current = head;
        int no = 1;
        while (current != nullptr) {
            char timeStr[26];
            ctime_r(&current->timestamp, timeStr);
            timeStr[24] = '\0';  // Remove newline
            cout << no++ << ". [" << timeStr << "] " 
                 << current->activity << endl;
            current = current->next;
        }
        cout << endl;
    }
    
    ~RadarLogBuffer() {
        while (head != nullptr) {
            RadarLog* temp = head;
            head = head->next;
            delete temp;
        }
    }
};

int main() {
    RadarLogBuffer buffer(3);  // Hanya simpan 3 log terakhir
    
    buffer.addLog("Pesawat terdeteksi di sektor A");
    buffer.addLog("Target bergerak ke utara");
    buffer.addLog("Sinyal radar normal");
    buffer.displayLogs();
    
    // Log ke-4 akan mengganti yang paling lama
    buffer.addLog("Cuaca buruk, visibilitas rendah");
    buffer.displayLogs();
    
    // Log ke-5
    buffer.addLog("Pesawat kedua terdeteksi");
    buffer.displayLogs();
    
    return 0;
}
```

---

## 10. Supplementary Problems

### Problem S1 ⭐
Implementasikan fungsi untuk menyalin (deep copy) sebuah single linked list.

**Jawaban Singkat:**
```cpp
Node* copyList(Node* head) {
    if (head == nullptr) return nullptr;
    
    Node* newHead = new Node(head->data);
    Node* current = head->next;
    Node* newCurrent = newHead;
    
    while (current != nullptr) {
        newCurrent->next = new Node(current->data);
        newCurrent = newCurrent->next;
        current = current->next;
    }
    
    return newHead;
}
```

### Problem S2 ⭐
Apa output dari kode berikut?
```cpp
Node* a = new Node(1);
Node* b = new Node(2);
Node* c = new Node(3);
a->next = b;
b->next = c;
Node* temp = a;
while (temp != nullptr) {
    cout << temp->data << " ";
    temp = temp->next;
}
```

**Jawaban:** `1 2 3`

### Problem S3 ⭐⭐
Tuliskan fungsi untuk menghitung rata-rata nilai dalam linked list.

**Jawaban Singkat:**
```cpp
double average(Node* head) {
    if (head == nullptr) return 0;
    
    double sum = 0;
    int count = 0;
    Node* current = head;
    
    while (current != nullptr) {
        sum += current->data;
        count++;
        current = current->next;
    }
    
    return sum / count;
}
```

### Problem S4 ⭐⭐
Mengapa kita perlu destructor di kelas linked list?

**Jawaban:** Untuk mencegah memory leak. Tanpa destructor, ketika objek linked list dihapus, node-node yang dialokasikan dengan `new` tidak akan otomatis dihapus, menyebabkan kebocoran memori.

### Problem S5 ⭐⭐⭐
Berapa kompleksitas waktu untuk mengakses elemen ke-n dalam linked list dibandingkan array?

**Jawaban:** 
- Array: O(1) - akses langsung dengan index
- Linked List: O(n) - harus traversal dari head

---

## Ringkasan

| Konsep | Penjelasan | Kompleksitas |
|--------|------------|--------------|
| **Linked List** | Struktur data linear dengan node yang terhubung melalui pointer | - |
| **Node** | Unit dasar: data + pointer next | - |
| **Head** | Pointer ke node pertama | - |
| **Tail** | Pointer ke node terakhir (opsional) | - |
| **Traversal** | Mengunjungi semua node dari head ke tail | O(n) |
| **Search** | Mencari nilai dalam list | O(n) |
| **Insert Beginning** | Menambah di awal | O(1) |
| **Insert End** | Menambah di akhir | O(n) / O(1) dengan tail |
| **Insert Position** | Menambah di posisi tertentu | O(n) |
| **Delete Beginning** | Menghapus di awal | O(1) |
| **Delete End** | Menghapus di akhir | O(n) |
| **Delete Position** | Menghapus di posisi tertentu | O(n) |

**Keunggulan Linked List:**
- Ukuran dinamis
- Insert/delete di awal sangat efisien O(1)
- Tidak ada pemborosan memori

**Kelemahan Linked List:**
- Tidak ada random access (harus traversal)
- Memory overhead untuk pointer
- Cache performance kurang optimal

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 10.2.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 3.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 7.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
