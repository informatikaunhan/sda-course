# Modul 01: Pengantar Struktur Data dan Review C++ Lanjut

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 01  
**Topik:** Pengantar Struktur Data dan Review C++ Lanjut

> **Capaian Pembelajaran:** Sub-CPMK-1.1, Sub-CPMK-1.3 â€” Mampu menjelaskan konsep ADT dan menerapkan teknik pointer lanjut serta dynamic memory management

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.10; Weiss Ch.1; Hubbard Ch.1-2

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** definisi dan konsep Abstract Data Type (ADT) dengan tepat
2. **Mengidentifikasi** hubungan antara ADT dan implementasi struktur data
3. **Menjelaskan** peran ADT dalam desain program yang modular dan maintainable
4. **Menggunakan** pointer dan referensi dalam C++ dengan benar
5. **Mengimplementasikan** dynamic memory allocation menggunakan operator `new` dan `delete`
6. **Mengidentifikasi** dan mencegah memory leak serta dangling pointer
7. **Memahami** konsep dasar smart pointer dan implementasi array dinamis

---

## 1. Pengantar Struktur Data

### 1.1 Apa itu Struktur Data?

> **Definisi:** Struktur data adalah cara mengorganisasikan, menyimpan, dan mengelola data dalam memori komputer sehingga dapat diakses dan dimodifikasi secara efisien.

Dalam konteks pemrograman, struktur data bukan hanya tentang "menyimpan data", tetapi juga tentang:
- **Organisasi**: Bagaimana data disusun dalam memori
- **Akses**: Bagaimana data dapat diambil atau diubah
- **Operasi**: Apa saja yang dapat dilakukan terhadap data tersebut

Pemilihan struktur data yang tepat sangat mempengaruhi efisiensi program. Sebuah program dengan algoritma yang baik tetapi struktur data yang tidak tepat dapat berjalan sangat lambat, dan sebaliknya.

### 1.2 Mengapa Struktur Data Penting?

Bayangkan sebuah sistem Command, Control, Communications, Computers, Cyber, Intelligence, Surveillance, and Reconnaissance (C6ISR) yang harus mengelola ribuan data posisi unit militer secara real-time. Tanpa struktur data yang tepat:
- Pencarian posisi satu unit dari ribuan data bisa memakan waktu lama
- Update posisi tidak dapat dilakukan dengan cepat
- Sistem menjadi tidak responsif saat situasi kritis

Dengan struktur data yang tepat (misalnya hash table untuk pencarian cepat, atau tree untuk data hierarkis), operasi-operasi tersebut dapat dilakukan dalam waktu yang sangat singkat.

### 1.3 Klasifikasi Struktur Data

![Klasifikasi Struktur Data](images/p01-04-klasifikasi-struktur-data.png)

*Gambar 1.1: Klasifikasi struktur data â€” Linear vs Non-Linear*


| Jenis | Karakteristik | Contoh Penggunaan |
|-------|---------------|-------------------|
| **Linear** | Elemen tersusun berurutan, satu demi satu | Antrian pesan, history command |
| **Non-Linear** | Elemen dapat terhubung ke banyak elemen lain | Struktur organisasi, jaringan komunikasi |

---

## 2. Abstract Data Type (ADT)

### 2.1 Konsep ADT

> **Definisi:** Abstract Data Type (ADT) adalah model matematis untuk tipe data yang didefinisikan oleh perilakunya (semantik) dari sudut pandang pengguna, khususnya dalam hal nilai yang mungkin, operasi yang dapat dilakukan, dan perilaku operasi tersebut.

ADT berbeda dengan struktur data konkret:

| Aspek | ADT | Struktur Data Konkret |
|-------|-----|----------------------|
| **Level** | Abstrak/Konseptual | Implementasi |
| **Fokus** | APA yang dilakukan | BAGAIMANA melakukannya |
| **Detail Implementasi** | Tersembunyi | Terlihat |
| **Contoh** | Stack (konsep LIFO) | Array-based Stack, Linked Stack |

### 2.2 Komponen ADT

Setiap ADT memiliki tiga komponen utama:

1. **Data**: Nilai-nilai yang dapat disimpan
2. **Operasi**: Fungsi-fungsi yang dapat dilakukan pada data
3. **Aturan/Aksioma**: Perilaku yang dijamin dari operasi tersebut

**Contoh ADT Stack:**
```
ADT Stack:
  Data:
    - Kumpulan elemen dengan tipe T
    
  Operasi:
    - push(item): Menambah item ke puncak stack
    - pop(): Menghapus dan mengembalikan item dari puncak
    - peek()/top(): Melihat item di puncak tanpa menghapus
    - isEmpty(): Mengecek apakah stack kosong
    - size(): Mengembalikan jumlah elemen
    
  Aturan:
    - LIFO (Last In First Out)
    - push lalu pop mengembalikan item yang sama
    - pop pada stack kosong menghasilkan error
```

### 2.3 Manfaat ADT

1. **Abstraksi**: Pengguna tidak perlu tahu detail implementasi
2. **Enkapsulasi**: Detail internal tersembunyi dan terlindungi
3. **Modularitas**: Komponen dapat dikembangkan secara independen
4. **Reusabilitas**: ADT yang sama dapat diimplementasikan dengan berbagai cara
5. **Maintainability**: Perubahan implementasi tidak mempengaruhi kode pengguna

---

### SOLVED PROBLEM 1 â­

**Soal:** Sebutkan dan jelaskan tiga operasi dasar yang harus dimiliki oleh ADT Queue!

**Penyelesaian:**

ADT Queue memiliki tiga operasi dasar berikut:

1. **enqueue(item)**: Menambahkan elemen baru ke belakang antrian
   - Input: Elemen yang akan ditambahkan
   - Output: Tidak ada (void)
   - Efek: Ukuran queue bertambah satu

2. **dequeue()**: Menghapus dan mengembalikan elemen dari depan antrian
   - Input: Tidak ada
   - Output: Elemen yang dihapus
   - Efek: Ukuran queue berkurang satu
   - Precondition: Queue tidak boleh kosong

3. **front()/peek()**: Melihat elemen di depan antrian tanpa menghapusnya
   - Input: Tidak ada
   - Output: Elemen di posisi depan
   - Efek: Tidak mengubah queue
   - Precondition: Queue tidak boleh kosong

Operasi tambahan yang sering disertakan: `isEmpty()`, `size()`, dan `isFull()` (untuk implementasi dengan kapasitas terbatas).

---

### SOLVED PROBLEM 2 â­

**Soal:** Jelaskan perbedaan antara ADT dan struktur data konkret dengan contoh!

**Penyelesaian:**

**ADT** adalah spesifikasi abstrak yang mendefinisikan:
- Apa yang dapat dilakukan (operasi)
- Tanpa menentukan bagaimana melakukannya (implementasi)

**Struktur Data Konkret** adalah implementasi nyata dari ADT.

**Contoh dengan ADT List:**

| ADT List (Spesifikasi) | Implementasi Konkret |
|------------------------|---------------------|
| `insert(index, item)` | Array: geser elemen, masukkan di posisi |
| | Linked List: buat node baru, hubungkan pointer |
| `delete(index)` | Array: geser elemen ke kiri |
| | Linked List: ubah pointer, dealokasi node |
| `get(index)` | Array: akses langsung `arr[index]` |
| | Linked List: traverse dari head |

Satu ADT (List) dapat memiliki banyak implementasi (Array-based, Linked List, dll), masing-masing dengan trade-off berbeda.

---

## 3. Review Pointer dalam C++

### 3.1 Konsep Pointer

> **Definisi:** Pointer adalah variabel yang menyimpan alamat memori dari variabel lain.

Pointer merupakan salah satu fitur paling powerful sekaligus berbahaya dalam C++. Pemahaman yang baik tentang pointer sangat penting untuk implementasi struktur data.

```cpp
#include <iostream>
using namespace std;

int main() {
    int nilai = 42;        // Variabel biasa
    int* ptr = &nilai;     // Pointer yang menyimpan alamat 'nilai'
    
    cout << "Nilai variabel: " << nilai << endl;
    cout << "Alamat variabel: " << &nilai << endl;
    cout << "Nilai pointer: " << ptr << endl;
    cout << "Nilai yang ditunjuk: " << *ptr << endl;
    
    return 0;
}
```

**Output:**
```
Nilai variabel: 42
Alamat variabel: 0x7ffd5e8c3a4c
Nilai pointer: 0x7ffd5e8c3a4c
Nilai yang ditunjuk: 42
```

### 3.2 Operator Pointer

| Operator | Nama | Fungsi | Contoh |
|----------|------|--------|--------|
| `&` | Address-of | Mengambil alamat variabel | `&x` â†’ alamat x |
| `*` | Dereference | Mengakses nilai di alamat | `*ptr` â†’ nilai di ptr |
| `->` | Arrow | Akses member via pointer | `ptr->member` |

### 3.3 Pointer dan Array

Array dan pointer memiliki hubungan erat dalam C++:

```cpp
#include <iostream>
using namespace std;

int main() {
    int arr[5] = {10, 20, 30, 40, 50};
    int* ptr = arr;  // Array name = alamat elemen pertama
    
    // Akses menggunakan indeks
    cout << "arr[2] = " << arr[2] << endl;
    
    // Akses menggunakan pointer arithmetic
    cout << "*(ptr + 2) = " << *(ptr + 2) << endl;
    
    // Keduanya menghasilkan nilai yang sama: 30
    
    return 0;
}
```

### 3.4 Pointer Arithmetic

```cpp
int arr[5] = {10, 20, 30, 40, 50};
int* ptr = arr;

ptr++;      // Pindah ke elemen berikutnya (bukan +1 byte, tapi +sizeof(int))
ptr += 2;   // Pindah 2 elemen ke depan
ptr--;      // Pindah ke elemen sebelumnya
```

![Pointer Arithmetic](images/p01-01-pointer-arithmetic.png)

*Gambar 1.2: Ilustrasi pointer arithmetic pada array integer*


---

### SOLVED PROBLEM 3 â­

**Soal:** Apa output dari kode berikut?

```cpp
int x = 10;
int* p = &x;
*p = 20;
cout << x << endl;
```

**Penyelesaian:**

**Output:** `20`

**Penjelasan langkah demi langkah:**

1. `int x = 10;` â†’ Variabel `x` dibuat dengan nilai 10
2. `int* p = &x;` â†’ Pointer `p` menyimpan alamat `x`
3. `*p = 20;` â†’ Nilai di alamat yang ditunjuk `p` (yaitu `x`) diubah menjadi 20
4. `cout << x << endl;` â†’ Mencetak nilai `x`, yang sekarang adalah 20

Karena `p` menunjuk ke `x`, mengubah `*p` sama dengan mengubah `x` secara langsung.

---

### SOLVED PROBLEM 4 â­

**Soal:** Tuliskan fungsi yang menukar dua nilai integer menggunakan pointer!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

void tukar(int* a, int* b) {
    int temp = *a;  // Simpan nilai di alamat a
    *a = *b;        // Copy nilai di alamat b ke alamat a
    *b = temp;      // Copy temp ke alamat b
}

int main() {
    int x = 5, y = 10;
    
    cout << "Sebelum: x = " << x << ", y = " << y << endl;
    tukar(&x, &y);  // Kirim alamat x dan y
    cout << "Sesudah: x = " << x << ", y = " << y << endl;
    
    return 0;
}
```

**Output:**
```
Sebelum: x = 5, y = 10
Sesudah: x = 10, y = 5
```

Fungsi menerima alamat variabel, sehingga perubahan yang dilakukan di dalam fungsi mempengaruhi variabel asli.

---

## 4. Referensi dalam C++

### 4.1 Konsep Referensi

> **Definisi:** Referensi adalah alias (nama lain) untuk variabel yang sudah ada. Setelah diinisialisasi, referensi selalu merujuk ke variabel yang sama.

```cpp
int nilai = 42;
int& ref = nilai;   // ref adalah alias untuk nilai

ref = 100;          // Sama dengan nilai = 100
cout << nilai;      // Output: 100
```

### 4.2 Perbedaan Pointer dan Referensi

| Aspek | Pointer | Referensi |
|-------|---------|-----------|
| **Inisialisasi** | Bisa tanpa nilai awal | Harus langsung diinisialisasi |
| **Null** | Bisa null | Tidak bisa null |
| **Reassignment** | Bisa menunjuk ke variabel lain | Selalu merujuk ke variabel yang sama |
| **Syntax** | Perlu `*` dan `&` | Langsung seperti variabel biasa |
| **Memory** | Memiliki alamat sendiri | Berbagi alamat dengan variabel asli |

### 4.3 Pass by Reference

```cpp
#include <iostream>
using namespace std;

// Pass by value - tidak mengubah variabel asli
void tambahSatu_nilai(int x) {
    x = x + 1;
}

// Pass by reference - mengubah variabel asli
void tambahSatu_ref(int& x) {
    x = x + 1;
}

int main() {
    int a = 5, b = 5;
    
    tambahSatu_nilai(a);
    tambahSatu_ref(b);
    
    cout << "a = " << a << endl;  // Output: 5 (tidak berubah)
    cout << "b = " << b << endl;  // Output: 6 (berubah)
    
    return 0;
}
```

---

### SOLVED PROBLEM 5 â­

**Soal:** Apa perbedaan utama antara `int* ptr` dan `int& ref`?

**Penyelesaian:**

| Karakteristik | `int* ptr` (Pointer) | `int& ref` (Referensi) |
|---------------|---------------------|------------------------|
| **Definisi** | Variabel yang menyimpan alamat | Alias untuk variabel lain |
| **Dapat null** | Ya, `int* ptr = nullptr;` | Tidak, harus merujuk ke variabel valid |
| **Dapat diubah** | Ya, `ptr = &other;` | Tidak, selalu merujuk ke variabel awal |
| **Operator akses** | `*ptr` untuk nilai | Langsung `ref` |
| **Ukuran memori** | Memiliki alamat sendiri | Tidak menambah memori |
| **Harus diinisialisasi** | Tidak (tapi sebaiknya ya) | Ya, wajib |

**Kapan menggunakan masing-masing:**
- **Pointer**: Ketika perlu null, atau perlu mengubah target
- **Referensi**: Untuk parameter fungsi yang lebih bersih dan aman

---

### SOLVED PROBLEM 6 â­â­

**Soal:** Tuliskan fungsi yang menghitung panjang string C-style (char array) menggunakan pointer!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

int hitungPanjang(const char* str) {
    const char* ptr = str;  // Pointer untuk traverse
    
    // Traverse sampai menemukan null terminator
    while (*ptr != '\0') {
        ptr++;
    }
    
    // Panjang = selisih posisi akhir dan awal
    return ptr - str;
}

int main() {
    const char* pesan = "Struktur Data C++";
    
    cout << "String: " << pesan << endl;
    cout << "Panjang: " << hitungPanjang(pesan) << " karakter" << endl;
    
    return 0;
}
```

**Output:**
```
String: Struktur Data C++
Panjang: 17 karakter
```

**Penjelasan:**
1. Pointer `ptr` dimulai dari awal string
2. Loop berjalan selama karakter bukan null terminator (`'\0'`)
3. Setiap iterasi, pointer maju satu karakter
4. Selisih `ptr - str` memberikan jumlah karakter

---

## 5. Dynamic Memory Allocation

### 5.1 Stack vs Heap Memory

Dalam C++, memori program dibagi menjadi beberapa segmen:

| Segmen | Karakteristik | Contoh |
|--------|---------------|--------|
| **Stack** | Otomatis dialokasi/dealokasi, ukuran terbatas, cepat | Variabel lokal, parameter fungsi |
| **Heap** | Manual dialokasi/dealokasi, ukuran besar, lebih lambat | Data dengan `new`, array dinamis |
| **Data** | Variabel global dan static | Global variables |
| **Code** | Instruksi program | Fungsi-fungsi |

![Stack vs Heap Memory](images/p01-02-stack-heap-memory.png)

*Gambar 1.3: Perbandingan Stack dan Heap Memory*


### 5.2 Operator `new` dan `delete`

C++ menyediakan operator `new` untuk alokasi memori di heap dan `delete` untuk dealokasi:

```cpp
#include <iostream>
using namespace std;

int main() {
    // Alokasi single variable
    int* ptr = new int;      // Alokasi memori untuk satu integer
    *ptr = 42;
    cout << "Nilai: " << *ptr << endl;
    delete ptr;              // Dealokasi memori
    
    // Alokasi dengan inisialisasi
    int* ptr2 = new int(100);
    cout << "Nilai: " << *ptr2 << endl;
    delete ptr2;
    
    return 0;
}
```

### 5.3 Alokasi Array Dinamis

```cpp
#include <iostream>
using namespace std;

int main() {
    int ukuran;
    cout << "Masukkan ukuran array: ";
    cin >> ukuran;
    
    // Alokasi array dinamis
    int* arr = new int[ukuran];
    
    // Mengisi array
    for (int i = 0; i < ukuran; i++) {
        arr[i] = i * 10;
    }
    
    // Menampilkan array
    cout << "Isi array: ";
    for (int i = 0; i < ukuran; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    // Dealokasi array - PENTING: gunakan delete[]
    delete[] arr;
    
    return 0;
}
```

> **Penting:** Untuk array yang dialokasikan dengan `new[]`, gunakan `delete[]` untuk dealokasi. Menggunakan `delete` (tanpa brackets) untuk array menyebabkan undefined behavior.

---

### SOLVED PROBLEM 7 â­

**Soal:** Apa perbedaan antara `delete ptr` dan `delete[] ptr`?

**Penyelesaian:**

| Operator | Penggunaan | Dealokasi |
|----------|------------|-----------|
| `delete ptr` | Untuk single object yang dialokasi dengan `new` | Memanggil destructor satu kali, dealokasi satu objek |
| `delete[] ptr` | Untuk array yang dialokasi dengan `new[]` | Memanggil destructor untuk setiap elemen, dealokasi seluruh array |

**Contoh penggunaan yang benar:**

```cpp
// Single object
int* single = new int(42);
delete single;  // BENAR

// Array
int* arr = new int[10];
delete[] arr;   // BENAR
```

**Konsekuensi kesalahan:**
- Menggunakan `delete` untuk array: Memory leak, undefined behavior
- Menggunakan `delete[]` untuk single object: Undefined behavior

---

### SOLVED PROBLEM 8 â­â­

**Soal:** Buatlah program yang membuat array dinamis untuk menyimpan nilai sensor suhu, kemudian menghitung rata-ratanya!

**Penyelesaian:**

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

int main() {
    int jumlahSensor;
    
    cout << "=== Sistem Monitoring Suhu ===" << endl;
    cout << "Jumlah sensor: ";
    cin >> jumlahSensor;
    
    // Validasi input
    if (jumlahSensor <= 0) {
        cout << "Error: Jumlah sensor harus positif!" << endl;
        return 1;
    }
    
    // Alokasi array dinamis
    double* suhu = new double[jumlahSensor];
    
    // Input data suhu
    cout << "\nMasukkan data suhu:" << endl;
    for (int i = 0; i < jumlahSensor; i++) {
        cout << "Sensor " << (i + 1) << ": ";
        cin >> suhu[i];
    }
    
    // Hitung rata-rata
    double total = 0;
    double suhuMax = suhu[0];
    double suhuMin = suhu[0];
    
    for (int i = 0; i < jumlahSensor; i++) {
        total += suhu[i];
        if (suhu[i] > suhuMax) suhuMax = suhu[i];
        if (suhu[i] < suhuMin) suhuMin = suhu[i];
    }
    
    double rataRata = total / jumlahSensor;
    
    // Tampilkan hasil
    cout << "\n=== Laporan ===" << endl;
    cout << fixed << setprecision(2);
    cout << "Rata-rata: " << rataRata << "Â°C" << endl;
    cout << "Suhu maksimum: " << suhuMax << "Â°C" << endl;
    cout << "Suhu minimum: " << suhuMin << "Â°C" << endl;
    
    // Dealokasi memori
    delete[] suhu;
    
    return 0;
}
```

**Contoh Output:**
```
=== Sistem Monitoring Suhu ===
Jumlah sensor: 5

Masukkan data suhu:
Sensor 1: 28.5
Sensor 2: 29.2
Sensor 3: 27.8
Sensor 4: 30.1
Sensor 5: 28.9

=== Laporan ===
Rata-rata: 28.90Â°C
Suhu maksimum: 30.10Â°C
Suhu minimum: 27.80Â°C
```

---

## 6. Memory Leak dan Dangling Pointer

### 6.1 Memory Leak

> **Definisi:** Memory leak terjadi ketika memori yang dialokasikan di heap tidak pernah didealokasi, menyebabkan memori tersebut tidak dapat digunakan kembali.

**Contoh memory leak:**

```cpp
void fungsiMasalah() {
    int* data = new int[1000];
    // ... melakukan operasi ...
    
    // MASALAH: fungsi berakhir tanpa delete[]
    // Memori 1000 integer hilang!
}

int main() {
    for (int i = 0; i < 100000; i++) {
        fungsiMasalah();  // Setiap panggilan = memory leak
    }
    // Program mungkin kehabisan memori!
    return 0;
}
```

**Penyebab umum memory leak:**
1. Lupa memanggil `delete` atau `delete[]`
2. Exception terjadi sebelum dealokasi
3. Pointer di-reassign tanpa dealokasi terlebih dahulu
4. Return dari fungsi sebelum dealokasi

### 6.2 Dangling Pointer

> **Definisi:** Dangling pointer adalah pointer yang menunjuk ke lokasi memori yang sudah tidak valid (sudah didealokasi atau di luar scope).

**Contoh dangling pointer:**

```cpp
#include <iostream>
using namespace std;

int* buatDangling() {
    int lokal = 42;
    return &lokal;  // BAHAYA! mengembalikan alamat variabel lokal
}  // lokal dihancurkan saat fungsi berakhir

int main() {
    int* ptr = new int(100);
    delete ptr;     // Memori didealokasi
    
    // ptr sekarang adalah dangling pointer!
    cout << *ptr;   // UNDEFINED BEHAVIOR
    
    int* danger = buatDangling();  // danger = dangling pointer
    cout << *danger;  // UNDEFINED BEHAVIOR
    
    return 0;
}
```

### 6.3 Praktik Terbaik

```cpp
#include <iostream>
using namespace std;

int main() {
    // 1. Selalu inisialisasi pointer
    int* ptr = nullptr;
    
    // 2. Periksa sebelum menggunakan
    if (ptr != nullptr) {
        cout << *ptr << endl;
    }
    
    // 3. Set ke nullptr setelah delete
    ptr = new int(42);
    cout << *ptr << endl;
    delete ptr;
    ptr = nullptr;  // Mencegah dangling pointer
    
    // 4. Periksa lagi setelah operasi
    if (ptr != nullptr) {
        cout << *ptr << endl;  // Tidak dieksekusi
    }
    
    return 0;
}
```

![Memory Leak dan Dangling Pointer](images/p01-03-memory-problems.png)

*Gambar 1.4: Ilustrasi Memory Leak dan Dangling Pointer*


---

### SOLVED PROBLEM 9 â­â­

**Soal:** Identifikasi semua masalah dalam kode berikut dan perbaiki!

```cpp
void prosesData() {
    int* data = new int[100];
    // ... proses data ...
    if (error) {
        return;  // Early return
    }
    delete[] data;
}
```

**Penyelesaian:**

**Masalah yang teridentifikasi:**
1. Memory leak jika `error` bernilai true (early return tanpa dealokasi)
2. Variabel `error` tidak didefinisikan

**Kode yang diperbaiki:**

```cpp
void prosesData() {
    int* data = new int[100];
    bool error = false;
    
    // ... proses data ...
    // Misalkan terjadi error
    error = true;
    
    if (error) {
        delete[] data;  // Dealokasi sebelum return
        return;
    }
    
    // Proses normal
    delete[] data;
}
```

**Solusi lebih baik dengan RAII pattern:**

```cpp
#include <memory>

void prosesData() {
    // unique_ptr otomatis dealokasi saat keluar scope
    std::unique_ptr<int[]> data(new int[100]);
    
    // ... proses data ...
    if (error) {
        return;  // Aman, unique_ptr akan dealokasi
    }
    
    // Tidak perlu delete manual
}
```

---

### SOLVED PROBLEM 10 â­â­

**Soal:** Apa yang salah dengan kode berikut? Jelaskan dan perbaiki!

```cpp
int* buatArray() {
    int arr[5] = {1, 2, 3, 4, 5};
    return arr;
}

int main() {
    int* hasil = buatArray();
    cout << hasil[0] << endl;
    return 0;
}
```

**Penyelesaian:**

**Masalah:** Fungsi mengembalikan pointer ke array lokal (stack-allocated). Ketika fungsi berakhir, array `arr` dihancurkan, sehingga `hasil` menjadi dangling pointer.

**Mengapa berbahaya:**
- Array lokal berada di stack
- Stack frame dihancurkan saat fungsi return
- Pointer yang dikembalikan menunjuk ke memori yang tidak valid
- Mengakses `hasil[0]` adalah undefined behavior

**Perbaikan menggunakan dynamic allocation:**

```cpp
int* buatArray() {
    int* arr = new int[5];  // Alokasi di heap
    for (int i = 0; i < 5; i++) {
        arr[i] = i + 1;
    }
    return arr;  // Aman, heap tidak dihancurkan saat return
}

int main() {
    int* hasil = buatArray();
    
    for (int i = 0; i < 5; i++) {
        cout << hasil[i] << " ";
    }
    cout << endl;
    
    delete[] hasil;  // Jangan lupa dealokasi!
    return 0;
}
```

---

## 7. Pengenalan Smart Pointer

### 7.1 Masalah dengan Raw Pointer

Raw pointer (`int*`, `char*`, dll) memiliki beberapa masalah:
- Tidak jelas siapa yang "memiliki" (owns) memori
- Mudah lupa dealokasi
- Exception safety sulit dicapai
- Kode menjadi rumit untuk menangani semua kasus

### 7.2 Smart Pointer di C++11

C++11 memperkenalkan smart pointer yang mengelola memori secara otomatis:

| Smart Pointer | Kepemilikan | Penggunaan |
|---------------|-------------|------------|
| `unique_ptr` | Exclusive (satu pemilik) | Default choice, tidak bisa di-copy |
| `shared_ptr` | Shared (banyak pemilik) | Ketika perlu berbagi kepemilikan |
| `weak_ptr` | Non-owning reference | Menghindari circular reference |

### 7.3 Contoh `unique_ptr`

```cpp
#include <iostream>
#include <memory>
using namespace std;

int main() {
    // Membuat unique_ptr
    unique_ptr<int> ptr1(new int(42));
    
    // Cara modern (C++14): make_unique
    // unique_ptr<int> ptr1 = make_unique<int>(42);
    
    cout << "Nilai: " << *ptr1 << endl;
    
    // unique_ptr tidak bisa di-copy
    // unique_ptr<int> ptr2 = ptr1;  // ERROR!
    
    // Tapi bisa di-move
    unique_ptr<int> ptr2 = move(ptr1);
    
    // Sekarang ptr1 adalah nullptr
    if (ptr1 == nullptr) {
        cout << "ptr1 sekarang null" << endl;
    }
    
    cout << "ptr2: " << *ptr2 << endl;
    
    // Otomatis dealokasi saat keluar scope
    return 0;
}
```

### 7.4 `unique_ptr` untuk Array

```cpp
#include <iostream>
#include <memory>
using namespace std;

int main() {
    // unique_ptr untuk array
    unique_ptr<int[]> arr(new int[5]);
    
    // Mengisi array
    for (int i = 0; i < 5; i++) {
        arr[i] = i * 10;
    }
    
    // Menampilkan
    for (int i = 0; i < 5; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
    
    // Tidak perlu delete[] - otomatis!
    return 0;
}
```

> **Catatan:** Smart pointer akan dibahas lebih detail pada mata kuliah Pemrograman Berorientasi Objek di Semester 3. Untuk saat ini, pahami konsep dasarnya sebagai solusi untuk masalah memory management.

---

### SOLVED PROBLEM 11 â­

**Soal:** Apa keuntungan utama menggunakan smart pointer dibandingkan raw pointer?

**Penyelesaian:**

**Keuntungan Smart Pointer:**

1. **Automatic Memory Management**
   - Memori otomatis didealokasi saat pointer keluar scope
   - Tidak perlu memanggil `delete` manual

2. **Exception Safety**
   - Jika exception terjadi, memori tetap didealokasi
   - Raw pointer dapat menyebabkan leak jika exception tidak ditangani

3. **Clear Ownership Semantics**
   - `unique_ptr`: satu pemilik, tidak ambigu
   - `shared_ptr`: kepemilikan bersama dengan reference counting

4. **Prevents Common Bugs**
   - Mencegah double-delete
   - Mencegah memory leak
   - Mencegah use-after-free (sebagian besar kasus)

5. **Self-documenting Code**
   - Kode lebih jelas tentang siapa yang mengelola memori

**Contoh perbandingan:**

```cpp
// Raw pointer - rawan error
void fungsiRaw() {
    int* ptr = new int(42);
    // Jika exception di sini, memory leak!
    riskyOperation();
    delete ptr;
}

// Smart pointer - aman
void fungsiSmart() {
    unique_ptr<int> ptr(new int(42));
    // Jika exception, ptr tetap dealokasi otomatis
    riskyOperation();
    // Tidak perlu delete
}
```

---

## 8. Array Dinamis

### 8.1 Keterbatasan Array Statis

Array statis di C++ memiliki keterbatasan:
- Ukuran harus diketahui saat compile time
- Tidak dapat berubah setelah deklarasi
- Membuang memori jika tidak digunakan penuh

```cpp
int arrStatis[100];  // Selalu menggunakan memori untuk 100 int
                     // Tidak bisa diperbesar
```

### 8.2 Implementasi Array Dinamis Sederhana

Array dinamis dapat tumbuh sesuai kebutuhan:

```cpp
#include <iostream>
#include <cstring>  // untuk memcpy
using namespace std;

class ArrayDinamis {
private:
    int* data;
    int ukuran;     // Jumlah elemen saat ini
    int kapasitas;  // Total kapasitas array

public:
    // Constructor
    ArrayDinamis(int kapasitasAwal = 10) {
        kapasitas = kapasitasAwal;
        ukuran = 0;
        data = new int[kapasitas];
    }
    
    // Destructor
    ~ArrayDinamis() {
        delete[] data;
    }
    
    // Tambah elemen
    void tambah(int nilai) {
        // Jika penuh, perbesar kapasitas
        if (ukuran == kapasitas) {
            perbesarKapasitas();
        }
        data[ukuran] = nilai;
        ukuran++;
    }
    
    // Akses elemen
    int ambil(int index) const {
        if (index < 0 || index >= ukuran) {
            throw out_of_range("Index di luar range!");
        }
        return data[index];
    }
    
    // Getter
    int getUkuran() const { return ukuran; }
    int getKapasitas() const { return kapasitas; }

private:
    // Perbesar kapasitas (double)
    void perbesarKapasitas() {
        int kapasitasBaru = kapasitas * 2;
        int* dataBaru = new int[kapasitasBaru];
        
        // Copy data lama ke array baru
        memcpy(dataBaru, data, ukuran * sizeof(int));
        
        // Hapus array lama
        delete[] data;
        
        // Update pointer dan kapasitas
        data = dataBaru;
        kapasitas = kapasitasBaru;
        
        cout << "[Info] Kapasitas diperbesar menjadi " 
             << kapasitas << endl;
    }
};

int main() {
    ArrayDinamis arr(3);  // Mulai dengan kapasitas 3
    
    cout << "Menambahkan elemen..." << endl;
    for (int i = 1; i <= 10; i++) {
        arr.tambah(i * 10);
        cout << "Tambah " << i * 10 
             << " | Ukuran: " << arr.getUkuran()
             << " | Kapasitas: " << arr.getKapasitas() << endl;
    }
    
    cout << "\nIsi array: ";
    for (int i = 0; i < arr.getUkuran(); i++) {
        cout << arr.ambil(i) << " ";
    }
    cout << endl;
    
    return 0;
}
```

**Output:**
```
Menambahkan elemen...
Tambah 10 | Ukuran: 1 | Kapasitas: 3
Tambah 20 | Ukuran: 2 | Kapasitas: 3
Tambah 30 | Ukuran: 3 | Kapasitas: 3
[Info] Kapasitas diperbesar menjadi 6
Tambah 40 | Ukuran: 4 | Kapasitas: 6
Tambah 50 | Ukuran: 5 | Kapasitas: 6
Tambah 60 | Ukuran: 6 | Kapasitas: 6
[Info] Kapasitas diperbesar menjadi 12
Tambah 70 | Ukuran: 7 | Kapasitas: 12
Tambah 80 | Ukuran: 8 | Kapasitas: 12
Tambah 90 | Ukuran: 9 | Kapasitas: 12
Tambah 100 | Ukuran: 10 | Kapasitas: 12

Isi array: 10 20 30 40 50 60 70 80 90 100
```

### 8.3 Strategi Pertumbuhan

| Strategi | Deskripsi | Kelebihan | Kekurangan |
|----------|-----------|-----------|------------|
| **Tambah tetap (+k)** | `newCap = oldCap + k` | Hemat memori | Banyak realokasi |
| **Lipat dua (Ã—2)** | `newCap = oldCap * 2` | Realokasi jarang | Boros memori |
| **Faktor 1.5** | `newCap = oldCap * 1.5` | Seimbang | Kompromi |

Strategi lipat dua memberikan amortized O(1) untuk operasi `tambah`.

---

### SOLVED PROBLEM 12 â­â­

**Soal:** Implementasikan method `hapus(int index)` untuk class ArrayDinamis!

**Penyelesaian:**

```cpp
// Tambahkan method ini ke class ArrayDinamis

void hapus(int index) {
    // Validasi index
    if (index < 0 || index >= ukuran) {
        throw out_of_range("Index di luar range!");
    }
    
    // Geser semua elemen setelah index ke kiri
    for (int i = index; i < ukuran - 1; i++) {
        data[i] = data[i + 1];
    }
    
    // Kurangi ukuran
    ukuran--;
    
    // Opsional: kurangi kapasitas jika terlalu banyak ruang kosong
    // if (ukuran < kapasitas / 4 && kapasitas > 10) {
    //     kurangiKapasitas();
    // }
}
```

**Ilustrasi proses hapus di index 2:**

![Proses Hapus Elemen Array](images/p01-05-array-delete-operation.png)

*Gambar 1.5: Ilustrasi proses penghapusan elemen pada array dinamis*


**Kompleksitas waktu:** O(n) karena perlu menggeser elemen

---

### SOLVED PROBLEM 13 â­â­

**Soal:** Mengapa strategi memperbesar array dengan mengalikan 2 lebih baik daripada menambah dengan konstanta tetap?

**Penyelesaian:**

**Analisis dengan menambahkan n elemen:**

**Strategi 1: Tambah tetap (+10)**
- Mulai kapasitas: 10
- Tambah 100 elemen â†’ realokasi saat: 10, 20, 30, 40, 50, 60, 70, 80, 90, 100
- Jumlah realokasi: 10 kali
- Total copy: 10+20+30+...+100 = **550 operasi copy**
- Kompleksitas per operasi: O(n) amortized

**Strategi 2: Lipat dua (Ã—2)**
- Mulai kapasitas: 10
- Tambah 100 elemen â†’ realokasi saat: 10, 20, 40, 80
- Jumlah realokasi: 4 kali
- Total copy: 10+20+40+80 = **150 operasi copy**
- Kompleksitas per operasi: O(1) amortized

**Tabel perbandingan untuk n operasi:**

| Strategi | Jumlah Realokasi | Total Copy | Amortized per Operasi |
|----------|------------------|------------|----------------------|
| +k (konstanta) | O(n/k) | O(nÂ²/k) | O(n) |
| Ã—2 (lipat dua) | O(log n) | O(n) | O(1) |

**Kesimpulan:** Strategi lipat dua memberikan performa amortized O(1) per operasi, jauh lebih efisien untuk jumlah operasi yang banyak.

---

### SOLVED PROBLEM 14 â­â­â­

**Soal:** Dalam konteks sistem pertahanan, jelaskan bagaimana array dinamis dapat digunakan untuk tracking objek radar dan implementasikan struktur dasarnya!

**Penyelesaian:**

**Skenario:** Sistem radar perlu melacak objek yang terdeteksi. Jumlah objek bervariasi dan tidak dapat diprediksi.

```cpp
#include <iostream>
#include <cstring>
#include <cmath>
using namespace std;

// Struktur untuk objek yang terdeteksi radar
struct ObjekRadar {
    int id;
    double jarak;      // km
    double azimuth;    // derajat
    double kecepatan;  // km/jam
    char jenis[20];    // pesawat, kapal, dll
    bool ancaman;
    
    void tampilkan() const {
        cout << "ID: " << id 
             << " | Jenis: " << jenis
             << " | Jarak: " << jarak << " km"
             << " | Azimuth: " << azimuth << "Â°"
             << " | Kecepatan: " << kecepatan << " km/jam"
             << " | Ancaman: " << (ancaman ? "YA" : "Tidak")
             << endl;
    }
};

class TrackerRadar {
private:
    ObjekRadar* objek;
    int jumlah;
    int kapasitas;
    int nextId;
    
    void perbesarKapasitas() {
        int kapasitasBaru = kapasitas * 2;
        ObjekRadar* dataBaru = new ObjekRadar[kapasitasBaru];
        memcpy(dataBaru, objek, jumlah * sizeof(ObjekRadar));
        delete[] objek;
        objek = dataBaru;
        kapasitas = kapasitasBaru;
        cout << "[SISTEM] Kapasitas tracking diperbesar: " 
             << kapasitas << " objek" << endl;
    }
    
public:
    TrackerRadar(int kapasitasAwal = 50) {
        kapasitas = kapasitasAwal;
        jumlah = 0;
        nextId = 1001;
        objek = new ObjekRadar[kapasitas];
    }
    
    ~TrackerRadar() {
        delete[] objek;
    }
    
    // Deteksi objek baru
    int deteksiObjek(double jarak, double azimuth, 
                     double kecepatan, const char* jenis) {
        if (jumlah == kapasitas) {
            perbesarKapasitas();
        }
        
        ObjekRadar& obj = objek[jumlah];
        obj.id = nextId++;
        obj.jarak = jarak;
        obj.azimuth = azimuth;
        obj.kecepatan = kecepatan;
        strncpy(obj.jenis, jenis, 19);
        obj.jenis[19] = '\0';
        
        // Analisis ancaman sederhana
        obj.ancaman = (jarak < 100 && kecepatan > 500);
        
        jumlah++;
        
        if (obj.ancaman) {
            cout << "[PERINGATAN] Objek ancaman terdeteksi! ID: " 
                 << obj.id << endl;
        }
        
        return obj.id;
    }
    
    // Hapus objek yang hilang dari radar
    bool hapusObjek(int id) {
        for (int i = 0; i < jumlah; i++) {
            if (objek[i].id == id) {
                // Geser elemen
                for (int j = i; j < jumlah - 1; j++) {
                    objek[j] = objek[j + 1];
                }
                jumlah--;
                return true;
            }
        }
        return false;
    }
    
    // Update posisi objek
    void updatePosisi(int id, double jarakBaru, double azimuthBaru) {
        for (int i = 0; i < jumlah; i++) {
            if (objek[i].id == id) {
                objek[i].jarak = jarakBaru;
                objek[i].azimuth = azimuthBaru;
                objek[i].ancaman = (jarakBaru < 100 && 
                                   objek[i].kecepatan > 500);
                return;
            }
        }
    }
    
    // Tampilkan semua objek
    void tampilkanSemua() const {
        cout << "\n=== STATUS RADAR ===" << endl;
        cout << "Total objek: " << jumlah << "/" << kapasitas << endl;
        cout << "-------------------" << endl;
        for (int i = 0; i < jumlah; i++) {
            objek[i].tampilkan();
        }
    }
    
    // Hitung jumlah ancaman
    int hitungAncaman() const {
        int count = 0;
        for (int i = 0; i < jumlah; i++) {
            if (objek[i].ancaman) count++;
        }
        return count;
    }
};

int main() {
    TrackerRadar radar(5);  // Mulai dengan kapasitas kecil untuk demo
    
    cout << "=== SIMULASI SISTEM RADAR ===" << endl << endl;
    
    // Deteksi beberapa objek
    radar.deteksiObjek(250, 45, 200, "Pesawat Komersial");
    radar.deteksiObjek(80, 120, 600, "Jet Tempur");
    radar.deteksiObjek(150, 200, 50, "Kapal Kargo");
    radar.deteksiObjek(50, 90, 800, "Rudal");
    radar.deteksiObjek(300, 270, 150, "Helikopter");
    radar.deteksiObjek(75, 180, 650, "Drone");
    
    radar.tampilkanSemua();
    
    cout << "\n[INFO] Total ancaman terdeteksi: " 
         << radar.hitungAncaman() << endl;
    
    return 0;
}
```

**Analisis Desain:**

1. **Dynamic Sizing**: Sistem dapat menangani jumlah objek yang tidak terduga
2. **Automatic Growth**: Kapasitas bertambah otomatis saat diperlukan
3. **Real-time Updates**: Posisi objek dapat diupdate terus-menerus
4. **Threat Assessment**: Analisis ancaman terintegrasi

---

### SOLVED PROBLEM 15 â­

**Soal:** Apa yang terjadi jika kita tidak mengimplementasikan destructor pada class ArrayDinamis?

**Penyelesaian:**

**Jika tidak ada destructor:**

```cpp
class ArrayDinamisTanpaDestructor {
private:
    int* data;
    int ukuran;
    int kapasitas;
    
public:
    ArrayDinamisTanpaDestructor(int kap = 10) {
        kapasitas = kap;
        ukuran = 0;
        data = new int[kapasitas];  // Alokasi di heap
    }
    
    // TIDAK ADA DESTRUCTOR!
    // ~ArrayDinamisTanpaDestructor() { delete[] data; }
};

void fungsiMasalah() {
    ArrayDinamisTanpaDestructor arr(100);
    // arr.data menunjuk ke 100 integer di heap
    
}   // arr keluar scope, TAPI data di heap TIDAK didealokasi!
    // Memory leak sebesar 100 * sizeof(int) = 400 bytes
```

**Konsekuensi:**

1. **Memory Leak**: Setiap kali objek ArrayDinamis dibuat dan dihancurkan, memori heap tidak dibebaskan

2. **Akumulasi**: Jika objek dibuat berkali-kali (misalnya dalam loop), memory leak terakumulasi

3. **Crash**: Program akhirnya kehabisan memori dan crash

4. **Resource Exhaustion**: Dalam sistem yang berjalan lama (seperti server), ini sangat berbahaya

**Solusi wajib:**

```cpp
~ArrayDinamis() {
    delete[] data;  // WAJIB ada untuk mencegah memory leak
}
```

---

### SOLVED PROBLEM 16 â­â­

**Soal:** Implementasikan fungsi `cariMaksimum` yang menerima array dinamis dan ukurannya, kemudian mengembalikan nilai maksimum menggunakan pointer arithmetic!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

int cariMaksimum(int* arr, int ukuran) {
    if (ukuran <= 0) {
        throw invalid_argument("Ukuran harus positif!");
    }
    
    int* ptr = arr;           // Pointer ke elemen pertama
    int* akhir = arr + ukuran; // Pointer melewati elemen terakhir
    int maks = *ptr;          // Inisialisasi dengan elemen pertama
    
    // Traverse menggunakan pointer
    while (ptr < akhir) {
        if (*ptr > maks) {
            maks = *ptr;
        }
        ptr++;  // Pindah ke elemen berikutnya
    }
    
    return maks;
}

int main() {
    // Buat array dinamis
    int ukuran = 7;
    int* data = new int[ukuran];
    
    // Isi dengan nilai
    data[0] = 23;
    data[1] = 45;
    data[2] = 12;
    data[3] = 89;
    data[4] = 34;
    data[5] = 67;
    data[6] = 56;
    
    // Cari maksimum
    int hasil = cariMaksimum(data, ukuran);
    
    cout << "Array: ";
    for (int i = 0; i < ukuran; i++) {
        cout << data[i] << " ";
    }
    cout << endl;
    
    cout << "Nilai maksimum: " << hasil << endl;
    
    // Dealokasi
    delete[] data;
    
    return 0;
}
```

**Output:**
```
Array: 23 45 12 89 34 67 56 
Nilai maksimum: 89
```

**Penjelasan Pointer Arithmetic:**
- `ptr++` memindahkan pointer ke elemen berikutnya (bukan +1 byte, tapi +sizeof(int))
- `ptr < akhir` membandingkan alamat untuk mengecek batas array
- `*ptr` mengakses nilai di alamat yang ditunjuk

---

### SOLVED PROBLEM 17 â­â­â­

**Soal:** Implementasikan fungsi yang menggabungkan dua array dinamis menjadi satu array baru yang terurut (merge)!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

// Fungsi untuk menggabungkan dua array terurut
// Asumsi: arr1 dan arr2 sudah terurut ascending
int* gabungTerurut(int* arr1, int ukuran1, 
                   int* arr2, int ukuran2, 
                   int& ukuranHasil) {
    ukuranHasil = ukuran1 + ukuran2;
    int* hasil = new int[ukuranHasil];
    
    int i = 0;  // Index untuk arr1
    int j = 0;  // Index untuk arr2
    int k = 0;  // Index untuk hasil
    
    // Merge selama kedua array masih punya elemen
    while (i < ukuran1 && j < ukuran2) {
        if (arr1[i] <= arr2[j]) {
            hasil[k] = arr1[i];
            i++;
        } else {
            hasil[k] = arr2[j];
            j++;
        }
        k++;
    }
    
    // Salin sisa arr1 (jika ada)
    while (i < ukuran1) {
        hasil[k] = arr1[i];
        i++;
        k++;
    }
    
    // Salin sisa arr2 (jika ada)
    while (j < ukuran2) {
        hasil[k] = arr2[j];
        j++;
        k++;
    }
    
    return hasil;
}

int main() {
    // Array pertama (terurut)
    int ukuran1 = 5;
    int* arr1 = new int[ukuran1];
    arr1[0] = 1; arr1[1] = 3; arr1[2] = 5; arr1[3] = 7; arr1[4] = 9;
    
    // Array kedua (terurut)
    int ukuran2 = 4;
    int* arr2 = new int[ukuran2];
    arr2[0] = 2; arr2[1] = 4; arr2[2] = 6; arr2[3] = 8;
    
    // Gabungkan
    int ukuranHasil;
    int* hasil = gabungTerurut(arr1, ukuran1, arr2, ukuran2, ukuranHasil);
    
    // Tampilkan
    cout << "Array 1: ";
    for (int i = 0; i < ukuran1; i++) cout << arr1[i] << " ";
    cout << endl;
    
    cout << "Array 2: ";
    for (int i = 0; i < ukuran2; i++) cout << arr2[i] << " ";
    cout << endl;
    
    cout << "Hasil merge: ";
    for (int i = 0; i < ukuranHasil; i++) cout << hasil[i] << " ";
    cout << endl;
    
    // Dealokasi semua array
    delete[] arr1;
    delete[] arr2;
    delete[] hasil;
    
    return 0;
}
```

**Output:**
```
Array 1: 1 3 5 7 9 
Array 2: 2 4 6 8 
Hasil merge: 1 2 3 4 5 6 7 8 9 
```

**Kompleksitas:**
- Waktu: O(n + m) dimana n dan m adalah ukuran kedua array
- Ruang: O(n + m) untuk array hasil

**Catatan:** Algoritma ini adalah dasar dari Merge Sort yang akan dipelajari pada Pertemuan 10.

---

### SOLVED PROBLEM 18 â­â­

**Soal:** Jelaskan apa yang terjadi di memori saat kode berikut dieksekusi!

```cpp
int* p1 = new int(10);
int* p2 = p1;
delete p1;
*p2 = 20;  // ???
```

**Penyelesaian:**

![Dangling Pointer Step by Step](images/p01-06-dangling-pointer-steps.png)

*Gambar 1.6: Proses terjadinya dangling pointer â€” langkah demi langkah*


**Penjelasan langkah:**

| Langkah | Kode | Stack | Heap | Status |
|---------|------|-------|------|--------|
| 1 | `int* p1 = new int(10);` | p1 â†’ 0x1000 | [0x1000]: 10 | âœ… Valid |
| 2 | `int* p2 = p1;` | p1, p2 â†’ 0x1000 | [0x1000]: 10 | âœ… Valid (shallow copy) |
| 3 | `delete p1;` | p1, p2 â†’ 0x1000 | [0x1000]: ??? | âŒ Dangling! |
| 4 | `*p2 = 20;` | - | - | âš ï¸ UNDEFINED BEHAVIOR! |

**Bahaya:** Memori di 0x1000 didealokasi, tapi p1 dan p2 masih menyimpan alamat tersebut â†’ **dangling pointer**.

**Kemungkinan yang bisa terjadi:**
- Tampak berhasil (berbahaya karena bisa corrupt data lain)
- Crash (segmentation fault)
- Memodifikasi data program lain

**Solusi yang benar:**

```cpp
int* p1 = new int(10);
int* p2 = p1;
*p2 = 20;  // Ubah nilai SEBELUM delete
delete p1;
p1 = nullptr;
p2 = nullptr;  // Penting: set semua pointer yang merujuk ke sini
```

---

### SOLVED PROBLEM 19 â­â­â­

**Soal:** Implementasikan class Matrix2D yang menggunakan dynamic memory allocation untuk matriks 2D dengan ukuran yang ditentukan saat runtime!

**Penyelesaian:**

```cpp
#include <iostream>
#include <iomanip>
using namespace std;

class Matrix2D {
private:
    double** data;
    int baris;
    int kolom;
    
public:
    // Constructor
    Matrix2D(int b, int k) : baris(b), kolom(k) {
        // Alokasi array of pointers
        data = new double*[baris];
        
        // Alokasi setiap baris
        for (int i = 0; i < baris; i++) {
            data[i] = new double[kolom];
            // Inisialisasi dengan 0
            for (int j = 0; j < kolom; j++) {
                data[i][j] = 0.0;
            }
        }
    }
    
    // Destructor
    ~Matrix2D() {
        // Dealokasi setiap baris
        for (int i = 0; i < baris; i++) {
            delete[] data[i];
        }
        // Dealokasi array of pointers
        delete[] data;
    }
    
    // Set nilai
    void set(int i, int j, double nilai) {
        if (i < 0 || i >= baris || j < 0 || j >= kolom) {
            throw out_of_range("Index di luar range!");
        }
        data[i][j] = nilai;
    }
    
    // Get nilai
    double get(int i, int j) const {
        if (i < 0 || i >= baris || j < 0 || j >= kolom) {
            throw out_of_range("Index di luar range!");
        }
        return data[i][j];
    }
    
    // Tampilkan matriks
    void tampilkan() const {
        for (int i = 0; i < baris; i++) {
            for (int j = 0; j < kolom; j++) {
                cout << setw(8) << fixed << setprecision(2) 
                     << data[i][j] << " ";
            }
            cout << endl;
        }
    }
    
    // Penjumlahan matriks
    Matrix2D operator+(const Matrix2D& other) const {
        if (baris != other.baris || kolom != other.kolom) {
            throw invalid_argument("Dimensi matriks tidak cocok!");
        }
        
        Matrix2D hasil(baris, kolom);
        for (int i = 0; i < baris; i++) {
            for (int j = 0; j < kolom; j++) {
                hasil.data[i][j] = data[i][j] + other.data[i][j];
            }
        }
        return hasil;
    }
    
    // Getter dimensi
    int getBaris() const { return baris; }
    int getKolom() const { return kolom; }
};

int main() {
    cout << "=== Demo Matrix 2D Dinamis ===" << endl << endl;
    
    // Buat matriks 3x3
    Matrix2D A(3, 3);
    Matrix2D B(3, 3);
    
    // Isi matriks A
    A.set(0, 0, 1); A.set(0, 1, 2); A.set(0, 2, 3);
    A.set(1, 0, 4); A.set(1, 1, 5); A.set(1, 2, 6);
    A.set(2, 0, 7); A.set(2, 1, 8); A.set(2, 2, 9);
    
    // Isi matriks B
    B.set(0, 0, 9); B.set(0, 1, 8); B.set(0, 2, 7);
    B.set(1, 0, 6); B.set(1, 1, 5); B.set(1, 2, 4);
    B.set(2, 0, 3); B.set(2, 1, 2); B.set(2, 2, 1);
    
    cout << "Matriks A:" << endl;
    A.tampilkan();
    
    cout << "\nMatriks B:" << endl;
    B.tampilkan();
    
    // Penjumlahan
    Matrix2D C = A + B;
    
    cout << "\nA + B:" << endl;
    C.tampilkan();
    
    return 0;
}
```

**Output:**
```
=== Demo Matrix 2D Dinamis ===

Matriks A:
    1.00     2.00     3.00 
    4.00     5.00     6.00 
    7.00     8.00     9.00 

Matriks B:
    9.00     8.00     7.00 
    6.00     5.00     4.00 
    3.00     2.00     1.00 

A + B:
   10.00    10.00    10.00 
   10.00    10.00    10.00 
   10.00    10.00    10.00 
```

**Catatan penting:**
- Matriks 2D dialokasikan sebagai "array of arrays"
- Destructor harus dealokasi dalam urutan yang benar (inner arrays dulu, baru outer array)
- Class ini belum mengimplementasikan copy constructor dan assignment operator (akan dipelajari di OOP Semester 3)

---

### SOLVED PROBLEM 20 â­

**Soal:** Apa output dari program berikut?

```cpp
int main() {
    int* arr = new int[5]{10, 20, 30, 40, 50};
    int* p = arr + 2;
    cout << *p << " " << *(p-1) << " " << *(p+1) << endl;
    delete[] arr;
    return 0;
}
```

**Penyelesaian:**

**Output:** `30 20 40`

**Penjelasan:**

1. `int* arr = new int[5]{10, 20, 30, 40, 50};`
   - Buat array di heap: `[10, 20, 30, 40, 50]`
   - arr menunjuk ke elemen pertama (index 0)

2. `int* p = arr + 2;`
   - p menunjuk ke elemen di index 2 (nilai 30)
   - Pointer arithmetic: arr + 2 = alamat arr + (2 Ã— sizeof(int))

3. `*p` â†’ nilai di index 2 = **30**

4. `*(p-1)` â†’ nilai di index 1 = **20**

5. `*(p+1)` â†’ nilai di index 3 = **40**

![Pointer Arithmetic Visualization](images/p01-07-pointer-arithmetic-array.png)

*Gambar 1.7: Visualisasi pointer arithmetic pada array*


---

### SOLVED PROBLEM 21 â­â­â­

**Soal:** Implementasikan fungsi yang melakukan operasi resize pada array dinamis dengan mempertahankan data yang ada!

**Penyelesaian:**

```cpp
#include <iostream>
#include <cstring>
using namespace std;

// Fungsi resize array dinamis
// Mengembalikan pointer ke array baru
// Parameter ukuranLama dan ukuranBaru di-pass by reference
// untuk melacak perubahan ukuran
int* resizeArray(int* arrLama, int ukuranLama, int ukuranBaru) {
    // Alokasi array baru
    int* arrBaru = new int[ukuranBaru];
    
    // Tentukan berapa banyak elemen yang di-copy
    int elemenCopy = (ukuranLama < ukuranBaru) ? ukuranLama : ukuranBaru;
    
    // Copy data dari array lama ke array baru
    for (int i = 0; i < elemenCopy; i++) {
        arrBaru[i] = arrLama[i];
    }
    
    // Jika ukuran baru lebih besar, inisialisasi elemen baru dengan 0
    for (int i = elemenCopy; i < ukuranBaru; i++) {
        arrBaru[i] = 0;
    }
    
    // Dealokasi array lama
    delete[] arrLama;
    
    return arrBaru;
}

void tampilkanArray(int* arr, int ukuran, const char* label) {
    cout << label << " (ukuran " << ukuran << "): [";
    for (int i = 0; i < ukuran; i++) {
        cout << arr[i];
        if (i < ukuran - 1) cout << ", ";
    }
    cout << "]" << endl;
}

int main() {
    // Buat array awal
    int ukuran = 5;
    int* data = new int[ukuran];
    for (int i = 0; i < ukuran; i++) {
        data[i] = (i + 1) * 10;
    }
    
    tampilkanArray(data, ukuran, "Array awal");
    
    // Perbesar array
    cout << "\n--- Memperbesar ke ukuran 8 ---" << endl;
    ukuran = 8;
    data = resizeArray(data, 5, ukuran);
    tampilkanArray(data, ukuran, "Setelah resize");
    
    // Isi elemen baru
    data[5] = 60;
    data[6] = 70;
    data[7] = 80;
    tampilkanArray(data, ukuran, "Setelah isi data");
    
    // Perkecil array
    cout << "\n--- Memperkecil ke ukuran 3 ---" << endl;
    int ukuranLama = ukuran;
    ukuran = 3;
    data = resizeArray(data, ukuranLama, ukuran);
    tampilkanArray(data, ukuran, "Setelah resize");
    
    // Cleanup
    delete[] data;
    
    return 0;
}
```

**Output:**
```
Array awal (ukuran 5): [10, 20, 30, 40, 50]

--- Memperbesar ke ukuran 8 ---
Setelah resize (ukuran 8): [10, 20, 30, 40, 50, 0, 0, 0]
Setelah isi data (ukuran 8): [10, 20, 30, 40, 50, 60, 70, 80]

--- Memperkecil ke ukuran 3 ---
Setelah resize (ukuran 3): [10, 20, 30]
```

**Poin penting:**
- Fungsi harus dealokasi array lama untuk mencegah memory leak
- Saat memperbesar, elemen baru diinisialisasi dengan nilai default
- Saat memperkecil, data yang "tidak muat" akan hilang
- Caller harus menggunakan return value (pointer baru), bukan pointer lama

---

### SOLVED PROBLEM 22 â­â­â­

**Soal:** Implementasikan class Stack sederhana menggunakan array dinamis yang dapat tumbuh otomatis!

**Penyelesaian:**

```cpp
#include <iostream>
#include <stdexcept>
using namespace std;

class StackDinamis {
private:
    int* data;
    int top;        // Index elemen teratas
    int kapasitas;
    
    void perbesarKapasitas() {
        int kapasitasBaru = kapasitas * 2;
        int* dataBaru = new int[kapasitasBaru];
        
        // Copy data
        for (int i = 0; i <= top; i++) {
            dataBaru[i] = data[i];
        }
        
        delete[] data;
        data = dataBaru;
        kapasitas = kapasitasBaru;
        
        cout << "[Stack] Kapasitas diperbesar: " << kapasitas << endl;
    }
    
public:
    // Constructor
    StackDinamis(int kapasitasAwal = 10) {
        kapasitas = kapasitasAwal;
        top = -1;  // Stack kosong
        data = new int[kapasitas];
    }
    
    // Destructor
    ~StackDinamis() {
        delete[] data;
    }
    
    // Push: tambah elemen ke puncak
    void push(int nilai) {
        if (top == kapasitas - 1) {
            perbesarKapasitas();
        }
        data[++top] = nilai;
    }
    
    // Pop: hapus dan kembalikan elemen puncak
    int pop() {
        if (isEmpty()) {
            throw underflow_error("Stack kosong!");
        }
        return data[top--];
    }
    
    // Peek: lihat elemen puncak tanpa menghapus
    int peek() const {
        if (isEmpty()) {
            throw underflow_error("Stack kosong!");
        }
        return data[top];
    }
    
    // Cek apakah kosong
    bool isEmpty() const {
        return top == -1;
    }
    
    // Jumlah elemen
    int size() const {
        return top + 1;
    }
    
    // Tampilkan isi stack
    void tampilkan() const {
        cout << "Stack (bawah ke atas): [";
        for (int i = 0; i <= top; i++) {
            cout << data[i];
            if (i < top) cout << ", ";
        }
        cout << "]" << endl;
        cout << "Ukuran: " << size() << ", Kapasitas: " << kapasitas << endl;
    }
};

int main() {
    cout << "=== Demo Stack Dinamis ===" << endl << endl;
    
    StackDinamis stack(3);  // Kapasitas awal kecil untuk demo
    
    // Push beberapa elemen
    cout << "Push: 10, 20, 30, 40, 50" << endl;
    stack.push(10);
    stack.push(20);
    stack.push(30);
    stack.push(40);  // Akan trigger resize
    stack.push(50);
    
    stack.tampilkan();
    
    // Peek
    cout << "\nPeek: " << stack.peek() << endl;
    
    // Pop beberapa elemen
    cout << "\nPop 3 elemen:" << endl;
    for (int i = 0; i < 3; i++) {
        cout << "Pop: " << stack.pop() << endl;
    }
    
    stack.tampilkan();
    
    return 0;
}
```

**Output:**
```
=== Demo Stack Dinamis ===

Push: 10, 20, 30, 40, 50
[Stack] Kapasitas diperbesar: 6
Stack (bawah ke atas): [10, 20, 30, 40, 50]
Ukuran: 5, Kapasitas: 6

Peek: 50

Pop 3 elemen:
Pop: 50
Pop: 40
Pop: 30
Stack (bawah ke atas): [10, 20]
Ukuran: 2, Kapasitas: 6
```

**Catatan:** Stack akan dipelajari lebih detail pada Pertemuan 5.

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan. Jawaban singkat tersedia di bagian akhir.

### Problem S1 â­
Apa output dari kode berikut?
```cpp
int a = 5;
int* p = &a;
int** pp = &p;
**pp = 10;
cout << a << endl;
```

### Problem S2 â­â­
Tuliskan fungsi `void isiDescending(int* arr, int n)` yang mengisi array dengan nilai n, n-1, n-2, ..., 1 menggunakan pointer arithmetic!

### Problem S3 â­â­
Identifikasi semua potensi masalah dalam kode berikut:
```cpp
int* buat() {
    int x = 100;
    return &x;
}
int main() {
    int* p = buat();
    cout << *p;
    return 0;
}
```

### Problem S4 â­â­â­
Implementasikan fungsi yang membalik array secara in-place menggunakan two-pointer technique!

### Problem S5 â­â­â­
Jelaskan perbedaan antara shallow copy dan deep copy dalam konteks dynamic memory allocation. Berikan contoh kode yang menunjukkan masalah dengan shallow copy!

---

## Ringkasan

| Konsep | Deskripsi | Contoh/Catatan |
|--------|-----------|----------------|
| **Struktur Data** | Cara mengorganisasi data dalam memori | Linear (array, list) dan non-linear (tree, graph) |
| **ADT** | Model matematis yang mendefinisikan operasi tanpa detail implementasi | Stack ADT: push, pop, peek, isEmpty |
| **Pointer** | Variabel yang menyimpan alamat memori | `int* ptr = &var;` |
| **Referensi** | Alias untuk variabel lain | `int& ref = var;` |
| **new** | Alokasi memori di heap | `int* p = new int;` |
| **delete** | Dealokasi memori heap | `delete p;` untuk single, `delete[] arr;` untuk array |
| **Memory Leak** | Memori yang dialokasi tidak pernah didealokasi | Penyebab: lupa delete, early return |
| **Dangling Pointer** | Pointer yang menunjuk ke memori tidak valid | Setelah delete, saat variabel lokal keluar scope |
| **Smart Pointer** | Pointer yang mengelola memori otomatis | `unique_ptr`, `shared_ptr` (C++11) |
| **Array Dinamis** | Array yang ukurannya dapat berubah saat runtime | Strategi resize: double capacity |

---

## Jawaban Supplementary Problems

**SP-1:** `10`
- `pp` adalah pointer ke pointer
- `**pp` mengakses nilai yang ditunjuk oleh `p`, yaitu `a`
- Mengubah `**pp` sama dengan mengubah `a`

**SP-2:**
```cpp
void isiDescending(int* arr, int n) {
    int* ptr = arr;
    for (int i = n; i >= 1; i--) {
        *ptr++ = i;  // Set nilai dan increment pointer
    }
}
```

**SP-3:** 
- Mengembalikan alamat variabel lokal â†’ dangling pointer
- `x` dihancurkan saat fungsi berakhir
- Mengakses `*p` adalah undefined behavior

**SP-4:**
```cpp
void balikArray(int* arr, int n) {
    int* kiri = arr;
    int* kanan = arr + n - 1;
    while (kiri < kanan) {
        int temp = *kiri;
        *kiri = *kanan;
        *kanan = temp;
        kiri++;
        kanan--;
    }
}
```

**SP-5:** 
- **Shallow copy**: Copy alamat pointer (kedua objek menunjuk ke memori yang sama)
- **Deep copy**: Alokasi memori baru dan copy nilai
- Masalah shallow copy: double-free saat kedua objek didestruksi

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 10.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 1.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapters 1-2.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

Â© 2026 Anindito
