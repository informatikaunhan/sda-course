# Modul 06: Queue

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 06  
**Topik:** Queue

> **Capaian Pembelajaran:** Sub-CPMK-2.3 — Mampu mengimplementasikan queue dan deque dengan berbagai representasi

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.10.1; Weiss Ch.3.7; Hubbard Ch.6

---

## Tujuan Pembelajaran

Setelah mempelajari modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** konsep FIFO (First In First Out) dan karakteristik ADT Queue
2. **Mengidentifikasi** operasi-operasi dasar pada queue (enqueue, dequeue, front, rear, isEmpty, isFull)
3. **Mengimplementasikan** queue menggunakan array linear beserta keterbatasannya
4. **Mengimplementasikan** circular queue untuk mengatasi keterbatasan array linear
5. **Mengimplementasikan** queue menggunakan linked list dengan operasi yang efisien
6. **Memahami** konsep deque (double-ended queue) dan variasinya
7. **Menerapkan** queue dalam aplikasi nyata seperti simulasi antrian, task scheduling, dan buffer

---

## 1. Konsep Dasar Queue

### 1.1 Definisi Queue

> **Queue** adalah struktur data linear yang mengikuti prinsip **FIFO (First In First Out)**, di mana elemen yang pertama kali masuk akan menjadi elemen yang pertama kali keluar.

Berbeda dengan Stack yang dipelajari pada Pertemuan 5 yang menggunakan prinsip LIFO, Queue menggunakan prinsip FIFO yang menyerupai antrian di kehidupan nyata.

![Konsep FIFO Queue](images/p06-01-konsep-fifo-queue.png)

*Gambar 1.1: Ilustrasi konsep FIFO pada Queue*


### 1.2 Analogi Kehidupan Nyata

Queue dapat ditemukan dalam berbagai situasi sehari-hari:

| Analogi | Penjelasan |
|---------|------------|
| **Antrian di bank/loket** | Orang yang datang pertama dilayani pertama |
| **Antrian kendaraan di gerbang tol** | Kendaraan yang tiba lebih dulu lewat lebih dulu |
| **Antrian cetak (print queue)** | Dokumen yang dikirim lebih dulu dicetak lebih dulu |
| **Antrian pasien di klinik** | Pasien yang mendaftar lebih awal diperiksa lebih awal |
| **Buffer keyboard** | Karakter yang diketik lebih dulu diproses lebih dulu |

**Konteks Pertahanan:**
- **Antrian pesan di sistem komunikasi militer**: Pesan yang dikirim lebih dulu harus diproses dan diteruskan lebih dulu untuk menjaga urutan kronologis informasi
- **Task scheduling pada sistem radar**: Pemrosesan sinyal radar dilakukan secara berurutan sesuai waktu kedatangan
- **Buffer data pada sistem surveillance**: Data video/audio disimpan sementara dalam antrian sebelum diproses

### 1.3 Karakteristik Queue

1. **Dua ujung berbeda**: Queue memiliki dua ujung - **front** (depan) untuk penghapusan dan **rear** (belakang) untuk penyisipan
2. **Operasi terbatas**: Penyisipan hanya di rear, penghapusan hanya di front
3. **Akses terbatas**: Tidak bisa mengakses elemen di tengah secara langsung
4. **Urutan terjaga**: Urutan elemen selalu sesuai waktu kedatangan

---

## 2. Abstract Data Type (ADT) Queue

### 2.1 Definisi ADT Queue

> **ADT Queue** mendefinisikan sekumpulan operasi yang dapat dilakukan pada queue tanpa menentukan bagaimana operasi tersebut diimplementasikan.

### 2.2 Operasi-operasi Dasar Queue

| Operasi | Deskripsi | Return Type |
|---------|-----------|-------------|
| `enqueue(item)` | Menambahkan item ke rear queue | void |
| `dequeue()` | Menghapus dan mengembalikan item dari front | item type |
| `front()` / `peek()` | Mengembalikan item di front tanpa menghapus | item type |
| `rear()` / `back()` | Mengembalikan item di rear tanpa menghapus | item type |
| `isEmpty()` | Mengecek apakah queue kosong | boolean |
| `isFull()` | Mengecek apakah queue penuh (untuk array) | boolean |
| `size()` | Mengembalikan jumlah elemen dalam queue | integer |

### 2.3 Interface Queue dalam C++

```cpp
template <typename T>
class QueueADT {
public:
    virtual void enqueue(const T& item) = 0;  // Menambah elemen ke rear
    virtual T dequeue() = 0;                   // Menghapus dari front
    virtual T front() const = 0;               // Melihat elemen front
    virtual T rear() const = 0;                // Melihat elemen rear
    virtual bool isEmpty() const = 0;          // Cek kosong
    virtual bool isFull() const = 0;           // Cek penuh
    virtual int size() const = 0;              // Jumlah elemen
    virtual ~QueueADT() {}
};
```

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Diberikan operasi queue berikut secara berurutan. Tentukan isi queue dan output setiap operasi!
```
enqueue(10), enqueue(20), enqueue(30), dequeue(), front(), enqueue(40), dequeue(), size()
```

**Penyelesaian:**

| Operasi | Isi Queue | Output | Penjelasan |
|---------|-----------|--------|------------|
| `enqueue(10)` | [10] | - | 10 masuk ke rear |
| `enqueue(20)` | [10, 20] | - | 20 masuk ke rear |
| `enqueue(30)` | [10, 20, 30] | - | 30 masuk ke rear |
| `dequeue()` | [20, 30] | 10 | 10 keluar dari front |
| `front()` | [20, 30] | 20 | Lihat front tanpa menghapus |
| `enqueue(40)` | [20, 30, 40] | - | 40 masuk ke rear |
| `dequeue()` | [30, 40] | 20 | 20 keluar dari front |
| `size()` | [30, 40] | 2 | Ada 2 elemen |

**Jawaban:** Isi akhir queue adalah [30, 40], dengan front = 30 dan rear = 40.

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Apa perbedaan mendasar antara Stack dan Queue? Berikan contoh kasus penggunaan masing-masing!

**Penyelesaian:**

| Aspek | Stack | Queue |
|-------|-------|-------|
| **Prinsip** | LIFO (Last In First Out) | FIFO (First In First Out) |
| **Penyisipan** | Di top (push) | Di rear (enqueue) |
| **Penghapusan** | Di top (pop) | Di front (dequeue) |
| **Akses** | Hanya top | Front dan rear |

**Contoh Penggunaan:**
- **Stack**: Undo/Redo, evaluasi ekspresi, backtracking
- **Queue**: Antrian printer, task scheduling, BFS traversal

---

## 3. Implementasi Queue dengan Array Linear

### 3.1 Konsep Dasar

Implementasi paling sederhana menggunakan array dengan dua variabel penunjuk:
- `front`: indeks elemen terdepan
- `rear`: indeks elemen terakhir

![Queue dengan Array Linear](images/p06-02-queue-array-linear.png)

*Gambar 3.1: Representasi queue dengan array linear*


### 3.2 Implementasi Lengkap

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

template <typename T>
class ArrayQueue {
private:
    T* data;
    int frontIndex;
    int rearIndex;
    int capacity;
    int count;

public:
    // Constructor
    ArrayQueue(int size = 100) {
        capacity = size;
        data = new T[capacity];
        frontIndex = 0;
        rearIndex = -1;
        count = 0;
    }

    // Destructor
    ~ArrayQueue() {
        delete[] data;
    }

    // Menambahkan elemen ke rear
    void enqueue(const T& item) {
        if (isFull()) {
            throw overflow_error("Queue penuh!");
        }
        rearIndex++;
        data[rearIndex] = item;
        count++;
    }

    // Menghapus dan mengembalikan elemen dari front
    T dequeue() {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        T item = data[frontIndex];
        frontIndex++;
        count--;
        return item;
    }

    // Melihat elemen di front
    T front() const {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        return data[frontIndex];
    }

    // Melihat elemen di rear
    T rear() const {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        return data[rearIndex];
    }

    // Mengecek apakah queue kosong
    bool isEmpty() const {
        return count == 0;
    }

    // Mengecek apakah queue penuh
    bool isFull() const {
        return rearIndex >= capacity - 1;
    }

    // Mengembalikan jumlah elemen
    int size() const {
        return count;
    }

    // Menampilkan isi queue
    void display() const {
        if (isEmpty()) {
            cout << "Queue kosong" << endl;
            return;
        }
        cout << "Queue: [";
        for (int i = frontIndex; i <= rearIndex; i++) {
            cout << data[i];
            if (i < rearIndex) cout << ", ";
        }
        cout << "]" << endl;
        cout << "Front: " << data[frontIndex] << ", Rear: " << data[rearIndex] << endl;
    }
};

// Contoh penggunaan
int main() {
    ArrayQueue<int> queue(5);

    queue.enqueue(10);
    queue.enqueue(20);
    queue.enqueue(30);
    queue.display();  // Queue: [10, 20, 30]

    cout << "Dequeue: " << queue.dequeue() << endl;  // 10
    queue.display();  // Queue: [20, 30]

    queue.enqueue(40);
    queue.enqueue(50);
    queue.display();  // Queue: [20, 30, 40, 50]

    return 0;
}
```

### 3.3 Analisis Kompleksitas Array Linear

| Operasi | Kompleksitas | Penjelasan |
|---------|-------------|------------|
| `enqueue()` | O(1) | Langsung tambah di rear |
| `dequeue()` | O(1) | Langsung hapus dari front |
| `front()` | O(1) | Akses langsung via indeks |
| `rear()` | O(1) | Akses langsung via indeks |
| `isEmpty()` | O(1) | Cek variabel count |
| `isFull()` | O(1) | Cek rear terhadap capacity |
| `size()` | O(1) | Return variabel count |

### 3.4 Kelemahan Array Linear

> **Masalah Utama:** Setelah beberapa operasi dequeue, ruang di awal array menjadi tidak terpakai meskipun masih ada slot kosong. Ini disebut **"false overflow"**.

![Masalah False Overflow](images/p06-03-false-overflow-problem.png)

*Gambar 3.2: Ilustrasi masalah false overflow pada array linear*


**Solusi untuk false overflow:**
1. **Menggeser semua elemen** ke depan setelah dequeue → O(n) untuk setiap dequeue
2. **Menggunakan Circular Queue** → Solusi optimal (dibahas di bagian selanjutnya)

---

### SOLVED PROBLEM 3 ⭐

**Soal:** Pada array queue dengan capacity 6, jelaskan kondisi false overflow!

**Penyelesaian:**

![Solved Problem 3 - False Overflow](images/p06-04-solved-problem-3-false-overflow.png)

*Gambar: Ilustrasi False Overflow pada Array Linear Queue*


Penjelasan:
- **State 1**: Queue awalnya berisi [10, 20, 30, 40, 50] dengan front=0 dan rear=4
- **State 2**: Setelah 3x dequeue, indeks 0, 1, 2 kosong, front=3, rear=4

Meskipun indeks 0, 1, 2 kosong, kita tidak bisa enqueue karena `rear` sudah di posisi 4 dan kondisi `isFull()` yang mengecek `rear >= capacity - 1` akan menghalangi.

**Kesimpulan:** 3 slot terbuang sia-sia (false overflow).

---

### SOLVED PROBLEM 4 ⭐⭐

**Soal:** Modifikasi fungsi `enqueue()` pada array linear dengan menambahkan fitur "shift elements" untuk mengatasi false overflow. Analisis kompleksitasnya!

**Penyelesaian:**

```cpp
void enqueueWithShift(const T& item) {
    if (count >= capacity) {
        throw overflow_error("Queue benar-benar penuh!");
    }
    
    // Jika rear sudah di akhir tapi masih ada ruang
    if (rearIndex >= capacity - 1 && frontIndex > 0) {
        // Geser semua elemen ke depan
        int shift = frontIndex;
        for (int i = frontIndex; i <= rearIndex; i++) {
            data[i - shift] = data[i];
        }
        frontIndex = 0;
        rearIndex = count - 1;
    }
    
    // Enqueue normal
    rearIndex++;
    data[rearIndex] = item;
    count++;
}
```

**Analisis Kompleksitas:**
- **Best case:** O(1) - tidak perlu shift
- **Worst case:** O(n) - perlu shift semua elemen
- **Average case:** Amortized O(1) jika shift jarang terjadi

---

## 4. Circular Queue (Antrian Melingkar)

### 4.1 Konsep Circular Queue

> **Circular Queue** adalah implementasi queue menggunakan array di mana indeks "melingkar" kembali ke awal ketika mencapai akhir array, sehingga memanfaatkan slot yang sudah kosong.

![Konsep Circular Queue](images/p06-05-circular-queue-concept.png)

*Gambar 4.1: Konsep circular queue sebagai array melingkar*


### 4.2 Formula Penting

Untuk circular queue dengan capacity `N`:

| Formula | Kegunaan |
|---------|----------|
| `(rear + 1) % N` | Posisi rear berikutnya |
| `(front + 1) % N` | Posisi front berikutnya |
| `(rear - front + N) % N` | Menghitung jumlah elemen |

### 4.3 Implementasi Circular Queue

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

template <typename T>
class CircularQueue {
private:
    T* data;
    int frontIndex;
    int rearIndex;
    int capacity;
    int count;

public:
    // Constructor
    CircularQueue(int size = 100) {
        capacity = size;
        data = new T[capacity];
        frontIndex = 0;
        rearIndex = -1;
        count = 0;
    }

    // Destructor
    ~CircularQueue() {
        delete[] data;
    }

    // Menambahkan elemen ke rear (circular)
    void enqueue(const T& item) {
        if (isFull()) {
            throw overflow_error("Queue penuh!");
        }
        // Formula circular: gerakkan rear secara melingkar
        rearIndex = (rearIndex + 1) % capacity;
        data[rearIndex] = item;
        count++;
    }

    // Menghapus dan mengembalikan elemen dari front
    T dequeue() {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        T item = data[frontIndex];
        // Formula circular: gerakkan front secara melingkar
        frontIndex = (frontIndex + 1) % capacity;
        count--;
        return item;
    }

    // Melihat elemen di front
    T front() const {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        return data[frontIndex];
    }

    // Melihat elemen di rear
    T rear() const {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        return data[rearIndex];
    }

    // Mengecek apakah queue kosong
    bool isEmpty() const {
        return count == 0;
    }

    // Mengecek apakah queue penuh
    bool isFull() const {
        return count == capacity;
    }

    // Mengembalikan jumlah elemen
    int size() const {
        return count;
    }

    // Menampilkan isi queue
    void display() const {
        if (isEmpty()) {
            cout << "Queue kosong" << endl;
            return;
        }
        cout << "Queue: [";
        int i = frontIndex;
        for (int j = 0; j < count; j++) {
            cout << data[i];
            if (j < count - 1) cout << ", ";
            i = (i + 1) % capacity;
        }
        cout << "]" << endl;
        cout << "Front index: " << frontIndex << ", Rear index: " << rearIndex << endl;
    }
};

// Contoh penggunaan
int main() {
    CircularQueue<int> cq(5);

    cq.enqueue(10);
    cq.enqueue(20);
    cq.enqueue(30);
    cq.enqueue(40);
    cq.enqueue(50);
    cq.display();  // Queue: [10, 20, 30, 40, 50]

    cout << "Dequeue: " << cq.dequeue() << endl;  // 10
    cout << "Dequeue: " << cq.dequeue() << endl;  // 20
    cq.display();  // Queue: [30, 40, 50]

    // Sekarang bisa enqueue lagi karena circular!
    cq.enqueue(60);
    cq.enqueue(70);
    cq.display();  // Queue: [30, 40, 50, 60, 70]

    return 0;
}
```

### 4.4 Visualisasi Operasi Circular Queue

![Operasi Circular Queue](images/p06-06-circular-queue-operations.png)

*Gambar 4.2: Langkah-langkah operasi pada circular queue*


---

### SOLVED PROBLEM 5 ⭐⭐

**Soal:** Pada circular queue dengan capacity 5, lakukan operasi berikut dan tunjukkan kondisi front, rear, serta isi array setiap langkah:
```
enqueue(A), enqueue(B), enqueue(C), dequeue(), dequeue(), enqueue(D), enqueue(E), enqueue(F)
```

**Penyelesaian:**

| Langkah | Operasi | Array | front | rear | count |
|---------|---------|-------|-------|------|-------|
| 0 | Initial | [-, -, -, -, -] | 0 | -1 | 0 |
| 1 | enqueue(A) | [A, -, -, -, -] | 0 | 0 | 1 |
| 2 | enqueue(B) | [A, B, -, -, -] | 0 | 1 | 2 |
| 3 | enqueue(C) | [A, B, C, -, -] | 0 | 2 | 3 |
| 4 | dequeue()→A | [-, B, C, -, -] | 1 | 2 | 2 |
| 5 | dequeue()→B | [-, -, C, -, -] | 2 | 2 | 1 |
| 6 | enqueue(D) | [-, -, C, D, -] | 2 | 3 | 2 |
| 7 | enqueue(E) | [-, -, C, D, E] | 2 | 4 | 3 |
| 8 | enqueue(F) | [F, -, C, D, E] | 2 | 0 | 4 |

**Perhatikan:** Pada langkah 8, rear "melingkar" dari indeks 4 ke indeks 0!

Urutan elemen dalam queue: C → D → E → F (dari front ke rear)

---

### SOLVED PROBLEM 6 ⭐⭐

**Soal:** Mengapa pada circular queue kita menggunakan variabel `count` terpisah? Apa masalah jika hanya menggunakan `front` dan `rear`?

**Penyelesaian:**

**Masalah tanpa variabel count:**

Jika hanya menggunakan `front` dan `rear`, kondisi **queue kosong** dan **queue penuh** menjadi ambigu:

1. **Queue kosong:** `front` dan `rear` berada di posisi yang sama setelah semua elemen di-dequeue
2. **Queue penuh:** `(rear + 1) % capacity == front`

```
Kondisi ambigu:
front = rear bisa berarti:
- Queue kosong (setelah dequeue terakhir)
- Queue dengan 1 elemen
```

**Solusi alternatif tanpa variabel count:**
1. **Sisakan 1 slot kosong:** Queue penuh jika `(rear + 2) % capacity == front`. Ini membuang 1 slot.
2. **Gunakan flag boolean:** `bool wasLastOperationEnqueue`

**Dengan variabel count:**
- `isEmpty(): count == 0`
- `isFull(): count == capacity`

Ini lebih jelas dan tidak membuang slot.

---

### SOLVED PROBLEM 7 ⭐

**Soal:** Hitung kompleksitas waktu dan ruang untuk circular queue!

**Penyelesaian:**

**Kompleksitas Waktu:**

| Operasi | Kompleksitas | Penjelasan |
|---------|-------------|------------|
| `enqueue()` | O(1) | Hanya update rear dan count |
| `dequeue()` | O(1) | Hanya update front dan count |
| `front()` | O(1) | Akses langsung |
| `rear()` | O(1) | Akses langsung |
| `isEmpty()` | O(1) | Cek count |
| `isFull()` | O(1) | Cek count |
| `size()` | O(1) | Return count |

**Kompleksitas Ruang:**
- O(n) di mana n adalah capacity array

**Keuntungan dibanding array linear:**
- Tidak ada false overflow
- Semua operasi tetap O(1)
- Pemanfaatan memori optimal

---

## 5. Implementasi Queue dengan Linked List

### 5.1 Konsep Queue dengan Linked List

> Queue dengan linked list menggunakan pointer `front` menunjuk ke node pertama dan pointer `rear` menunjuk ke node terakhir. Enqueue dilakukan di rear, dequeue dilakukan di front.

![Queue dengan Linked List](images/p06-07-queue-linked-list.png)

*Gambar 5.1: Representasi queue dengan linked list*


### 5.2 Implementasi Lengkap

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

template <typename T>
class LinkedQueue {
private:
    // Definisi Node
    struct Node {
        T data;
        Node* next;
        Node(const T& value) : data(value), next(nullptr) {}
    };

    Node* frontPtr;
    Node* rearPtr;
    int count;

public:
    // Constructor
    LinkedQueue() : frontPtr(nullptr), rearPtr(nullptr), count(0) {}

    // Destructor
    ~LinkedQueue() {
        while (!isEmpty()) {
            dequeue();
        }
    }

    // Menambahkan elemen ke rear
    void enqueue(const T& item) {
        Node* newNode = new Node(item);
        
        if (isEmpty()) {
            // Queue kosong: front dan rear sama
            frontPtr = newNode;
            rearPtr = newNode;
        } else {
            // Tambahkan di belakang rear
            rearPtr->next = newNode;
            rearPtr = newNode;
        }
        count++;
    }

    // Menghapus dan mengembalikan elemen dari front
    T dequeue() {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        
        Node* temp = frontPtr;
        T item = temp->data;
        
        frontPtr = frontPtr->next;
        
        // Jika queue menjadi kosong
        if (frontPtr == nullptr) {
            rearPtr = nullptr;
        }
        
        delete temp;
        count--;
        return item;
    }

    // Melihat elemen di front
    T front() const {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        return frontPtr->data;
    }

    // Melihat elemen di rear
    T rear() const {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        return rearPtr->data;
    }

    // Mengecek apakah queue kosong
    bool isEmpty() const {
        return frontPtr == nullptr;
    }

    // Queue linked list tidak pernah penuh (selama ada memori)
    bool isFull() const {
        return false;
    }

    // Mengembalikan jumlah elemen
    int size() const {
        return count;
    }

    // Menampilkan isi queue
    void display() const {
        if (isEmpty()) {
            cout << "Queue kosong" << endl;
            return;
        }
        cout << "Queue: FRONT -> [";
        Node* current = frontPtr;
        while (current != nullptr) {
            cout << current->data;
            if (current->next != nullptr) cout << ", ";
            current = current->next;
        }
        cout << "] <- REAR" << endl;
    }
};

// Contoh penggunaan
int main() {
    LinkedQueue<string> messageQueue;

    // Simulasi antrian pesan
    messageQueue.enqueue("Pesan Alpha");
    messageQueue.enqueue("Pesan Bravo");
    messageQueue.enqueue("Pesan Charlie");
    messageQueue.display();

    cout << "Memproses: " << messageQueue.dequeue() << endl;
    cout << "Memproses: " << messageQueue.dequeue() << endl;
    messageQueue.display();

    messageQueue.enqueue("Pesan Delta");
    messageQueue.display();

    return 0;
}
```

### 5.3 Perbandingan Implementasi Queue

| Aspek | Array Linear | Circular Array | Linked List |
|-------|--------------|----------------|-------------|
| **Enqueue** | O(1) | O(1) | O(1) |
| **Dequeue** | O(1) | O(1) | O(1) |
| **Ukuran** | Fixed | Fixed | Dynamic |
| **Memori** | Pre-allocated | Pre-allocated | On-demand |
| **False Overflow** | Ya | Tidak | Tidak ada |
| **Cache Locality** | Baik | Baik | Buruk |
| **Overhead per elemen** | Tidak ada | Tidak ada | Pointer (8 byte) |

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Implementasikan fungsi untuk membalik isi queue menggunakan stack tambahan!

**Penyelesaian:**

```cpp
#include <stack>

template <typename T>
void reverseQueue(LinkedQueue<T>& queue) {
    stack<T> tempStack;
    
    // Pindahkan semua elemen dari queue ke stack
    while (!queue.isEmpty()) {
        tempStack.push(queue.dequeue());
    }
    
    // Pindahkan kembali dari stack ke queue
    // Karena stack LIFO, urutan akan terbalik
    while (!tempStack.empty()) {
        queue.enqueue(tempStack.top());
        tempStack.pop();
    }
}

// Contoh penggunaan
int main() {
    LinkedQueue<int> q;
    q.enqueue(1);
    q.enqueue(2);
    q.enqueue(3);
    q.enqueue(4);
    
    cout << "Sebelum reverse: ";
    q.display();  // 1, 2, 3, 4
    
    reverseQueue(q);
    
    cout << "Setelah reverse: ";
    q.display();  // 4, 3, 2, 1
    
    return 0;
}
```

**Analisis:**
- Waktu: O(n) - setiap elemen dipindah 2 kali
- Ruang: O(n) - stack tambahan menyimpan semua elemen

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Implementasikan queue menggunakan dua stack! (Stack yang dipelajari di Pertemuan 5)

**Penyelesaian:**

Ide: Gunakan dua stack - satu untuk enqueue dan satu untuk dequeue.

```cpp
#include <stack>
#include <stdexcept>
using namespace std;

template <typename T>
class QueueUsingTwoStacks {
private:
    stack<T> stackIn;   // Untuk enqueue
    stack<T> stackOut;  // Untuk dequeue

    // Transfer dari stackIn ke stackOut jika stackOut kosong
    void transfer() {
        while (!stackIn.empty()) {
            stackOut.push(stackIn.top());
            stackIn.pop();
        }
    }

public:
    void enqueue(const T& item) {
        stackIn.push(item);  // Selalu push ke stackIn
    }

    T dequeue() {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        
        // Jika stackOut kosong, transfer dari stackIn
        if (stackOut.empty()) {
            transfer();
        }
        
        T item = stackOut.top();
        stackOut.pop();
        return item;
    }

    T front() {
        if (isEmpty()) {
            throw underflow_error("Queue kosong!");
        }
        
        if (stackOut.empty()) {
            transfer();
        }
        
        return stackOut.top();
    }

    bool isEmpty() const {
        return stackIn.empty() && stackOut.empty();
    }

    int size() const {
        return stackIn.size() + stackOut.size();
    }
};
```

**Analisis Kompleksitas:**
- **Enqueue:** O(1) - selalu
- **Dequeue:** 
  - Amortized O(1) - setiap elemen dipindah paling banyak 2 kali
  - Worst case O(n) - saat transfer

**Ilustrasi:**
```
enqueue(1): stackIn=[1], stackOut=[]
enqueue(2): stackIn=[1,2], stackOut=[]
enqueue(3): stackIn=[1,2,3], stackOut=[]
dequeue(): transfer → stackIn=[], stackOut=[3,2,1] → return 1
dequeue(): stackIn=[], stackOut=[3,2] → return 2
enqueue(4): stackIn=[4], stackOut=[3,2]
dequeue(): stackIn=[4], stackOut=[3] → return 3
```

---

### SOLVED PROBLEM 10 ⭐⭐⭐

**Soal:** Pada linked queue, mengapa kita memerlukan pointer `rear` terpisah? Bagaimana jika hanya menggunakan pointer `front`?

**Penyelesaian:**

**Tanpa pointer rear:**

```cpp
// Enqueue tanpa rear - TIDAK EFISIEN!
void enqueueWithoutRear(const T& item) {
    Node* newNode = new Node(item);
    
    if (isEmpty()) {
        frontPtr = newNode;
    } else {
        // Harus traverse sampai akhir
        Node* current = frontPtr;
        while (current->next != nullptr) {
            current = current->next;
        }
        current->next = newNode;
    }
    count++;
}
// Kompleksitas: O(n) - harus traverse!
```

**Dengan pointer rear:**

```cpp
// Enqueue dengan rear - EFISIEN!
void enqueue(const T& item) {
    Node* newNode = new Node(item);
    
    if (isEmpty()) {
        frontPtr = newNode;
        rearPtr = newNode;
    } else {
        rearPtr->next = newNode;
        rearPtr = newNode;
    }
    count++;
}
// Kompleksitas: O(1) - akses langsung!
```

**Kesimpulan:**
- Dengan rear: enqueue O(1)
- Tanpa rear: enqueue O(n)

Pointer rear adalah **trade-off** yang baik: sedikit memori tambahan (1 pointer) untuk peningkatan performa signifikan.

---

## 6. Deque (Double-Ended Queue)

### 6.1 Konsep Deque

> **Deque** (dibaca "deck") adalah struktur data yang memungkinkan penyisipan dan penghapusan dari **kedua ujung** (front dan rear).

![Konsep Deque](images/p06-08-deque-concept.png)

*Gambar 6.1: Ilustrasi operasi pada deque*


### 6.2 Operasi Deque

| Operasi | Deskripsi |
|---------|-----------|
| `insertFront(item)` | Sisipkan di depan |
| `insertRear(item)` | Sisipkan di belakang |
| `deleteFront()` | Hapus dari depan |
| `deleteRear()` | Hapus dari belakang |
| `getFront()` | Lihat elemen depan |
| `getRear()` | Lihat elemen belakang |
| `isEmpty()` | Cek kosong |
| `size()` | Jumlah elemen |

### 6.3 Variasi Deque

| Jenis | Operasi yang Diizinkan |
|-------|------------------------|
| **Input-Restricted Deque** | Insert hanya di satu ujung, delete di kedua ujung |
| **Output-Restricted Deque** | Insert di kedua ujung, delete hanya di satu ujung |

**Catatan:** Stack dan Queue adalah kasus khusus dari Deque:
- **Stack** = Deque dengan operasi hanya di satu ujung
- **Queue** = Deque dengan insert di satu ujung, delete di ujung lain

### 6.4 Implementasi Deque dengan Circular Array

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

template <typename T>
class Deque {
private:
    T* data;
    int frontIndex;
    int rearIndex;
    int capacity;
    int count;

public:
    Deque(int size = 100) {
        capacity = size;
        data = new T[capacity];
        frontIndex = 0;
        rearIndex = capacity - 1;
        count = 0;
    }

    ~Deque() {
        delete[] data;
    }

    // Sisipkan di depan
    void insertFront(const T& item) {
        if (isFull()) {
            throw overflow_error("Deque penuh!");
        }
        // Geser front ke belakang (circular)
        frontIndex = (frontIndex - 1 + capacity) % capacity;
        data[frontIndex] = item;
        count++;
    }

    // Sisipkan di belakang
    void insertRear(const T& item) {
        if (isFull()) {
            throw overflow_error("Deque penuh!");
        }
        // Geser rear ke depan (circular)
        rearIndex = (rearIndex + 1) % capacity;
        data[rearIndex] = item;
        count++;
    }

    // Hapus dari depan
    T deleteFront() {
        if (isEmpty()) {
            throw underflow_error("Deque kosong!");
        }
        T item = data[frontIndex];
        frontIndex = (frontIndex + 1) % capacity;
        count--;
        return item;
    }

    // Hapus dari belakang
    T deleteRear() {
        if (isEmpty()) {
            throw underflow_error("Deque kosong!");
        }
        T item = data[rearIndex];
        rearIndex = (rearIndex - 1 + capacity) % capacity;
        count--;
        return item;
    }

    T getFront() const {
        if (isEmpty()) throw underflow_error("Deque kosong!");
        return data[frontIndex];
    }

    T getRear() const {
        if (isEmpty()) throw underflow_error("Deque kosong!");
        return data[rearIndex];
    }

    bool isEmpty() const { return count == 0; }
    bool isFull() const { return count == capacity; }
    int size() const { return count; }

    void display() const {
        if (isEmpty()) {
            cout << "Deque kosong" << endl;
            return;
        }
        cout << "Deque: FRONT -> [";
        int i = frontIndex;
        for (int j = 0; j < count; j++) {
            cout << data[i];
            if (j < count - 1) cout << ", ";
            i = (i + 1) % capacity;
        }
        cout << "] <- REAR" << endl;
    }
};

int main() {
    Deque<int> dq(5);

    dq.insertRear(10);
    dq.insertRear(20);
    dq.insertFront(5);
    dq.display();  // [5, 10, 20]

    dq.insertFront(1);
    dq.insertRear(30);
    dq.display();  // [1, 5, 10, 20, 30]

    cout << "Delete front: " << dq.deleteFront() << endl;  // 1
    cout << "Delete rear: " << dq.deleteRear() << endl;    // 30
    dq.display();  // [5, 10, 20]

    return 0;
}
```

---

### SOLVED PROBLEM 11 ⭐

**Soal:** Bagaimana cara mengimplementasikan Stack menggunakan Deque?

**Penyelesaian:**

```cpp
template <typename T>
class StackUsingDeque {
private:
    Deque<T> deque;

public:
    void push(const T& item) {
        deque.insertRear(item);  // Atau insertFront
    }

    T pop() {
        return deque.deleteRear();  // Atau deleteFront
    }

    T top() {
        return deque.getRear();  // Atau getFront
    }

    bool isEmpty() {
        return deque.isEmpty();
    }
};
```

Karena Stack hanya menggunakan satu ujung, kita bisa pilih ujung mana saja dari Deque.

---

### SOLVED PROBLEM 12 ⭐

**Soal:** Bagaimana cara mengimplementasikan Queue menggunakan Deque?

**Penyelesaian:**

```cpp
template <typename T>
class QueueUsingDeque {
private:
    Deque<T> deque;

public:
    void enqueue(const T& item) {
        deque.insertRear(item);
    }

    T dequeue() {
        return deque.deleteFront();
    }

    T front() {
        return deque.getFront();
    }

    bool isEmpty() {
        return deque.isEmpty();
    }
};
```

Queue menggunakan dua ujung berbeda: insert di rear, delete di front.

---

## 7. Aplikasi Queue

### 7.1 Simulasi Antrian (Queue Simulation)

Salah satu aplikasi paling umum queue adalah simulasi antrian pelayanan.

**Contoh: Simulasi Antrian Posko Komando**

```cpp
#include <iostream>
#include <queue>
#include <string>
#include <ctime>
#include <cstdlib>
using namespace std;

struct Laporan {
    int id;
    string jenis;      // "Darurat", "Prioritas", "Normal"
    string pengirim;
    int waktuMasuk;
};

class PoskoAntrian {
private:
    queue<Laporan> antrianDarurat;
    queue<Laporan> antrianPrioritas;
    queue<Laporan> antrianNormal;
    int idCounter;
    int waktuSekarang;

public:
    PoskoAntrian() : idCounter(0), waktuSekarang(0) {}

    void terimaLaporan(const string& jenis, const string& pengirim) {
        Laporan lap = {++idCounter, jenis, pengirim, waktuSekarang};
        
        if (jenis == "Darurat") {
            antrianDarurat.push(lap);
        } else if (jenis == "Prioritas") {
            antrianPrioritas.push(lap);
        } else {
            antrianNormal.push(lap);
        }
        
        cout << "[T=" << waktuSekarang << "] Laporan #" << lap.id 
             << " (" << jenis << ") dari " << pengirim << " diterima." << endl;
    }

    void prosesLaporan() {
        Laporan lap;
        string dari;
        
        // Prioritas: Darurat > Prioritas > Normal
        if (!antrianDarurat.empty()) {
            lap = antrianDarurat.front();
            antrianDarurat.pop();
            dari = "Antrian Darurat";
        } else if (!antrianPrioritas.empty()) {
            lap = antrianPrioritas.front();
            antrianPrioritas.pop();
            dari = "Antrian Prioritas";
        } else if (!antrianNormal.empty()) {
            lap = antrianNormal.front();
            antrianNormal.pop();
            dari = "Antrian Normal";
        } else {
            cout << "[T=" << waktuSekarang << "] Tidak ada laporan untuk diproses." << endl;
            return;
        }
        
        int waktuTunggu = waktuSekarang - lap.waktuMasuk;
        cout << "[T=" << waktuSekarang << "] Memproses Laporan #" << lap.id 
             << " dari " << dari << " (tunggu: " << waktuTunggu << " menit)" << endl;
    }

    void majukanWaktu(int menit) {
        waktuSekarang += menit;
    }

    void tampilkanStatus() {
        cout << "\n=== Status Antrian (T=" << waktuSekarang << ") ===" << endl;
        cout << "Darurat: " << antrianDarurat.size() << " laporan" << endl;
        cout << "Prioritas: " << antrianPrioritas.size() << " laporan" << endl;
        cout << "Normal: " << antrianNormal.size() << " laporan" << endl;
    }
};

int main() {
    PoskoAntrian posko;

    // Simulasi penerimaan laporan
    posko.terimaLaporan("Normal", "Pos Alpha");
    posko.majukanWaktu(2);
    posko.terimaLaporan("Darurat", "Pos Bravo");
    posko.majukanWaktu(1);
    posko.terimaLaporan("Prioritas", "Pos Charlie");
    posko.majukanWaktu(1);
    posko.terimaLaporan("Normal", "Pos Delta");
    
    posko.tampilkanStatus();

    // Simulasi pemrosesan
    cout << "\n=== Mulai Pemrosesan ===" << endl;
    posko.majukanWaktu(2);
    posko.prosesLaporan();  // Darurat diproses duluan
    posko.majukanWaktu(3);
    posko.prosesLaporan();  // Prioritas
    posko.majukanWaktu(3);
    posko.prosesLaporan();  // Normal (yang pertama masuk)
    posko.majukanWaktu(3);
    posko.prosesLaporan();  // Normal (yang kedua)
    
    posko.tampilkanStatus();

    return 0;
}
```

### 7.2 BFS (Breadth-First Search) Traversal

Queue adalah struktur data utama dalam algoritma BFS. Topik ini akan dibahas lebih lanjut pada Pertemuan 11 (Tree) dan mata kuliah Kecerdasan Artifisial di Semester 4.

**Preview singkat:**

```cpp
// Pseudocode BFS
void BFS(Graph& graph, int startVertex) {
    queue<int> q;
    bool visited[MAX_VERTICES] = {false};
    
    visited[startVertex] = true;
    q.push(startVertex);
    
    while (!q.empty()) {
        int current = q.front();
        q.pop();
        process(current);
        
        for (each neighbor of current) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                q.push(neighbor);
            }
        }
    }
}
```

### 7.3 Task Scheduling dan Buffer

**Round-Robin Scheduling:**

```cpp
#include <iostream>
#include <queue>
#include <string>
using namespace std;

struct Process {
    string name;
    int burstTime;     // Waktu yang dibutuhkan
    int remainingTime; // Sisa waktu
};

void roundRobinScheduling(queue<Process>& processQueue, int timeQuantum) {
    int totalTime = 0;
    
    while (!processQueue.empty()) {
        Process p = processQueue.front();
        processQueue.pop();
        
        int execTime = min(timeQuantum, p.remainingTime);
        p.remainingTime -= execTime;
        totalTime += execTime;
        
        cout << "Waktu " << totalTime << ": Proses " << p.name 
             << " dieksekusi " << execTime << " unit";
        
        if (p.remainingTime > 0) {
            cout << " (sisa: " << p.remainingTime << ")" << endl;
            processQueue.push(p);  // Kembali ke antrian
        } else {
            cout << " - SELESAI" << endl;
        }
    }
}

int main() {
    queue<Process> pq;
    pq.push({"P1", 10, 10});
    pq.push({"P2", 5, 5});
    pq.push({"P3", 8, 8});
    
    int quantum = 3;
    cout << "Round-Robin Scheduling (Quantum = " << quantum << ")" << endl;
    cout << "===========================================" << endl;
    roundRobinScheduling(pq, quantum);
    
    return 0;
}
```

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Dalam sistem komunikasi militer, pesan memiliki 3 level prioritas: FLASH (tertinggi), IMMEDIATE, dan ROUTINE. Implementasikan sistem antrian pesan dengan prioritas!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <string>
using namespace std;

enum Priority { FLASH = 0, IMMEDIATE = 1, ROUTINE = 2 };

struct Message {
    int id;
    string content;
    Priority priority;
    string sender;
};

class MilitaryMessageQueue {
private:
    queue<Message> flashQueue;
    queue<Message> immediateQueue;
    queue<Message> routineQueue;
    int messageCounter;

public:
    MilitaryMessageQueue() : messageCounter(0) {}

    void sendMessage(const string& content, Priority priority, const string& sender) {
        Message msg = {++messageCounter, content, priority, sender};
        
        switch (priority) {
            case FLASH:
                flashQueue.push(msg);
                cout << "[FLASH] ";
                break;
            case IMMEDIATE:
                immediateQueue.push(msg);
                cout << "[IMMEDIATE] ";
                break;
            case ROUTINE:
                routineQueue.push(msg);
                cout << "[ROUTINE] ";
                break;
        }
        cout << "Pesan #" << msg.id << " dari " << sender << " ditambahkan." << endl;
    }

    Message processNextMessage() {
        Message msg;
        
        if (!flashQueue.empty()) {
            msg = flashQueue.front();
            flashQueue.pop();
            cout << "[PROSES FLASH] ";
        } else if (!immediateQueue.empty()) {
            msg = immediateQueue.front();
            immediateQueue.pop();
            cout << "[PROSES IMMEDIATE] ";
        } else if (!routineQueue.empty()) {
            msg = routineQueue.front();
            routineQueue.pop();
            cout << "[PROSES ROUTINE] ";
        } else {
            throw runtime_error("Tidak ada pesan!");
        }
        
        cout << "Pesan #" << msg.id << ": " << msg.content << endl;
        return msg;
    }

    int totalPending() const {
        return flashQueue.size() + immediateQueue.size() + routineQueue.size();
    }
};

int main() {
    MilitaryMessageQueue mq;

    mq.sendMessage("Laporan rutin harian", ROUTINE, "Pos A");
    mq.sendMessage("Pergerakan musuh terdeteksi!", FLASH, "Radar B");
    mq.sendMessage("Request logistik", IMMEDIATE, "Pos C");
    mq.sendMessage("Kontak dengan musuh!", FLASH, "Unit D");

    cout << "\n=== Memproses Pesan ===" << endl;
    while (mq.totalPending() > 0) {
        mq.processNextMessage();
    }

    return 0;
}
```

**Output:**
```
[ROUTINE] Pesan #1 dari Pos A ditambahkan.
[FLASH] Pesan #2 dari Radar B ditambahkan.
[IMMEDIATE] Pesan #3 dari Pos C ditambahkan.
[FLASH] Pesan #4 dari Unit D ditambahkan.

=== Memproses Pesan ===
[PROSES FLASH] Pesan #2: Pergerakan musuh terdeteksi!
[PROSES FLASH] Pesan #4: Kontak dengan musuh!
[PROSES IMMEDIATE] Pesan #3: Request logistik
[PROSES ROUTINE] Pesan #1: Laporan rutin harian
```

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Implementasikan fungsi untuk menggabungkan dua queue yang sudah terurut menjadi satu queue terurut!

**Penyelesaian:**

```cpp
#include <queue>
using namespace std;

queue<int> mergeSortedQueues(queue<int>& q1, queue<int>& q2) {
    queue<int> result;
    
    while (!q1.empty() && !q2.empty()) {
        if (q1.front() <= q2.front()) {
            result.push(q1.front());
            q1.pop();
        } else {
            result.push(q2.front());
            q2.pop();
        }
    }
    
    // Sisa elemen dari q1
    while (!q1.empty()) {
        result.push(q1.front());
        q1.pop();
    }
    
    // Sisa elemen dari q2
    while (!q2.empty()) {
        result.push(q2.front());
        q2.pop();
    }
    
    return result;
}

int main() {
    queue<int> q1, q2;
    
    // q1: 1, 3, 5, 7
    q1.push(1); q1.push(3); q1.push(5); q1.push(7);
    
    // q2: 2, 4, 6, 8, 10
    q2.push(2); q2.push(4); q2.push(6); q2.push(8); q2.push(10);
    
    queue<int> merged = mergeSortedQueues(q1, q2);
    
    cout << "Merged queue: ";
    while (!merged.empty()) {
        cout << merged.front() << " ";
        merged.pop();
    }
    // Output: 1 2 3 4 5 6 7 8 10
    
    return 0;
}
```

**Kompleksitas:**
- Waktu: O(n + m) di mana n dan m adalah ukuran kedua queue
- Ruang: O(n + m) untuk queue hasil

---

### SOLVED PROBLEM 15 ⭐⭐⭐

**Soal:** Implementasikan "Hot Potato" game menggunakan circular queue. N orang berdiri melingkar dan menghitung dari 1 sampai K. Orang ke-K tersingkir dan permainan dilanjutkan sampai tersisa 1 orang.

**Penyelesaian:**

Ini adalah variasi dari **Josephus Problem**.

```cpp
#include <iostream>
#include <queue>
#include <string>
using namespace std;

string hotPotatoGame(queue<string>& players, int k) {
    while (players.size() > 1) {
        // Lewati k-1 orang
        for (int i = 0; i < k - 1; i++) {
            string player = players.front();
            players.pop();
            players.push(player);  // Pindah ke belakang
        }
        
        // Orang ke-k tersingkir
        string eliminated = players.front();
        players.pop();
        cout << eliminated << " tersingkir!" << endl;
    }
    
    return players.front();
}

int main() {
    queue<string> players;
    players.push("Alpha");
    players.push("Bravo");
    players.push("Charlie");
    players.push("Delta");
    players.push("Echo");
    players.push("Foxtrot");
    
    int k = 3;  // Setiap hitungan ke-3
    
    cout << "=== Hot Potato Game (K=" << k << ") ===" << endl;
    string winner = hotPotatoGame(players, k);
    cout << "\nPemenang: " << winner << endl;
    
    return 0;
}
```

**Trace untuk N=6, K=3:**
```
Awal: [Alpha, Bravo, Charlie, Delta, Echo, Foxtrot]
Hitung 1-2-3: Charlie tersingkir
Sisa: [Delta, Echo, Foxtrot, Alpha, Bravo]
Hitung 1-2-3: Foxtrot tersingkir
Sisa: [Alpha, Bravo, Delta, Echo]
Hitung 1-2-3: Delta tersingkir
Sisa: [Echo, Alpha, Bravo]
Hitung 1-2-3: Alpha tersingkir
Sisa: [Bravo, Echo]
Hitung 1-2-3: Bravo tersingkir
Pemenang: Echo
```

---

### SOLVED PROBLEM 16 ⭐⭐

**Soal:** Implementasikan fungsi untuk mengecek apakah queue berbentuk palindrom tanpa menggunakan struktur data tambahan selain satu stack!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <stack>
using namespace std;

bool isQueuePalindrome(queue<int> q) {
    stack<int> s;
    int n = q.size();
    
    // Copy semua elemen ke stack
    queue<int> tempQ = q;
    while (!tempQ.empty()) {
        s.push(tempQ.front());
        tempQ.pop();
    }
    
    // Bandingkan queue (front to back) dengan stack (back to front)
    while (!q.empty()) {
        if (q.front() != s.top()) {
            return false;
        }
        q.pop();
        s.pop();
    }
    
    return true;
}

int main() {
    queue<int> q1, q2;
    
    // Queue palindrom: 1, 2, 3, 2, 1
    q1.push(1); q1.push(2); q1.push(3); q1.push(2); q1.push(1);
    
    // Queue bukan palindrom: 1, 2, 3, 4, 5
    q2.push(1); q2.push(2); q2.push(3); q2.push(4); q2.push(5);
    
    cout << "Queue 1 palindrom? " << (isQueuePalindrome(q1) ? "Ya" : "Tidak") << endl;
    cout << "Queue 2 palindrom? " << (isQueuePalindrome(q2) ? "Ya" : "Tidak") << endl;
    
    return 0;
}
```

---

### SOLVED PROBLEM 17 ⭐⭐

**Soal:** Implementasikan fungsi untuk merotasi queue sebanyak K posisi ke kiri (elemen depan pindah ke belakang)!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
using namespace std;

void rotateLeft(queue<int>& q, int k) {
    int n = q.size();
    k = k % n;  // Handle k > n
    
    for (int i = 0; i < k; i++) {
        int front = q.front();
        q.pop();
        q.push(front);
    }
}

void printQueue(queue<int> q) {
    cout << "[";
    while (!q.empty()) {
        cout << q.front();
        q.pop();
        if (!q.empty()) cout << ", ";
    }
    cout << "]" << endl;
}

int main() {
    queue<int> q;
    for (int i = 1; i <= 5; i++) q.push(i);
    
    cout << "Awal: ";
    printQueue(q);  // [1, 2, 3, 4, 5]
    
    rotateLeft(q, 2);
    
    cout << "Setelah rotasi 2 ke kiri: ";
    printQueue(q);  // [3, 4, 5, 1, 2]
    
    return 0;
}
```

**Kompleksitas:** O(k) waktu, O(1) ruang tambahan

---

### SOLVED PROBLEM 18 ⭐⭐⭐

**Soal:** Implementasikan queue yang mendukung operasi getMin() dalam O(1) dengan memanfaatkan deque tambahan!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <deque>
#include <stdexcept>
using namespace std;

class MinQueue {
private:
    queue<int> mainQueue;
    deque<int> minDeque;  // Menyimpan kandidat minimum

public:
    void enqueue(int value) {
        mainQueue.push(value);
        
        // Hapus elemen dari belakang minDeque yang lebih besar dari value
        while (!minDeque.empty() && minDeque.back() > value) {
            minDeque.pop_back();
        }
        minDeque.push_back(value);
    }

    int dequeue() {
        if (mainQueue.empty()) {
            throw underflow_error("Queue kosong!");
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
            throw underflow_error("Queue kosong!");
        }
        return minDeque.front();
    }

    bool isEmpty() const {
        return mainQueue.empty();
    }
};

int main() {
    MinQueue mq;
    
    mq.enqueue(5);
    cout << "Min: " << mq.getMin() << endl;  // 5
    
    mq.enqueue(3);
    cout << "Min: " << mq.getMin() << endl;  // 3
    
    mq.enqueue(7);
    cout << "Min: " << mq.getMin() << endl;  // 3
    
    mq.enqueue(2);
    cout << "Min: " << mq.getMin() << endl;  // 2
    
    mq.dequeue();  // Remove 5
    cout << "Min: " << mq.getMin() << endl;  // 2
    
    mq.dequeue();  // Remove 3
    cout << "Min: " << mq.getMin() << endl;  // 2
    
    mq.dequeue();  // Remove 7
    cout << "Min: " << mq.getMin() << endl;  // 2
    
    return 0;
}
```

**Analisis:**
- `enqueue()`: Amortized O(1)
- `dequeue()`: O(1)
- `getMin()`: O(1)

---

### SOLVED PROBLEM 19 ⭐⭐

**Soal:** Implementasikan simulasi antrian di loket bank dengan 3 teller. Pelanggan yang datang akan dilayani oleh teller dengan antrian terpendek!

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <string>
#include <vector>
using namespace std;

struct Customer {
    int id;
    int arrivalTime;
    int serviceTime;  // Waktu layanan yang dibutuhkan
};

class BankSimulation {
private:
    vector<queue<Customer>> tellerQueues;
    int numTellers;
    int customerCount;
    int currentTime;

public:
    BankSimulation(int tellers) : numTellers(tellers), customerCount(0), currentTime(0) {
        tellerQueues.resize(tellers);
    }

    // Mencari teller dengan antrian terpendek
    int findShortestQueue() {
        int minIndex = 0;
        int minSize = tellerQueues[0].size();
        
        for (int i = 1; i < numTellers; i++) {
            if (tellerQueues[i].size() < minSize) {
                minSize = tellerQueues[i].size();
                minIndex = i;
            }
        }
        
        return minIndex;
    }

    void customerArrives(int serviceTime) {
        Customer c = {++customerCount, currentTime, serviceTime};
        int tellerId = findShortestQueue();
        tellerQueues[tellerId].push(c);
        
        cout << "[T=" << currentTime << "] Pelanggan #" << c.id 
             << " (butuh " << serviceTime << " menit) ke Teller " << (tellerId + 1)
             << " (antrian: " << tellerQueues[tellerId].size() << ")" << endl;
    }

    void processOneTick() {
        currentTime++;
        
        for (int i = 0; i < numTellers; i++) {
            if (!tellerQueues[i].empty()) {
                Customer& c = tellerQueues[i].front();
                c.serviceTime--;
                
                if (c.serviceTime == 0) {
                    int waitTime = currentTime - c.arrivalTime;
                    cout << "[T=" << currentTime << "] Teller " << (i + 1) 
                         << " selesai melayani Pelanggan #" << c.id 
                         << " (total waktu: " << waitTime << " menit)" << endl;
                    tellerQueues[i].pop();
                }
            }
        }
    }

    void displayStatus() {
        cout << "\n=== Status Antrian (T=" << currentTime << ") ===" << endl;
        for (int i = 0; i < numTellers; i++) {
            cout << "Teller " << (i + 1) << ": " << tellerQueues[i].size() << " pelanggan" << endl;
        }
        cout << endl;
    }

    bool hasCustomers() {
        for (int i = 0; i < numTellers; i++) {
            if (!tellerQueues[i].empty()) return true;
        }
        return false;
    }

    void advanceTime() { currentTime++; }
    int getTime() { return currentTime; }
};

int main() {
    BankSimulation bank(3);

    // Simulasi kedatangan pelanggan
    bank.customerArrives(5);  // Pelanggan 1 butuh 5 menit
    bank.advanceTime();
    bank.customerArrives(3);  // Pelanggan 2 butuh 3 menit
    bank.advanceTime();
    bank.customerArrives(4);  // Pelanggan 3 butuh 4 menit
    bank.customerArrives(2);  // Pelanggan 4 butuh 2 menit

    bank.displayStatus();

    // Jalankan simulasi sampai semua selesai
    cout << "=== Proses Pelayanan ===" << endl;
    while (bank.hasCustomers()) {
        bank.processOneTick();
    }

    return 0;
}
```

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Implementasikan sliding window maximum menggunakan deque. Diberikan array dan ukuran window K, temukan nilai maksimum di setiap window!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
#include <deque>
using namespace std;

vector<int> slidingWindowMaximum(vector<int>& nums, int k) {
    vector<int> result;
    deque<int> dq;  // Menyimpan indeks
    
    for (int i = 0; i < nums.size(); i++) {
        // Hapus elemen di luar window
        while (!dq.empty() && dq.front() <= i - k) {
            dq.pop_front();
        }
        
        // Hapus elemen yang lebih kecil dari elemen saat ini
        while (!dq.empty() && nums[dq.back()] < nums[i]) {
            dq.pop_back();
        }
        
        dq.push_back(i);
        
        // Tambahkan ke result jika window sudah lengkap
        if (i >= k - 1) {
            result.push_back(nums[dq.front()]);
        }
    }
    
    return result;
}

int main() {
    vector<int> nums = {1, 3, -1, -3, 5, 3, 6, 7};
    int k = 3;
    
    cout << "Array: ";
    for (int n : nums) cout << n << " ";
    cout << endl;
    
    vector<int> maxes = slidingWindowMaximum(nums, k);
    
    cout << "Sliding window maximum (K=" << k << "): ";
    for (int m : maxes) cout << m << " ";
    cout << endl;
    
    // Window positions:
    // [1, 3, -1] -> 3
    // [3, -1, -3] -> 3
    // [-1, -3, 5] -> 5
    // [-3, 5, 3] -> 5
    // [5, 3, 6] -> 6
    // [3, 6, 7] -> 7
    // Output: 3 3 5 5 6 7
    
    return 0;
}
```

**Kompleksitas:**
- Waktu: O(n) - setiap elemen masuk dan keluar deque maksimal 1 kali
- Ruang: O(k) untuk deque

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Soal:** Implementasikan sistem antrian dengan waktu kadaluwarsa! Setiap elemen memiliki TTL (Time To Live), dan elemen yang sudah melewati TTL harus otomatis dihapus.

**Penyelesaian:**

```cpp
#include <iostream>
#include <queue>
#include <ctime>
using namespace std;

template <typename T>
struct TimedElement {
    T data;
    time_t expiryTime;
};

template <typename T>
class ExpiringQueue {
private:
    queue<TimedElement<T>> q;

    // Hapus elemen yang sudah kadaluwarsa dari depan
    void purgeExpired() {
        time_t now = time(nullptr);
        while (!q.empty() && q.front().expiryTime <= now) {
            cout << "Elemen '" << q.front().data << "' kadaluwarsa dan dihapus." << endl;
            q.pop();
        }
    }

public:
    void enqueue(const T& item, int ttlSeconds) {
        TimedElement<T> elem;
        elem.data = item;
        elem.expiryTime = time(nullptr) + ttlSeconds;
        q.push(elem);
    }

    T dequeue() {
        purgeExpired();
        if (q.empty()) {
            throw runtime_error("Queue kosong atau semua elemen kadaluwarsa!");
        }
        T item = q.front().data;
        q.pop();
        return item;
    }

    T front() {
        purgeExpired();
        if (q.empty()) {
            throw runtime_error("Queue kosong!");
        }
        return q.front().data;
    }

    bool isEmpty() {
        purgeExpired();
        return q.empty();
    }

    int size() {
        purgeExpired();
        return q.size();
    }
};

// Demo (dalam praktik, gunakan sleep atau timer)
int main() {
    ExpiringQueue<string> eq;
    
    eq.enqueue("Pesan A", 5);  // TTL 5 detik
    eq.enqueue("Pesan B", 10); // TTL 10 detik
    eq.enqueue("Pesan C", 3);  // TTL 3 detik
    
    cout << "Queue size: " << eq.size() << endl;
    
    // Simulasi: Dalam aplikasi nyata, waktu akan berjalan
    // dan elemen akan otomatis kadaluwarsa
    
    return 0;
}
```

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Analisis kompleksitas waktu dan ruang untuk setiap implementasi queue. Buat tabel perbandingan lengkap!

**Penyelesaian:**

| Implementasi | Enqueue | Dequeue | Front | Rear | isEmpty | isFull | Space |
|--------------|---------|---------|-------|------|---------|--------|-------|
| **Array Linear** | O(1) | O(1) | O(1) | O(1) | O(1) | O(1) | O(n) |
| **Circular Array** | O(1) | O(1) | O(1) | O(1) | O(1) | O(1) | O(n) |
| **Linked List** | O(1) | O(1) | O(1) | O(1) | O(1) | O(1)* | O(n) |
| **Two Stacks** | O(1) | Amort O(1) | Amort O(1) | O(n) | O(1) | O(1) | O(n) |
| **Deque (Array)** | O(1) | O(1) | O(1) | O(1) | O(1) | O(1) | O(n) |

*Linked List isFull() selalu false kecuali memori habis.

**Catatan Penting:**
1. **Array Linear** memiliki masalah false overflow
2. **Circular Array** adalah pilihan terbaik untuk ukuran tetap
3. **Linked List** terbaik untuk ukuran dinamis
4. **Two Stacks** berguna dalam beberapa skenario khusus
5. **Deque** paling fleksibel tapi memiliki overhead lebih besar

**Trade-offs:**

| Aspek | Array | Linked List |
|-------|-------|-------------|
| **Cache locality** | Baik | Buruk |
| **Memory overhead** | Tidak ada | Pointer per node |
| **Resize** | Mahal O(n) | Tidak perlu |
| **Random access** | Mungkin | Tidak |
| **Implementasi** | Lebih mudah | Sedikit kompleks |

---

## 8. STL Queue dan Deque di C++

### 8.1 std::queue

C++ menyediakan `std::queue` dalam header `<queue>`.

```cpp
#include <iostream>
#include <queue>
using namespace std;

int main() {
    queue<int> q;

    // Enqueue
    q.push(10);
    q.push(20);
    q.push(30);

    // Front dan back
    cout << "Front: " << q.front() << endl;  // 10
    cout << "Back: " << q.back() << endl;    // 30

    // Size
    cout << "Size: " << q.size() << endl;    // 3

    // Dequeue
    while (!q.empty()) {
        cout << q.front() << " ";
        q.pop();
    }
    cout << endl;  // 10 20 30

    return 0;
}
```

### 8.2 std::deque

```cpp
#include <iostream>
#include <deque>
using namespace std;

int main() {
    deque<int> dq;

    // Insert di kedua ujung
    dq.push_back(10);
    dq.push_front(5);
    dq.push_back(15);
    dq.push_front(1);

    // Deque sekarang: [1, 5, 10, 15]

    // Random access (berbeda dengan queue!)
    cout << "Element at index 2: " << dq[2] << endl;  // 10

    // Hapus dari kedua ujung
    dq.pop_front();  // Hapus 1
    dq.pop_back();   // Hapus 15

    // Deque sekarang: [5, 10]

    // Iterasi
    for (int val : dq) {
        cout << val << " ";
    }
    cout << endl;

    return 0;
}
```

---

## Supplementary Problems

### Problem S1 ⭐
Implementasikan fungsi `interleave()` yang menyisipkan elemen dari dua queue secara bergantian ke queue baru.

**Jawaban:**
```cpp
queue<int> interleave(queue<int>& q1, queue<int>& q2) {
    queue<int> result;
    while (!q1.empty() || !q2.empty()) {
        if (!q1.empty()) { result.push(q1.front()); q1.pop(); }
        if (!q2.empty()) { result.push(q2.front()); q2.pop(); }
    }
    return result;
}
```

### Problem S2 ⭐⭐
Jelaskan mengapa BFS menggunakan queue sementara DFS menggunakan stack!

**Jawaban:**
- BFS menjelajahi level demi level (tetangga dari node saat ini dulu), sesuai FIFO
- DFS menjelajahi sedalam mungkin dulu, sesuai LIFO
- Queue menjaga urutan "siapa duluan ditemukan, dia duluan dijelajahi"
- Stack menjaga urutan "siapa terakhir ditemukan, dia duluan dijelajahi"

### Problem S3 ⭐⭐
Bagaimana cara mendeteksi apakah sebuah linked queue memiliki cycle?

**Jawaban:**
Gunakan Floyd's Cycle Detection (tortoise and hare):
```cpp
bool hasCycle(Node* front) {
    if (front == nullptr) return false;
    Node* slow = front;
    Node* fast = front;
    while (fast != nullptr && fast->next != nullptr) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) return true;
    }
    return false;
}
```

### Problem S4 ⭐⭐
Implementasikan priority queue sederhana menggunakan multiple queues!

**Jawaban:**
```cpp
class SimplePriorityQueue {
    queue<int> high, medium, low;
public:
    void enqueue(int val, int priority) {
        if (priority == 1) high.push(val);
        else if (priority == 2) medium.push(val);
        else low.push(val);
    }
    int dequeue() {
        if (!high.empty()) { int v = high.front(); high.pop(); return v; }
        if (!medium.empty()) { int v = medium.front(); medium.pop(); return v; }
        if (!low.empty()) { int v = low.front(); low.pop(); return v; }
        throw runtime_error("Empty!");
    }
};
```

### Problem S5 ⭐⭐⭐
Analisis amortized cost untuk operasi dequeue pada implementasi queue dengan dua stack!

**Jawaban:**
- Setiap elemen dipush ke stackIn tepat 1 kali: O(1)
- Setiap elemen dipindah ke stackOut paling banyak 1 kali: O(1)
- Setiap elemen dipop dari stackOut tepat 1 kali: O(1)
- Total: setiap elemen mengalami 3 operasi O(1)
- Amortized cost per dequeue: O(1)

Meskipun worst case satu dequeue bisa O(n), jika kita amortize ke semua operasi, rata-rata menjadi O(1).

---

## Ringkasan

| Konsep | Penjelasan Singkat |
|--------|-------------------|
| **FIFO** | First In First Out - prinsip dasar queue |
| **ADT Queue** | enqueue, dequeue, front, rear, isEmpty, isFull, size |
| **Array Linear** | Implementasi sederhana, masalah false overflow |
| **Circular Queue** | Mengatasi false overflow dengan wrapping index |
| **Linked Queue** | Dinamis, tidak ada false overflow, overhead pointer |
| **Deque** | Double-ended queue, insert/delete di kedua ujung |
| **Aplikasi** | Simulasi antrian, BFS, scheduling, buffer |
| **Kompleksitas** | Semua operasi O(1) untuk implementasi yang baik |

---

## Referensi

1. Cormen, T.H., Leiserson, C.E., Rivest, R.L., & Stein, C. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 10.1
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 3.7
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 6

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
