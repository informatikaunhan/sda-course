# Latihan Mandiri 06: Queue

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 06  
**Topik:** Queue  
**Waktu:** 150 menit  
**Sifat:** Open Book

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal secara **mandiri**
2. Waktu pengerjaan: **150 menit** (sesuai alokasi praktikum)
3. Soal pilihan ganda: Pilih **satu jawaban** yang paling tepat
4. Soal uraian: Jawab dengan **lengkap dan sistematis**
5. Studi kasus: Sertakan **kode program** dan **analisis**

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

### Soal 1
Prinsip yang digunakan oleh struktur data Queue adalah...
- A. LIFO (Last In First Out)
- B. FIFO (First In First Out)
- C. FILO (First In Last Out)
- D. Random Access
- E. Priority Based

### Soal 2
Operasi untuk menambahkan elemen ke dalam queue disebut...
- A. push
- B. pop
- C. enqueue
- D. insert
- E. add

### Soal 3
Pada queue, operasi penghapusan elemen dilakukan pada posisi...
- A. Rear
- B. Front
- C. Middle
- D. Top
- E. Bottom

### Soal 4
Diberikan operasi queue berikut secara berurutan:
```
enqueue(5), enqueue(10), enqueue(15), dequeue(), enqueue(20), dequeue()
```
Apa isi queue setelah semua operasi selesai?
- A. [5, 10]
- B. [10, 15]
- C. [15, 20]
- D. [5, 20]
- E. [10, 20]

### Soal 5
Pada circular queue dengan capacity 5, jika front = 3 dan rear = 1, berapa jumlah elemen dalam queue?
- A. 2
- B. 3
- C. 4
- D. 5
- E. 1

### Soal 6
Masalah "false overflow" pada array linear queue terjadi ketika...
- A. Queue benar-benar penuh
- B. Queue kosong
- C. Ada slot kosong di awal array tapi rear sudah di akhir
- D. Front dan rear berada di posisi yang sama
- E. Terjadi memory leak

### Soal 7
Formula untuk menghitung posisi rear berikutnya pada circular queue adalah...
- A. rear = rear + 1
- B. rear = (rear + 1) % capacity
- C. rear = (rear - 1) % capacity
- D. rear = rear % capacity
- E. rear = (rear + 1) / capacity

### Soal 8
Pada linked list implementation queue, pointer `rear` diperlukan agar operasi...
- A. dequeue menjadi O(1)
- B. enqueue menjadi O(1)
- C. front() menjadi O(1)
- D. isEmpty() menjadi O(1)
- E. size() menjadi O(1)

### Soal 9
Deque (Double-Ended Queue) memungkinkan operasi...
- A. Insert dan delete hanya di front
- B. Insert dan delete hanya di rear
- C. Insert dan delete di kedua ujung (front dan rear)
- D. Insert di front, delete di rear saja
- E. Random access di semua posisi

### Soal 10
Manakah yang merupakan aplikasi yang TEPAT untuk struktur data Queue?
- A. Undo/Redo dalam text editor
- B. Evaluasi ekspresi postfix
- C. BFS (Breadth-First Search) traversal
- D. Function call stack
- E. Backtracking algorithm

### Soal 11
Pada circular queue dengan capacity 6, operasi `(rear + 1) % 6` ketika rear = 5 akan menghasilkan...
- A. 6
- B. 0
- C. 5
- D. 1
- E. -1

### Soal 12
Kompleksitas waktu untuk operasi enqueue dan dequeue pada circular queue adalah...
- A. O(1) dan O(n)
- B. O(n) dan O(1)
- C. O(n) dan O(n)
- D. O(1) dan O(1)
- E. O(log n) dan O(log n)

### Soal 13
Diberikan circular queue dengan capacity 4 dan kondisi awal kosong. Setelah operasi:
```
enqueue(A), enqueue(B), enqueue(C), dequeue(), dequeue(), enqueue(D), enqueue(E)
```
Nilai front dan rear adalah...
- A. front = 0, rear = 3
- B. front = 2, rear = 0
- C. front = 2, rear = 1
- D. front = 1, rear = 0
- E. front = 0, rear = 1

### Soal 14
Input-Restricted Deque adalah deque yang...
- A. Insert hanya di satu ujung, delete di kedua ujung
- B. Insert di kedua ujung, delete hanya di satu ujung
- C. Insert dan delete hanya di front
- D. Insert dan delete hanya di rear
- E. Tidak ada operasi insert

### Soal 15
Dalam implementasi queue menggunakan dua stack, operasi dequeue memiliki kompleksitas...
- A. O(1) selalu
- B. O(n) selalu
- C. Amortized O(1)
- D. O(log n)
- E. O(n²)

### Soal 16
Pada STL C++, untuk melihat elemen paling depan queue tanpa menghapusnya digunakan fungsi...
- A. queue.top()
- B. queue.peek()
- C. queue.front()
- D. queue.first()
- E. queue.head()

### Soal 17
Dalam simulasi round-robin scheduling, queue digunakan untuk...
- A. Menyimpan proses yang sudah selesai
- B. Mengurutkan proses berdasarkan prioritas
- C. Menyimpan proses yang menunggu giliran CPU
- D. Menghitung waktu eksekusi total
- E. Mendeteksi deadlock

### Soal 18
Perbedaan utama antara std::queue dan std::deque di C++ adalah...
- A. std::queue lebih cepat
- B. std::deque mendukung operasi di kedua ujung dan random access
- C. std::queue mendukung random access
- D. std::deque hanya untuk tipe data integer
- E. Tidak ada perbedaan

### Soal 19
Pada linked queue, kondisi queue kosong ditandai dengan...
- A. front == rear
- B. front == nullptr
- C. rear == nullptr
- D. front == nullptr && rear == nullptr
- E. count == capacity

### Soal 20
Untuk mengatasi false overflow pada array linear queue TANPA menggunakan circular array, solusinya adalah...
- A. Menambah capacity
- B. Menggunakan linked list
- C. Menggeser semua elemen ke depan setelah dequeue
- D. Menggunakan dua array
- E. Tidak ada solusi

---

## Bagian B: Soal Uraian (15 Soal)

### Soal 1 (Mudah)
Jelaskan perbedaan mendasar antara Stack dan Queue! Berikan masing-masing 2 contoh aplikasi nyata!

### Soal 2 (Mudah)
Diberikan operasi queue berikut:
```
enqueue(15), enqueue(25), enqueue(35), front(), dequeue(), enqueue(45), rear(), size(), dequeue(), dequeue()
```
Tunjukkan isi queue dan output setiap operasi dalam bentuk tabel!

### Soal 3 (Mudah)
Gambarkan representasi queue menggunakan array linear dengan capacity 6 yang berisi elemen [20, 30, 40] dengan front = 1 dan rear = 3! Jelaskan apa yang terjadi jika dilakukan enqueue(50) dan dequeue()!

### Soal 4 (Sedang)
Jelaskan masalah "false overflow" pada implementasi queue dengan array linear! Mengapa masalah ini tidak terjadi pada circular queue? Sertakan ilustrasi!

### Soal 5 (Sedang)
Implementasikan fungsi `enqueue()` dan `dequeue()` untuk circular queue dalam C++! Jelaskan setiap baris kode dengan komentar!

### Soal 6 (Sedang)
Pada circular queue dengan capacity 7, jika kondisi awal front = 5 dan rear = 2 dengan elemen [_, _, 10, _, _, 30, 40] (indeks 0-6), tentukan:
a. Jumlah elemen dalam queue
b. Hasil operasi enqueue(50)
c. Hasil 2 kali operasi dequeue()
d. Kondisi akhir front dan rear

### Soal 7 (Sedang)
Implementasikan fungsi `display()` untuk linked queue yang menampilkan semua elemen dari front ke rear!

### Soal 8 (Sedang)
Bandingkan implementasi queue menggunakan array (circular) dan linked list dari aspek:
a. Kompleksitas waktu setiap operasi
b. Penggunaan memori
c. Kelebihan dan kekurangan masing-masing
d. Kapan sebaiknya menggunakan masing-masing implementasi

### Soal 9 (Sedang)
Implementasikan fungsi `reverseQueue()` yang membalik isi queue menggunakan stack tambahan! Analisis kompleksitas waktu dan ruang!

### Soal 10 (Sulit)
Implementasikan queue yang mendukung operasi `getMin()` dengan kompleksitas O(1)! Jelaskan strategi yang digunakan!

### Soal 11 (Sulit)
Implementasikan fungsi untuk memeriksa apakah sebuah queue membentuk palindrom! Contoh: Queue [1, 2, 3, 2, 1] adalah palindrom.

### Soal 12 (Sulit)
Buatlah implementasi priority queue sederhana menggunakan 3 queue biasa (HIGH, MEDIUM, LOW priority)! Sertakan fungsi enqueue dengan parameter prioritas dan dequeue yang mengambil dari prioritas tertinggi terlebih dahulu!

### Soal 13 (Sedang)
Jelaskan konsep Deque dan implementasikan fungsi `insertFront()` dan `deleteRear()` pada circular array deque!

### Soal 14 (Sulit)
Implementasikan queue menggunakan dua stack! Jelaskan mengapa kompleksitas amortized untuk dequeue adalah O(1)!

### Soal 15 (Sulit)
Buatlah simulasi antrian pelanggan di kasir supermarket dengan ketentuan:
- Ada 2 kasir
- Pelanggan baru mengantri di kasir dengan antrian terpendek
- Setiap pelanggan memiliki waktu layanan berbeda (1-5 menit)
- Simulasikan kedatangan 10 pelanggan dan proses pelayanan!

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Antrian Pesan Komunikasi Militer

**Latar Belakang:**
Pusat Komando dan Kendali (Kodal) menerima berbagai jenis pesan dari unit-unit di lapangan. Pesan memiliki 3 tingkat prioritas sesuai standar NATO:
- **FLASH** (Z): Prioritas tertinggi, harus diproses segera (dalam hitungan detik)
- **IMMEDIATE** (O): Prioritas tinggi, diproses dalam 10-30 menit
- **ROUTINE** (R): Prioritas normal, diproses sesuai urutan

**Kebutuhan Sistem:**
1. Menerima pesan dengan informasi: ID, pengirim, waktu kirim, prioritas, dan isi pesan
2. Memproses pesan sesuai prioritas (FLASH > IMMEDIATE > ROUTINE)
3. Dalam satu tingkat prioritas, pesan diproses secara FIFO
4. Menampilkan statistik: total pesan diterima, rata-rata waktu tunggu per kategori

**Tugas:**
1. Rancang struktur data yang tepat untuk sistem ini (gunakan multiple queues)
2. Implementasikan dalam C++ dengan class `MilitaryMessageSystem`
3. Buatlah simulasi dengan minimal 15 pesan dari berbagai prioritas
4. Analisis mengapa queue adalah struktur data yang tepat untuk kasus ini

**Template Kode:**
```cpp
#include <iostream>
#include <queue>
#include <string>
#include <ctime>
using namespace std;

enum Priority { FLASH, IMMEDIATE, ROUTINE };

struct Message {
    int id;
    string sender;
    time_t timestamp;
    Priority priority;
    string content;
};

class MilitaryMessageSystem {
    // Implementasikan di sini
};

int main() {
    MilitaryMessageSystem system;
    
    // Simulasi penerimaan dan pemrosesan pesan
    
    return 0;
}
```

---

### Studi Kasus 2: Sistem Antrian Pesawat di Pangkalan Udara

**Latar Belakang:**
Pangkalan Udara TNI AU mengelola antrian pesawat untuk take-off dan landing. Sistem harus memprioritaskan:
1. **Emergency landing** (bahan bakar kritis, kerusakan mekanis)
2. **Combat mission** (misi tempur aktif)
3. **Training mission** (latihan rutin)
4. **Regular flight** (penerbangan biasa)

Selain itu, runway memiliki kapasitas terbatas dan perlu dijadwalkan secara efisien.

**Kebutuhan Sistem:**
1. Antrian terpisah untuk take-off dan landing
2. Landing selalu diprioritaskan daripada take-off (keselamatan)
3. Dalam kategori yang sama, gunakan FIFO
4. Catat waktu tunggu setiap pesawat
5. Batasi maksimal 5 pesawat dalam antrian per kategori

**Tugas:**
1. Desain struktur data menggunakan kombinasi queue dan priority handling
2. Implementasikan class `AirbaseQueueSystem`
3. Simulasikan skenario dengan 20 pesawat (campuran take-off dan landing)
4. Tampilkan log operasi dan statistik waktu tunggu rata-rata
5. Analisis kompleksitas waktu dan ruang dari solusi Anda

**Kriteria Penilaian:**
- Ketepatan implementasi queue (30%)
- Penanganan prioritas yang benar (25%)
- Kelengkapan simulasi (20%)
- Kualitas kode dan dokumentasi (15%)
- Analisis kompleksitas (10%)

---

## Kunci Jawaban

### BAGIAN A: PILIHAN GANDA

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | **B** | Queue menggunakan FIFO (First In First Out) |
| 2 | **C** | Enqueue adalah operasi menambah elemen ke queue |
| 3 | **B** | Dequeue mengambil elemen dari front |
| 4 | **C** | Setelah semua operasi: [15, 20] |
| 5 | **C** | (rear - front + capacity) % capacity + 1 = (1-3+5)%5+1 = 4 |
| 6 | **C** | False overflow = ada slot kosong di awal tapi tidak bisa enqueue |
| 7 | **B** | Formula circular: (rear + 1) % capacity |
| 8 | **B** | Pointer rear membuat enqueue O(1), tanpa perlu traverse |
| 9 | **C** | Deque = insert/delete di kedua ujung |
| 10 | **C** | BFS menggunakan queue untuk menjelajahi level per level |
| 11 | **B** | (5 + 1) % 6 = 0 (wrap-around ke awal) |
| 12 | **D** | Semua operasi circular queue O(1) |
| 13 | **C** | Trace: front=2 (setelah 2 dequeue), rear=1 (setelah wrap) |
| 14 | **A** | Input-Restricted: insert di satu ujung, delete di dua ujung |
| 15 | **C** | Setiap elemen dipindah max 2 kali, jadi amortized O(1) |
| 16 | **C** | std::queue menggunakan front() untuk melihat elemen depan |
| 17 | **C** | Round-robin menyimpan proses yang menunggu dalam queue |
| 18 | **B** | std::deque mendukung operasi di kedua ujung + random access |
| 19 | **D** | Queue kosong: front dan rear keduanya nullptr |
| 20 | **C** | Shift elements adalah solusi tanpa circular (tapi O(n)) |

---

### BAGIAN B: URAIAN

#### Jawaban Soal 1

**Perbedaan Stack dan Queue:**

| Aspek | Stack | Queue |
|-------|-------|-------|
| Prinsip | LIFO (Last In First Out) | FIFO (First In First Out) |
| Penyisipan | Di top (push) | Di rear (enqueue) |
| Penghapusan | Di top (pop) | Di front (dequeue) |
| Akses | Hanya top | Front dan rear |

**Contoh Aplikasi Stack:**
1. Undo/Redo dalam text editor
2. Evaluasi ekspresi matematika (postfix)

**Contoh Aplikasi Queue:**
1. Antrian print job pada printer
2. BFS traversal pada graph/tree

---

#### Jawaban Soal 2

| Langkah | Operasi | Isi Queue | Output |
|---------|---------|-----------|--------|
| 1 | enqueue(15) | [15] | - |
| 2 | enqueue(25) | [15, 25] | - |
| 3 | enqueue(35) | [15, 25, 35] | - |
| 4 | front() | [15, 25, 35] | **15** |
| 5 | dequeue() | [25, 35] | **15** |
| 6 | enqueue(45) | [25, 35, 45] | - |
| 7 | rear() | [25, 35, 45] | **45** |
| 8 | size() | [25, 35, 45] | **3** |
| 9 | dequeue() | [35, 45] | **25** |
| 10 | dequeue() | [45] | **35** |

**Isi akhir:** [45] dengan front = rear = 45

---

#### Jawaban Soal 3

![Jawaban Soal 3 - Array Linear Queue Operations](images/p06-09-latihan-soal3-array-operations.png)

*Gambar: Representasi Array Linear Queue dan operasi enqueue/dequeue*


**Penjelasan:**
- **Kondisi Awal**: Queue berisi [20, 30, 40] di indeks 1-3, front=1, rear=3
- **Setelah enqueue(50)**: Rear bergerak dari 3 ke 4, nilai 50 disimpan di indeks 4
- **Setelah dequeue()**: Elemen 20 dihapus, front bergerak dari 1 ke 2

---

#### Jawaban Soal 4

**Masalah False Overflow:**

False overflow terjadi ketika array linear queue dianggap penuh padahal masih ada slot kosong di awal array.

![Jawaban Soal 4 - False Overflow vs Circular Queue](images/p06-10-latihan-soal4-false-overflow-solution.png)

*Gambar: Perbandingan False Overflow pada Linear Queue vs Solusi Circular Queue*

**Penjelasan:**

**Masalah pada Linear Queue:**
- Setelah 3x dequeue, slot 0, 1, 2 kosong tapi tidak bisa digunakan
- rear sudah di index terakhir, tidak bisa enqueue lagi

**Solusi Circular Queue:**
- Formula `(index + 1) % capacity` memungkinkan wrap-around
- Contoh: `rear = (4 + 1) % 5 = 0` → rear kembali ke index 0
- Slot di awal bisa digunakan kembali!

---

#### Jawaban Soal 5

```cpp
template <typename T>
class CircularQueue {
private:
    T* data;          // Array untuk menyimpan elemen
    int frontIndex;   // Indeks elemen depan
    int rearIndex;    // Indeks elemen belakang
    int capacity;     // Kapasitas maksimum
    int count;        // Jumlah elemen saat ini

public:
    // Konstruktor
    CircularQueue(int size) {
        capacity = size;
        data = new T[capacity];
        frontIndex = 0;
        rearIndex = -1;  // Belum ada elemen
        count = 0;
    }

    // Menambahkan elemen ke rear
    void enqueue(const T& item) {
        // Cek apakah queue penuh
        if (count == capacity) {
            throw overflow_error("Queue penuh!");
        }
        
        // Hitung posisi rear berikutnya secara circular
        // Formula: (current + 1) % capacity
        rearIndex = (rearIndex + 1) % capacity;
        
        // Simpan elemen di posisi rear baru
        data[rearIndex] = item;
        
        // Tambah counter
        count++;
    }

    // Menghapus dan mengembalikan elemen dari front
    T dequeue() {
        // Cek apakah queue kosong
        if (count == 0) {
            throw underflow_error("Queue kosong!");
        }
        
        // Simpan elemen yang akan dihapus
        T item = data[frontIndex];
        
        // Gerakkan front ke posisi berikutnya secara circular
        frontIndex = (frontIndex + 1) % capacity;
        
        // Kurangi counter
        count--;
        
        // Kembalikan elemen yang dihapus
        return item;
    }
};
```

---

#### Jawaban Soal 6

![Jawaban Soal 6 - Circular Queue Trace](images/p06-11-latihan-soal6-circular-queue-trace.png)

*Gambar: Trace operasi pada Circular Queue dengan capacity 7*

**Penjelasan Jawaban:**

**a. Jumlah elemen awal:** 3 elemen (30, 40, 10 dalam urutan queue)

**b. Setelah enqueue(50):** 
- rear = (2 + 1) % 7 = 3
- Nilai 50 disimpan di indeks 3
- Jumlah elemen = 4

**c. Setelah 2x dequeue():**
- Dequeue 1: menghapus 30, front = (5+1)%7 = 6
- Dequeue 2: menghapus 40, front = (6+1)%7 = 0 (wrap-around!)

**d. Kondisi akhir:** front = 0, rear = 3, jumlah elemen = 2 (yaitu 10 di idx 2 dan 50 di idx 3)

---

#### Jawaban Soal 7

```cpp
template <typename T>
class LinkedQueue {
private:
    struct Node {
        T data;
        Node* next;
        Node(T val) : data(val), next(nullptr) {}
    };
    
    Node* frontPtr;
    Node* rearPtr;
    int count;

public:
    // Fungsi display() - menampilkan semua elemen
    void display() const {
        // Cek jika queue kosong
        if (frontPtr == nullptr) {
            cout << "Queue kosong" << endl;
            return;
        }
        
        cout << "Queue (front -> rear): [";
        
        // Traverse dari front ke rear
        Node* current = frontPtr;
        while (current != nullptr) {
            cout << current->data;
            
            // Tambah koma jika bukan elemen terakhir
            if (current->next != nullptr) {
                cout << ", ";
            }
            
            // Pindah ke node berikutnya
            current = current->next;
        }
        
        cout << "]" << endl;
        cout << "Size: " << count << endl;
    }
};
```

---

#### Jawaban Soal 8

**Perbandingan Array (Circular) vs Linked List:**

| Aspek | Circular Array | Linked List |
|-------|---------------|-------------|
| **a. Kompleksitas Waktu** | | |
| - enqueue | O(1) | O(1) |
| - dequeue | O(1) | O(1) |
| - front/rear | O(1) | O(1) |
| - isEmpty | O(1) | O(1) |
| **b. Penggunaan Memori** | | |
| - Total | O(capacity) - fixed | O(n) - sesuai jumlah elemen |
| - Per elemen | Hanya data | Data + pointer (8 byte) |
| - Overhead | Slot kosong jika tidak penuh | Pointer overhead |
| **c. Kelebihan** | Cache-friendly, no pointer overhead | Ukuran dinamis, tidak perlu resize |
| **d. Kekurangan** | Ukuran fixed, bisa waste memory | Cache-unfriendly, pointer overhead |

**Kapan menggunakan masing-masing:**
- **Circular Array**: Ketika ukuran maksimum diketahui, performa cache penting, memory limited
- **Linked List**: Ketika ukuran tidak terbatas/tidak diketahui, sering resize

---

#### Jawaban Soal 9

```cpp
#include <stack>
#include <queue>

template <typename T>
void reverseQueue(queue<T>& q) {
    stack<T> tempStack;
    
    // Langkah 1: Pindahkan semua elemen dari queue ke stack
    while (!q.empty()) {
        tempStack.push(q.front());
        q.pop();
    }
    
    // Langkah 2: Pindahkan kembali dari stack ke queue
    // Karena stack LIFO, urutan akan terbalik
    while (!tempStack.empty()) {
        q.push(tempStack.top());
        tempStack.pop();
    }
}

// Contoh penggunaan
int main() {
    queue<int> q;
    q.push(1); q.push(2); q.push(3); q.push(4);
    // Queue: [1, 2, 3, 4]
    
    reverseQueue(q);
    // Queue: [4, 3, 2, 1]
    
    return 0;
}
```

**Analisis Kompleksitas:**
- **Waktu:** O(n) - setiap elemen dipindah 2 kali (queue→stack, stack→queue)
- **Ruang:** O(n) - stack tambahan menyimpan semua n elemen

---

#### Jawaban Soal 10

```cpp
#include <queue>
#include <deque>

class MinQueue {
private:
    queue<int> mainQueue;    // Queue utama
    deque<int> minDeque;     // Menyimpan kandidat minimum
    
public:
    void enqueue(int value) {
        mainQueue.push(value);
        
        // Hapus elemen dari belakang minDeque yang lebih besar
        // dari value baru (tidak mungkin jadi minimum)
        while (!minDeque.empty() && minDeque.back() > value) {
            minDeque.pop_back();
        }
        
        // Tambahkan value ke minDeque
        minDeque.push_back(value);
    }
    
    int dequeue() {
        if (mainQueue.empty()) {
            throw runtime_error("Queue kosong!");
        }
        
        int value = mainQueue.front();
        mainQueue.pop();
        
        // Jika elemen yang dihapus adalah minimum saat ini
        if (value == minDeque.front()) {
            minDeque.pop_front();
        }
        
        return value;
    }
    
    int getMin() const {
        if (minDeque.empty()) {
            throw runtime_error("Queue kosong!");
        }
        return minDeque.front();  // O(1)!
    }
};
```

**Strategi:**
- Gunakan deque tambahan yang selalu menyimpan elemen dalam urutan menurun dari depan ke belakang
- Elemen paling depan deque adalah minimum
- Saat enqueue, hapus elemen yang lebih besar dari belakang (tidak berguna)
- Saat dequeue, jika elemen yang dihapus = min, hapus juga dari deque

---

#### Jawaban Soal 11

```cpp
#include <queue>
#include <stack>

bool isQueuePalindrome(queue<int> q) {
    stack<int> s;
    int n = q.size();
    
    // Copy semua elemen ke stack
    queue<int> tempQ = q;
    while (!tempQ.empty()) {
        s.push(tempQ.front());
        tempQ.pop();
    }
    
    // Bandingkan queue (front→back) dengan stack (back→front)
    while (!q.empty()) {
        if (q.front() != s.top()) {
            return false;  // Bukan palindrom
        }
        q.pop();
        s.pop();
    }
    
    return true;  // Palindrom!
}

// Contoh
int main() {
    queue<int> q1, q2;
    
    // Palindrom: 1, 2, 3, 2, 1
    q1.push(1); q1.push(2); q1.push(3); q1.push(2); q1.push(1);
    
    // Bukan palindrom: 1, 2, 3, 4, 5
    q2.push(1); q2.push(2); q2.push(3); q2.push(4); q2.push(5);
    
    cout << "Q1 palindrom? " << (isQueuePalindrome(q1) ? "Ya" : "Tidak") << endl;  // Ya
    cout << "Q2 palindrom? " << (isQueuePalindrome(q2) ? "Ya" : "Tidak") << endl;  // Tidak
    
    return 0;
}
```

---

#### Jawaban Soal 12

```cpp
#include <queue>
#include <string>
#include <iostream>
using namespace std;

enum Priority { HIGH = 0, MEDIUM = 1, LOW = 2 };

template <typename T>
class SimplePriorityQueue {
private:
    queue<T> highQueue;
    queue<T> mediumQueue;
    queue<T> lowQueue;
    
public:
    // Enqueue dengan prioritas
    void enqueue(const T& item, Priority priority) {
        switch (priority) {
            case HIGH:
                highQueue.push(item);
                cout << "[HIGH] Added: " << item << endl;
                break;
            case MEDIUM:
                mediumQueue.push(item);
                cout << "[MEDIUM] Added: " << item << endl;
                break;
            case LOW:
                lowQueue.push(item);
                cout << "[LOW] Added: " << item << endl;
                break;
        }
    }
    
    // Dequeue dari prioritas tertinggi yang tersedia
    T dequeue() {
        if (!highQueue.empty()) {
            T item = highQueue.front();
            highQueue.pop();
            cout << "[HIGH] Processed: " << item << endl;
            return item;
        } else if (!mediumQueue.empty()) {
            T item = mediumQueue.front();
            mediumQueue.pop();
            cout << "[MEDIUM] Processed: " << item << endl;
            return item;
        } else if (!lowQueue.empty()) {
            T item = lowQueue.front();
            lowQueue.pop();
            cout << "[LOW] Processed: " << item << endl;
            return item;
        } else {
            throw runtime_error("Priority queue kosong!");
        }
    }
    
    bool isEmpty() const {
        return highQueue.empty() && mediumQueue.empty() && lowQueue.empty();
    }
    
    int size() const {
        return highQueue.size() + mediumQueue.size() + lowQueue.size();
    }
};

int main() {
    SimplePriorityQueue<string> pq;
    
    pq.enqueue("Task A", LOW);
    pq.enqueue("Task B", HIGH);
    pq.enqueue("Task C", MEDIUM);
    pq.enqueue("Task D", HIGH);
    pq.enqueue("Task E", LOW);
    
    cout << "\n--- Processing ---\n";
    while (!pq.isEmpty()) {
        pq.dequeue();
    }
    
    return 0;
}
```

**Output:**
```
[LOW] Added: Task A
[HIGH] Added: Task B
[MEDIUM] Added: Task C
[HIGH] Added: Task D
[LOW] Added: Task E

--- Processing ---
[HIGH] Processed: Task B
[HIGH] Processed: Task D
[MEDIUM] Processed: Task C
[LOW] Processed: Task A
[LOW] Processed: Task E
```

---

#### Jawaban Soal 13

**Konsep Deque:**
Deque (Double-Ended Queue) adalah struktur data linear yang memungkinkan operasi insert dan delete di kedua ujung (front dan rear).

```cpp
template <typename T>
class CircularDeque {
private:
    T* data;
    int frontIndex;
    int rearIndex;
    int capacity;
    int count;

public:
    CircularDeque(int size) {
        capacity = size;
        data = new T[capacity];
        frontIndex = 0;
        rearIndex = capacity - 1;
        count = 0;
    }
    
    // Insert di depan
    void insertFront(const T& item) {
        if (count == capacity) {
            throw overflow_error("Deque penuh!");
        }
        
        // Geser front ke belakang (circular)
        frontIndex = (frontIndex - 1 + capacity) % capacity;
        data[frontIndex] = item;
        count++;
    }
    
    // Delete dari belakang
    T deleteRear() {
        if (count == 0) {
            throw underflow_error("Deque kosong!");
        }
        
        T item = data[rearIndex];
        // Geser rear ke depan (circular)
        rearIndex = (rearIndex - 1 + capacity) % capacity;
        count--;
        return item;
    }
    
    // Operasi lain: insertRear, deleteFront, getFront, getRear, isEmpty, isFull
};
```

---

#### Jawaban Soal 14

```cpp
#include <stack>
#include <stdexcept>
using namespace std;

template <typename T>
class QueueUsingTwoStacks {
private:
    stack<T> stackIn;   // Untuk enqueue
    stack<T> stackOut;  // Untuk dequeue
    
    // Transfer dari stackIn ke stackOut
    void transfer() {
        while (!stackIn.empty()) {
            stackOut.push(stackIn.top());
            stackIn.pop();
        }
    }

public:
    void enqueue(const T& item) {
        stackIn.push(item);  // Selalu O(1)
    }
    
    T dequeue() {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        
        // Transfer hanya jika stackOut kosong
        if (stackOut.empty()) {
            transfer();
        }
        
        T item = stackOut.top();
        stackOut.pop();
        return item;
    }
    
    bool isEmpty() const {
        return stackIn.empty() && stackOut.empty();
    }
};
```

**Mengapa Amortized O(1):**

Analisis per elemen:
1. Setiap elemen di-push ke stackIn tepat **1 kali** → O(1)
2. Setiap elemen di-transfer ke stackOut paling banyak **1 kali** → O(1)
3. Setiap elemen di-pop dari stackOut tepat **1 kali** → O(1)

Total: setiap elemen mengalami **3 operasi O(1)** sepanjang hidupnya.

Meskipun satu operasi dequeue bisa O(n) saat transfer, jika kita amortize (bagi rata) ke semua operasi, setiap dequeue rata-rata O(1).

**Contoh:**
- enqueue 1,2,3,4,5 → stackIn=[1,2,3,4,5]
- dequeue → transfer O(5) → stackOut=[5,4,3,2,1] → return 1
- dequeue → O(1) → return 2
- dequeue → O(1) → return 3
- dequeue → O(1) → return 4
- dequeue → O(1) → return 5

Total 5 dequeue, total work = 5 (transfer) + 5 (pop) = 10 = 2n
Amortized per dequeue = 10/5 = 2 = O(1)

---

#### Jawaban Soal 15

```cpp
#include <iostream>
#include <queue>
#include <string>
#include <cstdlib>
#include <ctime>
using namespace std;

struct Customer {
    int id;
    int serviceTime;  // 1-5 menit
    int arrivalTime;
};

class SupermarketSimulation {
private:
    queue<Customer> cashier1;
    queue<Customer> cashier2;
    int customerCount;
    int currentTime;
    int totalWaitTime1, totalWaitTime2;
    int servedCount1, servedCount2;
    int remainingTime1, remainingTime2;  // Sisa waktu layanan customer saat ini

public:
    SupermarketSimulation() {
        customerCount = 0;
        currentTime = 0;
        totalWaitTime1 = totalWaitTime2 = 0;
        servedCount1 = servedCount2 = 0;
        remainingTime1 = remainingTime2 = 0;
    }

    void customerArrives() {
        Customer c;
        c.id = ++customerCount;
        c.serviceTime = rand() % 5 + 1;  // 1-5 menit
        c.arrivalTime = currentTime;

        // Pilih kasir dengan antrian lebih pendek
        if (cashier1.size() <= cashier2.size()) {
            cashier1.push(c);
            cout << "[T=" << currentTime << "] Customer #" << c.id 
                 << " (service: " << c.serviceTime << " min) → Cashier 1 "
                 << "(queue: " << cashier1.size() << ")" << endl;
        } else {
            cashier2.push(c);
            cout << "[T=" << currentTime << "] Customer #" << c.id 
                 << " (service: " << c.serviceTime << " min) → Cashier 2 "
                 << "(queue: " << cashier2.size() << ")" << endl;
        }
    }

    void processOneMinute() {
        // Process Cashier 1
        if (remainingTime1 > 0) {
            remainingTime1--;
        }
        if (remainingTime1 == 0 && !cashier1.empty()) {
            Customer c = cashier1.front();
            cashier1.pop();
            int waitTime = currentTime - c.arrivalTime;
            totalWaitTime1 += waitTime;
            servedCount1++;
            cout << "[T=" << currentTime << "] Cashier 1 finished Customer #" 
                 << c.id << " (waited: " << waitTime << " min)" << endl;
            
            if (!cashier1.empty()) {
                remainingTime1 = cashier1.front().serviceTime;
            }
        }

        // Process Cashier 2
        if (remainingTime2 > 0) {
            remainingTime2--;
        }
        if (remainingTime2 == 0 && !cashier2.empty()) {
            Customer c = cashier2.front();
            cashier2.pop();
            int waitTime = currentTime - c.arrivalTime;
            totalWaitTime2 += waitTime;
            servedCount2++;
            cout << "[T=" << currentTime << "] Cashier 2 finished Customer #" 
                 << c.id << " (waited: " << waitTime << " min)" << endl;
            
            if (!cashier2.empty()) {
                remainingTime2 = cashier2.front().serviceTime;
            }
        }

        currentTime++;
    }

    void startFirstCustomers() {
        if (!cashier1.empty() && remainingTime1 == 0) {
            remainingTime1 = cashier1.front().serviceTime;
        }
        if (!cashier2.empty() && remainingTime2 == 0) {
            remainingTime2 = cashier2.front().serviceTime;
        }
    }

    bool hasCustomers() {
        return !cashier1.empty() || !cashier2.empty() || remainingTime1 > 0 || remainingTime2 > 0;
    }

    void printStatistics() {
        cout << "\n=== STATISTICS ===" << endl;
        cout << "Cashier 1: Served " << servedCount1 << " customers, "
             << "Avg wait: " << (servedCount1 ? (float)totalWaitTime1/servedCount1 : 0) << " min" << endl;
        cout << "Cashier 2: Served " << servedCount2 << " customers, "
             << "Avg wait: " << (servedCount2 ? (float)totalWaitTime2/servedCount2 : 0) << " min" << endl;
    }
};

int main() {
    srand(time(0));
    SupermarketSimulation sim;

    cout << "=== CUSTOMER ARRIVALS ===" << endl;
    // 10 customers datang di waktu berbeda
    for (int i = 0; i < 10; i++) {
        sim.customerArrives();
        if (i < 9 && rand() % 2 == 0) {
            // Kadang 2 customer datang bersamaan
            sim.customerArrives();
            i++;
        }
    }

    sim.startFirstCustomers();

    cout << "\n=== PROCESSING ===" << endl;
    while (sim.hasCustomers()) {
        sim.processOneMinute();
    }

    sim.printStatistics();

    return 0;
}
```

---

### BAGIAN C: STUDI KASUS

#### Panduan Penilaian Studi Kasus 1

**Rubrik Penilaian:**

| Kriteria | Bobot | Deskripsi |
|----------|-------|-----------|
| Struktur Data | 30% | Penggunaan 3 queue untuk 3 prioritas |
| Prioritas Handling | 25% | FLASH → IMMEDIATE → ROUTINE |
| FIFO per Kategori | 15% | Pesan dalam kategori sama diproses sesuai urutan masuk |
| Statistik | 15% | Total pesan, rata-rata waktu tunggu |
| Kode & Dokumentasi | 15% | Komentar, struktur kode, naming |

#### Panduan Penilaian Studi Kasus 2

**Rubrik Penilaian:**

| Kriteria | Bobot | Deskripsi |
|----------|-------|-----------|
| Implementasi Queue | 30% | Antrian take-off dan landing terpisah |
| Priority Handling | 25% | Emergency > Combat > Training > Regular |
| Landing Priority | 15% | Landing selalu diprioritaskan dari take-off |
| Simulasi Lengkap | 20% | 20 pesawat, log operasi, statistik |
| Analisis Kompleksitas | 10% | Waktu dan ruang |

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
