# Latihan Mandiri 01: Pengantar Struktur Data dan Review C++ Lanjut

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 01  
**Topik:** Pengantar Struktur Data dan Review C++ Lanjut  
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
Manakah pernyataan yang **BENAR** tentang Abstract Data Type (ADT)?

A. ADT menjelaskan bagaimana data disimpan dalam memori  
B. ADT fokus pada implementasi detail dari struktur data  
C. ADT mendefinisikan operasi yang dapat dilakukan tanpa menentukan cara implementasinya  
D. ADT hanya dapat diimplementasikan dengan satu cara  
E. ADT sama dengan struktur data konkret  

### Soal 2
Perhatikan kode berikut:
```cpp
int x = 10;
int* p = &x;
int** pp = &p;
cout << **pp;
```
Berapakah output dari kode di atas?

A. Alamat memori x  
B. Alamat memori p  
C. 10  
D. Error kompilasi  
E. Undefined behavior  

### Soal 3
Apa perbedaan utama antara Stack memory dan Heap memory?

A. Stack lebih besar dari Heap  
B. Heap dialokasi otomatis, Stack manual  
C. Stack dialokasi otomatis, Heap perlu dialokasi manual  
D. Keduanya sama-sama otomatis  
E. Stack hanya untuk array, Heap untuk variabel  

### Soal 4
Manakah yang merupakan contoh struktur data **non-linear**?

A. Array  
B. Queue  
C. Stack  
D. Binary Tree  
E. Linked List  

### Soal 5
Perhatikan kode berikut:
```cpp
int* arr = new int[50];
delete arr;
```
Apa masalah dengan kode di atas?

A. Tidak ada masalah  
B. Seharusnya menggunakan `delete[] arr`  
C. Seharusnya `new int(50)`  
D. Variabel `arr` tidak diinisialisasi  
E. Ukuran array terlalu besar  

### Soal 6
Manakah pernyataan yang **BENAR** tentang referensi dalam C++?

A. Referensi dapat di-reassign ke variabel lain  
B. Referensi dapat bernilai null  
C. Referensi harus diinisialisasi saat deklarasi  
D. Referensi memiliki alamat memori sendiri  
E. Referensi sama dengan pointer  

### Soal 7
Apa yang dimaksud dengan "memory leak"?

A. Memori yang corrupt  
B. Memori yang dialokasikan tapi tidak pernah didealokasi  
C. Pointer yang menunjuk ke memori yang sudah dihapus  
D. Memori yang tidak cukup  
E. Kesalahan akses memori  

### Soal 8
Perhatikan kode berikut:
```cpp
void fungsi(int& x) {
    x = x * 2;
}
int main() {
    int a = 5;
    fungsi(a);
    cout << a;
}
```
Berapakah output dari kode di atas?

A. 5  
B. 10  
C. 0  
D. Error kompilasi  
E. Undefined behavior  

### Soal 9
Manakah yang merupakan komponen dari ADT?

A. Hanya data dan operasi  
B. Hanya operasi dan aturan  
C. Data, operasi, dan aturan/aksioma  
D. Hanya implementasi  
E. Hanya data  

### Soal 10
Perhatikan kode berikut:
```cpp
int arr[5] = {10, 20, 30, 40, 50};
int* p = arr + 3;
cout << *p;
```
Berapakah output dari kode di atas?

A. 10  
B. 20  
C. 30  
D. 40  
E. 50  

### Soal 11
Apa yang dimaksud dengan "dangling pointer"?

A. Pointer yang bernilai null  
B. Pointer yang menunjuk ke memori yang sudah tidak valid  
C. Pointer yang tidak diinisialisasi  
D. Pointer ke pointer  
E. Pointer yang menunjuk ke array  

### Soal 12
Perhatikan kode berikut:
```cpp
int* buatData() {
    int data = 100;
    return &data;
}
int main() {
    int* p = buatData();
    cout << *p;
}
```
Apa yang salah dengan kode di atas?

A. Tidak ada yang salah  
B. Mengembalikan alamat variabel lokal (dangling pointer)  
C. Seharusnya menggunakan referensi  
D. Tipe data tidak sesuai  
E. Fungsi tidak boleh mengembalikan pointer  

### Soal 13
Manakah smart pointer yang memiliki **satu pemilik** (exclusive ownership)?

A. `shared_ptr`  
B. `weak_ptr`  
C. `unique_ptr`  
D. `auto_ptr`  
E. `raw_ptr`  

### Soal 14
Dalam strategi pertumbuhan array dinamis, mengapa "lipat dua" (×2) lebih efisien daripada "tambah tetap" (+k)?

A. Menggunakan lebih sedikit memori  
B. Memberikan amortized O(1) per operasi  
C. Tidak pernah memerlukan realokasi  
D. Lebih mudah diimplementasikan  
E. Tidak ada perbedaan signifikan  

### Soal 15
Perhatikan kode berikut:
```cpp
int* p = new int(42);
int* q = p;
delete p;
p = nullptr;
```
Setelah eksekusi kode di atas, apa status pointer `q`?

A. Null pointer  
B. Dangling pointer  
C. Menunjuk ke nilai 42  
D. Error kompilasi  
E. Menunjuk ke alamat p  

### Soal 16
Manakah operasi yang **BUKAN** merupakan operasi dasar ADT Stack?

A. push()  
B. pop()  
C. peek()  
D. insert(index)  
E. isEmpty()  

### Soal 17
Perhatikan kode berikut:
```cpp
int x = 5, y = 10;
int* px = &x;
int* py = &y;
*px = *py;
cout << x << " " << y;
```
Berapakah output dari kode di atas?

A. 5 10  
B. 10 5  
C. 10 10  
D. 5 5  
E. Error kompilasi  

### Soal 18
Apa keuntungan utama menggunakan ADT dalam desain program?

A. Program berjalan lebih cepat  
B. Menggunakan lebih sedikit memori  
C. Abstraksi yang memisahkan interface dari implementasi  
D. Tidak perlu menggunakan pointer  
E. Kode lebih pendek  

### Soal 19
Perhatikan kode berikut:
```cpp
void tukar(int* a, int* b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}
int main() {
    int x = 3, y = 7;
    tukar(&x, &y);
    cout << x << " " << y;
}
```
Berapakah output dari kode di atas?

A. 3 7  
B. 7 3  
C. 7 7  
D. 3 3  
E. Error kompilasi  

### Soal 20
Manakah praktik terbaik dalam mengelola dynamic memory?

A. Tidak perlu menggunakan delete karena otomatis  
B. Set pointer ke nullptr setelah delete  
C. Selalu gunakan global pointer  
D. Hindari penggunaan new sama sekali  
E. Gunakan delete[] untuk semua alokasi  

---

## Bagian B: Soal Uraian (8 Soal)

### Soal 1 (Mudah)
Jelaskan perbedaan antara ADT dan struktur data konkret! Berikan contoh masing-masing satu!

### Soal 2 (Mudah)
Perhatikan kode berikut:
```cpp
int main() {
    int arr[] = {1, 2, 3, 4, 5};
    int* p = arr;
    
    cout << *(p + 2) << endl;
    cout << *(arr + 4) << endl;
    cout << p[3] << endl;
    
    return 0;
}
```
Tuliskan output dari program di atas dan jelaskan mengapa!

### Soal 3 (Mudah)
Jelaskan tiga penyebab memory leak dan bagaimana cara mencegahnya!

### Soal 4 (Sedang)
Perhatikan kode berikut:
```cpp
class Data {
private:
    int* values;
    int size;
    
public:
    Data(int n) {
        size = n;
        values = new int[n];
    }
};

int main() {
    Data d1(100);
    Data d2(200);
    return 0;
}
```
Identifikasi masalah dalam kode di atas dan tuliskan perbaikannya!

### Soal 5 (Mudah)
Bandingkan pass-by-value, pass-by-reference, dan pass-by-pointer dalam konteks parameter fungsi! Kapan sebaiknya menggunakan masing-masing?

### Soal 6 (Sedang)
Tuliskan fungsi C++ `double hitungRata(int* arr, int n)` yang menghitung rata-rata elemen array menggunakan pointer arithmetic!

### Soal 7 (Mudah)
Jelaskan konsep LIFO pada Stack dan berikan 4 contoh aplikasi nyata yang menggunakan Stack!

### Soal 8 (Sulit)
Implementasikan method `tambah(int nilai)` dan destructor untuk class ArrayDinamis yang menggunakan strategi pertumbuhan ×2!

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Komunikasi Taktis

**Latar Belakang:**
Unit komunikasi pertahanan memerlukan sistem penyimpanan pesan taktis yang efisien. Setiap pesan memiliki atribut: ID, pengirim (max 50 karakter), isi pesan (panjang variabel), timestamp, dan status baca.

**Tugas:**
a. **(2 poin)** Rancang struktur data `Pesan` yang tepat dengan mempertimbangkan efisiensi memori!

b. **(2 poin)** Jelaskan mengapa isi pesan sebaiknya menggunakan dynamic memory allocation!

c. **(3 poin)** Implementasikan fungsi `bool tambahPesan(...)` yang menambahkan pesan baru ke array pesan dengan kapasitas dinamis!

---

### Studi Kasus 2: Sistem Tracking Kendaraan

**Latar Belakang:**
Komando pusat memerlukan sistem tracking untuk memantau posisi kendaraan operasional. Jumlah kendaraan bervariasi tergantung operasi yang sedang berjalan.

**Tugas:**
a. **(3 poin)** Rancang ADT `TrackerKendaraan` lengkap dengan data, operasi, dan aturan/batasan!

b. **(2 poin)** Jelaskan mengapa array statis tidak cocok untuk sistem ini!

c. **(3 poin)** Implementasikan method `Kendaraan* cariKendaraan(int id)` yang mencari kendaraan berdasarkan ID!

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | C | ADT mendefinisikan operasi tanpa cara implementasi |
| 2 | C | **pp adalah nilai x = 10 |
| 3 | C | Stack otomatis, Heap manual |
| 4 | D | Binary Tree adalah non-linear |
| 5 | B | Array harus delete[] |
| 6 | C | Referensi wajib diinisialisasi |
| 7 | B | Memory leak = alokasi tanpa dealokasi |
| 8 | B | Pass by reference mengubah nilai asli |
| 9 | C | ADT = data + operasi + aturan |
| 10 | D | arr+3 menunjuk ke elemen ke-4 (40) |
| 11 | B | Dangling pointer = menunjuk memori invalid |
| 12 | B | Return alamat variabel lokal = dangling |
| 13 | C | unique_ptr = exclusive ownership |
| 14 | B | ×2 memberikan amortized O(1) |
| 15 | B | q menjadi dangling setelah delete p |
| 16 | D | insert(index) bukan operasi Stack |
| 17 | C | *px = *py meng-copy nilai y ke x |
| 18 | C | ADT memisahkan interface dari implementasi |
| 19 | B | Fungsi tukar menukar nilai via pointer |
| 20 | B | Best practice: set nullptr setelah delete |

---

### Bagian B: Soal Uraian

#### Jawaban Soal 1

**Perbedaan ADT dan Struktur Data Konkret:**

| Aspek | ADT | Struktur Data Konkret |
|-------|-----|----------------------|
| Level | Abstrak/konseptual | Implementasi nyata |
| Fokus | APA yang dilakukan | BAGAIMANA melakukannya |
| Detail | Tersembunyi | Terlihat |

**Contoh:**
- **ADT Stack**: Mendefinisikan operasi push, pop, peek, isEmpty tanpa menentukan cara penyimpanan
- **Struktur Data Konkret**: Array-based Stack (menggunakan array) atau Linked Stack (menggunakan linked list)

---

#### Jawaban Soal 2

**Output:**
```
3
5
4
```

**Penjelasan:**
- `*(p + 2)`: p menunjuk ke arr[0], p+2 menunjuk ke arr[2], nilainya **3**
- `*(arr + 4)`: arr+4 menunjuk ke arr[4], nilainya **5**
- `p[3]`: Sama dengan *(p + 3), menunjuk ke arr[3], nilainya **4**

Array dan pointer dapat digunakan secara interchangeable dalam C++.

---

#### Jawaban Soal 3

**Tiga penyebab memory leak:**

1. **Lupa memanggil delete/delete[]**
   - Penyebab: Programmer tidak mendealokasi memori setelah selesai
   - Pencegahan: Selalu pasangkan new dengan delete, gunakan smart pointer

2. **Exception sebelum dealokasi**
   - Penyebab: Error terjadi sebelum kode delete dieksekusi
   - Pencegahan: Gunakan try-catch dengan dealokasi di finally, atau gunakan RAII/smart pointer

3. **Pointer di-reassign tanpa delete**
   - Penyebab: `ptr = new int(10); ptr = new int(20);` - memori pertama hilang
   - Pencegahan: Selalu delete sebelum reassign pointer ke memori baru

---

#### Jawaban Soal 4

**Masalah:** Class `Data` tidak memiliki destructor, sehingga memori yang dialokasi dengan `new int[n]` tidak pernah didealokasi → **memory leak**.

**Perbaikan:**
```cpp
class Data {
private:
    int* values;
    int size;
    
public:
    Data(int n) {
        size = n;
        values = new int[n];
    }
    
    // Tambahkan destructor
    ~Data() {
        delete[] values;  // Dealokasi memori
    }
};
```

Setiap kali objek `Data` keluar scope atau dihapus, destructor akan dipanggil dan memori dibebaskan.

---

#### Jawaban Soal 5

| Metode | Mekanisme | Kapan Digunakan |
|--------|-----------|-----------------|
| **Pass-by-value** | Copy nilai ke parameter | Data kecil, tidak ingin mengubah asli |
| **Pass-by-reference** | Alias ke variabel asli | Perlu mengubah asli, atau data besar (efisien) |
| **Pass-by-pointer** | Copy alamat memori | Perlu mengubah asli, atau bisa null |

**Rekomendasi:**
- **Value**: Tipe primitif (int, double) yang tidak perlu diubah
- **Reference**: Objek besar, parameter output, menghindari copy
- **Pointer**: Ketika null adalah nilai valid, atau perlu array

---

#### Jawaban Soal 6

```cpp
double hitungRata(int* arr, int n) {
    if (n <= 0) return 0.0;  // Handle edge case
    
    int* ptr = arr;
    int* akhir = arr + n;
    double total = 0.0;
    
    while (ptr < akhir) {
        total += *ptr;
        ptr++;
    }
    
    return total / n;
}
```

**Penjelasan:**
- Menggunakan pointer `ptr` untuk traverse array
- `ptr++` memindahkan pointer ke elemen berikutnya
- Loop berjalan selama `ptr < akhir`
- Return rata-rata dengan pembagian floating point

---

#### Jawaban Soal 7

**Konsep LIFO (Last In First Out):**
- Elemen yang terakhir masuk akan menjadi yang pertama keluar
- Seperti tumpukan piring: piring terakhir ditaruh ada di atas, diambil pertama

**Operasi utama:**
- **push**: Menambah elemen ke puncak stack
- **pop**: Menghapus dan mengembalikan elemen dari puncak

**Contoh aplikasi:**
1. **Undo/Redo** di text editor: Aksi terakhir di-undo pertama
2. **Function call stack**: Fungsi terakhir dipanggil, return pertama
3. **Browser history**: Halaman terakhir dikunjungi, back pertama
4. **Parsing ekspresi matematika**: Evaluasi operator dengan precedence

---

#### Jawaban Soal 8

```cpp
void tambah(int nilai) {
    // Jika array penuh, perbesar kapasitas
    if (ukuran == kapasitas) {
        // Alokasi array baru dengan kapasitas 2x lipat
        int kapasitasBaru = kapasitas * 2;
        int* dataBaru = new int[kapasitasBaru];
        
        // Copy data lama ke array baru
        for (int i = 0; i < ukuran; i++) {
            dataBaru[i] = data[i];
        }
        
        // Hapus array lama
        delete[] data;
        
        // Update pointer dan kapasitas
        data = dataBaru;
        kapasitas = kapasitasBaru;
    }
    
    // Tambahkan nilai baru
    data[ukuran] = nilai;
    ukuran++;
}

~ArrayDinamis() {
    delete[] data;  // Dealokasi memori
}
```

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Komunikasi Taktis

**a) Struktur data untuk pesan:**
```cpp
struct Pesan {
    int id;
    char pengirim[51];     // +1 untuk null terminator
    char* isiPesan;        // Dynamic untuk panjang variabel
    long timestamp;        // Unix timestamp
    bool sudahDibaca;
};
```

**b) Alasan dynamic memory allocation:**
- Panjang pesan bervariasi (bisa pendek seperti "Siap!" atau panjang berisi instruksi detail)
- Menghemat memori dengan hanya mengalokasi sesuai kebutuhan
- Jika menggunakan array statis, harus menentukan ukuran maksimum yang mungkin tidak terpakai

**c) Fungsi tambahPesan:**
```cpp
bool tambahPesan(Pesan** daftarPesan, int& jumlah, int& kapasitas,
                 const char* pengirim, const char* isi) {
    // Cek apakah perlu resize
    if (jumlah >= kapasitas) {
        int kapasitasBaru = kapasitas * 2;
        Pesan* temp = new Pesan[kapasitasBaru];
        
        // Copy pesan lama
        for (int i = 0; i < jumlah; i++) {
            temp[i] = (*daftarPesan)[i];
        }
        
        delete[] *daftarPesan;
        *daftarPesan = temp;
        kapasitas = kapasitasBaru;
    }
    
    // Tambah pesan baru
    Pesan& p = (*daftarPesan)[jumlah];
    p.id = jumlah + 1;
    strncpy(p.pengirim, pengirim, 50);
    
    // Alokasi memori untuk isi pesan
    p.isiPesan = new char[strlen(isi) + 1];
    strcpy(p.isiPesan, isi);
    
    p.timestamp = time(nullptr);
    p.sudahDibaca = false;
    
    jumlah++;
    return true;
}
```

---

#### Studi Kasus 2: Sistem Tracking Kendaraan

**a) Desain ADT:**

```
ADT TrackerKendaraan:
  Data:
    - Koleksi kendaraan dengan atribut: id, tipe, posisi, kecepatan, status
    - Jumlah kendaraan saat ini
    - Kapasitas maksimum
    
  Operasi:
    - tambahKendaraan(kendaraan): Menambah kendaraan baru ke tracking
    - hapusKendaraan(id): Menghapus kendaraan dari tracking
    - updatePosisi(id, lat, long): Update posisi kendaraan
    - cariKendaraan(id): Mencari kendaraan berdasarkan ID
    - dapatkanSemuaAktif(): Mendapatkan daftar kendaraan aktif
    - hitungJumlah(): Mengembalikan jumlah kendaraan
    
  Aturan/Batasan:
    - ID kendaraan harus unik
    - Posisi harus dalam range valid (-90 to 90, -180 to 180)
    - Kecepatan tidak boleh negatif
    - Tidak boleh menambah kendaraan dengan ID yang sudah ada
```

**b) Alasan array statis tidak cocok:**

1. **Jumlah kendaraan tidak tetap**: Kendaraan bisa masuk/keluar area operasi kapan saja. Array statis memaksa kita menentukan ukuran maksimum di awal, yang bisa terlalu besar (boros memori) atau terlalu kecil (tidak cukup).

2. **Operasi hapus tidak efisien**: Pada array statis, menghapus elemen di tengah memerlukan penggeseran semua elemen setelahnya. Dengan array dinamis, kita bisa mengimplementasikan strategi yang lebih fleksibel.

3. **Tidak dapat menyesuaikan kebutuhan memori**: Saat situasi tenang, mungkin hanya ada sedikit kendaraan. Saat operasi besar, bisa ada ratusan. Array dinamis dapat menyesuaikan.

**c) Method cariKendaraan:**
```cpp
Kendaraan* cariKendaraan(int id) {
    for (int i = 0; i < jumlah; i++) {
        if (daftar[i].id == id) {
            return &daftar[i];  // Kembalikan pointer ke kendaraan
        }
    }
    return nullptr;  // Tidak ditemukan
}
```

**Penjelasan:**
- Linear search melalui array
- Mengembalikan pointer agar pemanggil bisa mengakses/memodifikasi data
- nullptr jika tidak ditemukan, memungkinkan pengecekan oleh pemanggil

---

## Kriteria Penilaian

| Bagian | Jumlah Soal | Poin per Soal | Total |
|--------|-------------|---------------|-------|
| Pilihan Ganda | 20 | 2 | 40 |
| Uraian | 8 | Bervariasi | 45 |
| Studi Kasus | 2 | Bervariasi | 15 |
| **Total** | | | **100** |

---

## Catatan untuk Pengajar

- Soal-soal mencakup semua Sub-CPMK untuk Pertemuan 1 (Sub-CPMK-1.1 dan Sub-CPMK-1.3)
- Studi kasus dirancang dengan konteks pertahanan Indonesia
- Tingkat kesulitan bervariasi untuk mengakomodasi berbagai level kemampuan mahasiswa
- Soal uraian dan studi kasus memerlukan pemahaman konseptual, bukan sekadar hafalan

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
