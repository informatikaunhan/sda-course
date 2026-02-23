# Latihan Mandiri 10: Algoritma Sorting Lanjut

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 10  
**Topik:** Algoritma Sorting Lanjut (Merge Sort dan Quick Sort)  
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

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

Pilih jawaban yang paling tepat untuk setiap soal berikut.

**1.** Apa kompleksitas waktu **worst case** dari algoritma Merge Sort?

a) O(n)  
b) O(n log n)  
c) O(n²)  
d) O(log n)  
e) O(n² log n)

**2.** Apa kompleksitas waktu **worst case** dari algoritma Quick Sort?

a) O(n)  
b) O(n log n)  
c) O(n²)  
d) O(log n)  
e) O(2ⁿ)

**3.** Manakah pernyataan yang **BENAR** tentang Merge Sort?

a) Merge Sort adalah algoritma in-place  
b) Merge Sort memiliki kompleksitas ruang O(1)  
c) Merge Sort adalah algoritma stable  
d) Merge Sort lebih cepat dari Quick Sort dalam semua kasus  
e) Merge Sort menggunakan strategi greedy

**4.** Paradigma yang digunakan oleh Merge Sort dan Quick Sort adalah:

a) Greedy  
b) Dynamic Programming  
c) Divide and Conquer  
d) Brute Force  
e) Backtracking

**5.** Pada algoritma Quick Sort, apa yang dimaksud dengan "pivot"?

a) Elemen pertama dalam array  
b) Elemen yang digunakan sebagai pembanding untuk partisi  
c) Elemen terbesar dalam array  
d) Elemen tengah hasil sorting  
e) Elemen yang selalu dihapus

**6.** Perhatikan array berikut: `[8, 3, 5, 1, 9, 2]`. Jika menggunakan Merge Sort, berapa kali proses merge dilakukan hingga array terurut?

a) 3 kali  
b) 4 kali  
c) 5 kali  
d) 6 kali  
e) 7 kali

**7.** Apa kompleksitas ruang (space complexity) dari Merge Sort standar?

a) O(1)  
b) O(log n)  
c) O(n)  
d) O(n log n)  
e) O(n²)

**8.** Manakah strategi pemilihan pivot yang dapat **meminimalkan** kemungkinan worst case pada Quick Sort?

a) Selalu pilih elemen pertama  
b) Selalu pilih elemen terakhir  
c) Median-of-three  
d) Selalu pilih elemen terbesar  
e) Selalu pilih elemen terkecil

**9.** Apa yang terjadi jika Quick Sort selalu memilih pivot yang merupakan elemen terkecil atau terbesar?

a) Algoritma berjalan optimal O(n log n)  
b) Algoritma menjadi O(n²)  
c) Algoritma menjadi O(n)  
d) Algoritma tidak dapat berjalan  
e) Tidak ada pengaruh

**10.** Dalam proses partisi Lomuto pada Quick Sort dengan array `[5, 2, 8, 1, 9]` dan pivot = 5 (elemen pertama), posisi akhir pivot setelah partisi adalah:

a) Index 0  
b) Index 1  
c) Index 2  
d) Index 3  
e) Index 4

**11.** Manakah pernyataan yang **BENAR** tentang lower bound sorting berbasis perbandingan?

a) Lower bound adalah O(n)  
b) Lower bound adalah Ω(n log n)  
c) Lower bound adalah O(n²)  
d) Tidak ada lower bound untuk sorting  
e) Lower bound tergantung pada algoritma

**12.** Mengapa Merge Sort lebih cocok untuk sorting linked list dibandingkan Quick Sort?

a) Merge Sort lebih cepat  
b) Merge memerlukan akses sekuensial yang cocok dengan linked list  
c) Quick Sort tidak bisa digunakan untuk linked list  
d) Merge Sort menggunakan lebih sedikit memori  
e) Tidak ada perbedaan

**13.** Perhatikan rekurensi berikut: T(n) = 2T(n/2) + O(n). Solusi dari rekurensi ini adalah:

a) O(n)  
b) O(n log n)  
c) O(n²)  
d) O(log n)  
e) O(2ⁿ)

**14.** Jika array sudah hampir terurut, algoritma mana yang cenderung memiliki performa TERBAIK?

a) Merge Sort  
b) Quick Sort dengan pivot elemen pertama  
c) Quick Sort dengan random pivot  
d) Selection Sort  
e) Bubble Sort dengan early termination

**15.** Apa keuntungan utama Quick Sort dibandingkan Merge Sort?

a) Selalu lebih cepat  
b) In-place (tidak memerlukan memori tambahan O(n))  
c) Lebih mudah diimplementasikan  
d) Selalu stable  
e) Worst case lebih baik

**16.** Dalam algoritma Merge Sort, operasi "conquer" merujuk pada:

a) Membagi array menjadi dua bagian  
b) Menggabungkan dua array terurut  
c) Melakukan rekursi pada subarray  
d) Memilih pivot  
e) Menukar elemen

**17.** Perhatikan array `[4, 1, 3, 2, 5]`. Setelah satu kali partisi dengan pivot = 3 (elemen tengah) menggunakan skema Hoare, manakah konfigurasi yang MUNGKIN?

a) `[1, 2, 3, 4, 5]`  
b) `[2, 1, 3, 4, 5]`  
c) `[4, 1, 3, 2, 5]`  
d) `[5, 4, 3, 2, 1]`  
e) `[1, 2, 3, 5, 4]`

**18.** Algoritma hybrid yang menggabungkan Quick Sort, Heap Sort, dan Insertion Sort adalah:

a) Timsort  
b) Introsort  
c) Smoothsort  
d) Shellsort  
e) Radix Sort

**19.** Berapa jumlah perbandingan minimum yang diperlukan untuk mengurutkan n elemen menggunakan comparison-based sorting?

a) n  
b) n log n  
c) ⌈log₂(n!)⌉  
d) n²  
e) 2ⁿ

**20.** Manakah yang BUKAN merupakan langkah dalam paradigma Divide and Conquer?

a) Divide: membagi masalah menjadi submasalah  
b) Conquer: menyelesaikan submasalah secara rekursif  
c) Combine: menggabungkan solusi submasalah  
d) Optimize: mengoptimalkan solusi dengan dynamic programming  
e) Base case: menyelesaikan masalah trivial secara langsung

---

## Bagian B: Soal Uraian (15 Soal)

### Soal Uraian 1 (3 poin) ⭐

Jelaskan tiga langkah utama dalam paradigma Divide and Conquer! Berikan contoh penerapannya pada Merge Sort!

---

### Soal Uraian 2 (3 poin) ⭐

Perhatikan array berikut: `[38, 27, 43, 3, 9, 82, 10]`

Tunjukkan proses Merge Sort langkah demi langkah hingga array terurut! Gambarkan pohon rekursi yang terbentuk!

---

### Soal Uraian 3 (3 poin) ⭐

Jelaskan mengapa Merge Sort disebut sebagai algoritma "stable"! Berikan contoh kasus di mana sifat stable ini penting!

---

### Soal Uraian 4 (3 poin) ⭐

Tuliskan pseudocode untuk fungsi `merge(arr, left, mid, right)` yang menggabungkan dua subarray terurut!

---

### Soal Uraian 5 (3 poin) ⭐

Perhatikan array berikut: `[5, 2, 8, 1, 9, 3]`

Lakukan partisi menggunakan skema Lomuto dengan pivot = elemen terakhir (3). Tunjukkan langkah-langkahnya!

---

### Soal Uraian 6 (3 poin) ⭐

Bandingkan tiga strategi pemilihan pivot pada Quick Sort: (1) elemen pertama, (2) elemen terakhir, (3) median-of-three. Jelaskan kelebihan dan kekurangan masing-masing!

---

### Soal Uraian 7 (3 poin) ⭐⭐

Selesaikan rekurensi berikut menggunakan metode substitusi atau Master Theorem:
- T(n) = 2T(n/2) + n
- T(1) = 1

Tunjukkan langkah-langkah penyelesaiannya!

---

### Soal Uraian 8 (3 poin) ⭐⭐

Jelaskan mengapa lower bound untuk comparison-based sorting adalah Ω(n log n)! Gunakan konsep decision tree dalam penjelasan Anda!

---

### Soal Uraian 9 (3 poin) ⭐⭐

Implementasikan fungsi Quick Sort dalam C++ dengan strategi pivot median-of-three!

---

### Soal Uraian 10 (3 poin) ⭐⭐

Perhatikan array berikut: `[10, 80, 30, 90, 40, 50, 70]`

Lakukan Quick Sort lengkap dengan pivot = elemen terakhir. Tunjukkan kondisi array setelah setiap partisi!

---

### Soal Uraian 11 (3 poin) ⭐⭐

Jelaskan konsep "introsort" dan mengapa algoritma ini digunakan sebagai implementasi `std::sort` di C++!

---

### Soal Uraian 12 (3 poin) ⭐⭐

Analisis kompleksitas waktu Quick Sort untuk kasus:
a) Best case
b) Average case  
c) Worst case

Jelaskan kondisi input yang menyebabkan masing-masing kasus!

---

### Soal Uraian 13 (3 poin) ⭐⭐⭐

Implementasikan Merge Sort untuk linked list dalam C++! Jelaskan mengapa pendekatan ini berbeda dari Merge Sort untuk array!

---

### Soal Uraian 14 (3 poin) ⭐⭐⭐

Diberikan array dengan 1.000.000 elemen. Bandingkan perkiraan jumlah operasi yang diperlukan oleh:
a) Bubble Sort (O(n²))
b) Merge Sort (O(n log n))
c) Quick Sort average case (O(n log n))

Hitung rasio perbandingannya!

---

### Soal Uraian 15 (3 poin) ⭐⭐⭐

Desain algoritma hybrid yang menggunakan Merge Sort untuk data besar dan Insertion Sort untuk subarray kecil (threshold = 16). Jelaskan mengapa pendekatan ini lebih efisien!

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Prioritas Target Radar (7 poin)

**Latar Belakang:**
Sistem radar pertahanan udara mendeteksi multiple objek yang perlu diurutkan berdasarkan tingkat ancaman. Setiap objek memiliki atribut: ID, jarak (km), kecepatan (km/jam), altitude (m), dan threat score (0-100).

Kriteria pengurutan multi-level:
1. Prioritas utama: threat score (descending - tertinggi dulu)
2. Jika threat score sama: jarak (ascending - terdekat dulu)
3. Jika jarak sama: kecepatan (descending - tercepat dulu)

**Data Target:**
```
ID    | Jarak | Kecepatan | Altitude | Threat Score
------|-------|-----------|----------|-------------
T-101 |  45   |    800    |   5000   |     85
T-102 |  30   |    600    |   3000   |     90
T-103 |  45   |    750    |   4500   |     85
T-104 |  25   |    900    |   6000   |     90
T-105 |  50   |    500    |   2000   |     75
T-106 |  30   |    850    |   5500   |     90
```

**Pertanyaan:**

a) **(2 poin)** Algoritma sorting mana yang paling tepat untuk sistem ini? Jelaskan alasannya dengan mempertimbangkan:
   - Kebutuhan stabilitas
   - Jumlah data yang mungkin besar
   - Kebutuhan real-time

b) **(2 poin)** Tunjukkan urutan target setelah sorting berdasarkan kriteria multi-level di atas!

c) **(3 poin)** Implementasikan fungsi comparator dalam C++ untuk kriteria pengurutan ini!

---

### Studi Kasus 2: Sistem Log Komunikasi Militer (8 poin)

**Latar Belakang:**
Pusat komando menyimpan log komunikasi yang perlu dianalisis. Setiap log memiliki timestamp, unit pengirim, prioritas (1-5, dengan 1 tertinggi), dan ukuran pesan. Sistem harus mampu mengurutkan jutaan log untuk analisis forensik.

**Spesifikasi Sistem:**
- Jumlah log: 5.000.000 record
- RAM tersedia: 4 GB
- Setiap record: ~200 bytes
- Kebutuhan: sorting stabil berdasarkan timestamp

**Pertanyaan:**

a) **(2 poin)** Hitung estimasi memori yang dibutuhkan untuk menyimpan semua log! Apakah muat di RAM?

b) **(2 poin)** Jika data muat di RAM, algoritma apa yang Anda rekomendasikan? Berikan justifikasi berdasarkan:
   - Kompleksitas waktu
   - Kebutuhan stabilitas
   - Overhead memori

c) **(2 poin)** Estimasikan waktu eksekusi sorting jika satu operasi perbandingan memakan 1 mikrodetik! Bandingkan jika menggunakan:
   - Merge Sort: O(n log n)
   - Quick Sort average: O(n log n)
   - Bubble Sort: O(n²)

d) **(2 poin)** Jelaskan bagaimana Anda akan memodifikasi algoritma jika data TIDAK muat di RAM (external sorting)!

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Pembahasan Singkat |
|:--:|:-------:|-------------------|
| 1 | B | Merge Sort selalu O(n log n) di semua kasus |
| 2 | C | Quick Sort worst case O(n²) saat pivot selalu min/max |
| 3 | C | Merge Sort adalah stable, mempertahankan urutan relatif |
| 4 | C | Divide and Conquer: bagi, selesaikan, gabungkan |
| 5 | B | Pivot adalah elemen pembanding untuk partisi |
| 6 | C | 6 elemen → 5 kali merge (pohon rekursi level 3) |
| 7 | C | Merge Sort memerlukan O(n) memori tambahan |
| 8 | C | Median-of-three meminimalkan kemungkinan worst case |
| 9 | B | Partisi tidak seimbang → O(n²) |
| 10 | C | Setelah partisi: [2,1,5,8,9], pivot 5 di index 2 |
| 11 | B | Lower bound Ω(n log n) untuk comparison-based sorting |
| 12 | B | Merge hanya perlu akses sekuensial |
| 13 | B | Master Theorem case 2: O(n log n) |
| 14 | E | Bubble Sort dengan early termination O(n) untuk data hampir terurut |
| 15 | B | Quick Sort adalah in-place (O(log n) stack space) |
| 16 | C | Conquer = rekursi pada subproblem |
| 17 | B | Setelah partisi dengan pivot 3: elemen ≤3 di kiri |
| 18 | B | Introsort = Quick Sort + Heap Sort + Insertion Sort |
| 19 | C | ⌈log₂(n!)⌉ adalah information-theoretic lower bound |
| 20 | D | Optimize dengan DP bukan bagian dari D&C |

---

### Bagian B: Soal Uraian

#### Jawaban Soal Uraian 1

**Tiga langkah Divide and Conquer:**

1. **Divide (Bagi):** Membagi masalah menjadi submasalah yang lebih kecil dengan struktur sama
   - Pada Merge Sort: Bagi array menjadi dua bagian sama besar

2. **Conquer (Taklukkan):** Selesaikan submasalah secara rekursif; jika cukup kecil, selesaikan langsung
   - Pada Merge Sort: Rekursif sort kedua bagian; base case = 1 elemen

3. **Combine (Gabungkan):** Gabungkan solusi submasalah menjadi solusi masalah awal
   - Pada Merge Sort: Merge dua subarray terurut menjadi satu array terurut

---

#### Jawaban Soal Uraian 2

**Array:** `[38, 27, 43, 3, 9, 82, 10]`

**Pohon Rekursi:**
```
                [38,27,43,3,9,82,10]
                /                  \
        [38,27,43,3]            [9,82,10]
        /          \            /       \
    [38,27]      [43,3]      [9,82]    [10]
    /    \       /    \      /    \
  [38]  [27]  [43]   [3]   [9]   [82]
```

**Proses Merge (bottom-up):**
1. Merge [38] dan [27] → [27, 38]
2. Merge [43] dan [3] → [3, 43]
3. Merge [9] dan [82] → [9, 82]
4. Merge [27,38] dan [3,43] → [3, 27, 38, 43]
5. Merge [9,82] dan [10] → [9, 10, 82]
6. Merge [3,27,38,43] dan [9,10,82] → **[3, 9, 10, 27, 38, 43, 82]**

---

#### Jawaban Soal Uraian 3

**Stable sorting** berarti jika dua elemen memiliki kunci yang sama, urutan relatif mereka dalam input dipertahankan dalam output.

**Mengapa Merge Sort stable:**
- Saat merge, jika elemen dari kiri dan kanan sama, elemen dari kiri (yang asalnya lebih dulu) dipilih terlebih dahulu
- Ini mempertahankan urutan relatif elemen dengan kunci sama

**Contoh pentingnya stabilitas:**
Sorting data mahasiswa berdasarkan nilai, kemudian berdasarkan nama:
- Input: [(Budi, 85), (Ani, 85), (Citra, 90)]
- Sort by nilai (descending): [(Citra, 90), (Budi, 85), (Ani, 85)]
- Dengan stable sort, Budi tetap sebelum Ani (urutan asli)
- Jika tidak stable, bisa jadi [(Citra, 90), (Ani, 85), (Budi, 85)] - urutan berubah

---

#### Jawaban Soal Uraian 4

```
FUNCTION merge(arr, left, mid, right):
    n1 ← mid - left + 1
    n2 ← right - mid
    
    CREATE L[n1], R[n2]
    
    // Copy data ke array sementara
    FOR i ← 0 TO n1-1:
        L[i] ← arr[left + i]
    FOR j ← 0 TO n2-1:
        R[j] ← arr[mid + 1 + j]
    
    // Merge kembali ke arr
    i ← 0, j ← 0, k ← left
    
    WHILE i < n1 AND j < n2:
        IF L[i] <= R[j]:    // <= untuk stabilitas
            arr[k] ← L[i]
            i ← i + 1
        ELSE:
            arr[k] ← R[j]
            j ← j + 1
        k ← k + 1
    
    // Copy sisa elemen
    WHILE i < n1:
        arr[k] ← L[i]
        i ← i + 1
        k ← k + 1
    
    WHILE j < n2:
        arr[k] ← R[j]
        j ← j + 1
        k ← k + 1
```

---

#### Jawaban Soal Uraian 5

**Array:** `[5, 2, 8, 1, 9, 3]`, Pivot = 3 (elemen terakhir)

**Lomuto Partition:**
- i = -1 (posisi terakhir elemen ≤ pivot)
- j iterasi dari 0 sampai n-2

| j | arr[j] | arr[j] ≤ 3? | Aksi | Array | i |
|---|--------|-------------|------|-------|---|
| - | - | - | initial | [5,2,8,1,9,3] | -1 |
| 0 | 5 | No | - | [5,2,8,1,9,3] | -1 |
| 1 | 2 | Yes | i++, swap(1,1) | [5,2,8,1,9,3] | 0 |
| 2 | 8 | No | - | [5,2,8,1,9,3] | 0 |
| 3 | 1 | Yes | i++, swap(1,3) | [5,1,8,2,9,3] | 1 |

**Koreksi:** Mari ulang dengan benar:
- i = -1
- j=0: arr[0]=5 > 3, skip
- j=1: arr[1]=2 ≤ 3, i=0, swap(arr[0], arr[1]) → [2,5,8,1,9,3]
- j=2: arr[2]=8 > 3, skip
- j=3: arr[3]=1 ≤ 3, i=1, swap(arr[1], arr[3]) → [2,1,8,5,9,3]
- j=4: arr[4]=9 > 3, skip
- Selesai: swap(arr[i+1], arr[pivot]) = swap(arr[2], arr[5]) → **[2,1,3,5,9,8]**

Pivot 3 berada di index 2 (posisi akhir yang benar).

---

#### Jawaban Soal Uraian 6

| Strategi | Kelebihan | Kekurangan |
|----------|-----------|------------|
| **Elemen Pertama** | Sederhana, O(1) | Worst case pada data terurut/terurut terbalik |
| **Elemen Terakhir** | Sederhana, O(1) | Sama dengan elemen pertama, rawan worst case |
| **Median-of-three** | Menghindari worst case untuk data terurut, mendekati median sebenarnya | Sedikit lebih kompleks, O(1) tetapi ada overhead |

**Rekomendasi:** Median-of-three karena memberikan keseimbangan antara kesederhanaan dan robustness terhadap data yang sudah terurut.

---

#### Jawaban Soal Uraian 7

**Rekurensi:** T(n) = 2T(n/2) + n, T(1) = 1

**Menggunakan Master Theorem:**
- a = 2, b = 2, f(n) = n
- n^(log_b(a)) = n^(log_2(2)) = n^1 = n
- f(n) = n = Θ(n^(log_b(a)))
- Ini adalah **Case 2**: f(n) = Θ(n^(log_b(a)))
- Solusi: T(n) = Θ(n^(log_b(a)) × log n) = **Θ(n log n)**

**Verifikasi dengan substitusi:**
- T(n) = 2T(n/2) + n
- Guess: T(n) = cn log n
- T(n) = 2 × c(n/2)log(n/2) + n
- T(n) = cn(log n - 1) + n
- T(n) = cn log n - cn + n
- T(n) = cn log n + n(1-c)

Untuk c = 1: T(n) = n log n ✓

---

#### Jawaban Soal Uraian 8

**Lower bound Ω(n log n) untuk comparison-based sorting:**

**Konsep Decision Tree:**
- Setiap comparison-based sorting dapat direpresentasikan sebagai decision tree
- Setiap internal node = satu perbandingan
- Setiap leaf = satu permutasi hasil sorting
- Untuk n elemen, ada n! kemungkinan permutasi

**Argument:**
1. Decision tree harus memiliki minimal n! leaves (satu untuk setiap permutasi)
2. Binary tree dengan tinggi h memiliki maksimal 2^h leaves
3. Maka: 2^h ≥ n!
4. h ≥ log₂(n!)
5. Menggunakan Stirling's approximation: log₂(n!) ≈ n log₂ n - n log₂ e
6. Maka: h = Ω(n log n)

**Kesimpulan:** Setiap comparison-based sorting algorithm memerlukan minimal Ω(n log n) perbandingan dalam worst case.

---

#### Jawaban Soal Uraian 9

```cpp
#include <iostream>
using namespace std;

// Fungsi untuk mendapatkan median-of-three
int medianOfThree(int arr[], int low, int high) {
    int mid = low + (high - low) / 2;
    
    // Sort three elements
    if (arr[low] > arr[mid])
        swap(arr[low], arr[mid]);
    if (arr[low] > arr[high])
        swap(arr[low], arr[high]);
    if (arr[mid] > arr[high])
        swap(arr[mid], arr[high]);
    
    // Place median at high-1 position
    swap(arr[mid], arr[high - 1]);
    return arr[high - 1];
}

int partition(int arr[], int low, int high) {
    int pivot = medianOfThree(arr, low, high);
    int i = low;
    int j = high - 1;
    
    while (true) {
        while (arr[++i] < pivot);
        while (arr[--j] > pivot);
        if (i < j)
            swap(arr[i], arr[j]);
        else
            break;
    }
    swap(arr[i], arr[high - 1]);  // Restore pivot
    return i;
}

void quickSort(int arr[], int low, int high) {
    if (low + 2 <= high) {  // Minimal 3 elemen untuk median-of-three
        int pivotIndex = partition(arr, low, high);
        quickSort(arr, low, pivotIndex - 1);
        quickSort(arr, pivotIndex + 1, high);
    } else if (low < high) {
        // 2 elemen: simple comparison
        if (arr[low] > arr[high])
            swap(arr[low], arr[high]);
    }
}

int main() {
    int arr[] = {10, 80, 30, 90, 40, 50, 70};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    quickSort(arr, 0, n - 1);
    
    cout << "Sorted: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    
    return 0;
}
```

---

#### Jawaban Soal Uraian 10

**Array:** `[10, 80, 30, 90, 40, 50, 70]`, Pivot = elemen terakhir

**Partisi 1:** Pivot = 70
- Hasil: `[10, 30, 40, 50, 70, 90, 80]`
- Pivot 70 di posisi 4

**Partisi 2 (kiri):** Array `[10, 30, 40, 50]`, Pivot = 50
- Hasil: `[10, 30, 40, 50]`
- Pivot 50 di posisi 3

**Partisi 3 (kiri kiri):** Array `[10, 30, 40]`, Pivot = 40
- Hasil: `[10, 30, 40]`
- Pivot 40 di posisi 2

**Partisi 4 (kiri kiri kiri):** Array `[10, 30]`, Pivot = 30
- Hasil: `[10, 30]`
- Sudah terurut

**Partisi 5 (kanan):** Array `[90, 80]`, Pivot = 80
- Hasil: `[80, 90]`

**Hasil akhir:** `[10, 30, 40, 50, 70, 80, 90]`

---

#### Jawaban Soal Uraian 11

**Introsort (Introspective Sort):**

Introsort adalah algoritma hybrid yang menggabungkan:
1. **Quick Sort** - untuk performa rata-rata yang baik
2. **Heap Sort** - sebagai fallback jika rekursi terlalu dalam
3. **Insertion Sort** - untuk subarray kecil

**Cara kerja:**
1. Mulai dengan Quick Sort
2. Monitor kedalaman rekursi
3. Jika kedalaman melebihi 2 × log₂(n), switch ke Heap Sort
4. Untuk subarray < 16 elemen, gunakan Insertion Sort

**Mengapa digunakan di std::sort:**
- **Worst case O(n log n)** - dijamin oleh Heap Sort fallback
- **Average case cepat** - Quick Sort untuk kasus umum
- **Cache-friendly** - Insertion Sort untuk data kecil
- **In-place** - tidak memerlukan memori tambahan O(n)

---

#### Jawaban Soal Uraian 12

**Analisis Kompleksitas Quick Sort:**

**a) Best Case: O(n log n)**
- Kondisi: Pivot selalu membagi array menjadi dua bagian sama besar
- Rekurensi: T(n) = 2T(n/2) + O(n)
- Terjadi saat pivot = median sebenarnya

**b) Average Case: O(n log n)**
- Kondisi: Pivot membagi array dalam proporsi konstan (misalnya 1:9)
- Rekurensi: T(n) = T(n/10) + T(9n/10) + O(n) masih O(n log n)
- Terjadi dengan random pivot atau median-of-three

**c) Worst Case: O(n²)**
- Kondisi: Pivot selalu elemen terkecil atau terbesar
- Rekurensi: T(n) = T(n-1) + O(n) = O(n²)
- Terjadi saat:
  - Data sudah terurut + pivot = elemen pertama/terakhir
  - Data terurut terbalik + pivot = elemen pertama/terakhir
  - Semua elemen sama

---

#### Jawaban Soal Uraian 13

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

// Mendapatkan node tengah
Node* getMiddle(Node* head) {
    if (!head) return head;
    
    Node* slow = head;
    Node* fast = head->next;
    
    while (fast && fast->next) {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}

// Merge dua linked list terurut
Node* merge(Node* left, Node* right) {
    if (!left) return right;
    if (!right) return left;
    
    Node* result = nullptr;
    
    if (left->data <= right->data) {
        result = left;
        result->next = merge(left->next, right);
    } else {
        result = right;
        result->next = merge(left, right->next);
    }
    return result;
}

// Merge Sort untuk Linked List
Node* mergeSort(Node* head) {
    // Base case
    if (!head || !head->next)
        return head;
    
    // Dapatkan node tengah
    Node* middle = getMiddle(head);
    Node* nextOfMiddle = middle->next;
    
    // Putus linked list menjadi dua
    middle->next = nullptr;
    
    // Rekursif sort kedua bagian
    Node* left = mergeSort(head);
    Node* right = mergeSort(nextOfMiddle);
    
    // Merge hasil
    return merge(left, right);
}
```

**Perbedaan dengan array:**
1. **Tidak perlu O(n) memori tambahan** - hanya mengubah pointer
2. **Pembagian menggunakan slow-fast pointer** - O(n) untuk menemukan tengah
3. **Merge in-place** - hanya manipulasi pointer, tidak perlu copy

---

#### Jawaban Soal Uraian 14

**n = 1,000,000 elemen**

**a) Bubble Sort O(n²):**
- Operasi ≈ n² = (10⁶)² = **10¹² operasi**

**b) Merge Sort O(n log n):**
- log₂(10⁶) ≈ 20
- Operasi ≈ n × log₂(n) = 10⁶ × 20 = **2 × 10⁷ operasi**

**c) Quick Sort average O(n log n):**
- Operasi ≈ n × log₂(n) = 10⁶ × 20 = **2 × 10⁷ operasi**
- (Konstanta Quick Sort biasanya lebih kecil dari Merge Sort)

**Rasio Perbandingan:**
| Algoritma | Operasi | Rasio vs Merge Sort |
|-----------|---------|---------------------|
| Bubble Sort | 10¹² | 50,000× lebih lambat |
| Merge Sort | 2×10⁷ | 1× (baseline) |
| Quick Sort | 2×10⁷ | ~1× (sedikit lebih cepat) |

**Waktu estimasi (1 μs per operasi):**
- Bubble Sort: 10¹² μs = **11.6 hari**
- Merge/Quick Sort: 2×10⁷ μs = **20 detik**

---

#### Jawaban Soal Uraian 15

```cpp
const int THRESHOLD = 16;

void insertionSort(int arr[], int left, int right) {
    for (int i = left + 1; i <= right; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= left && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

void merge(int arr[], int left, int mid, int right) {
    // Implementasi merge standar
    // ... (sama seperti sebelumnya)
}

void hybridMergeSort(int arr[], int left, int right) {
    if (right - left + 1 <= THRESHOLD) {
        // Gunakan Insertion Sort untuk subarray kecil
        insertionSort(arr, left, right);
        return;
    }
    
    if (left < right) {
        int mid = left + (right - left) / 2;
        hybridMergeSort(arr, left, mid);
        hybridMergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}
```

**Mengapa lebih efisien:**
1. **Overhead rekursi berkurang** - tidak ada rekursi untuk subarray ≤16 elemen
2. **Cache efficiency** - Insertion Sort baik untuk data kecil yang fit di cache
3. **Konstanta kecil** - Insertion Sort memiliki konstanta lebih kecil dari Merge Sort
4. **O(n²) tidak masalah untuk n kecil** - 16² = 256 operasi sangat cepat

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Prioritas Target Radar

**a) Algoritma yang tepat: Merge Sort**

**Alasan:**
1. **Stabilitas diperlukan** - untuk sorting multi-level, elemen dengan kunci primer sama harus mempertahankan urutan dari sorting sekunder
2. **Konsistensi** - O(n log n) dijamin, penting untuk sistem real-time dengan deadline ketat
3. **Jumlah data besar** - Merge Sort efisien untuk data yang tidak fit di cache
4. **Prediktabilitas** - tidak ada worst case O(n²) seperti Quick Sort

**b) Urutan setelah sorting:**

Kriteria: Threat Score (desc) → Jarak (asc) → Kecepatan (desc)

| Urutan | ID | Threat | Jarak | Kecepatan |
|:------:|:---|:------:|:-----:|:---------:|
| 1 | T-104 | 90 | 25 | 900 |
| 2 | T-106 | 90 | 30 | 850 |
| 3 | T-102 | 90 | 30 | 600 |
| 4 | T-103 | 85 | 45 | 750 |
| 5 | T-101 | 85 | 45 | 800 |

**Koreksi urutan T-101 dan T-103:**
- Keduanya threat=85, jarak=45
- T-101 kecepatan 800, T-103 kecepatan 750
- Kecepatan descending → T-101 sebelum T-103

| Urutan | ID | Threat | Jarak | Kecepatan |
|:------:|:---|:------:|:-----:|:---------:|
| 1 | T-104 | 90 | 25 | 900 |
| 2 | T-106 | 90 | 30 | 850 |
| 3 | T-102 | 90 | 30 | 600 |
| 4 | T-101 | 85 | 45 | 800 |
| 5 | T-103 | 85 | 45 | 750 |
| 6 | T-105 | 75 | 50 | 500 |

**c) Fungsi comparator:**

```cpp
struct Target {
    string id;
    int jarak;
    int kecepatan;
    int altitude;
    int threatScore;
};

bool compareTarget(const Target& a, const Target& b) {
    // Prioritas 1: Threat score (descending)
    if (a.threatScore != b.threatScore)
        return a.threatScore > b.threatScore;
    
    // Prioritas 2: Jarak (ascending)
    if (a.jarak != b.jarak)
        return a.jarak < b.jarak;
    
    // Prioritas 3: Kecepatan (descending)
    return a.kecepatan > b.kecepatan;
}

// Penggunaan:
// stable_sort(targets.begin(), targets.end(), compareTarget);
```

---

#### Studi Kasus 2: Sistem Log Komunikasi Militer

**a) Estimasi memori:**
- Jumlah log: 5,000,000 record
- Ukuran per record: 200 bytes
- Total: 5,000,000 × 200 = 1,000,000,000 bytes = **~953 MB ≈ 1 GB**

**Kesimpulan:** Ya, muat di RAM 4 GB dengan sisa ~3 GB untuk working memory.

**b) Rekomendasi: Merge Sort (atau Timsort)**

**Justifikasi:**
- **Kompleksitas:** O(n log n) dijamin, tidak ada worst case O(n²)
- **Stabilitas:** Merge Sort stable, penting untuk mempertahankan urutan relatif log dengan timestamp sama
- **Memory:** Memerlukan ~1 GB tambahan untuk merge, total ~2 GB masih cukup
- **Alternatif:** Timsort (hybrid) yang digunakan Python, optimal untuk data dengan "runs" terurut

**c) Estimasi waktu (1 μs per perbandingan):**

n = 5,000,000

| Algoritma | Operasi | Waktu |
|-----------|---------|-------|
| Merge Sort | n × log₂(n) = 5×10⁶ × 22.3 ≈ 1.1×10⁸ | **110 detik** |
| Quick Sort | ~1.4 × n × log₂(n) ≈ 1.5×10⁸ | **150 detik** |
| Bubble Sort | n² = 2.5×10¹³ | **289 hari** |

**d) External Sorting (jika tidak muat di RAM):**

**Pendekatan: External Merge Sort**

1. **Divide:** Bagi data menjadi chunks yang muat di RAM (misal 500 MB)
2. **Sort in-memory:** Sort setiap chunk menggunakan Merge Sort
3. **Write to disk:** Tulis setiap sorted chunk ke file temporary
4. **K-way merge:** 
   - Baca sedikit dari setiap file ke buffer
   - Gunakan min-heap untuk merge k file sekaligus
   - Tulis hasil ke file output

**Kompleksitas I/O:** O((n/B) × log(n/M))
- B = ukuran block disk
- M = ukuran memory

```
Ilustrasi External Merge Sort:
[5GB data on disk]
       ↓ read 500MB chunks
[chunk1] [chunk2] ... [chunk10]
       ↓ sort in memory
[sorted1] [sorted2] ... [sorted10]
       ↓ write to temp files
       ↓ k-way merge with min-heap
[final sorted output]
```

---

## Kriteria Penilaian

| Bagian | Jumlah Soal | Poin per Soal | Total |
|--------|-------------|---------------|-------|
| Pilihan Ganda | 20 | 2 | 40 |
| Uraian | 15 | 3 | 45 |
| Studi Kasus 1 | 3 sub | 2+2+3 | 7 |
| Studi Kasus 2 | 4 sub | 2+2+2+2 | 8 |
| **Total** | | | **100** |

---

## Catatan untuk Pengajar

- Soal-soal mencakup Sub-CPMK-4.2 (merge sort, quick sort) dan Sub-CPMK-4.3 (pemilihan algoritma)
- Studi kasus menggunakan konteks pertahanan Indonesia (radar dan sistem komunikasi militer)
- Soal uraian memerlukan pemahaman konseptual dan kemampuan implementasi
- Tingkat kesulitan: ⭐ (mudah), ⭐⭐ (sedang), ⭐⭐⭐ (sulit)

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
