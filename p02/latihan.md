# Latihan Mandiri 02: Analisis Algoritma dan Kompleksitas

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 02  
**Topik:** Analisis Algoritma dan Kompleksitas  
**Waktu:** 150 menit  
**Sifat:** Open Book

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal secara mandiri
2. Untuk soal pilihan ganda, pilih jawaban yang **paling tepat**
3. Untuk soal uraian, tunjukkan **langkah-langkah penyelesaian**
4. Studi kasus dikerjakan dengan analisis mendalam
5. Gunakan notasi Big-O kecuali diminta notasi lain

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

### Soal 1
Manakah yang BUKAN merupakan operasi dasar (primitive operation)?
A. Akses elemen array dengan indeks
B. Operasi perbandingan
C. Sorting seluruh array
D. Assignment variabel
E. Operasi aritmatika dasar

### Soal 2
Jika T(n) = 5n² + 3n + 100, maka notasi Big-O yang paling tepat adalah:
A. O(5n²)
B. O(n² + n)
C. O(n²)
D. O(100)
E. O(n³)

### Soal 3
Pernyataan manakah yang BENAR tentang notasi Big-O?
A. O(n) selalu lebih cepat dari O(n²) untuk semua nilai n
B. O(2n) berbeda dengan O(n)
C. Big-O menunjukkan batas atas pertumbuhan fungsi
D. Konstanta pengali tidak boleh diabaikan
E. O(log n) lebih lambat dari O(n)

### Soal 4
Kompleksitas waktu dari kode berikut adalah:
```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        for (int k = 0; k < n; k++) {
            x++;
        }
    }
}
```
A. O(n)
B. O(n²)
C. O(n³)
D. O(3n)
E. O(n log n)

### Soal 5
Notasi Big-Ω (Omega) menunjukkan:
A. Batas atas pertumbuhan fungsi
B. Batas bawah pertumbuhan fungsi
C. Batas ketat pertumbuhan fungsi
D. Waktu rata-rata algoritma
E. Worst case dari algoritma

### Soal 6
Jika f(n) = O(n²) dan g(n) = O(n), maka f(n) + g(n) adalah:
A. O(n³)
B. O(n² + n)
C. O(n²)
D. O(2n²)
E. O(n)

### Soal 7
Kompleksitas waktu Binary Search adalah:
A. O(1)
B. O(n)
C. O(log n)
D. O(n log n)
E. O(n²)

### Soal 8
Algoritma dengan kompleksitas O(2ⁿ) disebut:
A. Linear
B. Logaritmik
C. Polinomial
D. Eksponensial
E. Faktorial

### Soal 9
Manakah urutan kompleksitas dari yang paling efisien ke paling tidak efisien?
A. O(n) < O(log n) < O(n²) < O(1)
B. O(1) < O(log n) < O(n) < O(n log n) < O(n²)
C. O(log n) < O(1) < O(n) < O(n²)
D. O(n²) < O(n log n) < O(n) < O(log n)
E. O(1) < O(n) < O(log n) < O(n²)

### Soal 10
Kompleksitas waktu dari kode berikut adalah:
```cpp
for (int i = 1; i < n; i *= 2) {
    cout << i << endl;
}
```
A. O(n)
B. O(n²)
C. O(log n)
D. O(n log n)
E. O(2ⁿ)

### Soal 11
Untuk algoritma Linear Search pada array tidak terurut, best case terjadi ketika:
A. Elemen dicari ada di akhir array
B. Elemen dicari tidak ada di array
C. Elemen dicari ada di awal array
D. Array berukuran sangat besar
E. Array sudah terurut

### Soal 12
Jika T(n) = T(n-1) + c dengan T(1) = c, maka kompleksitas waktu adalah:
A. O(1)
B. O(log n)
C. O(n)
D. O(n²)
E. O(2ⁿ)

### Soal 13
Kompleksitas waktu dari kode berikut adalah:
```cpp
for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        x++;
    }
}
```
A. O(n)
B. O(n log n)
C. O(n²)
D. O(n³)
E. O(2ⁿ)

### Soal 14
Menurut Master Theorem, jika T(n) = 2T(n/2) + n, maka kompleksitasnya adalah:
A. O(n)
B. O(n log n)
C. O(n²)
D. O(log n)
E. O(2ⁿ)

### Soal 15
Mana pernyataan yang SALAH tentang analisis worst case?
A. Memberikan garansi batas atas waktu eksekusi
B. Selalu lebih besar atau sama dengan average case
C. Berguna untuk aplikasi real-time
D. Selalu terjadi dalam setiap eksekusi
E. Penting untuk sistem kritis seperti pertahanan

### Soal 16
Jika suatu algoritma memiliki kompleksitas O(n log n), berapa kali operasi dilakukan untuk n = 1024?
A. 1024
B. 10240
C. 1048576
D. 10
E. 100

### Soal 17
Amortized analysis berguna untuk:
A. Menghitung waktu eksekusi satu operasi
B. Menentukan worst case tunggal
C. Menganalisis rata-rata per operasi dalam sekuens
D. Membandingkan dua algoritma berbeda
E. Menghitung space complexity

### Soal 18
Kompleksitas waktu dari implementasi Fibonacci rekursif naif adalah:
A. O(n)
B. O(log n)
C. O(n²)
D. O(2ⁿ)
E. O(n!)

### Soal 19
Jika f(n) = Θ(n²), maka pernyataan mana yang BENAR?
A. f(n) = O(n²) saja
B. f(n) = Ω(n²) saja
C. f(n) = O(n²) dan f(n) = Ω(n²)
D. f(n) bisa O(n) atau O(n²)
E. f(n) selalu O(n³)

### Soal 20
Kompleksitas waktu dari kode berikut adalah:
```cpp
int sum = 0;
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= n; j += i) {
        sum++;
    }
}
```
A. O(n)
B. O(n log n)
C. O(n²)
D. O(n² log n)
E. O(n³)

---

## Bagian B: Soal Uraian (15 Soal)

### Soal 1 (Mudah)
Jelaskan perbedaan antara analisis algoritma secara empiris dan teoritis! Berikan contoh kapan masing-masing pendekatan lebih tepat digunakan.

### Soal 2 (Mudah)
Hitung jumlah operasi dasar pada kode berikut:
```cpp
int total = 0;
for (int i = 0; i < n; i++) {
    total = total + arr[i] * 2;
}
return total;
```

### Soal 3 (Mudah)
Buktikan secara formal bahwa 4n³ + 2n² + 5 = O(n³)! Tentukan nilai c dan n₀ yang memenuhi definisi Big-O.

### Soal 4 (Mudah)
Sederhanakan notasi Big-O berikut dan jelaskan langkah-langkahnya:
a) O(5n² + 3n log n + 1000)
b) O(n/2 + 100)
c) O(2ⁿ + n³)

### Soal 5 (Sedang)
Tentukan kompleksitas waktu dari kode berikut dan jelaskan analisis Anda:
```cpp
void function1(int n) {
    for (int i = 0; i < n; i++) {
        cout << i << endl;
    }
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << i + j << endl;
        }
    }
    for (int i = 0; i < 100; i++) {
        cout << "Hello" << endl;
    }
}
```

### Soal 6 (Sedang)
Analisis best case, worst case, dan average case dari fungsi berikut:
```cpp
int findElement(int arr[], int n, int key) {
    for (int i = 0; i < n; i++) {
        if (arr[i] == key) {
            return i;
        }
    }
    return -1;
}
```

### Soal 7 (Sedang)
Tentukan kompleksitas waktu dari nested loop berikut:
```cpp
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= i * i; j++) {
        cout << j << endl;
    }
}
```

### Soal 8 (Sedang)
Selesaikan relasi rekurens berikut menggunakan metode substitusi:
T(n) = T(n-1) + n, dengan T(1) = 1

### Soal 9 (Sedang)
Algoritma A berjalan dalam O(n²) dan Algoritma B dalam O(n log n). 
a) Untuk n berapa A dan B memiliki waktu yang sama jika T_A(n) = 0.1n² dan T_B(n) = 10n log₂ n?
b) Untuk n = 10.000, algoritma mana yang lebih cepat dan berapa kali lebih cepat?

### Soal 10 (Sedang)
Tentukan kompleksitas waktu dari fungsi rekursif berikut:
```cpp
int power(int x, int n) {
    if (n == 0) return 1;
    if (n % 2 == 0) {
        int half = power(x, n/2);
        return half * half;
    } else {
        return x * power(x, n-1);
    }
}
```

### Soal 11 (Sulit)
Gunakan Master Theorem untuk menentukan kompleksitas dari relasi rekurens berikut:
a) T(n) = 4T(n/2) + n
b) T(n) = 2T(n/4) + √n
c) T(n) = T(n/2) + n²

### Soal 12 (Sulit)
Buktikan bahwa n! tumbuh lebih cepat dari 2ⁿ untuk n cukup besar. Gunakan bukti informal dengan membandingkan suku-sukunya.

### Soal 13 (Sulit)
Perhatikan kode berikut:
```cpp
void mystery(int n) {
    if (n <= 1) return;
    
    for (int i = 0; i < n; i++) {
        cout << i << endl;
    }
    
    mystery(n / 2);
    mystery(n / 2);
}
```
a) Tulis relasi rekurens untuk T(n)
b) Selesaikan menggunakan metode pohon rekursi
c) Tentukan kompleksitas Big-O

### Soal 14 (Sulit)
Jelaskan konsep amortized analysis dan berikan contoh mengapa operasi push_back pada std::vector C++ memiliki amortized complexity O(1) meskipun kadang memerlukan O(n)!

### Soal 15 (Sulit)
Sebuah algoritma pengurutan memiliki kompleksitas:
- Best case: O(n)
- Average case: O(n log n)  
- Worst case: O(n²)

a) Algoritma sorting apa yang memiliki karakteristik ini?
b) Jelaskan kondisi yang menyebabkan masing-masing case
c) Kapan sebaiknya algoritma ini digunakan dan kapan sebaiknya dihindari?

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Pelacakan Sasaran Radar

**Latar Belakang:**
Anda adalah pengembang sistem radar pertahanan yang harus memproses data dari n titik deteksi. Terdapat tiga algoritma yang diusulkan:

- **Algoritma ALPHA**: Kompleksitas O(n³), dapat mendeteksi semua jenis sasaran
- **Algoritma BETA**: Kompleksitas O(n²), dapat mendeteksi 90% jenis sasaran
- **Algoritma GAMMA**: Kompleksitas O(n log n), dapat mendeteksi 80% jenis sasaran

**Data Operasional:**
- Jumlah titik deteksi normal: 1.000 titik
- Jumlah titik deteksi saat siaga: 10.000 titik
- Jumlah titik deteksi saat darurat: 100.000 titik
- Waktu respons maksimum yang diizinkan: 100 milidetik
- Kecepatan pemrosesan: 10⁹ operasi per detik

**Tugas:**

1. **Analisis Waktu Eksekusi (25 poin)**
   - Hitung waktu eksekusi masing-masing algoritma untuk setiap kondisi operasional (normal, siaga, darurat)
   - Sajikan dalam bentuk tabel

2. **Evaluasi Kelayakan (20 poin)**
   - Tentukan algoritma mana yang layak digunakan untuk masing-masing kondisi berdasarkan batas waktu 100 ms
   - Jelaskan trade-off antara akurasi dan kecepatan

3. **Rekomendasi Sistem (15 poin)**
   - Rancang strategi pemilihan algoritma adaptif berdasarkan kondisi operasional
   - Pertimbangkan aspek keamanan dan keandalan sistem pertahanan

---

### Studi Kasus 2: Optimasi Jaringan Komunikasi Militer

**Latar Belakang:**
Batalyon komunikasi perlu mengoptimalkan rute pesan rahasia melalui n node jaringan. Setiap node dapat terhubung ke node lain dengan tingkat keamanan berbeda.

**Skenario Algoritma:**

**Algoritma SECURE-A:**
```
function findSecureRoute(nodes[], n):
    for each possible route (n! routes):
        calculate security score
    return route with max score
```

**Algoritma SECURE-B:**
```
function findSecureRoute(nodes[], n):
    build security graph  // O(n²)
    for each node:
        for each neighbor:
            update optimal path  // O(n)
    return optimal route
```

**Algoritma SECURE-C:**
```
function findSecureRoute(nodes[], n, source, dest):
    if source == dest: return
    divide nodes into two groups  // O(n)
    recursively find route in each group  // 2T(n/2)
    merge results  // O(n)
```

**Data Jaringan:**
- Jaringan batalyon: 20 node
- Jaringan divisi: 100 node
- Jaringan teater operasi: 500 node

**Tugas:**

1. **Identifikasi Kompleksitas (20 poin)**
   - Tentukan kompleksitas waktu masing-masing algoritma
   - Untuk SECURE-C, tulis relasi rekurens dan selesaikan

2. **Analisis Skalabilitas (20 poin)**
   - Hitung estimasi waktu untuk setiap algoritma pada ketiga skala jaringan
   - Asumsikan 10⁶ operasi per detik (jaringan secure lebih lambat)
   - Tentukan algoritma mana yang praktis untuk setiap skala

3. **Keamanan vs Efisiensi (20 poin)**
   - SECURE-A memberikan hasil optimal 100%
   - SECURE-B memberikan hasil optimal 95% dalam sebagian besar kasus
   - SECURE-C memberikan hasil optimal 85% dengan asumsi pembagian merata
   
   Analisis trade-off dan berikan rekomendasi untuk:
   - Pengiriman pesan rutin
   - Pengiriman pesan taktis mendesak
   - Pengiriman pesan strategis tingkat tinggi

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | C | Sorting adalah operasi kompleks, bukan primitive |
| 2 | C | Suku dominan n², konstanta diabaikan |
| 3 | C | Definisi Big-O: batas atas pertumbuhan |
| 4 | C | 3 loop bersarang = O(n × n × n) = O(n³) |
| 5 | B | Big-Ω adalah lower bound |
| 6 | C | Max(n², n) = n², aturan sum |
| 7 | C | Binary search membagi setengah setiap langkah |
| 8 | D | 2ⁿ adalah eksponensial |
| 9 | B | Urutan benar dari cepat ke lambat |
| 10 | C | i dikali 2 setiap iterasi = O(log n) |
| 11 | C | Best case = ditemukan di iterasi pertama |
| 12 | C | Linear rekurens = O(n) |
| 13 | C | 0+1+2+...+(n-1) = n(n-1)/2 = O(n²) |
| 14 | B | Master Theorem: a=b^d → O(n log n) |
| 15 | D | Worst case tidak selalu terjadi setiap eksekusi |
| 16 | B | 1024 × log₂(1024) = 1024 × 10 = 10240 |
| 17 | C | Definisi amortized analysis |
| 18 | D | T(n) = T(n-1) + T(n-2) ≈ O(2ⁿ) |
| 19 | C | Θ = O dan Ω sekaligus |
| 20 | B | Deret harmonik × n = O(n log n) |

---

### Bagian B: Uraian

#### Jawaban Soal 1
**Analisis Empiris:**
- Mengukur waktu eksekusi aktual dengan data nyata
- Tergantung hardware, compiler, dan kondisi sistem
- Cocok untuk: benchmarking sistem spesifik, tuning parameter

**Analisis Teoritis:**
- Menghitung operasi dasar sebagai fungsi dari n
- Independen dari hardware
- Cocok untuk: membandingkan algoritma secara umum, prediksi skalabilitas

---

#### Jawaban Soal 2
| Operasi | Jumlah |
|---------|--------|
| int total = 0 | 1 |
| int i = 0 | 1 |
| i < n | n+1 |
| i++ | n |
| arr[i] | n |
| * 2 | n |
| total + ... | n |
| total = ... | n |
| return | 1 |

**Total: 6n + 4 operasi = O(n)**

---

#### Jawaban Soal 3
Perlu menunjukkan: 4n³ + 2n² + 5 ≤ c·n³ untuk n ≥ n₀

Untuk n ≥ 1:
- 2n² ≤ 2n³
- 5 ≤ 5n³

Jadi: 4n³ + 2n² + 5 ≤ 4n³ + 2n³ + 5n³ = 11n³

**Dengan c = 11 dan n₀ = 1, terbukti O(n³)** ∎

---

#### Jawaban Soal 4
a) **O(5n² + 3n log n + 1000)**
   - Suku dominan: 5n²
   - Hapus suku kecil: O(5n²)
   - Hapus konstanta: **O(n²)**

b) **O(n/2 + 100)**
   - Suku dominan: n/2
   - n/2 = (1/2)n = O(n)
   - Hapus konstanta 100
   - **O(n)**

c) **O(2ⁿ + n³)**
   - 2ⁿ tumbuh lebih cepat dari n³ untuk n besar
   - **O(2ⁿ)**

---

#### Jawaban Soal 5
- Loop 1: O(n)
- Loop 2: O(n²)
- Loop 3: O(100) = O(1)

**Total: O(n) + O(n²) + O(1) = O(n²)**

---

#### Jawaban Soal 6
- **Best case:** key di arr[0], O(1)
- **Worst case:** key tidak ada atau di arr[n-1], O(n)
- **Average case:** key di posisi acak, rata-rata n/2 perbandingan, O(n)

---

#### Jawaban Soal 7
Total iterasi loop dalam:
- i=1: 1
- i=2: 4
- i=3: 9
- ...
- i=n: n²

Total = 1 + 4 + 9 + ... + n² = n(n+1)(2n+1)/6 = **O(n³)**

---

#### Jawaban Soal 8
T(n) = T(n-1) + n
T(n) = T(n-2) + (n-1) + n
T(n) = T(n-3) + (n-2) + (n-1) + n
...
T(n) = T(1) + 2 + 3 + ... + n
T(n) = 1 + (n(n+1)/2 - 1)
T(n) = n(n+1)/2 = **O(n²)**

---

#### Jawaban Soal 9
a) 0.1n² = 10n log₂n
   0.01n = log₂n
   Dengan trial: n ≈ 170-180

b) Untuk n = 10.000:
   - T_A = 0.1 × (10⁴)² = 10⁷
   - T_B = 10 × 10⁴ × log₂(10⁴) ≈ 10 × 10⁴ × 13.3 ≈ 1.33 × 10⁶
   
   B lebih cepat ≈ **7.5 kali**

---

#### Jawaban Soal 10
- Jika n genap: T(n) = T(n/2) + O(1) → O(log n)
- Jika n ganjil: T(n) = T(n-1) + O(1)

Worst case (semua ganjil): O(n)
Average case dengan campuran: **O(log n)**

(Ini adalah algoritma exponentiation by squaring)

---

#### Jawaban Soal 11
a) T(n) = 4T(n/2) + n
   - a=4, b=2, d=1, b^d=2
   - a > b^d → **O(n^(log₂4)) = O(n²)**

b) T(n) = 2T(n/4) + √n
   - a=2, b=4, d=0.5, b^d = 4^0.5 = 2
   - a = b^d → **O(√n log n)**

c) T(n) = T(n/2) + n²
   - a=1, b=2, d=2, b^d = 4
   - a < b^d → **O(n²)**

---

#### Jawaban Soal 12
n! = n × (n-1) × (n-2) × ... × 2 × 1
2ⁿ = 2 × 2 × 2 × ... × 2 (n kali)

Untuk n > 4:
n! / 2ⁿ = (n/2) × ((n-1)/2) × ((n-2)/2) × ... × (3/2) × (2/2) × (1/2)

Mulai dari faktor ke-3, setiap faktor > 1 (untuk n > 4), sehingga produk terus membesar.
Oleh karena itu, **n! > 2ⁿ untuk n cukup besar** (n ≥ 4). ∎

---

#### Jawaban Soal 13
a) T(n) = 2T(n/2) + n, T(1) = c

b) Pohon rekursi:
   - Level 0: n kerja
   - Level 1: 2 × (n/2) = n kerja
   - Level 2: 4 × (n/4) = n kerja
   - ...
   - Level log n: n node × O(1) = n kerja
   
   Total: n × (log n + 1) level

c) **O(n log n)**

---

#### Jawaban Soal 14
- Vector mengalokasikan kapasitas lebih besar dari size
- Saat push_back dan capacity penuh, alokasi baru 2× lipat
- Copy semua elemen: O(n)
- Namun, resize hanya terjadi setelah n operasi
- Total cost untuk n operasi ≈ n + n/2 + n/4 + ... ≈ 2n
- Amortized per operasi: 2n/n = O(1)

---

#### Jawaban Soal 15
a) **Quick Sort**

b) 
   - Best: Pivot selalu membagi array sama rata
   - Average: Pivot cukup baik secara statistik
   - Worst: Pivot selalu elemen terkecil/terbesar (array terurut + pivot = elemen pertama)

c)
   - **Gunakan:** Data acak, perlu in-place sorting, memori terbatas
   - **Hindari:** Data hampir terurut, membutuhkan stabilitas, sistem kritis yang butuh garansi performa

---

### Bagian C: Studi Kasus

#### Studi Kasus 1

**1. Tabel Waktu Eksekusi:**

| Kondisi | n | ALPHA (n³) | BETA (n²) | GAMMA (n log n) |
|---------|---|------------|-----------|-----------------|
| Normal | 1.000 | 1 detik | 1 ms | 0.01 ms |
| Siaga | 10.000 | 1000 detik | 100 ms | 0.13 ms |
| Darurat | 100.000 | 10⁶ detik | 10 detik | 1.66 ms |

**2. Evaluasi Kelayakan (batas 100 ms):**

| Kondisi | ALPHA | BETA | GAMMA |
|---------|-------|------|-------|
| Normal | ❌ | ✅ | ✅ |
| Siaga | ❌ | ⚠️ (tepat) | ✅ |
| Darurat | ❌ | ❌ | ✅ |

Trade-off: ALPHA paling akurat tapi terlalu lambat. GAMMA tercepat tapi akurasi 80%.

**3. Rekomendasi Strategi Adaptif:**
- **Normal:** Gunakan BETA (90% akurasi, waktu cukup)
- **Siaga:** Mulai dengan GAMMA, validasi dengan BETA jika waktu tersisa
- **Darurat:** GAMMA wajib, tidak ada alternatif praktis

Pertimbangan keamanan: Siapkan fallback ke GAMMA jika sistem overload.

---

#### Studi Kasus 2

**1. Kompleksitas:**
- SECURE-A: **O(n!)** (brute force semua permutasi)
- SECURE-B: **O(n³)** (n × n × n dari 3 loop)
- SECURE-C: T(n) = 2T(n/2) + n → **O(n log n)**

**2. Estimasi Waktu (10⁶ ops/detik):**

| Jaringan | n | SECURE-A | SECURE-B | SECURE-C |
|----------|---|----------|----------|----------|
| Batalyon | 20 | 2.4×10¹⁸ detik | 8 ms | 0.086 ms |
| Divisi | 100 | ∞ | 1 detik | 0.66 ms |
| Teater | 500 | ∞ | 125 detik | 4.5 ms |

Praktis:
- Batalyon: B, C
- Divisi: C (B marginal)
- Teater: C saja

**3. Rekomendasi:**
- **Pesan rutin:** SECURE-C (cepat, akurasi 85% cukup)
- **Pesan taktis mendesak:** SECURE-C (kecepatan prioritas)
- **Pesan strategis:** SECURE-B untuk jaringan kecil (batalyon), SECURE-C dengan verifikasi manual untuk jaringan besar

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
