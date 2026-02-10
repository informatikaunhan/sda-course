# Modul 02: Analisis Algoritma dan Kompleksitas

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 02  
**Topik:** Analisis Algoritma dan Kompleksitas

> **Capaian Pembelajaran:** Sub-CPMK-1.2 — Mampu menganalisis kompleksitas waktu dan ruang menggunakan notasi Big-O, Big-Ω, Big-Θ

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.2-3; Weiss Ch.2; Goodrich Ch.4

---

## Tujuan Pembelajaran

Setelah mempelajari modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** pentingnya analisis algoritma dalam pengembangan perangkat lunak
2. **Menghitung** kompleksitas waktu algoritma menggunakan notasi Big-O
3. **Membedakan** notasi asimptotik Big-O, Big-Ω, dan Big-Θ
4. **Menganalisis** best case, worst case, dan average case dari suatu algoritma
5. **Menerapkan** aturan penjumlahan dan perkalian dalam analisis kompleksitas
6. **Mengidentifikasi** dan membandingkan kelas-kelas kompleksitas umum
7. **Menganalisis** kompleksitas algoritma iteratif dan rekursif sederhana

---

## 1. Pendahuluan: Mengapa Analisis Algoritma Penting?

### 1.1 Definisi Algoritma

> **Algoritma** adalah urutan langkah-langkah komputasi yang terdefinisi dengan baik untuk menyelesaikan suatu masalah, menerima input dan menghasilkan output yang diinginkan dalam waktu terbatas.

Dalam konteks pemrograman, algoritma adalah "resep" yang memberitahu komputer cara menyelesaikan masalah. Namun, untuk masalah yang sama, bisa ada banyak algoritma berbeda dengan performa yang sangat bervariasi.

### 1.2 Pentingnya Efisiensi Algoritma

Bayangkan Anda memiliki dua algoritma untuk mencari data dari database personel militer:
- **Algoritma A**: Memproses 1 juta data dalam 1 detik
- **Algoritma B**: Memproses 1 juta data dalam 1 jam

Keduanya menghasilkan hasil yang benar, tetapi perbedaan waktu sangat signifikan. Dalam operasi pertahanan, keterlambatan informasi dapat berakibat fatal.

### 1.3 Faktor yang Mempengaruhi Waktu Eksekusi

Waktu eksekusi program dipengaruhi oleh:
1. **Kecepatan hardware** (CPU, RAM, storage)
2. **Bahasa pemrograman** dan compiler/interpreter
3. **Kualitas implementasi** (coding style)
4. **Ukuran input** (n)
5. **Algoritma yang digunakan**

Analisis algoritma fokus pada faktor ke-5, karena ini yang dapat dikontrol programmer terlepas dari hardware atau bahasa pemrograman.

### 1.4 Pendekatan Analisis: Empiris vs Teoritis

| Aspek | Analisis Empiris | Analisis Teoritis |
|-------|------------------|-------------------|
| **Metode** | Mengukur waktu eksekusi aktual | Menghitung operasi dasar |
| **Ketergantungan Hardware** | Tinggi | Tidak ada |
| **Input yang Dibutuhkan** | Harus ada data aktual | Bisa untuk semua ukuran n |
| **Hasil** | Waktu dalam detik/milidetik | Fungsi pertumbuhan |
| **Kegunaan** | Benchmarking sistem tertentu | Perbandingan algoritma universal |

---

### SOLVED PROBLEM 1 ⭐

**Pertanyaan:** Jelaskan mengapa kita tidak cukup hanya mengukur waktu eksekusi aktual untuk membandingkan dua algoritma!

**Penyelesaian:**

Mengukur waktu eksekusi aktual memiliki beberapa kelemahan fundamental:

1. **Ketergantungan Hardware**: Algoritma yang sama akan berjalan berbeda di komputer berbeda. Algoritma A mungkin lebih cepat di komputer X tapi lebih lambat di komputer Y.

2. **Variasi Kondisi**: Waktu eksekusi dipengaruhi program lain yang berjalan, suhu CPU, penggunaan memori, dll.

3. **Keterbatasan Input**: Kita hanya bisa mengukur dengan input tertentu. Bagaimana dengan input yang belum pernah diuji?

4. **Tidak Scalable**: Hasil pengukuran untuk n=1000 tidak bisa langsung diprediksi untuk n=1.000.000.

Oleh karena itu, analisis teoritis menggunakan notasi asimptotik diperlukan untuk mendapatkan gambaran universal tentang efisiensi algoritma.

---

## 2. Menghitung Operasi Dasar

### 2.1 Operasi Dasar (Primitive Operations)

> **Operasi dasar** adalah instruksi komputasi yang diasumsikan membutuhkan waktu konstan, terlepas dari ukuran input.

Operasi dasar meliputi:
- Operasi aritmatika (+, -, *, /, %)
- Operasi perbandingan (<, >, ==, !=, <=, >=)
- Operasi assignment (=)
- Akses elemen array dengan indeks
- Mengikuti pointer/referensi
- Pemanggilan dan return fungsi

### 2.2 Model Analisis

Dalam analisis algoritma, kita menggunakan **model RAM (Random Access Machine)**:
- Setiap operasi dasar membutuhkan waktu 1 unit
- Akses memori membutuhkan waktu konstan
- Tidak ada paralelisme

### 2.3 Contoh Penghitungan Operasi

```cpp
int findMax(int arr[], int n) {
    int max = arr[0];           // 2 operasi: akses array + assignment
    for (int i = 1; i < n; i++) { // 1 + (n-1) + (n-1) operasi
        if (arr[i] > max) {     // 2 operasi per iterasi: akses + perbandingan
            max = arr[i];       // 2 operasi: akses + assignment
        }
    }
    return max;                 // 1 operasi
}
```

**Analisis detail:**
- Inisialisasi `max`: 2 operasi
- Inisialisasi loop `i = 1`: 1 operasi
- Kondisi loop `i < n`: (n-1) kali perbandingan
- Increment `i++`: (n-1) kali
- Akses `arr[i]` dan perbandingan: 2(n-1) operasi
- Assignment dalam if (worst case): 2(n-1) operasi
- Return: 1 operasi

**Total (worst case)**: 2 + 1 + (n-1) + (n-1) + 2(n-1) + 2(n-1) + 1 = **6n - 2** operasi

---

### SOLVED PROBLEM 2 ⭐

**Pertanyaan:** Hitung jumlah operasi dasar pada kode berikut untuk array berukuran n:

```cpp
int sum = 0;
for (int i = 0; i < n; i++) {
    sum = sum + arr[i];
}
```

**Penyelesaian:**

| Baris | Operasi | Jumlah Eksekusi | Total |
|-------|---------|-----------------|-------|
| `int sum = 0` | Assignment | 1 | 1 |
| `int i = 0` | Assignment | 1 | 1 |
| `i < n` | Perbandingan | n+1 | n+1 |
| `i++` | Increment | n | n |
| `arr[i]` | Akses array | n | n |
| `sum + arr[i]` | Penjumlahan | n | n |
| `sum = ...` | Assignment | n | n |

**Total operasi = 1 + 1 + (n+1) + n + n + n + n = 5n + 3**

---

### SOLVED PROBLEM 3 ⭐

**Pertanyaan:** Analisis jumlah operasi pada nested loop berikut:

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        cout << i * j << " ";
    }
}
```

**Penyelesaian:**

Loop luar berjalan **n kali**. Untuk setiap iterasi loop luar, loop dalam berjalan **n kali**.

Operasi dalam loop terdalam (per eksekusi):
- Perkalian `i * j`: 1 operasi
- Output `cout`: 1 operasi

Total operasi dalam loop terdalam: n × n × 2 = **2n²**

Operasi loop overhead:
- Inisialisasi, perbandingan, increment loop luar: ~3n
- Inisialisasi, perbandingan, increment loop dalam: ~3n²

**Total ≈ 5n² + 3n**

Untuk n besar, suku dominan adalah **n²**.

---

## 3. Notasi Asimptotik

### 3.1 Konsep Pertumbuhan Fungsi

Ketika menganalisis algoritma, kita tertarik pada bagaimana waktu eksekusi **tumbuh** seiring bertambahnya ukuran input n. Untuk n yang sangat besar:
- Konstanta dan suku-suku kecil menjadi tidak signifikan
- Hanya suku dengan pangkat tertinggi yang dominan

Contoh: Jika T(n) = 3n² + 5n + 100
- Untuk n = 10: 3(100) + 50 + 100 = 450
- Untuk n = 1000: 3(1.000.000) + 5000 + 100 = 3.005.100

Suku n² mendominasi ~99.8% dari total!

### 3.2 Notasi Big-O (Upper Bound)

> **Definisi Formal:** f(n) = O(g(n)) jika terdapat konstanta positif c dan n₀ sedemikian sehingga f(n) ≤ c·g(n) untuk semua n ≥ n₀.

**Interpretasi:** Big-O memberikan batas atas pertumbuhan fungsi. Jika T(n) = O(n²), maka untuk input cukup besar, waktu eksekusi **paling banyak** tumbuh secara kuadratik.

![Visualisasi Big-O](images/p02-01-big-o-visualization.png)

*Gambar 2.1: Visualisasi notasi Big-O — f(n) dibatasi oleh c·g(n) untuk n ≥ n₀*


### 3.3 Notasi Big-Ω (Omega - Lower Bound)

> **Definisi Formal:** f(n) = Ω(g(n)) jika terdapat konstanta positif c dan n₀ sedemikian sehingga f(n) ≥ c·g(n) untuk semua n ≥ n₀.

**Interpretasi:** Big-Ω memberikan batas bawah. Jika T(n) = Ω(n), maka waktu eksekusi **paling sedikit** tumbuh secara linear.

### 3.4 Notasi Big-Θ (Theta - Tight Bound)

> **Definisi Formal:** f(n) = Θ(g(n)) jika dan hanya jika f(n) = O(g(n)) dan f(n) = Ω(g(n)).

**Interpretasi:** Big-Θ memberikan batas ketat. Jika T(n) = Θ(n²), maka waktu eksekusi tumbuh **tepat** secara kuadratik (tidak lebih cepat, tidak lebih lambat).

### 3.5 Perbandingan Notasi

| Notasi | Analogi | Makna |
|--------|---------|-------|
| O(g(n)) | ≤ | Batas atas (paling buruk) |
| Ω(g(n)) | ≥ | Batas bawah (paling baik) |
| Θ(g(n)) | = | Batas ketat (exact order) |

---

### SOLVED PROBLEM 4 ⭐⭐

**Pertanyaan:** Buktikan bahwa 3n² + 5n + 100 = O(n²)!

**Penyelesaian:**

Menurut definisi Big-O, kita perlu menemukan c dan n₀ sehingga:
3n² + 5n + 100 ≤ c·n² untuk semua n ≥ n₀

**Langkah 1:** Untuk n ≥ 1:
- 5n ≤ 5n²
- 100 ≤ 100n² (untuk n ≥ 1)

**Langkah 2:** Substitusi:
3n² + 5n + 100 ≤ 3n² + 5n² + 100n² = 108n²

**Langkah 3:** Pilih c = 108 dan n₀ = 1

**Verifikasi untuk n = 1:**
- f(1) = 3 + 5 + 100 = 108
- c·g(1) = 108 · 1 = 108
- 108 ≤ 108 ✓

**Verifikasi untuk n = 10:**
- f(10) = 300 + 50 + 100 = 450
- c·g(10) = 108 · 100 = 10800
- 450 ≤ 10800 ✓

**Kesimpulan:** 3n² + 5n + 100 = O(n²) dengan c = 108 dan n₀ = 1. ∎

---

### SOLVED PROBLEM 5 ⭐⭐

**Pertanyaan:** Buktikan bahwa n² ≠ O(n)!

**Penyelesaian:**

Kita akan membuktikan dengan kontradiksi.

**Asumsi:** Misalkan n² = O(n), maka ada c > 0 dan n₀ > 0 sehingga:
n² ≤ c·n untuk semua n ≥ n₀

**Manipulasi aljabar:**
n² ≤ c·n
n ≤ c (untuk n > 0, bagi kedua sisi dengan n)

**Kontradiksi:**
Ini berarti n dibatasi oleh konstanta c untuk semua n ≥ n₀. Namun, n bisa tumbuh tanpa batas!

Pilih n = c + 1:
- n² = (c+1)²
- c·n = c(c+1) = c² + c

(c+1)² = c² + 2c + 1 > c² + c = c·n

Ini kontradiksi dengan asumsi n² ≤ c·n.

**Kesimpulan:** n² ≠ O(n). ∎

---

### SOLVED PROBLEM 6 ⭐

**Pertanyaan:** Jika f(n) = 5n³ + 2n² + 100, tentukan notasi Big-O yang paling ketat!

**Penyelesaian:**

Identifikasi suku dominan: **5n³** (pangkat tertinggi)

Untuk Big-O yang ketat, kita pilih fungsi dengan pangkat sama:

f(n) = 5n³ + 2n² + 100 = **O(n³)**

**Verifikasi:**
- 5n³ ≤ 5n³
- 2n² ≤ 2n³ untuk n ≥ 1
- 100 ≤ 100n³ untuk n ≥ 1

Total: 5n³ + 2n² + 100 ≤ 107n³

Dengan c = 107 dan n₀ = 1, terbukti f(n) = O(n³). ∎

---

## 4. Aturan Penyederhanaan Notasi Big-O

### 4.1 Aturan Konstanta

> Konstanta pengali dapat diabaikan: O(c·f(n)) = O(f(n))

Contoh: O(5n) = O(n), O(100n²) = O(n²)

**Alasan:** Konstanta tidak mempengaruhi *tingkat pertumbuhan*.

### 4.2 Aturan Suku Dominan

> Suku dengan pertumbuhan lebih lambat dapat diabaikan: O(f(n) + g(n)) = O(max(f(n), g(n)))

Contoh: O(n² + n) = O(n²), O(n³ + 1000n²) = O(n³)

### 4.3 Aturan Penjumlahan (Sum Rule)

> Untuk dua segmen kode berurutan:
> T(n) = T₁(n) + T₂(n) → O(max(T₁(n), T₂(n)))

```cpp
// Segmen 1: O(n)
for (int i = 0; i < n; i++) { /* ... */ }

// Segmen 2: O(n²)
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) { /* ... */ }
}
// Total: O(n² + n) = O(n²)
```

### 4.4 Aturan Perkalian (Product Rule)

> Untuk loop bersarang:
> T(n) = T₁(n) × T₂(n) → O(T₁(n) × T₂(n))

```cpp
// Loop luar: n kali
for (int i = 0; i < n; i++) {
    // Loop dalam: n kali per iterasi luar
    for (int j = 0; j < n; j++) {
        /* O(1) operation */
    }
}
// Total: O(n × n) = O(n²)
```

---

### SOLVED PROBLEM 7 ⭐

**Pertanyaan:** Sederhanakan notasi Big-O berikut: O(3n³ + 100n² + n + 5000)

**Penyelesaian:**

**Langkah 1:** Identifikasi suku dominan
- 3n³ (tumbuh paling cepat)
- 100n² (tumbuh lebih lambat dari n³)
- n (tumbuh lebih lambat dari n²)
- 5000 (konstanta)

**Langkah 2:** Terapkan aturan suku dominan
O(3n³ + 100n² + n + 5000) = O(3n³)

**Langkah 3:** Terapkan aturan konstanta
O(3n³) = **O(n³)**

---

### SOLVED PROBLEM 8 ⭐⭐

**Pertanyaan:** Tentukan kompleksitas waktu dari kode berikut:

```cpp
void process(int n) {
    // Bagian A
    for (int i = 0; i < n; i++) {
        cout << i << endl;
    }
    
    // Bagian B
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << i + j << endl;
        }
    }
    
    // Bagian C
    for (int i = 0; i < 1000; i++) {
        cout << "Hello" << endl;
    }
}
```

**Penyelesaian:**

**Bagian A:** Single loop dari 0 sampai n-1
- Kompleksitas: O(n)

**Bagian B:** Nested loop, masing-masing n kali
- Kompleksitas: O(n × n) = O(n²)

**Bagian C:** Loop dengan batas konstan (1000)
- Kompleksitas: O(1000) = O(1)

**Total (aturan penjumlahan):**
T(n) = O(n) + O(n²) + O(1) = O(max(n, n², 1)) = **O(n²)**

---

### SOLVED PROBLEM 9 ⭐⭐

**Pertanyaan:** Tentukan kompleksitas dari kode berikut:

```cpp
void mystery(int n) {
    for (int i = 1; i < n; i = i * 2) {
        for (int j = 0; j < n; j++) {
            cout << i << " " << j << endl;
        }
    }
}
```

**Penyelesaian:**

**Analisis loop luar:**
- i dimulai dari 1 dan dikali 2 setiap iterasi
- Nilai i: 1, 2, 4, 8, 16, ..., hingga i ≥ n
- Berapa kali loop berjalan? 
- 2^k ≥ n → k ≥ log₂(n)
- Loop luar berjalan **O(log n)** kali

**Analisis loop dalam:**
- Loop dari 0 sampai n-1
- Kompleksitas: **O(n)**

**Total (aturan perkalian):**
T(n) = O(log n) × O(n) = **O(n log n)**

---

## 5. Kelas-Kelas Kompleksitas Umum

### 5.1 Hierarki Kompleksitas

Berikut adalah kelas-kelas kompleksitas dari yang paling efisien hingga paling tidak efisien:

| Notasi | Nama | Contoh Algoritma |
|--------|------|------------------|
| O(1) | Konstanta | Akses array dengan indeks |
| O(log n) | Logaritmik | Binary search |
| O(n) | Linear | Linear search, traversal array |
| O(n log n) | Linearitmik | Merge sort, Quick sort (avg) |
| O(n²) | Kuadratik | Bubble sort, Selection sort |
| O(n³) | Kubik | Matrix multiplication (naif) |
| O(2ⁿ) | Eksponensial | Subset generation (brute force) |
| O(n!) | Faktorial | Permutation generation |

![Perbandingan Kelas Kompleksitas](images/p02-02-complexity-comparison.png)

*Gambar 2.2: Perbandingan pertumbuhan berbagai kelas kompleksitas*


### 5.2 Dampak Praktis Perbedaan Kompleksitas

Asumsikan komputer dapat melakukan 10⁹ operasi per detik:

| n | O(log n) | O(n) | O(n log n) | O(n²) | O(2ⁿ) |
|---|----------|------|------------|-------|-------|
| 10 | 3 ns | 10 ns | 33 ns | 100 ns | 1 μs |
| 100 | 7 ns | 100 ns | 664 ns | 10 μs | 10¹⁴ tahun |
| 1000 | 10 ns | 1 μs | 10 μs | 1 ms | ∞ |
| 10⁶ | 20 ns | 1 ms | 20 ms | 17 menit | ∞ |
| 10⁹ | 30 ns | 1 detik | 30 detik | 31 tahun | ∞ |

**Catatan:** Untuk n besar, algoritma eksponensial praktis tidak dapat diselesaikan!

### 5.3 Analogi Militer untuk Memahami Kompleksitas

Bayangkan operasi verifikasi identitas personel:

- **O(1)**: Periksa badge ID elektronik — langsung teridentifikasi
- **O(log n)**: Cari nama di buku registrasi terurut — buka tengah, bandingkan, ulangi
- **O(n)**: Panggil absen satu per satu — waktu berbanding lurus dengan jumlah personel
- **O(n²)**: Setiap personel menyalami semua personel lain — meeting besar sangat lama
- **O(2ⁿ)**: Evaluasi semua kemungkinan kombinasi tim — tidak praktis untuk tim besar

---

### SOLVED PROBLEM 10 ⭐

**Pertanyaan:** Algoritma A berjalan dalam O(n²) dan algoritma B dalam O(n log n). Untuk n = 1.000.000, berapa kali lebih cepat algoritma B?

**Penyelesaian:**

**Waktu A:** n² = (10⁶)² = 10¹² operasi

**Waktu B:** n log₂ n = 10⁶ × log₂(10⁶) = 10⁶ × 20 = 2 × 10⁷ operasi

**Rasio:**
Waktu A / Waktu B = 10¹² / (2 × 10⁷) = 5 × 10⁴ = **50.000 kali**

Algoritma B **50.000 kali lebih cepat** untuk n = 1.000.000!

---

### SOLVED PROBLEM 11 ⭐⭐

**Pertanyaan:** Sebuah algoritma memiliki waktu eksekusi T(n) = 5n² + 3n log n + 1000. Tentukan notasi Θ yang tepat!

**Penyelesaian:**

Untuk menentukan Θ(f(n)), kita perlu membuktikan bahwa T(n) adalah O(f(n)) dan Ω(f(n)).

**Identifikasi suku dominan:**
- 5n² tumbuh lebih cepat dari 3n log n (karena n² > n log n untuk n besar)
- 5n² tumbuh lebih cepat dari 1000

**Buktikan O(n²):**
5n² + 3n log n + 1000 ≤ 5n² + 3n² + n² = 9n² untuk n ≥ 1000
Dengan c = 9 dan n₀ = 1000, T(n) = O(n²) ✓

**Buktikan Ω(n²):**
5n² + 3n log n + 1000 ≥ 5n² untuk semua n ≥ 1
Dengan c = 5 dan n₀ = 1, T(n) = Ω(n²) ✓

**Kesimpulan:** T(n) = **Θ(n²)** ∎

---

## 6. Analisis Best Case, Worst Case, dan Average Case

### 6.1 Konsep Dasar

Untuk input berukuran n yang sama, algoritma bisa memiliki waktu eksekusi berbeda tergantung **konfigurasi input**.

> **Worst Case T(n):** Waktu maksimum untuk input berukuran n  
> **Best Case T(n):** Waktu minimum untuk input berukuran n  
> **Average Case T(n):** Waktu rata-rata untuk semua kemungkinan input berukuran n

### 6.2 Contoh: Linear Search

```cpp
int linearSearch(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key) {
            return i;  // Ditemukan
        }
    }
    return -1;  // Tidak ditemukan
}
```

**Analisis:**

| Case | Kondisi | Jumlah Perbandingan | Kompleksitas |
|------|---------|---------------------|--------------|
| Best | key di posisi pertama | 1 | O(1) |
| Worst | key tidak ada atau di akhir | n | O(n) |
| Average | key di posisi acak | n/2 | O(n) |

### 6.3 Contoh: Insertion Sort (Preview)

Pada insertion sort (akan dibahas di Pertemuan 9), kompleksitasnya:

| Case | Kondisi | Kompleksitas |
|------|---------|--------------|
| Best | Array sudah terurut | O(n) |
| Worst | Array terurut terbalik | O(n²) |
| Average | Array acak | O(n²) |

### 6.4 Mana yang Paling Penting?

> Dalam praktik, **worst case** paling sering digunakan karena memberikan **garansi performa**. Kita bisa yakin algoritma tidak akan lebih lambat dari batas ini.

Average case berguna untuk algoritma yang worst case-nya jarang terjadi (seperti Quick Sort).

---

### SOLVED PROBLEM 12 ⭐⭐

**Pertanyaan:** Analisis best case, worst case, dan average case dari algoritma berikut:

```cpp
bool hasDuplicate(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            if (arr[i] == arr[j]) {
                return true;
            }
        }
    }
    return false;
}
```

**Penyelesaian:**

**Best Case:**
- Kondisi: Dua elemen pertama sama (arr[0] == arr[1])
- Perbandingan: 1
- Kompleksitas: **O(1)**

**Worst Case:**
- Kondisi: Tidak ada duplikat (semua elemen unik)
- Loop dalam berjalan: (n-1) + (n-2) + ... + 1 = n(n-1)/2
- Kompleksitas: **O(n²)**

**Average Case:**
- Jika ada duplikat, rata-rata akan ditemukan setelah sekitar n(n-1)/4 perbandingan
- Jika tidak ada duplikat, perlu n(n-1)/2 perbandingan
- Kompleksitas: **O(n²)**

---

### SOLVED PROBLEM 13 ⭐⭐⭐

**Pertanyaan:** Sebuah algoritma memiliki:
- Best case: O(n)
- Worst case: O(n²)

Jika dalam 1000 kali eksekusi, 990 kali mencapai best case dan 10 kali mencapai worst case, tentukan average case!

**Penyelesaian:**

**Pendekatan:** Average case adalah weighted average dari semua kemungkinan.

Misalkan:
- Probabilitas best case: p = 990/1000 = 0.99
- Probabilitas worst case: q = 10/1000 = 0.01
- T_best(n) = c₁·n
- T_worst(n) = c₂·n²

**Average case:**
T_avg(n) = p × T_best(n) + q × T_worst(n)
T_avg(n) = 0.99 × c₁·n + 0.01 × c₂·n²

**Analisis asimptotik:**
Untuk n kecil, suku c₁·n mungkin dominan.
Untuk n besar, suku 0.01 × c₂·n² akan mendominasi.

Secara asimptotik, **T_avg(n) = O(n²)** karena suku n² tetap ada (meskipun dengan koefisien kecil).

**Namun**, dalam praktik untuk n yang tidak terlalu besar, algoritma ini akan terasa cepat karena 99% kasus mencapai O(n).

---

## 7. Analisis Algoritma Iteratif

### 7.1 Pola Loop Tunggal

```cpp
// Pola 1: Loop linear
for (int i = 0; i < n; i++) { ... }  // O(n)

// Pola 2: Loop dengan increment konstan
for (int i = 0; i < n; i += 2) { ... }  // O(n/2) = O(n)

// Pola 3: Loop dengan pengali
for (int i = 1; i < n; i *= 2) { ... }  // O(log n)

// Pola 4: Loop dengan pembagi
for (int i = n; i > 0; i /= 2) { ... }  // O(log n)
```

### 7.2 Pola Loop Bersarang

```cpp
// Pola 1: Nested linear
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) { ... }  // O(n²)
}

// Pola 2: Loop dalam bergantung pada i
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) { ... }  // O(n²/2) = O(n²)
}

// Pola 3: Loop luar logaritmik
for (int i = 1; i < n; i *= 2) {
    for (int j = 0; j < n; j++) { ... }  // O(n log n)
}
```

### 7.3 Teknik Menghitung Loop Bergantung

Untuk loop dalam yang bergantung pada loop luar:

```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        // operasi O(1)
    }
}
```

**Hitung total iterasi loop dalam:**
- Ketika i = 0: j berjalan 0 kali
- Ketika i = 1: j berjalan 1 kali
- Ketika i = 2: j berjalan 2 kali
- ...
- Ketika i = n-1: j berjalan n-1 kali

**Total:** 0 + 1 + 2 + ... + (n-1) = n(n-1)/2 = **O(n²)**

---

### SOLVED PROBLEM 14 ⭐⭐

**Pertanyaan:** Tentukan kompleksitas waktu dari kode berikut:

```cpp
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j += i) {
        cout << i << " " << j << endl;
    }
}
```

**Penyelesaian:**

**Analisis loop dalam untuk setiap nilai i:**
- i = 1: j = 1, 2, 3, ..., n → n iterasi
- i = 2: j = 1, 3, 5, 7, ..., n → n/2 iterasi
- i = 3: j = 1, 4, 7, 10, ..., n → n/3 iterasi
- ...
- i = n: j = 1 → 1 iterasi

**Total iterasi:**
T(n) = n + n/2 + n/3 + ... + n/n = n(1 + 1/2 + 1/3 + ... + 1/n)

Deret 1 + 1/2 + 1/3 + ... + 1/n adalah **deret harmonik** Hₙ.

Diketahui: Hₙ = Θ(log n)

**Kesimpulan:** T(n) = n × Θ(log n) = **Θ(n log n)** ∎

---

### SOLVED PROBLEM 15 ⭐⭐

**Pertanyaan:** Analisis kompleksitas kode berikut:

```cpp
void complex(int n) {
    for (int i = 1; i <= n; i *= 2) {
        for (int j = 1; j <= n; j *= 2) {
            cout << i * j << endl;
        }
    }
}
```

**Penyelesaian:**

**Loop luar:**
- i mulai dari 1, dikali 2 setiap iterasi
- Berhenti saat i > n
- Jumlah iterasi: log₂(n)

**Loop dalam:**
- j mulai dari 1, dikali 2 setiap iterasi
- Berhenti saat j > n
- Jumlah iterasi: log₂(n)

**Total:**
T(n) = log₂(n) × log₂(n) = (log₂n)² = **O(log² n)** atau **O((log n)²)**

---

## 8. Analisis Algoritma Rekursif

### 8.1 Recurrence Relation

Untuk algoritma rekursif, kompleksitas dinyatakan dalam **relasi rekurens**:

```cpp
void printN(int n) {
    if (n <= 0) return;        // Base case
    cout << n << endl;         // O(1)
    printN(n - 1);             // T(n-1)
}
```

**Relasi rekurens:**
- T(0) = 1 (base case)
- T(n) = T(n-1) + 1 (untuk n > 0)

### 8.2 Metode Substitusi (Iterasi)

**Langkah-langkah:**
1. Tulis beberapa suku pertama
2. Identifikasi pola
3. Buktikan dengan substitusi

**Contoh:** Selesaikan T(n) = T(n-1) + 1, T(0) = 1

T(n) = T(n-1) + 1
T(n) = [T(n-2) + 1] + 1 = T(n-2) + 2
T(n) = [T(n-3) + 1] + 2 = T(n-3) + 3
...
T(n) = T(n-k) + k

Ketika k = n:
T(n) = T(0) + n = 1 + n = **O(n)**

### 8.3 Contoh: Factorial Rekursif

```cpp
long factorial(int n) {
    if (n <= 1) return 1;      // T(1) = O(1)
    return n * factorial(n-1); // T(n) = T(n-1) + O(1)
}
```

**Relasi rekurens:** T(n) = T(n-1) + c, T(1) = c

**Solusi:** T(n) = c·n = **O(n)**

### 8.4 Contoh: Fibonacci Rekursif (Naive)

```cpp
long fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);  // Dua pemanggilan rekursif!
}
```

**Relasi rekurens:** T(n) = T(n-1) + T(n-2) + c, T(0) = T(1) = c

**Solusi (dapat dibuktikan):** T(n) ≈ O(2ⁿ)

Ini menunjukkan implementasi rekursif naif Fibonacci **sangat tidak efisien**!

![Pohon Rekursi Fibonacci](images/p02-03-fibonacci-recursion-tree.png)

*Gambar 2.3: Pohon rekursi Fibonacci — banyak perhitungan redundan*


---

### SOLVED PROBLEM 16 ⭐⭐

**Pertanyaan:** Selesaikan relasi rekurens: T(n) = 2T(n/2) + n, dengan T(1) = 1

**Penyelesaian menggunakan metode iterasi:**

**Langkah 1:** Ekspansi
T(n) = 2T(n/2) + n
     = 2[2T(n/4) + n/2] + n
     = 4T(n/4) + n + n
     = 4T(n/4) + 2n

**Langkah 2:** Lanjutkan ekspansi
     = 4[2T(n/8) + n/4] + 2n
     = 8T(n/8) + n + 2n
     = 8T(n/8) + 3n

**Langkah 3:** Identifikasi pola
Setelah k langkah: T(n) = 2^k · T(n/2^k) + k·n

**Langkah 4:** Base case tercapai ketika n/2^k = 1, yaitu k = log₂(n)

T(n) = 2^(log n) · T(1) + log(n) · n
     = n · 1 + n log n
     = n + n log n
     = **O(n log n)**

**Catatan:** Ini adalah kompleksitas Merge Sort yang akan dibahas di Pertemuan 10!

---

### SOLVED PROBLEM 17 ⭐⭐⭐

**Pertanyaan:** Tentukan kompleksitas dari fungsi rekursif berikut:

```cpp
int mystery(int n) {
    if (n <= 1) return 1;
    return mystery(n/2) + mystery(n/2) + n;
}
```

**Penyelesaian:**

**Identifikasi relasi rekurens:**
- Base case: T(1) = c (konstanta)
- Recursive case: T(n) = 2T(n/2) + n

**Ini sama dengan Solved Problem 16!**

Menggunakan hasil sebelumnya: T(n) = **O(n log n)**

**Verifikasi dengan pohon rekursi:**
- Level 0: 1 node dengan kerja n
- Level 1: 2 node dengan kerja n/2 masing-masing → total n
- Level 2: 4 node dengan kerja n/4 masing-masing → total n
- ...
- Level log n: n node dengan kerja 1 masing-masing → total n

Total kerja = n × (log n + 1) = **O(n log n)** ✓

---

### SOLVED PROBLEM 18 ⭐⭐⭐

**Pertanyaan:** Analisis kompleksitas Binary Search rekursif:

```cpp
int binarySearch(int arr[], int low, int high, int key) {
    if (low > high) return -1;
    
    int mid = low + (high - low) / 2;
    
    if (arr[mid] == key) return mid;
    else if (arr[mid] > key)
        return binarySearch(arr, low, mid - 1, key);
    else
        return binarySearch(arr, mid + 1, high, key);
}
```

**Penyelesaian:**

**Relasi rekurens:**
- Setiap pemanggilan membagi rentang pencarian menjadi setengah
- Operasi per pemanggilan (selain rekursi): O(1)

T(n) = T(n/2) + c, dengan T(1) = c

**Metode iterasi:**
T(n) = T(n/2) + c
     = T(n/4) + c + c = T(n/4) + 2c
     = T(n/8) + 3c
     ...
     = T(n/2^k) + k·c

Ketika n/2^k = 1 → k = log₂(n):
T(n) = T(1) + log₂(n) · c = c + c·log₂(n) = **O(log n)**

Binary Search sangat efisien karena kompleksitasnya logaritmik!

---

## 9. Pengenalan Master Theorem

### 9.1 Bentuk Umum Relasi Rekurens Divide-and-Conquer

Banyak algoritma divide-and-conquer memiliki relasi rekurens berbentuk:

**T(n) = aT(n/b) + f(n)**

Dimana:
- a ≥ 1: jumlah subproblem
- b > 1: faktor pembagi ukuran subproblem
- f(n): waktu untuk membagi dan menggabungkan

### 9.2 Master Theorem (Simplified)

Untuk T(n) = aT(n/b) + n^d dimana a ≥ 1, b > 1, d ≥ 0:

| Kondisi | Kompleksitas |
|---------|--------------|
| a < b^d | O(n^d) |
| a = b^d | O(n^d log n) |
| a > b^d | O(n^(log_b a)) |

### 9.3 Contoh Penerapan

**Contoh 1:** T(n) = 2T(n/2) + n
- a = 2, b = 2, d = 1
- b^d = 2^1 = 2
- a = b^d → **O(n log n)** (Merge Sort!)

**Contoh 2:** T(n) = T(n/2) + 1
- a = 1, b = 2, d = 0
- b^d = 2^0 = 1
- a = b^d → **O(log n)** (Binary Search!)

**Contoh 3:** T(n) = 4T(n/2) + n
- a = 4, b = 2, d = 1
- b^d = 2^1 = 2
- a > b^d → **O(n^(log_2 4)) = O(n²)**

---

### SOLVED PROBLEM 19 ⭐⭐

**Pertanyaan:** Gunakan Master Theorem untuk menyelesaikan: T(n) = 3T(n/2) + n

**Penyelesaian:**

**Identifikasi parameter:**
- a = 3 (3 subproblem)
- b = 2 (ukuran dibagi 2)
- f(n) = n → d = 1

**Hitung b^d:**
b^d = 2^1 = 2

**Bandingkan a dan b^d:**
a = 3 > 2 = b^d

**Terapkan kasus ketiga Master Theorem:**
T(n) = O(n^(log_b a)) = O(n^(log_2 3)) ≈ O(n^1.585)

**Kesimpulan:** T(n) = **O(n^(log₂3)) ≈ O(n^1.585)**

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Pertanyaan:** Dalam sistem radar pertahanan, algoritma deteksi sasaran memiliki kompleksitas T(n) = 8T(n/2) + n² untuk memproses n titik data. Tentukan kompleksitasnya dan jelaskan implikasinya!

**Penyelesaian:**

**Master Theorem:**
- a = 8, b = 2, d = 2 (karena f(n) = n²)
- b^d = 2² = 4
- a = 8 > 4 = b^d

**Kasus ketiga:**
T(n) = O(n^(log_2 8)) = O(n^3) = **O(n³)**

**Implikasi praktis:**
Algoritma ini tidak scalable untuk data besar. Untuk 1000 titik data, diperlukan ~10⁹ operasi. Untuk sistem pertahanan real-time, perlu dipertimbangkan:

1. **Optimasi algoritma** ke kompleksitas lebih rendah
2. **Hardware khusus** (GPU, FPGA) untuk paralelisasi
3. **Sampling data** untuk mengurangi n
4. **Algoritma aproksimasi** jika hasil exact tidak diperlukan

---

## 10. Pengenalan Amortized Analysis

### 10.1 Konsep Dasar

> **Amortized analysis** menganalisis waktu rata-rata per operasi dalam sekuens operasi, bukan worst case satu operasi.

Ini berguna ketika operasi mahal jarang terjadi.

### 10.2 Contoh: Dynamic Array (Vector)

Pada dynamic array (seperti `std::vector` di C++), operasi `push_back`:
- **Biasanya:** O(1) - insert di akhir
- **Kadang:** O(n) - ketika perlu resize dan copy semua elemen

Meskipun worst case adalah O(n), **amortized cost** adalah O(1) karena resize jarang terjadi.

### 10.3 Intuisi

Bayangkan resize terjadi ketika kapasitas penuh, dan kapasitas digandakan:
- Insert 1: cost 1 (alokasi awal)
- Insert 2: cost 2 (1 + resize & copy 1)
- Insert 3: cost 1
- Insert 4: cost 4 (1 + resize & copy 3)
- Insert 5-8: cost 1 masing-masing
- Insert 9: cost 9 (1 + resize & copy 8)

Total cost untuk n insert ≈ n + n/2 + n/4 + ... = O(n)
Amortized cost per insert = O(n)/n = **O(1)**

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Pertanyaan:** Jelaskan mengapa operasi `push_back` pada `std::vector` C++ memiliki amortized complexity O(1) meskipun kadang memerlukan O(n)!

**Penyelesaian:**

**Mekanisme vector:**
- Vector memiliki `size` (jumlah elemen) dan `capacity` (ruang dialokasi)
- Ketika size == capacity dan push_back dipanggil:
  1. Alokasi memori baru dengan kapasitas 2× lipat
  2. Copy semua elemen ke memori baru: O(n)
  3. Dealokasi memori lama
  4. Insert elemen baru

**Analisis accounting method:**
- Setiap insert "membayar" 3 token
- 1 token untuk insert saat ini
- 2 token disimpan sebagai "kredit"

Ketika resize diperlukan setelah n insert:
- Elemen yang perlu di-copy: n
- Token tersedia dari insert sebelumnya: n × 2 = 2n
- Cost copy: n (cukup ditanggung kredit!)

**Kesimpulan:**
Meskipun satu operasi bisa O(n), total biaya n operasi adalah O(n), sehingga biaya amortized per operasi adalah **O(1)**.

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Pertanyaan:** Sebuah stack diimplementasikan dengan operasi:
- `push(x)`: O(1)
- `pop()`: O(1)
- `multiPop(k)`: pop k elemen, O(min(k, size))

Jika dilakukan n operasi campuran, apa amortized cost per operasi?

**Penyelesaian:**

**Analisis potential method:**

Definisikan potential function Φ = jumlah elemen di stack.
- Φ selalu ≥ 0
- Φ awal = 0, Φ akhir ≥ 0

**Amortized cost:**
- push: actual cost = 1, ΔΦ = +1 → amortized = 1 + 1 = 2
- pop: actual cost = 1, ΔΦ = -1 → amortized = 1 - 1 = 0
- multiPop(k): actual cost = k, ΔΦ = -k → amortized = k - k = 0

**Total amortized cost untuk n operasi:**
- Maximum: 2n (jika semua push)
- Per operasi: **O(1)**

Meskipun satu multiPop bisa memakan O(n) waktu, amortized cost tetap O(1) karena elemen harus di-push dulu sebelum bisa di-pop!

---

## Ringkasan

| Topik | Poin Kunci |
|-------|------------|
| **Analisis Algoritma** | Mengevaluasi efisiensi berdasarkan pertumbuhan waktu terhadap ukuran input |
| **Big-O** | Batas atas (upper bound), f(n) ≤ c·g(n) |
| **Big-Ω** | Batas bawah (lower bound), f(n) ≥ c·g(n) |
| **Big-Θ** | Batas ketat (tight bound), Big-O dan Big-Ω sama |
| **Aturan Sum** | O(f + g) = O(max(f, g)) |
| **Aturan Product** | O(f × g) = O(f) × O(g) |
| **Best/Worst/Avg** | Tergantung konfigurasi input; worst case untuk garansi |
| **Loop Tunggal** | O(n) untuk linear, O(log n) untuk multiplicative |
| **Nested Loop** | Kalikan kompleksitas tiap level |
| **Rekursi** | Buat relasi rekurens, selesaikan dengan substitusi |
| **Master Theorem** | T(n) = aT(n/b) + n^d, bandingkan a dengan b^d |
| **Amortized** | Rata-rata per operasi dalam sekuens |

| Kompleksitas | Nama | Efisiensi |
|--------------|------|-----------|
| O(1) | Konstanta | ⭐⭐⭐⭐⭐ |
| O(log n) | Logaritmik | ⭐⭐⭐⭐ |
| O(n) | Linear | ⭐⭐⭐ |
| O(n log n) | Linearitmik | ⭐⭐⭐ |
| O(n²) | Kuadratik | ⭐⭐ |
| O(2ⁿ) | Eksponensial | ⭐ |
| O(n!) | Faktorial | ☆ |

---

## Supplementary Problems

### Problem S1 ⭐
Tentukan notasi Big-O untuk: f(n) = 100 + 200log(n) + 50n

**Jawaban:** O(n). Suku 50n mendominasi untuk n besar.

### Problem S2 ⭐⭐
Berapa jumlah operasi pada kode berikut?
```cpp
for (int i = n; i > 0; i /= 3) {
    for (int j = 0; j < i; j++) {
        x++;
    }
}
```

**Jawaban:** O(n). Loop dalam total: n + n/3 + n/9 + ... ≈ 1.5n = O(n)

### Problem S3 ⭐⭐
Selesaikan: T(n) = T(n-1) + n, T(1) = 1

**Jawaban:** T(n) = n + (n-1) + ... + 1 = n(n+1)/2 = O(n²)

### Problem S4 ⭐⭐
Gunakan Master Theorem untuk: T(n) = 2T(n/4) + √n

**Jawaban:** a=2, b=4, d=0.5. b^d = 4^0.5 = 2 = a. Jadi O(√n log n).

### Problem S5 ⭐⭐⭐
Algoritma A: O(n²), Algoritma B: O(n log n). Untuk input kecil (n < 100), A lebih cepat karena konstanta lebih kecil. Kapan sebaiknya switch ke B?

**Jawaban:** Ketika T_A(n) > T_B(n). Jika T_A(n) = c₁n² dan T_B(n) = c₂n log n, switch ketika n > c₂/c₁ × log n. Perlu diukur secara empiris untuk c₁ dan c₂ spesifik.

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapters 2-3.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 2.
3. Goodrich, M.T., et al. (2011). *Data Structures and Algorithms in C++* (2nd Ed.). Wiley. Chapter 4.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
