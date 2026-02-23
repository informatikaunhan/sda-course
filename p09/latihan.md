# Latihan Mandiri 09: Algoritma Sorting Dasar

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 09  
**Topik:** Algoritma Sorting Dasar (Bubble Sort, Selection Sort, Insertion Sort)  
**Waktu:** 150 menit  
**Sifat:** Open Book

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal dengan teliti dan sistematis
2. Soal pilihan ganda bernilai 2 poin per soal (total 40 poin)
3. Soal uraian bernilai sesuai bobot yang tertera (total 45 poin)
4. Studi kasus bernilai 15 poin (total 15 poin)
5. Total nilai maksimum: 100 poin
6. Tunjukkan langkah-langkah penyelesaian untuk soal uraian
7. Gunakan notasi Big-O untuk analisis kompleksitas

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

Pilih jawaban yang paling tepat untuk setiap soal berikut.

### Soal 1
Manakah pernyataan yang **BENAR** tentang Bubble Sort?

A. Kompleksitas best case adalah O(n²)  
B. Elemen terkecil "menggelembung" ke posisi awal  
C. Elemen terbesar "menggelembung" ke posisi akhir di setiap pass  
D. Merupakan algoritma unstable sort  
E. Memerlukan memori tambahan O(n)  

### Soal 2
Berapa banyak **swap** yang dilakukan Bubble Sort untuk mengurutkan array `[4, 3, 2, 1]`?

A. 4 swap  
B. 5 swap  
C. 6 swap  
D. 7 swap  
E. 8 swap  

### Soal 3
Apa keunggulan utama Selection Sort dibandingkan algoritma sorting dasar lainnya?

A. Kompleksitas waktu terbaik O(n)  
B. Merupakan algoritma stable sort  
C. Melakukan jumlah swap minimum (maksimum n-1)  
D. Adaptive terhadap data yang hampir terurut  
E. Dapat digunakan untuk online sorting  

### Soal 4
Perhatikan kode berikut:
```cpp
for (int i = 0; i < n - 1; i++) {
    for (int j = 0; j < n - 1 - i; j++) {
        if (arr[j] > arr[j + 1]) {
            swap(arr[j], arr[j + 1]);
        }
    }
}
```
Algoritma apakah ini?

A. Selection Sort  
B. Insertion Sort  
C. Bubble Sort  
D. Merge Sort  
E. Quick Sort  

### Soal 5
Manakah algoritma sorting yang **BUKAN** merupakan stable sort?

A. Bubble Sort  
B. Insertion Sort  
C. Selection Sort  
D. Merge Sort  
E. Counting Sort  

### Soal 6
Untuk array yang **sudah terurut**, algoritma mana yang memiliki kompleksitas terbaik?

A. Bubble Sort (tanpa optimasi) — O(n²)  
B. Selection Sort — O(n²)  
C. Insertion Sort — O(n)  
D. Semua sama — O(n²)  
E. Bubble Sort dan Insertion Sort sama — O(n)  

### Soal 7
Perhatikan proses Selection Sort pada array `[64, 25, 12, 22, 11]`. Setelah **satu iterasi** (pass pertama), array menjadi:

A. `[11, 25, 12, 22, 64]`  
B. `[11, 64, 25, 12, 22]`  
C. `[25, 12, 22, 11, 64]`  
D. `[11, 25, 64, 22, 12]`  
E. `[64, 11, 12, 22, 25]`  

### Soal 8
Apa yang dimaksud dengan **adaptive sorting algorithm**?

A. Algoritma yang dapat bekerja dengan berbagai tipe data  
B. Algoritma yang performanya meningkat jika data sudah hampir terurut  
C. Algoritma yang dapat diparalelkan  
D. Algoritma yang menggunakan memori adaptif  
E. Algoritma yang dapat mengubah strategi sorting secara otomatis  

### Soal 9
Perhatikan kode Insertion Sort berikut:
```cpp
for (int i = 1; i < n; i++) {
    int key = arr[i];
    int j = i - 1;
    while (j >= 0 && arr[j] > key) {
        arr[j + 1] = arr[j];
        j--;
    }
    arr[j + 1] = key;
}
```
Berapa kompleksitas waktu **worst case** algoritma ini?

A. O(1)  
B. O(n)  
C. O(n log n)  
D. O(n²)  
E. O(2ⁿ)  

### Soal 10
Jika array `[5, 2, 8, 1, 9]` diurutkan dengan Insertion Sort, berapa kali operasi **perbandingan** dilakukan hingga array terurut?

A. 5 kali  
B. 7 kali  
C. 8 kali  
D. 10 kali  
E. 12 kali  

### Soal 11
Manakah skenario yang paling cocok untuk menggunakan Selection Sort?

A. Data berukuran sangat besar (n > 1.000.000)  
B. Data sudah hampir terurut  
C. Operasi swap sangat mahal (misalnya sorting file besar)  
D. Data terus-menerus ditambahkan (online sorting)  
E. Memerlukan stable sort  

### Soal 12
Apa tujuan dari optimasi **early termination** pada Bubble Sort?

A. Mengurangi penggunaan memori  
B. Membuat algoritma menjadi stable  
C. Menghentikan algoritma lebih awal jika array sudah terurut  
D. Mengurangi jumlah swap  
E. Membuat algoritma menjadi non-comparison based  

### Soal 13
Perhatikan array: `[(A, 3), (B, 1), (C, 3), (D, 2)]`. Jika diurutkan berdasarkan nilai angka dengan **stable sort**, hasilnya adalah:

A. `[(B, 1), (D, 2), (A, 3), (C, 3)]`  
B. `[(B, 1), (D, 2), (C, 3), (A, 3)]`  
C. `[(D, 2), (B, 1), (A, 3), (C, 3)]`  
D. `[(B, 1), (D, 2), (A, 3), (C, 3)]` atau `[(B, 1), (D, 2), (C, 3), (A, 3)]`  
E. Tidak dapat diprediksi  

### Soal 14
Berapa **space complexity** dari ketiga algoritma sorting dasar (Bubble, Selection, Insertion)?

A. O(1), O(1), O(1)  
B. O(n), O(1), O(1)  
C. O(1), O(n), O(1)  
D. O(n), O(n), O(n)  
E. O(log n), O(1), O(1)  

### Soal 15
Pada Bubble Sort, mengapa inner loop menggunakan `j < n - 1 - i` bukan `j < n - 1`?

A. Untuk membuat algoritma menjadi stable  
B. Karena elemen terakhir sudah pasti terbesar setelah setiap pass  
C. Untuk mengurangi penggunaan memori  
D. Supaya tidak terjadi index out of bounds  
E. Tidak ada perbedaan, keduanya sama  

### Soal 16
Algoritma sorting mana yang paling cocok untuk **online sorting** (data datang satu per satu)?

A. Bubble Sort  
B. Selection Sort  
C. Insertion Sort  
D. Merge Sort  
E. Quick Sort  

### Soal 17
Perhatikan Bubble Sort dengan optimasi berikut:
```cpp
for (int i = 0; i < n - 1; i++) {
    bool swapped = false;
    for (int j = 0; j < n - 1 - i; j++) {
        if (arr[j] > arr[j + 1]) {
            swap(arr[j], arr[j + 1]);
            swapped = true;
        }
    }
    if (!swapped) break;
}
```
Untuk array `[1, 2, 3, 4, 5]` yang sudah terurut, berapa kali outer loop dieksekusi?

A. 0 kali  
B. 1 kali  
C. 4 kali  
D. 5 kali  
E. n-1 kali  

### Soal 18
Manakah pernyataan yang **SALAH** tentang Insertion Sort?

A. Kompleksitas best case adalah O(n)  
B. Merupakan algoritma stable sort  
C. Efisien untuk array berukuran kecil  
D. Selalu melakukan n-1 swap  
E. Inner loop bergerak dari kanan ke kiri  

### Soal 19
Jika sebuah sistem perlu mengurutkan data yang sering berubah (data baru ditambahkan secara berkala), algoritma mana yang paling efisien?

A. Bubble Sort — karena simple  
B. Selection Sort — karena jumlah swap minimum  
C. Insertion Sort — karena adaptive dan online  
D. Semua sama efisiennya  
E. Tidak ada yang efisien, perlu algoritma lain  

### Soal 20
Berapa jumlah **perbandingan** yang dilakukan Selection Sort untuk array berukuran n?

A. n  
B. n - 1  
C. n(n-1)/2  
D. n²  
E. n log n  

---

## Bagian B: Soal Uraian (15 Soal)

### Soal U1 (2 poin) — Mudah
Jelaskan perbedaan mendasar antara cara kerja Bubble Sort dan Selection Sort!

### Soal U2 (2 poin) — Mudah
Apa yang dimaksud dengan **stable sort**? Berikan contoh kasus di mana stabilitas sorting menjadi penting!

### Soal U3 (3 poin) — Mudah
Tuliskan langkah-langkah Bubble Sort untuk mengurutkan array `[5, 1, 4, 2, 8]`! Tunjukkan kondisi array setelah setiap pass!

### Soal U4 (3 poin) — Mudah
Mengapa Insertion Sort memiliki kompleksitas best case O(n) sedangkan Selection Sort selalu O(n²)? Jelaskan dengan menganalisis inner loop kedua algoritma!

### Soal U5 (3 poin) — Sedang
Implementasikan fungsi Bubble Sort dengan optimasi early termination dalam C++!

### Soal U6 (3 poin) — Sedang
Perhatikan array `[3, 1, 4, 1, 5, 9, 2, 6]`. Tuliskan langkah-langkah Selection Sort hingga array terurut! Tunjukkan posisi minimum dan swap di setiap iterasi!

### Soal U7 (3 poin) — Sedang
Implementasikan Selection Sort yang mengurutkan array secara **descending** (dari besar ke kecil)!

### Soal U8 (3 poin) — Sedang
Tuliskan langkah-langkah Insertion Sort untuk mengurutkan array `[12, 11, 13, 5, 6]`! Tunjukkan bagian terurut dan key di setiap iterasi!

### Soal U9 (3 poin) — Sedang
Modifikasi Insertion Sort untuk mendeteksi dan menghitung jumlah **inversi** dalam array! Inversi adalah pasangan (i, j) dimana i < j tetapi arr[i] > arr[j].

### Soal U10 (4 poin) — Sedang
Bandingkan performa teoritis Bubble Sort, Selection Sort, dan Insertion Sort untuk tiga kasus:
- Array sudah terurut ascending
- Array terurut descending (reverse)
- Array dengan elemen acak

Gunakan tabel untuk menyajikan perbandingan!

### Soal U11 (3 poin) — Sulit
Implementasikan fungsi sorting generik menggunakan function pointer yang dapat menerima fungsi comparator custom!

### Soal U12 (4 poin) — Sulit
Mengapa Selection Sort disebut sebagai algoritma **unstable**? Berikan contoh konkret dengan array yang membuktikan ketidakstabilan Selection Sort!

### Soal U13 (3 poin) — Sulit
Implementasikan **Binary Insertion Sort** yang menggunakan binary search untuk menemukan posisi penyisipan! Apa kompleksitas waktu algoritma ini?

### Soal U14 (3 poin) — Sulit
Buatlah fungsi yang membandingkan performa ketiga algoritma sorting dengan menghitung jumlah perbandingan dan swap. Fungsi menerima array dan mengembalikan statistik untuk ketiga algoritma!

### Soal U15 (4 poin) — Sulit
Jelaskan mengapa **Insertion Sort** sering digunakan sebagai bagian dari algoritma sorting yang lebih kompleks seperti Timsort dan Introsort! Apa keunggulan spesifik yang dimanfaatkan?

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Prioritas Pesan Militer (7 poin)

**Latar Belakang:**
Pusat komando militer menerima pesan dari berbagai unit di lapangan. Setiap pesan memiliki atribut:
- **ID Pesan**: Nomor unik
- **Tingkat Prioritas**: 1 (tertinggi) sampai 5 (terendah)
- **Timestamp**: Waktu pengiriman (dalam detik sejak awal operasi)
- **Unit Pengirim**: Kode unit (string 4 karakter)

Pesan harus diproses berdasarkan prioritas tertinggi terlebih dahulu. Jika prioritas sama, pesan yang lebih dulu dikirim harus diproses lebih dulu (FIFO).

**Data Sample:**
```
ID | Prioritas | Timestamp | Unit
---|-----------|-----------|------
P1 |     2     |    100    | ALFA
P2 |     1     |    150    | BRVO
P3 |     2     |    080    | CHRL
P4 |     3     |    120    | DLTA
P5 |     1     |    090    | ECHO
P6 |     2     |    110    | FXTR
```

**Pertanyaan:**

a. **(2 poin)** Definisikan struct `PesanMiliter` yang merepresentasikan pesan dan implementasikan fungsi comparator untuk sorting!

b. **(2 poin)** Algoritma sorting mana yang paling tepat untuk kasus ini? Jelaskan alasannya dengan mempertimbangkan: stabilitas, efisiensi, dan karakteristik data!

c. **(3 poin)** Implementasikan fungsi `void sortPesanByPriority(PesanMiliter arr[], int n)` menggunakan algoritma yang Anda pilih! Tunjukkan urutan pesan setelah sorting!

---

### Studi Kasus 2: Sistem Tracking Target Radar (8 poin)

**Latar Belakang:**
Sistem radar pertahanan udara mendeteksi objek terbang dan perlu menampilkan daftar target berdasarkan tingkat ancaman. Setiap target memiliki atribut:
- **ID Target**: Nomor identifikasi
- **Jarak**: Jarak dari stasiun radar (dalam km)
- **Kecepatan**: Kecepatan target (dalam km/jam)
- **Altitude**: Ketinggian target (dalam meter)
- **Jenis**: UNKNOWN, FRIENDLY, HOSTILE

Level ancaman dihitung dengan formula:
```
threat_level = (HOSTILE ? 100 : (UNKNOWN ? 50 : 0)) + (500 - jarak)/10 + kecepatan/100
```

Target dengan threat level lebih tinggi harus ditampilkan lebih dulu. Sistem menerima update posisi setiap 2 detik, dan data biasanya sudah hampir terurut karena perubahan posisi kecil.

**Data Sample (sebelum update):**
```
ID | Jarak | Kecepatan | Altitude | Jenis   | Threat Level
---|-------|-----------|----------|---------|-------------
T1 |  150  |    800    |   5000   | HOSTILE |    143
T2 |  300  |    400    |   8000   | UNKNOWN |     74
T3 |  100  |    600    |   3000   | HOSTILE |    146
T4 |  400  |    200    |  10000   | FRIENDLY|     12
T5 |  200  |    500    |   6000   | UNKNOWN |     85
```

**Pertanyaan:**

a. **(2 poin)** Definisikan struct `TargetRadar` dan implementasikan fungsi untuk menghitung threat level!

b. **(2 poin)** Mengapa Insertion Sort adalah pilihan yang baik untuk sistem ini? Jelaskan dengan mempertimbangkan karakteristik data yang "hampir terurut"!

c. **(2 poin)** Implementasikan fungsi `void sortTargetByThreat(TargetRadar arr[], int n)` menggunakan Insertion Sort!

d. **(2 poin)** Jika sistem perlu menampilkan **top 3** target dengan ancaman tertinggi saja (tanpa mengurutkan seluruh array), algoritma apa yang lebih efisien? Jelaskan dan implementasikan!

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|:-------:|-------------------|
| 1 | C | Elemen terbesar "bubbles up" ke akhir di setiap pass |
| 2 | C | Pass 1: 3 swap, Pass 2: 2 swap, Pass 3: 1 swap = 6 total |
| 3 | C | Selection Sort melakukan maksimum n-1 swap |
| 4 | C | Pattern khas Bubble Sort: bandingkan & swap adjacent |
| 5 | C | Selection Sort adalah unstable (swap melewati elemen sama) |
| 6 | C | Insertion Sort O(n) karena inner loop tidak berjalan |
| 7 | A | Minimum adalah 11, ditukar dengan 64 di posisi 0 |
| 8 | B | Adaptive = performa lebih baik untuk data hampir terurut |
| 9 | D | Worst case: array reverse, setiap key digeser ke awal |
| 10 | C | i=1:1, i=2:2, i=3:3, i=4:2 perbandingan = 8 total |
| 11 | C | Selection Sort optimal saat swap mahal (min swap) |
| 12 | C | Jika tidak ada swap dalam satu pass, array sudah terurut |
| 13 | A | Stable sort menjaga urutan relatif A sebelum C |
| 14 | A | Ketiganya in-place dengan O(1) extra space |
| 15 | B | Elemen di posisi n-i sampai n-1 sudah terurut |
| 16 | C | Insertion Sort dapat menyisipkan elemen baru dengan efisien |
| 17 | B | 1 kali, tidak ada swap, langsung break |
| 18 | D | Insertion Sort menggunakan shift, bukan swap |
| 19 | C | Insertion Sort adaptive dan mendukung online sorting |
| 20 | C | n-1 + n-2 + ... + 1 = n(n-1)/2 perbandingan |

---

### Bagian B: Soal Uraian

#### Jawaban U1

**Perbedaan Bubble Sort dan Selection Sort:**

| Aspek | Bubble Sort | Selection Sort |
|-------|-------------|----------------|
| **Cara Kerja** | Membandingkan dan menukar elemen **berdekatan** berulang kali | Mencari elemen **minimum** dari bagian belum terurut, taruh di depan |
| **Jumlah Swap** | Bisa sangat banyak (worst case: n(n-1)/2) | Maksimum n-1 swap |
| **Elemen Terurut** | Elemen **terbesar** terurut duluan (dari belakang) | Elemen **terkecil** terurut duluan (dari depan) |
| **Stabilitas** | Stable | Unstable |

---

#### Jawaban U2

**Stable Sort** adalah algoritma sorting yang mempertahankan urutan relatif elemen-elemen yang memiliki kunci (key) sama.

**Contoh kasus penting:**
Sorting data mahasiswa berdasarkan nilai, di mana beberapa mahasiswa memiliki nilai sama. Jika data awalnya sudah terurut berdasarkan nama, stable sort akan menjaga urutan nama untuk mahasiswa dengan nilai sama.

```
Input (urut nama): [(Andi, 85), (Budi, 90), (Citra, 85), (Doni, 90)]
Stable sort by nilai: [(Andi, 85), (Citra, 85), (Budi, 90), (Doni, 90)]
Unstable sort mungkin: [(Citra, 85), (Andi, 85), (Doni, 90), (Budi, 90)]
```

---

#### Jawaban U3

**Langkah Bubble Sort untuk `[5, 1, 4, 2, 8]`:**

```
Array awal: [5, 1, 4, 2, 8]

Pass 1:
  [5, 1, 4, 2, 8] → 5 > 1? Ya, swap → [1, 5, 4, 2, 8]
  [1, 5, 4, 2, 8] → 5 > 4? Ya, swap → [1, 4, 5, 2, 8]
  [1, 4, 5, 2, 8] → 5 > 2? Ya, swap → [1, 4, 2, 5, 8]
  [1, 4, 2, 5, 8] → 5 > 8? Tidak
  Hasil Pass 1: [1, 4, 2, 5, 8]

Pass 2:
  [1, 4, 2, 5, 8] → 1 > 4? Tidak
  [1, 4, 2, 5, 8] → 4 > 2? Ya, swap → [1, 2, 4, 5, 8]
  [1, 2, 4, 5, 8] → 4 > 5? Tidak
  Hasil Pass 2: [1, 2, 4, 5, 8]

Pass 3:
  Tidak ada swap → Array sudah terurut!

Hasil akhir: [1, 2, 4, 5, 8]
```

---

#### Jawaban U4

**Perbedaan kompleksitas best case:**

**Insertion Sort — O(n):**
```cpp
for (int i = 1; i < n; i++) {
    int key = arr[i];
    int j = i - 1;
    while (j >= 0 && arr[j] > key) {  // Inner loop
        arr[j + 1] = arr[j];
        j--;
    }
    arr[j + 1] = key;
}
```
Untuk array terurut: `arr[j] > key` selalu **false** (karena arr[j] ≤ key), jadi inner loop **tidak pernah berjalan**. Total operasi: O(n).

**Selection Sort — O(n²):**
```cpp
for (int i = 0; i < n - 1; i++) {
    int minIdx = i;
    for (int j = i + 1; j < n; j++) {  // Inner loop SELALU berjalan
        if (arr[j] < arr[minIdx]) {
            minIdx = j;
        }
    }
    swap(arr[i], arr[minIdx]);
}
```
Inner loop **selalu** berjalan penuh untuk mencari minimum, tidak peduli apakah array sudah terurut atau belum. Total: (n-1) + (n-2) + ... + 1 = O(n²).

---

#### Jawaban U5

```cpp
void bubbleSortOptimized(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        bool swapped = false;  // Flag untuk deteksi swap
        
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }
        
        // Jika tidak ada swap, array sudah terurut
        if (!swapped) {
            break;
        }
    }
}
```

---

#### Jawaban U6

**Langkah Selection Sort untuk `[3, 1, 4, 1, 5, 9, 2, 6]`:**

```
Array awal: [3, 1, 4, 1, 5, 9, 2, 6]

Iterasi 1: Cari minimum di [3,1,4,1,5,9,2,6], min=1 di index 1
  Swap arr[0] dengan arr[1]: [1, 3, 4, 1, 5, 9, 2, 6]

Iterasi 2: Cari minimum di [3,4,1,5,9,2,6], min=1 di index 3
  Swap arr[1] dengan arr[3]: [1, 1, 4, 3, 5, 9, 2, 6]

Iterasi 3: Cari minimum di [4,3,5,9,2,6], min=2 di index 6
  Swap arr[2] dengan arr[6]: [1, 1, 2, 3, 5, 9, 4, 6]

Iterasi 4: Cari minimum di [3,5,9,4,6], min=3 di index 3
  Tidak perlu swap (sudah di posisi): [1, 1, 2, 3, 5, 9, 4, 6]

Iterasi 5: Cari minimum di [5,9,4,6], min=4 di index 6
  Swap arr[4] dengan arr[6]: [1, 1, 2, 3, 4, 9, 5, 6]

Iterasi 6: Cari minimum di [9,5,6], min=5 di index 6
  Swap arr[5] dengan arr[6]: [1, 1, 2, 3, 4, 5, 9, 6]

Iterasi 7: Cari minimum di [9,6], min=6 di index 7
  Swap arr[6] dengan arr[7]: [1, 1, 2, 3, 4, 5, 6, 9]

Hasil akhir: [1, 1, 2, 3, 4, 5, 6, 9]
```

---

#### Jawaban U7

```cpp
void selectionSortDescending(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int maxIdx = i;  // Cari MAXIMUM bukan minimum
        
        for (int j = i + 1; j < n; j++) {
            if (arr[j] > arr[maxIdx]) {  // Ubah < menjadi >
                maxIdx = j;
            }
        }
        
        if (maxIdx != i) {
            int temp = arr[i];
            arr[i] = arr[maxIdx];
            arr[maxIdx] = temp;
        }
    }
}
```

---

#### Jawaban U8

**Langkah Insertion Sort untuk `[12, 11, 13, 5, 6]`:**

```
Array awal: [12, 11, 13, 5, 6]
Bagian terurut: [12] (elemen pertama)

Iterasi 1: key = 11
  Bandingkan 11 dengan 12: 12 > 11, geser 12
  [_, 12, 13, 5, 6], sisipkan 11 di posisi 0
  Hasil: [11, 12, 13, 5, 6]
  Bagian terurut: [11, 12]

Iterasi 2: key = 13
  Bandingkan 13 dengan 12: 12 < 13, stop
  13 sudah di posisi yang benar
  Hasil: [11, 12, 13, 5, 6]
  Bagian terurut: [11, 12, 13]

Iterasi 3: key = 5
  Bandingkan 5 dengan 13: 13 > 5, geser 13
  Bandingkan 5 dengan 12: 12 > 5, geser 12
  Bandingkan 5 dengan 11: 11 > 5, geser 11
  [_, 11, 12, 13, 6], sisipkan 5 di posisi 0
  Hasil: [5, 11, 12, 13, 6]
  Bagian terurut: [5, 11, 12, 13]

Iterasi 4: key = 6
  Bandingkan 6 dengan 13: 13 > 6, geser 13
  Bandingkan 6 dengan 12: 12 > 6, geser 12
  Bandingkan 6 dengan 11: 11 > 6, geser 11
  Bandingkan 6 dengan 5: 5 < 6, stop
  [5, _, 11, 12, 13], sisipkan 6 di posisi 1
  Hasil: [5, 6, 11, 12, 13]

Hasil akhir: [5, 6, 11, 12, 13]
```

---

#### Jawaban U9

```cpp
int countInversions(int arr[], int n) {
    int inversions = 0;
    
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            inversions++;  // Setiap geser = satu inversi
            j--;
        }
        arr[j + 1] = key;
    }
    
    return inversions;
}
```

**Penjelasan:** Setiap kali elemen digeser ke kanan, itu berarti ada satu pasangan inversi. Jumlah total penggeseran sama dengan jumlah inversi dalam array.

---

#### Jawaban U10

| Kondisi Array | Bubble Sort | Selection Sort | Insertion Sort |
|--------------|-------------|----------------|----------------|
| **Sudah terurut** | O(n)* | O(n²) | **O(n)** |
| **Terurut terbalik** | O(n²) | O(n²) | O(n²) |
| **Acak** | O(n²) | O(n²) | O(n²) |

*dengan optimasi early termination

**Analisis:**
- **Sudah terurut:** Insertion Sort terbaik karena inner loop tidak berjalan. Bubble Sort dengan optimasi juga O(n). Selection Sort tetap O(n²) karena harus mencari minimum.
- **Terurut terbalik:** Worst case untuk semua algoritma.
- **Acak:** Average case, semua O(n²).

---

#### Jawaban U11

```cpp
#include <iostream>
using namespace std;

// Tipe function pointer untuk comparator
typedef bool (*Comparator)(int, int);

// Comparator untuk ascending
bool ascending(int a, int b) {
    return a > b;  // True jika perlu swap
}

// Comparator untuk descending
bool descending(int a, int b) {
    return a < b;  // True jika perlu swap
}

// Generic Insertion Sort dengan function pointer
void insertionSortGeneric(int arr[], int n, Comparator compare) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && compare(arr[j], key)) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

int main() {
    int arr1[] = {64, 34, 25, 12, 22};
    int arr2[] = {64, 34, 25, 12, 22};
    int n = 5;
    
    insertionSortGeneric(arr1, n, ascending);
    cout << "Ascending: ";
    for (int i = 0; i < n; i++) cout << arr1[i] << " ";
    cout << endl;
    
    insertionSortGeneric(arr2, n, descending);
    cout << "Descending: ";
    for (int i = 0; i < n; i++) cout << arr2[i] << " ";
    cout << endl;
    
    return 0;
}
```

---

#### Jawaban U12

**Selection Sort Unstable:**

Selection Sort tidak stable karena operasi swap dapat memindahkan elemen melewati elemen lain dengan nilai yang sama.

**Contoh:**
```
Input: [(A, 5), (B, 3), (C, 5), (D, 2)]
       Index 0    1      2      3

Iterasi 1: Minimum adalah (D, 2) di index 3
  Swap index 0 dan 3:
  [(D, 2), (B, 3), (C, 5), (A, 5)]
  
  Perhatikan: (A, 5) awalnya di index 0, sekarang di index 3
              (C, 5) tetap di index 2
              Urutan relatif (A, C) berubah menjadi (C, A)!

Hasil akhir: [(D, 2), (B, 3), (C, 5), (A, 5)]
  - Untuk nilai 5, urutan awal adalah A lalu C
  - Setelah sort, urutan menjadi C lalu A → TIDAK STABLE!
```

---

#### Jawaban U13

```cpp
// Binary search untuk menemukan posisi penyisipan
int binarySearch(int arr[], int item, int low, int high) {
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == item)
            return mid + 1;
        else if (arr[mid] < item)
            low = mid + 1;
        else
            high = mid - 1;
    }
    return low;
}

void binaryInsertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        // Gunakan binary search untuk menemukan posisi
        int pos = binarySearch(arr, key, 0, j);
        
        // Geser elemen
        while (j >= pos) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

**Kompleksitas:**
- **Perbandingan:** O(n log n) — Binary search O(log n) untuk setiap dari n elemen
- **Penggeseran:** O(n²) — Masih perlu menggeser elemen
- **Total:** O(n²) — Didominasi oleh operasi geser

Binary Insertion Sort mengurangi jumlah perbandingan tetapi tidak mengubah kompleksitas overall karena penggeseran tetap O(n²).

---

#### Jawaban U14

```cpp
#include <iostream>
using namespace std;

struct SortStats {
    int comparisons;
    int swaps;
};

SortStats bubbleSortWithStats(int arr[], int n) {
    SortStats stats = {0, 0};
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - 1 - i; j++) {
            stats.comparisons++;
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                stats.swaps++;
            }
        }
    }
    return stats;
}

SortStats selectionSortWithStats(int arr[], int n) {
    SortStats stats = {0, 0};
    for (int i = 0; i < n - 1; i++) {
        int minIdx = i;
        for (int j = i + 1; j < n; j++) {
            stats.comparisons++;
            if (arr[j] < arr[minIdx]) {
                minIdx = j;
            }
        }
        if (minIdx != i) {
            swap(arr[i], arr[minIdx]);
            stats.swaps++;
        }
    }
    return stats;
}

SortStats insertionSortWithStats(int arr[], int n) {
    SortStats stats = {0, 0};
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0) {
            stats.comparisons++;
            if (arr[j] > key) {
                arr[j + 1] = arr[j];
                stats.swaps++;  // Hitung shift sebagai swap
                j--;
            } else {
                break;
            }
        }
        arr[j + 1] = key;
    }
    return stats;
}

void compareAlgorithms(int original[], int n) {
    int arr1[100], arr2[100], arr3[100];
    for (int i = 0; i < n; i++) {
        arr1[i] = arr2[i] = arr3[i] = original[i];
    }
    
    SortStats bubble = bubbleSortWithStats(arr1, n);
    SortStats selection = selectionSortWithStats(arr2, n);
    SortStats insertion = insertionSortWithStats(arr3, n);
    
    cout << "Algorithm     | Comparisons | Swaps" << endl;
    cout << "--------------|-------------|------" << endl;
    cout << "Bubble Sort   | " << bubble.comparisons << "          | " << bubble.swaps << endl;
    cout << "Selection Sort| " << selection.comparisons << "          | " << selection.swaps << endl;
    cout << "Insertion Sort| " << insertion.comparisons << "          | " << insertion.swaps << endl;
}
```

---

#### Jawaban U15

**Insertion Sort dalam Algoritma Kompleks:**

**1. Timsort (Python, Java):**
Timsort membagi array menjadi "run" (subsequence terurut) dan menggabungkannya dengan merge. Untuk run yang kecil, Timsort menggunakan **Insertion Sort** karena:
- Overhead rendah untuk data kecil
- Adaptive: run yang hampir terurut diproses sangat cepat
- Cache-friendly: akses memori berurutan

**2. Introsort (C++ STL):**
Introsort memulai dengan Quick Sort, beralih ke Heap Sort jika rekursi terlalu dalam, dan menggunakan **Insertion Sort** untuk partisi kecil (biasanya n < 16) karena:
- Quick Sort memiliki overhead untuk partisi kecil
- Insertion Sort lebih efisien untuk data kecil

**Keunggulan spesifik yang dimanfaatkan:**
1. **Overhead rendah:** Tidak ada overhead rekursi atau struktur data tambahan
2. **Cache efficiency:** Akses memori berurutan, optimal untuk CPU cache
3. **Adaptivitas:** O(n) untuk data hampir terurut (sering terjadi setelah partisi)
4. **Stabilitas:** Timsort memerlukan stable sort, Insertion Sort memenuhi ini
5. **In-place:** Tidak memerlukan memori tambahan

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Prioritas Pesan Militer

**a) Definisi struct dan comparator:**

```cpp
#include <iostream>
#include <cstring>
using namespace std;

struct PesanMiliter {
    char id[10];
    int prioritas;      // 1 = tertinggi, 5 = terendah
    int timestamp;      // Detik sejak awal operasi
    char unit[5];
};

// Comparator: true jika a harus diproses sebelum b
bool shouldProcessFirst(const PesanMiliter& a, const PesanMiliter& b) {
    // Prioritas lebih kecil = lebih penting
    if (a.prioritas != b.prioritas) {
        return a.prioritas < b.prioritas;
    }
    // Jika prioritas sama, timestamp lebih kecil = lebih dulu (FIFO)
    return a.timestamp < b.timestamp;
}
```

**b) Algoritma yang tepat: Insertion Sort**

**Alasan:**
1. **Stabilitas:** Jika ada dua pesan dengan prioritas dan timestamp sama, urutan relatif terjaga. Insertion Sort adalah stable sort.
2. **Efisiensi untuk data kecil:** Jumlah pesan yang masuk dalam interval waktu biasanya kecil.
3. **Adaptivitas:** Pesan sering sudah hampir terurut (pesan baru memiliki timestamp lebih besar). Insertion Sort O(n) untuk kasus ini.
4. **Online processing:** Pesan bisa langsung diproses saat masuk tanpa menunggu batch.

**c) Implementasi dan hasil:**

```cpp
void sortPesanByPriority(PesanMiliter arr[], int n) {
    for (int i = 1; i < n; i++) {
        PesanMiliter key = arr[i];
        int j = i - 1;
        
        // Geser pesan yang prioritasnya lebih rendah
        while (j >= 0 && !shouldProcessFirst(arr[j], key)) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// Penggunaan dengan data sample
int main() {
    PesanMiliter pesan[6] = {
        {"P1", 2, 100, "ALFA"},
        {"P2", 1, 150, "BRVO"},
        {"P3", 2, 80,  "CHRL"},
        {"P4", 3, 120, "DLTA"},
        {"P5", 1, 90,  "ECHO"},
        {"P6", 2, 110, "FXTR"}
    };
    
    sortPesanByPriority(pesan, 6);
    
    cout << "Urutan setelah sorting:" << endl;
    for (int i = 0; i < 6; i++) {
        cout << pesan[i].id << " (P" << pesan[i].prioritas 
             << ", T" << pesan[i].timestamp << ")" << endl;
    }
    
    return 0;
}
```

**Output:**
```
Urutan setelah sorting:
P5 (P1, T90)   ← Prioritas 1, timestamp 90
P2 (P1, T150)  ← Prioritas 1, timestamp 150
P3 (P2, T80)   ← Prioritas 2, timestamp 80
P1 (P2, T100)  ← Prioritas 2, timestamp 100
P6 (P2, T110)  ← Prioritas 2, timestamp 110
P4 (P3, T120)  ← Prioritas 3
```

---

#### Studi Kasus 2: Sistem Tracking Target Radar

**a) Definisi struct dan fungsi threat level:**

```cpp
#include <iostream>
using namespace std;

enum JenisTarget { UNKNOWN, FRIENDLY, HOSTILE };

struct TargetRadar {
    int id;
    double jarak;       // km
    double kecepatan;   // km/jam
    double altitude;    // meter
    JenisTarget jenis;
    double threatLevel;
};

double hitungThreatLevel(const TargetRadar& t) {
    double baseScore = 0;
    
    switch (t.jenis) {
        case HOSTILE:  baseScore = 100; break;
        case UNKNOWN:  baseScore = 50;  break;
        case FRIENDLY: baseScore = 0;   break;
    }
    
    // Formula: baseScore + (500 - jarak)/10 + kecepatan/100
    return baseScore + (500 - t.jarak) / 10.0 + t.kecepatan / 100.0;
}

void updateThreatLevels(TargetRadar arr[], int n) {
    for (int i = 0; i < n; i++) {
        arr[i].threatLevel = hitungThreatLevel(arr[i]);
    }
}
```

**b) Mengapa Insertion Sort cocok:**

1. **Data hampir terurut:** Setelah update posisi, perubahan threat level biasanya kecil. Target tidak berpindah jauh dalam 2 detik, sehingga urutan hampir sama dengan sebelumnya.

2. **Kompleksitas:** Untuk data hampir terurut, Insertion Sort mendekati O(n), jauh lebih baik dari O(n²) untuk data acak.

3. **Real-time requirement:** Sistem radar memerlukan respons cepat. Insertion Sort dengan overhead rendah cocok untuk update berkala.

4. **Online capability:** Target baru bisa langsung disisipkan ke urutan yang benar tanpa re-sort seluruh array.

**c) Implementasi Insertion Sort:**

```cpp
void sortTargetByThreat(TargetRadar arr[], int n) {
    for (int i = 1; i < n; i++) {
        TargetRadar key = arr[i];
        int j = i - 1;
        
        // Urutkan descending (threat level tinggi di depan)
        while (j >= 0 && arr[j].threatLevel < key.threatLevel) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

**d) Algoritma untuk Top-K:**

Untuk mencari **top 3** tanpa mengurutkan seluruh array, gunakan **Partial Selection Sort** atau **Partial Heap**:

```cpp
void findTopKTargets(TargetRadar arr[], int n, int k, TargetRadar result[]) {
    // Copy ke result untuk tidak memodifikasi original
    for (int i = 0; i < n; i++) {
        result[i] = arr[i];
    }
    
    // Partial Selection Sort: hanya k iterasi
    for (int i = 0; i < k && i < n; i++) {
        int maxIdx = i;
        
        // Cari target dengan threat level tertinggi
        for (int j = i + 1; j < n; j++) {
            if (result[j].threatLevel > result[maxIdx].threatLevel) {
                maxIdx = j;
            }
        }
        
        // Swap ke posisi i
        if (maxIdx != i) {
            TargetRadar temp = result[i];
            result[i] = result[maxIdx];
            result[maxIdx] = temp;
        }
    }
    
    // result[0..k-1] sekarang berisi top-k targets
}
```

**Kompleksitas:**
- Full sort: O(n²)
- Partial sort untuk top-k: O(k × n) = O(n) untuk k konstan (k=3)

Ini lebih efisien karena kita hanya perlu menemukan 3 elemen terbesar, bukan mengurutkan seluruh array.

---

## Kriteria Penilaian

| Bagian | Jumlah Soal | Poin per Soal | Total |
|--------|-------------|---------------|-------|
| Pilihan Ganda | 20 | 2 | 40 |
| Uraian | 15 | Bervariasi | 45 |
| Studi Kasus | 2 | Bervariasi | 15 |
| **Total** | | | **100** |

---

## Catatan untuk Pengajar

- Soal-soal mencakup Sub-CPMK-4.1: Implementasi dan analisis algoritma sorting dasar
- Studi kasus dirancang dengan konteks pertahanan yang relevan
- Tingkat kesulitan bervariasi untuk mengakomodasi berbagai level kemampuan mahasiswa
- Soal uraian dan studi kasus memerlukan pemahaman konseptual dan kemampuan implementasi

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
