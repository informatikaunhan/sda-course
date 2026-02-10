# Latihan Mandiri 03: Single Linked List

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 03  
**Topik:** Single Linked List  
**Waktu:** 150 menit  
**Sifat:** Open Book  

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal secara mandiri
2. Untuk soal pilihan ganda, pilih **satu** jawaban yang paling tepat
3. Untuk soal uraian, jelaskan dengan lengkap dan sertakan kode jika diminta
4. Studi kasus dikerjakan secara individual atau kelompok (sesuai instruksi dosen)

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

### Soal 1
Apa komponen dasar penyusun sebuah node dalam single linked list?

A. Data dan index  
B. Key dan value  
C. Data dan pointer next  
D. Head dan tail  
E. Array dan pointer  

---

### Soal 2
Perhatikan ilustrasi berikut:
```
head → [10] → [20] → [30] → NULL
```
Berapa banyak node dalam linked list tersebut?

A. 2  
B. 3  
C. 4  
D. 5  
E. 6  

---

### Soal 3
Apa keuntungan utama linked list dibandingkan array?

A. Akses elemen lebih cepat  
B. Ukuran dapat berubah secara dinamis  
C. Memori yang digunakan lebih sedikit  
D. Cache performance lebih baik  
E. Implementasi lebih sederhana  

---

### Soal 4
Kompleksitas waktu untuk operasi **insert di awal** single linked list adalah:

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

---

### Soal 5
Kompleksitas waktu untuk operasi **insert di akhir** single linked list **tanpa** pointer tail adalah:

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

---

### Soal 6
Apa yang akan terjadi jika kita melakukan `delete head` tanpa menyimpan `head->next` terlebih dahulu?

A. Program berjalan normal  
B. Memory leak  
C. Dangling pointer dan undefined behavior  
D. Segmentation fault pasti terjadi  
E. Semua node terhapus otomatis  

---

### Soal 7
Perhatikan kode berikut:
```cpp
Node* a = new Node(5);
Node* b = new Node(10);
Node* c = new Node(15);
a->next = b;
b->next = c;
Node* head = a;
```
Apa output jika kita traversal dari head?

A. 15 → 10 → 5 → NULL  
B. 5 → 10 → 15 → NULL  
C. 10 → 5 → 15 → NULL  
D. 5 → 15 → 10 → NULL  
E. Error, kode tidak valid  

---

### Soal 8
Diberikan linked list: `head → [A] → [B] → [C] → [D] → NULL`

Setelah operasi `deleteAtBeginning()`, linked list menjadi:

A. head → [A] → [B] → [C] → NULL  
B. head → [B] → [C] → [D] → NULL  
C. head → [A] → [C] → [D] → NULL  
D. head → [A] → [B] → [D] → NULL  
E. head → NULL  

---

### Soal 9
Mengapa operasi `deleteAtEnd()` pada single linked list memiliki kompleksitas O(n) meskipun memiliki pointer tail?

A. Karena harus menghapus semua node  
B. Karena tidak bisa mundur ke node sebelumnya  
C. Karena tail tidak menyimpan alamat yang valid  
D. Karena harus melakukan sorting terlebih dahulu  
E. Karena memory allocation lambat  

---

### Soal 10
Perhatikan kode berikut:
```cpp
void insertAtPosition(int value, int position) {
    Node* prev = head;
    for (int i = 0; i < position - 1; i++) {
        prev = prev->next;
    }
    Node* newNode = new Node(value);
    newNode->next = prev->next;
    prev->next = newNode;
}
```
Jika linked list adalah `head → [10] → [30] → [40] → NULL` dan dipanggil `insertAtPosition(20, 1)`, hasilnya adalah:

A. head → [20] → [10] → [30] → [40] → NULL  
B. head → [10] → [20] → [30] → [40] → NULL  
C. head → [10] → [30] → [20] → [40] → NULL  
D. head → [10] → [30] → [40] → [20] → NULL  
E. Error, index out of bounds  

---

### Soal 11
Apa fungsi dari statement `newNode->next = head` pada operasi insert di awal?

A. Menghubungkan head ke node baru  
B. Menghubungkan node baru ke node pertama yang lama  
C. Menghapus node pertama yang lama  
D. Membuat head menjadi NULL  
E. Mengalokasikan memori untuk node baru  

---

### Soal 12
Dalam kondisi apa kita harus menangani kasus khusus saat delete di akhir?

A. Ketika list kosong  
B. Ketika list hanya memiliki satu node  
C. Kedua kondisi di atas  
D. Tidak ada kasus khusus  
E. Ketika list memiliki lebih dari 10 node  

---

### Soal 13
Teknik **two pointers** dengan fast dan slow pointer dapat digunakan untuk:

A. Mengurutkan linked list  
B. Mencari nilai maksimum  
C. Mendeteksi cycle dalam linked list  
D. Menambah node di tengah  
E. Menghapus semua node  

---

### Soal 14
Perhatikan fungsi berikut:
```cpp
int mystery(Node* head) {
    int count = 0;
    Node* current = head;
    while (current != nullptr) {
        count++;
        current = current->next;
    }
    return count;
}
```
Apa yang dilakukan fungsi tersebut?

A. Mencari nilai maksimum  
B. Menghitung jumlah node  
C. Mencari nilai minimum  
D. Menghitung total nilai  
E. Membalik linked list  

---

### Soal 15
Jika kita ingin mengimplementasikan Stack menggunakan single linked list, operasi mana yang paling efisien untuk push dan pop?

A. Push di akhir, Pop di akhir  
B. Push di awal, Pop di akhir  
C. Push di akhir, Pop di awal  
D. Push di awal, Pop di awal  
E. Tidak bisa diimplementasikan  

---

### Soal 16
Apa output dari kode berikut jika linked list adalah `head → [1] → [2] → [3] → NULL`?
```cpp
Node* current = head;
while (current->next != nullptr) {
    current = current->next;
}
cout << current->data;
```

A. 1  
B. 2  
C. 3  
D. NULL  
E. Error  

---

### Soal 17
Mana pernyataan yang **SALAH** tentang single linked list?

A. Setiap node memiliki pointer ke node berikutnya  
B. Traversal hanya bisa dilakukan dari head ke tail  
C. Insert di awal memiliki kompleksitas O(1)  
D. Akses elemen ke-n memiliki kompleksitas O(1)  
E. Ukuran dapat berubah secara dinamis  

---

### Soal 18
Dalam implementasi linked list, mengapa penting untuk memiliki destructor?

A. Untuk menambah node baru  
B. Untuk mencegah memory leak  
C. Untuk mempercepat pencarian  
D. Untuk mengurutkan data  
E. Untuk mengecek validitas pointer  

---

### Soal 19
Diberikan linked list: `head → [5] → [10] → [15] → [20] → NULL`

Berapa kali perbandingan yang diperlukan untuk mencari nilai 15 dengan linear search?

A. 1  
B. 2  
C. 3  
D. 4  
E. 5  

---

### Soal 20
Perhatikan operasi berikut pada linked list `head → [A] → [B] → [C] → NULL`:
```
1. insertAtEnd(D)
2. deleteAtBeginning()
3. insertAtBeginning(X)
```
Hasil akhir linked list adalah:

A. head → [X] → [A] → [B] → [C] → [D] → NULL  
B. head → [X] → [B] → [C] → [D] → NULL  
C. head → [A] → [B] → [C] → [D] → [X] → NULL  
D. head → [B] → [C] → [D] → [X] → NULL  
E. head → [X] → [B] → [C] → NULL  

---

## Bagian B: Soal Uraian (15 Soal)

### Soal 1 (Mudah)
Jelaskan perbedaan antara **array** dan **linked list** dalam hal:
a. Alokasi memori
b. Akses elemen
c. Operasi insert di awal

---

### Soal 2 (Mudah)
Gambarkan struktur linked list setelah operasi berikut dijalankan secara berurutan:
```cpp
SingleLinkedList list;
list.insertAtEnd(10);
list.insertAtEnd(20);
list.insertAtBeginning(5);
list.insertAtPosition(15, 2);
```

---

### Soal 3 (Mudah)
Tuliskan kode C++ untuk membuat struct Node yang dapat menyimpan data bertipe `string` (misalnya untuk menyimpan nama).

---

### Soal 4 (Sedang)
Implementasikan fungsi `int sumAll(Node* head)` yang mengembalikan jumlah total semua nilai dalam linked list.

---

### Soal 5 (Sedang)
Implementasikan fungsi `bool isPalindrome(Node* head)` untuk mengecek apakah linked list membentuk palindrome.

Contoh:
- `1 → 2 → 3 → 2 → 1` adalah palindrome
- `1 → 2 → 3 → 4` bukan palindrome

---

### Soal 6 (Sedang)
Diberikan dua sorted linked list:
```
L1: 1 → 3 → 5 → NULL
L2: 2 → 4 → 6 → NULL
```
Tuliskan algoritma (pseudocode atau kode C++) untuk menggabungkan keduanya menjadi satu sorted linked list.

---

### Soal 7 (Sedang)
Jelaskan langkah-langkah untuk membalik (reverse) single linked list secara **in-place** (tanpa membuat linked list baru). Sertakan kode implementasinya.

---

### Soal 8 (Sedang)
Implementasikan fungsi `void removeDuplicates(Node* head)` yang menghapus semua node duplikat dari **sorted** linked list.

Contoh: `1 → 1 → 2 → 3 → 3 → 3` menjadi `1 → 2 → 3`

---

### Soal 9 (Sedang)
Analisis kompleksitas waktu dan ruang untuk operasi berikut pada single linked list:
a. `insertAtPosition(value, n/2)` - insert di tengah
b. `deleteByValue(value)` - delete berdasarkan nilai
c. `getMiddle()` - mendapatkan nilai node di tengah

---

### Soal 10 (Sulit)
Implementasikan fungsi `Node* findIntersection(Node* headA, Node* headB)` yang menemukan node di mana dua linked list bertemu (intersection point).

```
A:    a1 → a2 ↘
                c1 → c2 → c3
B: b1 → b2 → b3 ↗
```
Return: pointer ke c1

---

### Soal 11 (Sulit)
Implementasikan fungsi untuk mendeteksi cycle dalam linked list menggunakan **Floyd's Cycle Detection Algorithm**. Jika cycle terdeteksi, kembalikan node di mana cycle dimulai.

---

### Soal 12 (Sulit)
Desain dan implementasikan kelas `LinkedListWithTail` yang memiliki pointer head dan tail, sehingga:
- `insertAtEnd()` menjadi O(1)
- `deleteAtEnd()` tetap O(n) - jelaskan mengapa

---

### Soal 13 (Sedang)
Implementasikan fungsi `void rotate(Node*& head, int k)` yang merotasi linked list ke kanan sebanyak k posisi.

Contoh: `1 → 2 → 3 → 4 → 5`, k=2 menjadi `4 → 5 → 1 → 2 → 3`

---

### Soal 14 (Sedang)
Jelaskan bagaimana single linked list dapat digunakan untuk mengimplementasikan Queue (antrian). Operasi mana yang menjadi enqueue dan dequeue? Apa kompleksitasnya?

---

### Soal 15 (Sulit)
Implementasikan kelas `SortedLinkedList` di mana setiap insert otomatis menempatkan node pada posisi yang tepat agar list selalu terurut ascending.

---

## Bagian C: Studi Kasus Pertahanan (2 Soal)

### Studi Kasus 1: Sistem Manajemen Personel Pasukan

**Latar Belakang:**
Sebuah batalyon infanteri memerlukan sistem untuk mengelola daftar personel yang bertugas dalam sebuah misi. Sistem harus dapat:
1. Menambahkan personel baru ke dalam daftar
2. Menghapus personel yang sudah selesai bertugas
3. Mencari personel berdasarkan NRP (Nomor Registrasi Personel)
4. Menampilkan semua personel dalam formasi

**Data Personel:**
```
struct Personel {
    string nrp;        // Nomor Registrasi Personel
    string nama;       // Nama lengkap
    string pangkat;    // Pangkat (Serda, Sertu, Serma, dll)
    string satuan;     // Satuan tugas
};
```

**Tugas:**

1. **(30 poin)** Desain dan implementasikan kelas `PersonelList` menggunakan single linked list dengan operasi:
   - `void tambahPersonel(Personel p)` - menambah di akhir
   - `void tambahPersonelUrgent(Personel p)` - menambah di awal (untuk penugasan darurat)
   - `bool hapusPersonel(string nrp)` - hapus berdasarkan NRP
   - `Personel* cariPersonel(string nrp)` - cari berdasarkan NRP
   - `void tampilkanFormasi()` - tampilkan semua personel

2. **(20 poin)** Implementasikan fungsi `void urutkanBerdasarkanPangkat()` yang mengurutkan personel berdasarkan hirarki pangkat (dari pangkat tertinggi ke terendah).

3. **(10 poin)** Analisis kompleksitas waktu setiap operasi dan jelaskan mengapa linked list cocok atau tidak cocok untuk sistem ini dibandingkan array.

**Contoh Output:**
```
=== FORMASI PERSONEL BATALYON A ===
1. Serma Budi Santoso (NRP: 2198765) - Satuan: Kompi A
2. Sertu Ahmad Wijaya (NRP: 2198766) - Satuan: Kompi A
3. Serda Rudi Hartono (NRP: 2198767) - Satuan: Kompi B
Total: 3 personel
```

---

### Studi Kasus 2: Sistem Log Aktivitas Radar

**Latar Belakang:**
Sebuah pos radar pantai perlu mencatat semua aktivitas deteksi yang terjadi. Karena keterbatasan memori, sistem hanya dapat menyimpan **N log terakhir** (circular buffer behavior). Ketika buffer penuh, log paling lama akan digantikan dengan log baru.

**Data Log:**
```
struct RadarLog {
    time_t timestamp;      // Waktu deteksi
    string jenis_target;   // "Kapal", "Pesawat", "Unknown"
    double latitude;       // Koordinat
    double longitude;
    double kecepatan;      // knot
    int bearing;           // derajat (0-359)
};
```

**Tugas:**

1. **(30 poin)** Implementasikan kelas `RadarLogBuffer` menggunakan single linked list dengan fitur:
   - Constructor menerima parameter `maxSize` untuk batas maksimum log
   - `void addLog(RadarLog log)` - menambah log baru, jika penuh maka log paling lama dihapus
   - `void displayRecent(int n)` - menampilkan n log terakhir
   - `void displayAll()` - menampilkan semua log
   - `vector<RadarLog> searchByType(string jenis)` - mencari log berdasarkan jenis target

2. **(20 poin)** Implementasikan fungsi `RadarLog* getThreatAlert()` yang mengembalikan log dengan kriteria ancaman:
   - Jarak dari pos radar < 50 km (hitung dari koordinat)
   - Kecepatan > 30 knot
   - Jenis target = "Unknown"

3. **(10 poin)** Dalam skenario ini, apakah lebih baik menggunakan linked list atau circular array? Berikan analisis perbandingan untuk operasi:
   - Menambah log baru
   - Menghapus log lama
   - Mencari log tertentu

**Contoh Output:**
```
=== RADAR LOG BUFFER (5/10 entries) ===
[2025-01-15 08:30:15] Kapal @ -6.1234, 106.5678 | 15 knot | Bearing: 045°
[2025-01-15 08:31:22] Unknown @ -6.1250, 106.5700 | 45 knot | Bearing: 270°
[2025-01-15 08:32:45] Pesawat @ -6.1100, 106.5500 | 200 knot | Bearing: 180°
...

⚠️ THREAT ALERT: Unknown target detected!
   Posisi: -6.1250, 106.5700
   Kecepatan: 45 knot
   Jarak dari pos: 12.5 km
```

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | **C** | Node terdiri dari data dan pointer next |
| 2 | **B** | Ada 3 node: [10], [20], [30] |
| 3 | **B** | Linked list dapat grow/shrink secara dinamis |
| 4 | **A** | Insert di awal hanya perlu update pointer, O(1) |
| 5 | **C** | Perlu traversal ke akhir tanpa tail |
| 6 | **C** | Akses memory yang sudah di-deallocate = undefined behavior |
| 7 | **B** | Traversal dari a: 5 → 10 → 15 → NULL |
| 8 | **B** | Node pertama [A] dihapus |
| 9 | **B** | Single linked list tidak punya pointer ke node sebelumnya |
| 10 | **B** | Posisi 1 = setelah node index 0 |
| 11 | **B** | Menghubungkan node baru ke head yang lama |
| 12 | **C** | Perlu handle list kosong dan satu node |
| 13 | **C** | Floyd's algorithm untuk cycle detection |
| 14 | **B** | Menghitung jumlah node dengan traversal |
| 15 | **D** | Push dan pop di awal keduanya O(1) |
| 16 | **C** | Loop berhenti di node terakhir yang berisi 3 |
| 17 | **D** | Akses elemen ke-n adalah O(n), bukan O(1) |
| 18 | **B** | Destructor membebaskan memori semua node |
| 19 | **C** | Perbandingan: [5]≠15, [10]≠15, [15]=15 (3x) |
| 20 | **B** | 1. A→B→C→D, 2. B→C→D, 3. X→B→C→D |

---

### Bagian B: Uraian (Jawaban Singkat)

#### Soal 1
a. **Alokasi memori**: Array = contiguous (berurutan), Linked List = scattered (tersebar)
b. **Akses elemen**: Array = O(1) random access, Linked List = O(n) sequential
c. **Insert di awal**: Array = O(n) perlu geser, Linked List = O(1)

#### Soal 2
```
head → [5] → [10] → [15] → [20] → NULL
```
Langkah: insertEnd(10) → [10], insertEnd(20) → [10]→[20], insertBegin(5) → [5]→[10]→[20], insertPos(15,2) → [5]→[10]→[15]→[20]

#### Soal 3
```cpp
struct Node {
    string data;
    Node* next;
    Node(string value) : data(value), next(nullptr) {}
};
```

#### Soal 4
```cpp
int sumAll(Node* head) {
    int total = 0;
    Node* current = head;
    while (current != nullptr) {
        total += current->data;
        current = current->next;
    }
    return total;
}
```

#### Soal 5
```cpp
bool isPalindrome(Node* head) {
    // Cari tengah, reverse setengah kedua, bandingkan
    if (!head || !head->next) return true;
    
    Node *slow = head, *fast = head;
    while (fast->next && fast->next->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    
    // Reverse dari slow->next
    Node* secondHalf = reverse(slow->next);
    Node* firstHalf = head;
    
    while (secondHalf) {
        if (firstHalf->data != secondHalf->data) return false;
        firstHalf = firstHalf->next;
        secondHalf = secondHalf->next;
    }
    return true;
}
```

#### Soal 6
```cpp
Node* mergeSorted(Node* l1, Node* l2) {
    Node dummy(0);
    Node* tail = &dummy;
    
    while (l1 && l2) {
        if (l1->data <= l2->data) {
            tail->next = l1;
            l1 = l1->next;
        } else {
            tail->next = l2;
            l2 = l2->next;
        }
        tail = tail->next;
    }
    tail->next = l1 ? l1 : l2;
    return dummy.next;
}
```

#### Soal 7
```cpp
void reverse(Node*& head) {
    Node *prev = nullptr, *curr = head, *next = nullptr;
    while (curr) {
        next = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next;
    }
    head = prev;
}
```

#### Soal 8
```cpp
void removeDuplicates(Node* head) {
    Node* current = head;
    while (current && current->next) {
        if (current->data == current->next->data) {
            Node* dup = current->next;
            current->next = current->next->next;
            delete dup;
        } else {
            current = current->next;
        }
    }
}
```

#### Soal 9
a. `insertAtPosition(n/2)`: O(n) waktu, O(1) ruang
b. `deleteByValue`: O(n) waktu (search + delete), O(1) ruang
c. `getMiddle`: O(n) waktu (dengan two pointers), O(1) ruang

#### Soal 10
```cpp
Node* findIntersection(Node* headA, Node* headB) {
    int lenA = length(headA), lenB = length(headB);
    
    // Align starting points
    while (lenA > lenB) { headA = headA->next; lenA--; }
    while (lenB > lenA) { headB = headB->next; lenB--; }
    
    // Find intersection
    while (headA != headB) {
        headA = headA->next;
        headB = headB->next;
    }
    return headA;
}
```

#### Soal 11
```cpp
Node* detectCycleStart(Node* head) {
    Node *slow = head, *fast = head;
    
    // Detect cycle
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
        if (slow == fast) break;
    }
    if (!fast || !fast->next) return nullptr;
    
    // Find cycle start
    slow = head;
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;
    }
    return slow;
}
```

#### Soal 12
`deleteAtEnd` tetap O(n) karena single linked list tidak memiliki pointer prev. Meskipun kita bisa langsung akses tail, kita tetap perlu traversal untuk menemukan node sebelum tail untuk update next-nya menjadi nullptr.

#### Soal 13
```cpp
void rotate(Node*& head, int k) {
    if (!head || k == 0) return;
    
    int len = 1;
    Node* tail = head;
    while (tail->next) { tail = tail->next; len++; }
    
    k = k % len;
    if (k == 0) return;
    
    Node* newTail = head;
    for (int i = 0; i < len - k - 1; i++) newTail = newTail->next;
    
    tail->next = head;
    head = newTail->next;
    newTail->next = nullptr;
}
```

#### Soal 14
- **Enqueue**: `insertAtEnd()` - O(n) atau O(1) dengan tail
- **Dequeue**: `deleteAtBeginning()` - O(1)
- Dengan tail pointer, kedua operasi bisa menjadi O(1)

#### Soal 15
```cpp
void insertSorted(int value) {
    Node* newNode = new Node(value);
    
    if (!head || head->data >= value) {
        newNode->next = head;
        head = newNode;
        return;
    }
    
    Node* current = head;
    while (current->next && current->next->data < value) {
        current = current->next;
    }
    newNode->next = current->next;
    current->next = newNode;
}
```

---

### Bagian C: Studi Kasus (Panduan Penilaian)

#### Studi Kasus 1: Sistem Manajemen Personel
- **30 poin**: Implementasi lengkap semua operasi dengan benar
- **20 poin**: Sorting berdasarkan hirarki pangkat dengan mapping yang tepat
- **10 poin**: Analisis kompleksitas yang tepat dan argumentasi yang logis

#### Studi Kasus 2: Sistem Log Radar
- **30 poin**: Buffer dengan penggantian log lama ketika penuh
- **20 poin**: Fungsi threat detection dengan perhitungan jarak menggunakan Haversine formula
- **10 poin**: Perbandingan linked list vs circular array yang komprehensif

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
