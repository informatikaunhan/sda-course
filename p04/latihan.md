# Latihan Mandiri 04: Double dan Circular Linked List

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 04  
**Topik:** Double Linked List dan Circular Linked List  
**Waktu:** 150 menit  
**Sifat:** Open Book

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal secara mandiri
2. Untuk soal pilihan ganda, pilih **satu jawaban yang paling tepat**
3. Untuk soal uraian, tuliskan jawaban dengan lengkap beserta penjelasan
4. Untuk soal pemrograman, tuliskan kode C++ yang dapat dikompilasi
5. Kumpulkan jawaban sesuai format yang ditentukan

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

### Soal 1
Berapa banyak pointer yang dimiliki setiap node pada Double Linked List?

A. 1 pointer  
B. 2 pointer  
C. 3 pointer  
D. 4 pointer  
E. Tergantung implementasi

---

### Soal 2
Apa keuntungan utama Double Linked List dibandingkan Single Linked List?

A. Menggunakan lebih sedikit memori  
B. Insert di depan lebih cepat  
C. Dapat melakukan traversal dua arah  
D. Tidak memerlukan alokasi dinamis  
E. Lebih mudah diimplementasikan

---

### Soal 3
Pada Double Linked List dengan head dan tail pointer, kompleksitas waktu untuk operasi `deleteBack()` adalah:

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)

---

### Soal 4
Dalam Circular Linked List, node terakhir menunjuk ke:

A. NULL  
B. Node pertama (head)  
C. Node tengah  
D. Dirinya sendiri  
E. Node sebelumnya

---

### Soal 5
Mengapa pada Single Circular Linked List lebih disarankan menyimpan pointer ke `tail` daripada `head`?

A. Karena tail lebih mudah diakses  
B. Karena dengan tail, head dapat diakses via tail->next  
C. Karena tail menggunakan lebih sedikit memori  
D. Karena tail tidak berubah  
E. Tidak ada perbedaan

---

### Soal 6
Apa kondisi untuk menghentikan traversal pada Circular Linked List?

A. `current != nullptr`  
B. `current->next != nullptr`  
C. `current != startNode` (kembali ke node awal)  
D. `size == 0`  
E. `current == tail`

---

### Soal 7
Sentinel node pada linked list berfungsi untuk:

A. Menyimpan data tambahan  
B. Menghitung jumlah node  
C. Menyederhanakan penanganan edge cases  
D. Mempercepat pencarian  
E. Menghemat memori

---

### Soal 8
Pada Double Linked List, jika kita sudah memiliki pointer ke node yang ingin dihapus, kompleksitas operasi delete adalah:

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)

---

### Soal 9
Manakah aplikasi yang paling cocok menggunakan Circular Linked List?

A. Implementasi stack  
B. Penyimpanan data terurut  
C. Round-robin scheduling  
D. Binary search  
E. Sorting data

---

### Soal 10
Untuk mengimplementasikan fitur "undo/redo" pada text editor, linked list jenis apa yang paling tepat?

A. Single Linked List  
B. Double Linked List  
C. Single Circular Linked List  
D. Array  
E. Binary Tree

---

### Soal 11
Pada Double Circular Linked List dengan head pointer, bagaimana cara mengakses tail?

A. `head->next`  
B. `head->prev`  
C. Traversal dari head sampai akhir  
D. Tidak bisa diakses  
E. `head->tail`

---

### Soal 12
Berapa memori tambahan (overhead) per node pada Double Linked List dibandingkan Single Linked List?

A. 0 (sama)  
B. 1 pointer  
C. 2 pointer  
D. 3 pointer  
E. Tergantung tipe data

---

### Soal 13
Dalam algoritma Floyd's Cycle Detection, dua pointer bergerak dengan kecepatan:

A. Sama cepat  
B. Slow 1 langkah, Fast 2 langkah  
C. Slow 2 langkah, Fast 1 langkah  
D. Keduanya 2 langkah  
E. Random

---

### Soal 14
Apa yang terjadi jika kita mencoba traversal Circular Linked List menggunakan kondisi `while(current != nullptr)`?

A. Traversal berjalan normal  
B. Traversal berhenti di tengah  
C. Infinite loop  
D. Error kompilasi  
E. Hanya mengunjungi satu node

---

### Soal 15
Pada Double Linked List dengan sentinel nodes, berapa minimal jumlah node yang selalu ada di list (termasuk sentinel)?

A. 0  
B. 1  
C. 2  
D. 3  
E. Tergantung data

---

### Soal 16
Manakah pernyataan yang BENAR tentang Double Circular Linked List?

A. Tidak ada NULL pointer  
B. Head->prev adalah NULL  
C. Tail->next adalah NULL  
D. Memerlukan traversal O(n) untuk akses tail  
E. Hanya bisa insert di depan

---

### Soal 17
Untuk playlist musik yang bisa loop, skip, dan previous, linked list jenis apa yang paling tepat?

A. Single Linked List  
B. Double Linked List  
C. Single Circular Linked List  
D. Double Circular Linked List  
E. Array

---

### Soal 18
Kompleksitas waktu operasi `insertAt(position)` pada Double Linked List adalah:

A. O(1)  
B. O(log n)  
C. O(n/2) ≈ O(n)  
D. O(n²)  
E. O(2^n)

---

### Soal 19
Apa keunggulan DLL dengan traversal dari kedua arah pada operasi `insertAt()`?

A. Tidak ada keunggulan  
B. Rata-rata hanya perlu traversal n/2 node  
C. Selalu O(1)  
D. Tidak perlu validasi posisi  
E. Tidak perlu alokasi memori

---

### Soal 20
Pada sistem rotasi penjagaan 4 shift yang berputar terus 24/7, struktur data apa yang paling tepat?

A. Array  
B. Single Linked List  
C. Stack  
D. Double Circular Linked List  
E. Queue

---

## Bagian B: Soal Uraian (15 Soal)

### Soal 1 (Mudah)
Jelaskan perbedaan utama antara Single Linked List dan Double Linked List dalam hal:
a) Struktur node
b) Kemampuan traversal
c) Operasi delete di akhir list

---

### Soal 2 (Mudah)
Gambarkan ilustrasi proses insert node dengan nilai 25 di tengah Double Linked List berikut (antara 20 dan 30):
```
NULL <- [10] <-> [20] <-> [30] <-> [40] -> NULL
```
Tunjukkan perubahan pointer yang terjadi.

---

### Soal 3 (Mudah)
Tuliskan kode C++ untuk fungsi `displayBackward()` pada Double Linked List yang menampilkan isi list dari belakang ke depan.

---

### Soal 4 (Sedang)
Implementasikan fungsi `insertAt(int value, int position)` untuk Double Linked List yang:
- Menyisipkan node pada posisi tertentu
- Memanfaatkan traversal dua arah untuk efisiensi
- Menangani semua edge cases (posisi tidak valid, list kosong, dll.)

---

### Soal 5 (Mudah)
Jelaskan mengapa pada Circular Linked List disarankan menggunakan `do-while` loop untuk traversal daripada `while` loop biasa. Berikan contoh kode untuk kedua kasus.

---

### Soal 6 (Sedang)
Implementasikan fungsi `deleteValue(int value)` untuk Single Circular Linked List yang menghapus node pertama yang memiliki nilai tertentu.

---

### Soal 7 (Mudah)
Apa yang dimaksud dengan Sentinel Node? Jelaskan keuntungannya dalam implementasi Double Linked List dengan memberikan contoh konkret.

---

### Soal 8 (Sulit)
Implementasikan class `DoublyCircularLinkedList` lengkap dengan operasi:
- `insertFront(int value)`
- `insertBack(int value)`
- `deleteFront()`
- `deleteBack()`
- `display()`

---

### Soal 9 (Mudah)
Jelaskan algoritma Floyd's Cycle Detection (Tortoise and Hare) untuk mendeteksi cycle dalam linked list. Mengapa algoritma ini efisien?

---

### Soal 10 (Mudah)
Bandingkan penggunaan memori antara:
- Array dengan 100 elemen integer
- Double Linked List dengan 100 node integer

Asumsikan sizeof(int) = 4 bytes dan sizeof(pointer) = 8 bytes.

---

### Soal 11 (Sedang)
Implementasikan fungsi `reverse()` untuk membalik Double Linked List secara in-place (tanpa membuat list baru).

---

### Soal 12 (Sulit)
Implementasikan fungsi `merge(CircularLinkedList& other)` untuk menggabungkan dua Single Circular Linked List menjadi satu.

---

### Soal 13 (Mudah)
Dalam konteks pertahanan, berikan 3 contoh aplikasi yang cocok menggunakan:
a) Double Linked List
b) Circular Linked List

---

### Soal 14 (Sedang)
Implementasikan destructor untuk Double Circular Linked List yang dengan benar membebaskan semua memori tanpa menyebabkan infinite loop atau memory leak.

---

### Soal 15 (Mudah)
Jelaskan kriteria pemilihan antara Single LL, Double LL, Circular LL, dan Double Circular LL. Kapan sebaiknya menggunakan masing-masing jenis?

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Rotasi Penjagaan Pos Militer (50 poin)

**Latar Belakang:**
Sebuah pos militer memerlukan sistem rotasi penjagaan 24 jam dengan 4 shift:
- Shift 1: 00:00 - 06:00
- Shift 2: 06:00 - 12:00
- Shift 3: 12:00 - 18:00
- Shift 4: 18:00 - 24:00

Setiap shift memiliki informasi: nama personel, pangkat, dan status (aktif/cadangan).

**Tugas:**

1. **(15 poin)** Tentukan struktur data yang paling tepat dan jelaskan alasannya.

2. **(20 poin)** Implementasikan class `DutyRoster` dengan fitur:
   - Menambah personel ke shift tertentu
   - Menghapus personel dari shift
   - Menampilkan jadwal shift saat ini
   - Pindah ke shift berikutnya/sebelumnya
   - Mencari personel berdasarkan nama

3. **(10 poin)** Implementasikan fungsi untuk mencetak laporan rotasi 24 jam penuh.

4. **(5 poin)** Analisis kompleksitas waktu untuk setiap operasi.

---

### Studi Kasus 2: Sistem Navigasi Waypoint Drone Militer (50 poin)

**Latar Belakang:**
Drone militer untuk misi pengintaian perlu menyimpan daftar waypoint (titik koordinat) yang harus dikunjungi. Drone harus bisa:
- Terbang ke waypoint berikutnya atau sebelumnya
- Kembali ke waypoint awal kapan saja
- Menambah/menghapus waypoint di tengah perjalanan
- Mode patrol: mengulang rute secara terus-menerus

**Struktur Waypoint:**
```cpp
struct Waypoint {
    int id;
    double latitude;
    double longitude;
    double altitude;
    string description;  // Misal: "Titik observasi A"
};
```

**Tugas:**

1. **(10 poin)** Tentukan struktur data yang paling tepat dan jelaskan alasannya.

2. **(25 poin)** Implementasikan class `DroneNavigation` dengan fitur:
   - `addWaypoint(Waypoint wp)` - menambah waypoint di akhir rute
   - `insertWaypoint(Waypoint wp, int position)` - menyisipkan waypoint
   - `removeCurrentWaypoint()` - menghapus waypoint saat ini
   - `nextWaypoint()` - pindah ke waypoint berikutnya
   - `previousWaypoint()` - kembali ke waypoint sebelumnya
   - `returnToBase()` - kembali ke waypoint pertama
   - `togglePatrolMode()` - aktifkan/nonaktifkan mode patrol (circular)
   - `displayRoute()` - tampilkan seluruh rute

3. **(10 poin)** Implementasikan fungsi `calculateTotalDistance()` yang menghitung estimasi jarak total rute.

4. **(5 poin)** Bagaimana sistem menangani jika drone kehilangan koneksi di tengah misi? Berikan rekomendasi fitur fail-safe.

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan |
|----|---------|------------|
| 1 | B | Setiap node DLL memiliki 2 pointer: prev dan next |
| 2 | C | DLL memungkinkan traversal bidirectional (maju dan mundur) |
| 3 | A | Dengan tail pointer, deleteBack() hanya O(1) karena langsung akses node terakhir dan prev-nya |
| 4 | B | Pada Circular LL, node terakhir menunjuk kembali ke head (node pertama) |
| 5 | B | Dengan tail, head = tail->next, sehingga insert di depan dan belakang keduanya O(1) |
| 6 | C | Pada Circular LL, traversal berhenti saat current kembali ke node awal |
| 7 | C | Sentinel node adalah dummy node yang menyederhanakan penanganan edge cases |
| 8 | A | Dengan pointer ke node dan akses ke prev/next, delete dapat dilakukan O(1) |
| 9 | C | Round-robin scheduling memerlukan rotasi berputar yang cocok dengan Circular LL |
| 10 | B | Undo/redo memerlukan traversal dua arah (mundur untuk undo, maju untuk redo) |
| 11 | B | Pada Double Circular LL, tail = head->prev |
| 12 | B | DLL memerlukan 1 pointer tambahan (prev) per node dibanding SLL |
| 13 | B | Floyd's algorithm: slow bergerak 1 langkah, fast bergerak 2 langkah |
| 14 | C | Karena tidak ada NULL di Circular LL, while(current != nullptr) akan infinite loop |
| 15 | C | Minimal ada 2 sentinel node (head dan tail sentinel) |
| 16 | A | Pada Double Circular LL, semua pointer terhubung (tidak ada NULL) |
| 17 | D | Playlist dengan loop, skip, dan previous memerlukan Double Circular LL |
| 18 | C | Worst case perlu traversal sampai posisi, rata-rata n/2, sehingga O(n) |
| 19 | B | DLL dapat traversal dari depan atau belakang, rata-rata hanya n/2 node |
| 20 | D | Rotasi 4 shift yang berputar terus cocok dengan Double Circular LL |

---

### Bagian B: Uraian

#### Jawaban Soal 1
**Jawaban:**

a) **Struktur Node:**
- SLL: data + next (2 field)
- DLL: data + prev + next (3 field)

b) **Kemampuan Traversal:**
- SLL: Hanya forward (dari head ke tail)
- DLL: Bidirectional (forward dan backward)

c) **Operasi Delete di Akhir:**
- SLL: O(n) karena harus traversal untuk mencari node sebelum tail
- DLL: O(1) karena langsung akses tail->prev

---

#### Jawaban Soal 2
**Jawaban:**

![Proses Insert Node 25 di Tengah Double Linked List](images/p04-09-dll-insert-middle.png)

*Gambar: Ilustrasi proses insert node [25] di antara node [20] dan [30] pada Double Linked List*


**Penjelasan langkah-langkah:**

| Langkah | Operasi | Keterangan |
|---------|---------|------------|
| 1 | Buat node baru [25] | Alokasi memori untuk node baru |
| 2 | `newNode->next = node30` | Node 25 menunjuk ke node 30 |
| 3 | `newNode->prev = node20` | Node 25 menunjuk balik ke node 20 |
| 4 | `node20->next = newNode` | Node 20 sekarang menunjuk ke node 25 |
| 5 | `node30->prev = newNode` | Node 30 sekarang menunjuk balik ke node 25 |

**Hasil akhir:** Double Linked List dengan 5 node: `NULL ← [10] ↔ [20] ↔ [25] ↔ [30] ↔ [40] → NULL`

---

#### Jawaban Soal 3
**Jawaban:**

```cpp
void DoublyLinkedList::displayBackward() {
    if (tail == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    cout << "Backward: ";
    Node* current = tail;
    while (current != nullptr) {
        cout << current->data;
        if (current->prev != nullptr) {
            cout << " <- ";
        }
        current = current->prev;
    }
    cout << endl;
}
```

---

#### Jawaban Soal 4
**Jawaban:**

```cpp
void DoublyLinkedList::insertAt(int value, int position) {
    // Validasi posisi
    if (position < 0 || position > size) {
        cout << "Posisi tidak valid!" << endl;
        return;
    }
    
    // Edge cases
    if (position == 0) {
        insertFront(value);
        return;
    }
    if (position == size) {
        insertBack(value);
        return;
    }
    
    Node* newNode = new Node(value);
    Node* current;
    
    // Pilih arah traversal yang optimal
    if (position <= size / 2) {
        // Dari depan
        current = head;
        for (int i = 0; i < position; i++) {
            current = current->next;
        }
    } else {
        // Dari belakang (keuntungan DLL)
        current = tail;
        for (int i = size - 1; i > position; i--) {
            current = current->prev;
        }
    }
    
    // Insert sebelum current
    newNode->next = current;
    newNode->prev = current->prev;
    current->prev->next = newNode;
    current->prev = newNode;
    
    size++;
}
```

---

#### Jawaban Soal 5
**Jawaban:**

**Alasan menggunakan do-while:**

Pada Circular Linked List, tidak ada NULL yang bisa dijadikan kondisi berhenti. Jika menggunakan `while(current != start)`, loop tidak akan pernah masuk karena kondisi langsung false di awal (current sudah sama dengan start).

**Contoh dengan while (SALAH):**
```cpp
// SALAH - tidak akan pernah masuk loop
Node* current = start;
while (current != start) {  // Kondisi false dari awal!
    cout << current->data << " ";
    current = current->next;
}
```

**Contoh dengan do-while (BENAR):**
```cpp
// BENAR - setidaknya eksekusi sekali
Node* current = start;
do {
    cout << current->data << " ";
    current = current->next;
} while (current != start);  // Cek setelah iterasi pertama
```

---

#### Jawaban Soal 6
**Jawaban:**

```cpp
void CircularLinkedList::deleteValue(int value) {
    if (tail == nullptr) {
        cout << "List kosong!" << endl;
        return;
    }
    
    Node* current = tail->next;  // head
    Node* prev = tail;
    
    // Cari node dengan nilai yang dicari
    do {
        if (current->data == value) {
            // Kasus hanya satu node
            if (current == tail && current->next == tail) {
                delete current;
                tail = nullptr;
            }
            // Kasus node yang dihapus adalah tail
            else if (current == tail) {
                prev->next = current->next;
                tail = prev;
                delete current;
            }
            // Kasus node biasa
            else {
                prev->next = current->next;
                delete current;
            }
            size--;
            return;
        }
        prev = current;
        current = current->next;
    } while (current != tail->next);
    
    cout << "Nilai " << value << " tidak ditemukan!" << endl;
}
```

---

#### Jawaban Soal 7
**Jawaban:**

**Sentinel Node** adalah node khusus (dummy) yang tidak menyimpan data aktual, tetapi digunakan untuk menyederhanakan implementasi.

**Keuntungan:**
1. Menghilangkan pengecekan khusus untuk list kosong
2. Menghilangkan pengecekan khusus untuk operasi di head/tail
3. Menyederhanakan kode dan mengurangi bug

**Contoh Konkret:**

Tanpa Sentinel:
```cpp
void deleteNode(Node* node) {
    if (node == nullptr) return;
    
    // Harus cek apakah node adalah head
    if (node == head) {
        head = head->next;
        if (head) head->prev = nullptr;
    }
    // Harus cek apakah node adalah tail
    else if (node == tail) {
        tail = tail->prev;
        if (tail) tail->next = nullptr;
    }
    // Baru kasus normal
    else {
        node->prev->next = node->next;
        node->next->prev = node->prev;
    }
    delete node;
}
```

Dengan Sentinel:
```cpp
void deleteNode(Node* node) {
    // Tidak perlu cek apakah head/tail
    // Karena sentinel menjamin prev dan next selalu valid
    node->prev->next = node->next;
    node->next->prev = node->prev;
    delete node;
}
```

---

#### Jawaban Soal 8
**Jawaban:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* prev;
    Node* next;
    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

class DoublyCircularLinkedList {
private:
    Node* head;
    int size;
    
public:
    DoublyCircularLinkedList() : head(nullptr), size(0) {}
    
    void insertFront(int value) {
        Node* newNode = new Node(value);
        
        if (head == nullptr) {
            head = newNode;
            newNode->next = newNode;
            newNode->prev = newNode;
        } else {
            Node* tail = head->prev;
            newNode->next = head;
            newNode->prev = tail;
            head->prev = newNode;
            tail->next = newNode;
            head = newNode;
        }
        size++;
    }
    
    void insertBack(int value) {
        if (head == nullptr) {
            insertFront(value);
            return;
        }
        
        Node* newNode = new Node(value);
        Node* tail = head->prev;
        
        newNode->next = head;
        newNode->prev = tail;
        tail->next = newNode;
        head->prev = newNode;
        
        size++;
    }
    
    void deleteFront() {
        if (head == nullptr) {
            cout << "List kosong!" << endl;
            return;
        }
        
        if (head->next == head) {  // Satu node
            delete head;
            head = nullptr;
        } else {
            Node* tail = head->prev;
            Node* newHead = head->next;
            tail->next = newHead;
            newHead->prev = tail;
            delete head;
            head = newHead;
        }
        size--;
    }
    
    void deleteBack() {
        if (head == nullptr) {
            cout << "List kosong!" << endl;
            return;
        }
        
        if (head->next == head) {  // Satu node
            delete head;
            head = nullptr;
        } else {
            Node* tail = head->prev;
            Node* newTail = tail->prev;
            newTail->next = head;
            head->prev = newTail;
            delete tail;
        }
        size--;
    }
    
    void display() {
        if (head == nullptr) {
            cout << "List kosong!" << endl;
            return;
        }
        
        cout << "Double Circular List: ";
        Node* current = head;
        do {
            cout << current->data;
            current = current->next;
            if (current != head) cout << " <-> ";
        } while (current != head);
        cout << " <-> (back to " << head->data << ")" << endl;
    }
};
```

---

#### Jawaban Soal 9
**Jawaban:**

**Algoritma Floyd's Cycle Detection (Tortoise and Hare):**

1. Gunakan dua pointer: slow (tortoise) dan fast (hare)
2. Slow bergerak 1 langkah per iterasi
3. Fast bergerak 2 langkah per iterasi
4. Jika ada cycle, fast akan "mengejar" slow dari belakang dan mereka akan bertemu
5. Jika tidak ada cycle, fast akan mencapai NULL

**Mengapa Efisien:**
- **Time Complexity:** O(n) - dalam worst case, slow traversal semua node sekali
- **Space Complexity:** O(1) - hanya menggunakan 2 pointer, tidak perlu struktur data tambahan
- Dibandingkan dengan metode hash set yang memerlukan O(n) space

---

#### Jawaban Soal 10
**Jawaban:**

**Array:**
- Data: 100 × 4 bytes = 400 bytes
- Overhead array (size, capacity): ≈ 16 bytes
- **Total: ≈ 416 bytes**

**Double Linked List:**
- Setiap node: 4 (data) + 8 (prev) + 8 (next) = 20 bytes
- 100 node: 100 × 20 = 2000 bytes
- Head & tail pointer: 2 × 8 = 16 bytes
- **Total: ≈ 2016 bytes**

**Kesimpulan:** DLL menggunakan sekitar 4.8x lebih banyak memori dibanding array untuk data yang sama. Trade-off ini diimbangi dengan fleksibilitas operasi insert/delete.

---

#### Jawaban Soal 11
**Jawaban:**

```cpp
void DoublyLinkedList::reverse() {
    if (head == nullptr || head == tail) return;
    
    Node* current = head;
    Node* temp = nullptr;
    
    // Tukar prev dan next untuk setiap node
    while (current != nullptr) {
        temp = current->prev;
        current->prev = current->next;
        current->next = temp;
        current = current->prev;  // Maju ke "next" yang sekarang adalah prev
    }
    
    // Tukar head dan tail
    temp = head;
    head = tail;
    tail = temp;
}
```

---

#### Jawaban Soal 12
**Jawaban:**

```cpp
void CircularLinkedList::merge(CircularLinkedList& other) {
    if (other.tail == nullptr) return;
    if (this->tail == nullptr) {
        this->tail = other.tail;
        this->size = other.size;
        other.tail = nullptr;
        other.size = 0;
        return;
    }
    
    // Simpan head kedua list
    Node* head1 = this->tail->next;
    Node* head2 = other.tail->next;
    
    // Hubungkan: tail1 -> head2 dan tail2 -> head1
    this->tail->next = head2;
    other.tail->next = head1;
    
    // Update tail list pertama
    this->tail = other.tail;
    this->size += other.size;
    
    // Kosongkan list kedua
    other.tail = nullptr;
    other.size = 0;
}
```

---

#### Jawaban Soal 13
**Jawaban:**

**a) Double Linked List:**
1. **Browser History Sistem Komando** - Navigasi maju/mundur halaman informasi taktis
2. **Undo/Redo Dokumen Operasi** - Membatalkan atau mengulangi perubahan rencana operasi
3. **Navigasi Peta Digital** - Berpindah antar waypoint yang sudah dikunjungi

**b) Circular Linked List:**
1. **Rotasi Penjagaan** - Jadwal shift yang berputar 24/7
2. **Radar Sweep** - Pemindaian 360° yang berputar terus-menerus
3. **Token Passing dalam Jaringan Taktis** - Protokol komunikasi bergilir antar unit

---

#### Jawaban Soal 14
**Jawaban:**

```cpp
DoublyCircularLinkedList::~DoublyCircularLinkedList() {
    if (head == nullptr) return;
    
    // Metode 1: Putuskan circle dulu
    Node* tail = head->prev;
    tail->next = nullptr;  // Putuskan koneksi circular
    
    Node* current = head;
    while (current != nullptr) {
        Node* next = current->next;
        delete current;
        current = next;
    }
    
    head = nullptr;
    size = 0;
    
    // Alternatif Metode 2: Gunakan counter
    /*
    Node* current = head;
    for (int i = 0; i < size; i++) {
        Node* next = current->next;
        delete current;
        current = next;
    }
    head = nullptr;
    size = 0;
    */
}
```

---

#### Jawaban Soal 15
**Jawaban:**

| Jenis | Kapan Digunakan |
|-------|-----------------|
| **Single LL** | Memori terbatas, hanya perlu traversal forward, implementasi sederhana (stack, queue sederhana) |
| **Double LL** | Perlu traversal dua arah, operasi delete cepat jika pointer sudah diketahui, undo/redo |
| **Circular LL** | Data berputar, round-robin, tidak perlu cek NULL, buffer circular |
| **Double Circular LL** | Kombinasi kebutuhan di atas: playlist dengan loop+skip+previous, rotasi dengan akses dua arah |

**Kriteria Pemilihan:**
1. Apakah perlu traversal backward? → DLL
2. Apakah data berputar/cyclic? → Circular
3. Apakah memori sangat terbatas? → SLL
4. Apakah perlu O(1) delete jika pointer diketahui? → DLL

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Rotasi Penjagaan

**1. Struktur Data yang Tepat: Double Circular Linked List**

**Alasan:**
- **Circular** karena rotasi shift berputar terus (setelah shift 4, kembali ke shift 1)
- **Double** karena supervisor perlu melihat shift sebelumnya dan sesudahnya untuk koordinasi serah terima

**2. Implementasi:**

```cpp
#include <iostream>
#include <string>
using namespace std;

struct Personel {
    string nama;
    string pangkat;
    bool aktif;  // true = aktif, false = cadangan
};

struct ShiftNode {
    int shiftNumber;
    string waktu;
    Personel* personelList;
    int jumlahPersonel;
    int kapasitas;
    ShiftNode* prev;
    ShiftNode* next;
    
    ShiftNode(int num, string time, int cap = 5) 
        : shiftNumber(num), waktu(time), kapasitas(cap),
          jumlahPersonel(0), prev(nullptr), next(nullptr) {
        personelList = new Personel[kapasitas];
    }
};

class DutyRoster {
private:
    ShiftNode* currentShift;
    int totalShift;
    
public:
    DutyRoster() : currentShift(nullptr), totalShift(0) {
        // Inisialisasi 4 shift
        initializeShifts();
    }
    
    void initializeShifts() {
        ShiftNode* shift1 = new ShiftNode(1, "00:00-06:00");
        ShiftNode* shift2 = new ShiftNode(2, "06:00-12:00");
        ShiftNode* shift3 = new ShiftNode(3, "12:00-18:00");
        ShiftNode* shift4 = new ShiftNode(4, "18:00-24:00");
        
        // Hubungkan circular
        shift1->next = shift2; shift2->prev = shift1;
        shift2->next = shift3; shift3->prev = shift2;
        shift3->next = shift4; shift4->prev = shift3;
        shift4->next = shift1; shift1->prev = shift4;
        
        currentShift = shift1;
        totalShift = 4;
    }
    
    void addPersonel(int shiftNum, string nama, string pangkat, bool aktif = true) {
        ShiftNode* shift = findShift(shiftNum);
        if (shift == nullptr) {
            cout << "Shift tidak ditemukan!" << endl;
            return;
        }
        
        if (shift->jumlahPersonel >= shift->kapasitas) {
            cout << "Shift penuh!" << endl;
            return;
        }
        
        Personel& p = shift->personelList[shift->jumlahPersonel++];
        p.nama = nama;
        p.pangkat = pangkat;
        p.aktif = aktif;
        
        cout << "Siap! " << pangkat << " " << nama 
             << " ditambahkan ke Shift " << shiftNum << endl;
    }
    
    ShiftNode* findShift(int shiftNum) {
        ShiftNode* temp = currentShift;
        do {
            if (temp->shiftNumber == shiftNum) return temp;
            temp = temp->next;
        } while (temp != currentShift);
        return nullptr;
    }
    
    Personel* findPersonel(string nama) {
        ShiftNode* temp = currentShift;
        do {
            for (int i = 0; i < temp->jumlahPersonel; i++) {
                if (temp->personelList[i].nama == nama) {
                    cout << "Ditemukan di Shift " << temp->shiftNumber << endl;
                    return &temp->personelList[i];
                }
            }
            temp = temp->next;
        } while (temp != currentShift);
        return nullptr;
    }
    
    void nextShift() {
        currentShift = currentShift->next;
        cout << "Beralih ke Shift " << currentShift->shiftNumber 
             << " (" << currentShift->waktu << ")" << endl;
    }
    
    void previousShift() {
        currentShift = currentShift->prev;
        cout << "Kembali ke Shift " << currentShift->shiftNumber 
             << " (" << currentShift->waktu << ")" << endl;
    }
    
    void displayCurrentShift() {
        cout << "\n=== SHIFT " << currentShift->shiftNumber 
             << " (" << currentShift->waktu << ") ===" << endl;
        
        for (int i = 0; i < currentShift->jumlahPersonel; i++) {
            Personel& p = currentShift->personelList[i];
            cout << "- " << p.pangkat << " " << p.nama 
                 << " [" << (p.aktif ? "AKTIF" : "CADANGAN") << "]" << endl;
        }
        
        if (currentShift->jumlahPersonel == 0) {
            cout << "(Belum ada personel)" << endl;
        }
    }
    
    void printFullRotation() {
        cout << "\n========== LAPORAN ROTASI 24 JAM ==========" << endl;
        ShiftNode* temp = currentShift;
        do {
            cout << "\nShift " << temp->shiftNumber 
                 << " (" << temp->waktu << "):" << endl;
            for (int i = 0; i < temp->jumlahPersonel; i++) {
                Personel& p = temp->personelList[i];
                cout << "  " << p.pangkat << " " << p.nama << endl;
            }
            temp = temp->next;
        } while (temp != currentShift);
        cout << "==========================================\n" << endl;
    }
};
```

**3. Laporan Rotasi:**
Fungsi `printFullRotation()` sudah diimplementasikan di atas.

**4. Analisis Kompleksitas:**

| Operasi | Kompleksitas |
|---------|-------------|
| addPersonel | O(1) untuk akses shift, O(k) untuk cari shift k |
| findPersonel | O(n×m) worst case (n shift, m personel per shift) |
| nextShift | O(1) |
| previousShift | O(1) |
| displayCurrentShift | O(m) dimana m = jumlah personel di shift |
| printFullRotation | O(n×m) |

---

#### Studi Kasus 2: Sistem Navigasi Drone

**1. Struktur Data: Double Circular Linked List (dengan mode toggle)**

**Alasan:**
- Perlu traversal dua arah (next/previous waypoint)
- Mode patrol memerlukan circular
- Insert/delete di tengah perjalanan memerlukan O(1) jika pointer diketahui

**2. Implementasi:**

```cpp
#include <iostream>
#include <string>
#include <cmath>
using namespace std;

struct Waypoint {
    int id;
    double latitude;
    double longitude;
    double altitude;
    string description;
};

struct WaypointNode {
    Waypoint data;
    WaypointNode* prev;
    WaypointNode* next;
    
    WaypointNode(Waypoint wp) : data(wp), prev(nullptr), next(nullptr) {}
};

class DroneNavigation {
private:
    WaypointNode* head;
    WaypointNode* current;
    int size;
    bool patrolMode;
    
public:
    DroneNavigation() : head(nullptr), current(nullptr), 
                        size(0), patrolMode(false) {}
    
    void addWaypoint(Waypoint wp) {
        WaypointNode* newNode = new WaypointNode(wp);
        
        if (head == nullptr) {
            head = current = newNode;
            if (patrolMode) {
                newNode->next = newNode;
                newNode->prev = newNode;
            }
        } else {
            if (patrolMode) {
                // Circular mode
                WaypointNode* tail = head->prev;
                newNode->next = head;
                newNode->prev = tail;
                tail->next = newNode;
                head->prev = newNode;
            } else {
                // Linear mode
                WaypointNode* temp = head;
                while (temp->next != nullptr && temp->next != head) {
                    temp = temp->next;
                }
                temp->next = newNode;
                newNode->prev = temp;
            }
        }
        size++;
        cout << "Waypoint " << wp.id << " ditambahkan: " << wp.description << endl;
    }
    
    void insertWaypoint(Waypoint wp, int position) {
        if (position < 0 || position > size) {
            cout << "Posisi tidak valid!" << endl;
            return;
        }
        
        if (position == 0) {
            WaypointNode* newNode = new WaypointNode(wp);
            if (head == nullptr) {
                head = current = newNode;
            } else {
                newNode->next = head;
                head->prev = newNode;
                head = newNode;
            }
            size++;
            return;
        }
        
        WaypointNode* temp = head;
        for (int i = 0; i < position - 1; i++) {
            temp = temp->next;
        }
        
        WaypointNode* newNode = new WaypointNode(wp);
        newNode->next = temp->next;
        newNode->prev = temp;
        if (temp->next) temp->next->prev = newNode;
        temp->next = newNode;
        size++;
    }
    
    void removeCurrentWaypoint() {
        if (current == nullptr) {
            cout << "Tidak ada waypoint!" << endl;
            return;
        }
        
        cout << "Menghapus waypoint: " << current->data.description << endl;
        
        if (size == 1) {
            delete current;
            head = current = nullptr;
        } else {
            WaypointNode* toDelete = current;
            
            if (current == head) {
                head = head->next;
            }
            
            if (current->prev) current->prev->next = current->next;
            if (current->next) current->next->prev = current->prev;
            
            current = current->next ? current->next : head;
            delete toDelete;
        }
        size--;
    }
    
    void nextWaypoint() {
        if (current == nullptr) {
            cout << "Tidak ada waypoint!" << endl;
            return;
        }
        
        if (!patrolMode && current->next == nullptr) {
            cout << "Sudah di waypoint terakhir!" << endl;
            return;
        }
        
        current = current->next;
        cout << "Moving to: " << current->data.description << endl;
        displayCurrentPosition();
    }
    
    void previousWaypoint() {
        if (current == nullptr) {
            cout << "Tidak ada waypoint!" << endl;
            return;
        }
        
        if (!patrolMode && current == head) {
            cout << "Sudah di waypoint pertama!" << endl;
            return;
        }
        
        current = current->prev;
        cout << "Returning to: " << current->data.description << endl;
        displayCurrentPosition();
    }
    
    void returnToBase() {
        if (head == nullptr) {
            cout << "Tidak ada waypoint!" << endl;
            return;
        }
        current = head;
        cout << "Returning to base..." << endl;
        displayCurrentPosition();
    }
    
    void togglePatrolMode() {
        patrolMode = !patrolMode;
        
        if (head == nullptr) {
            cout << "Patrol mode: " << (patrolMode ? "ON" : "OFF") << endl;
            return;
        }
        
        if (patrolMode) {
            // Convert to circular
            WaypointNode* tail = head;
            while (tail->next != nullptr) {
                tail = tail->next;
            }
            tail->next = head;
            head->prev = tail;
        } else {
            // Convert to linear
            WaypointNode* tail = head->prev;
            tail->next = nullptr;
            head->prev = nullptr;
        }
        
        cout << "Patrol mode: " << (patrolMode ? "ON" : "OFF") << endl;
    }
    
    void displayCurrentPosition() {
        if (current == nullptr) return;
        cout << "Current: [" << current->data.id << "] " 
             << current->data.description 
             << " (" << current->data.latitude << ", " 
             << current->data.longitude << ", " 
             << current->data.altitude << "m)" << endl;
    }
    
    void displayRoute() {
        if (head == nullptr) {
            cout << "Route kosong!" << endl;
            return;
        }
        
        cout << "\n=== DRONE ROUTE ===" << endl;
        cout << "Mode: " << (patrolMode ? "PATROL (Loop)" : "LINEAR") << endl;
        cout << "Total waypoints: " << size << endl;
        
        WaypointNode* temp = head;
        int visited = 0;
        
        while (visited < size) {
            cout << (temp == current ? ">>> " : "    ");
            cout << "[" << temp->data.id << "] " << temp->data.description;
            cout << " (" << temp->data.latitude << ", " 
                 << temp->data.longitude << ")" << endl;
            temp = temp->next;
            visited++;
        }
        
        if (patrolMode) {
            cout << "    -> (loop back to start)" << endl;
        }
        cout << "==================\n" << endl;
    }
    
    double calculateDistance(Waypoint& a, Waypoint& b) {
        // Simplified distance calculation (not actual GPS distance)
        double dlat = b.latitude - a.latitude;
        double dlon = b.longitude - a.longitude;
        double dalt = b.altitude - a.altitude;
        return sqrt(dlat*dlat + dlon*dlon + dalt*dalt) * 111;  // km approximation
    }
    
    double calculateTotalDistance() {
        if (head == nullptr || size < 2) return 0;
        
        double total = 0;
        WaypointNode* temp = head;
        
        for (int i = 0; i < size - 1; i++) {
            total += calculateDistance(temp->data, temp->next->data);
            temp = temp->next;
        }
        
        if (patrolMode) {
            // Tambahkan jarak kembali ke start
            total += calculateDistance(temp->data, head->data);
        }
        
        cout << "Total estimated distance: " << total << " km" << endl;
        return total;
    }
};
```

**3. calculateTotalDistance():**
Sudah diimplementasikan di atas dengan formula jarak sederhana.

**4. Rekomendasi Fail-safe:**

Jika drone kehilangan koneksi:

1. **Store Last Known Position** - Simpan posisi terakhir di memori non-volatile
2. **Auto Return to Base** - Jika koneksi hilang lebih dari X detik, otomatis `returnToBase()`
3. **Waypoint Caching** - Simpan seluruh route di onboard memory drone
4. **Circular Hover** - Drone berputar di posisi current sambil mencoba reconnect
5. **Emergency Landing Protocol** - Jika baterai kritis + no connection, cari area aman untuk landing

```cpp
void emergencyProtocol() {
    if (connectionLost && elapsedTime > TIMEOUT) {
        if (batteryLow) {
            emergencyLanding();
        } else {
            returnToBase();  // Otomatis kembali
        }
    }
}
```

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
