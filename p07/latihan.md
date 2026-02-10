# Latihan Mandiri 07: Rekursi Lanjut dan Divide-and-Conquer

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 07  
**Topik:** Rekursi Lanjut dan Divide-and-Conquer  
**Waktu:** 150 menit  
**Sifat:** Open Book

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal secara mandiri
2. Untuk soal pilihan ganda, pilih **satu jawaban yang paling tepat**
3. Untuk soal uraian, tuliskan jawaban dengan **lengkap dan sistematis**
4. Studi kasus dikerjakan dengan **implementasi kode C++**
5. Kunci jawaban tersedia di bagian akhir dokumen

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

### Soal 1
Dalam fungsi rekursif, komponen yang berfungsi sebagai kondisi penghenti rekursi disebut...

A. Recursive case  
B. Base case  
C. Terminal case  
D. Stop condition  
E. Exit point

---

### Soal 2
Perhatikan fungsi berikut:
```cpp
int mystery(int n) {
    if (n == 0) return 0;
    return n + mystery(n - 1);
}
```
Apa hasil dari `mystery(5)`?

A. 5  
B. 10  
C. 15  
D. 20  
E. 25

---

### Soal 3
Recurrence relation untuk algoritma Binary Search adalah...

A. T(n) = T(n-1) + O(1)  
B. T(n) = T(n/2) + O(1)  
C. T(n) = 2T(n/2) + O(1)  
D. T(n) = 2T(n/2) + O(n)  
E. T(n) = T(n-1) + O(n)

---

### Soal 4
Berdasarkan Master Theorem, untuk T(n) = 2T(n/2) + n, kompleksitas waktunya adalah...

A. O(n)  
B. O(n²)  
C. O(log n)  
D. O(n log n)  
E. O(2ⁿ)

---

### Soal 5
Berapa jumlah langkah minimum yang diperlukan untuk menyelesaikan Tower of Hanoi dengan 8 disk?

A. 127  
B. 255  
C. 511  
D. 1023  
E. 2047

---

### Soal 6
Apa yang dimaksud dengan tail recursion?

A. Rekursi yang menggunakan stack  
B. Rekursi yang memanggil dirinya sendiri dua kali  
C. Rekursi di mana pemanggilan rekursif adalah operasi terakhir  
D. Rekursi yang tidak memiliki base case  
E. Rekursi yang berjalan dari belakang

---

### Soal 7
Perhatikan fungsi Fibonacci naive:
```cpp
int fib(int n) {
    if (n <= 1) return n;
    return fib(n-1) + fib(n-2);
}
```
Kompleksitas waktu fungsi ini adalah...

A. O(n)  
B. O(n²)  
C. O(log n)  
D. O(n log n)  
E. O(2ⁿ)

---

### Soal 8
Teknik yang menyimpan hasil komputasi untuk menghindari perhitungan berulang disebut...

A. Caching  
B. Memoization  
C. Buffering  
D. Optimization  
E. Tabulation

---

### Soal 9
Dalam paradigma Divide-and-Conquer, langkah untuk memecah masalah menjadi sub-masalah disebut...

A. Conquer  
B. Combine  
C. Divide  
D. Split  
E. Partition

---

### Soal 10
Untuk Master Theorem dengan T(n) = aT(n/b) + f(n), jika f(n) = O(n^(log_b(a) - ε)) untuk ε > 0, maka kompleksitasnya adalah...

A. Θ(f(n))  
B. Θ(n^(log_b(a)))  
C. Θ(n^(log_b(a)) · log n)  
D. Θ(n · log n)  
E. Θ(n²)

---

### Soal 11
Perhatikan recurrence relation T(n) = 4T(n/2) + n. Berapa nilai log₂(4)?

A. 1  
B. 2  
C. 3  
D. 4  
E. 0.5

---

### Soal 12
Fungsi mana yang merupakan contoh tail recursion?

A.
```cpp
int f(int n) { return n * f(n-1); }
```

B.
```cpp
int f(int n, int acc) { 
    if (n==0) return acc; 
    return f(n-1, n*acc); 
}
```

C.
```cpp
int f(int n) { return f(n-1) + f(n-2); }
```

D.
```cpp
int f(int n) { return n + f(n-1); }
```

E.
```cpp
int f(int n) { return f(n/2) * 2; }
```

---

### Soal 13
Dalam Binary Search, jika array memiliki 1024 elemen, berapa maksimum perbandingan yang diperlukan untuk menemukan elemen?

A. 8  
B. 9  
C. 10  
D. 11  
E. 12

---

### Soal 14
Apa keuntungan utama memoization pada Fibonacci?

A. Mengurangi kompleksitas ruang  
B. Menghilangkan overlapping subproblems  
C. Membuat kode lebih sederhana  
D. Meningkatkan keamanan  
E. Mengurangi penggunaan stack

---

### Soal 15
Perhatikan fungsi berikut:
```cpp
int power(int a, int n) {
    if (n == 0) return 1;
    if (n % 2 == 0) {
        int half = power(a, n/2);
        return half * half;
    }
    return a * power(a, n-1);
}
```
Kompleksitas waktu fungsi ini adalah...

A. O(n)  
B. O(n²)  
C. O(log n)  
D. O(n log n)  
E. O(2ⁿ)

---

### Soal 16
Untuk T(n) = 9T(n/3) + n, menggunakan Master Theorem, kompleksitasnya adalah...

A. Θ(n)  
B. Θ(n²)  
C. Θ(n log n)  
D. Θ(n² log n)  
E. Θ(n³)

---

### Soal 17
Apa yang terjadi jika fungsi rekursif tidak memiliki base case yang valid?

A. Fungsi berjalan lebih cepat  
B. Fungsi mengembalikan 0  
C. Stack overflow  
D. Compile error  
E. Fungsi berhenti otomatis

---

### Soal 18
Dalam konversi rekursi ke iterasi, struktur data apa yang digunakan untuk mensimulasikan call stack?

A. Queue  
B. Linked List  
C. Stack  
D. Array  
E. Tree

---

### Soal 19
Algoritma mana yang BUKAN merupakan contoh Divide-and-Conquer?

A. Merge Sort  
B. Quick Sort  
C. Binary Search  
D. Bubble Sort  
E. Tower of Hanoi

---

### Soal 20
Jika T(n) = 2T(n/4) + √n, menggunakan Master Theorem (log₄2 = 0.5, n^0.5 = √n), kompleksitasnya adalah...

A. Θ(√n)  
B. Θ(√n · log n)  
C. Θ(n)  
D. Θ(n log n)  
E. Θ(n²)

---

## Bagian B: Soal Uraian (15 Soal)

### Soal 1 (Mudah)
Jelaskan perbedaan antara **base case** dan **recursive case** dalam fungsi rekursif. Berikan contoh masing-masing dari fungsi faktorial.

---

### Soal 2 (Mudah)
Lakukan tracing untuk fungsi berikut dengan input `sumDigits(1234)`:
```cpp
int sumDigits(int n) {
    if (n < 10) return n;
    return (n % 10) + sumDigits(n / 10);
}
```
Tunjukkan setiap langkah pemanggilan rekursif dan nilai yang dikembalikan.

---

### Soal 3 (Mudah)
Tuliskan recurrence relation untuk masing-masing algoritma berikut:
1. Linear Search
2. Faktorial
3. Merge Sort

---

### Soal 4 (Sedang)
Gunakan **Master Theorem** untuk menentukan kompleksitas dari:
```
T(n) = 3T(n/3) + n
```
Tunjukkan langkah-langkah penyelesaiannya.

---

### Soal 5 (Sedang)
Konversikan fungsi faktorial berikut menjadi **tail recursive**:
```cpp
int faktorial(int n) {
    if (n <= 1) return 1;
    return n * faktorial(n - 1);
}
```
Jelaskan mengapa versi tail recursive lebih efisien dalam penggunaan memori.

---

### Soal 6 (Sedang)
Jelaskan mengapa **memoization** efektif untuk optimasi Fibonacci tetapi tidak terlalu berguna untuk optimasi faktorial. Gunakan konsep **overlapping subproblems** dalam penjelasan Anda.

---

### Soal 7 (Sedang)
Gambarkan **pohon rekursi** untuk T(n) = 2T(n/2) + n dengan n = 8. Hitung total cost di setiap level dan tentukan kompleksitas akhirnya.

---

### Soal 8 (Sedang)
Implementasikan fungsi **Binary Search rekursif** yang mengembalikan indeks elemen jika ditemukan, atau -1 jika tidak ditemukan. Tuliskan juga analisis kompleksitas waktu dan ruangnya.

---

### Soal 9 (Sedang)
Dalam Tower of Hanoi:
1. Jelaskan strategi Divide-and-Conquer yang digunakan
2. Buktikan bahwa jumlah langkah minimum adalah 2ⁿ - 1
3. Jika setiap pemindahan membutuhkan 2 detik, berapa waktu yang dibutuhkan untuk 10 disk?

---

### Soal 10 (Sulit)
Implementasikan fungsi Fibonacci dengan **memoization** menggunakan `unordered_map`. Bandingkan waktu eksekusi untuk fib(40) antara versi naive dan memoization.

---

### Soal 11 (Sulit)
Konversikan fungsi **Tower of Hanoi rekursif** menjadi **iteratif dengan stack eksplisit**. Jelaskan struktur data yang Anda gunakan untuk menyimpan state.

---

### Soal 12 (Sulit)
Diberikan array terurut dengan elemen yang mungkin duplikat. Implementasikan fungsi untuk mencari:
1. **Lower bound**: indeks pertama di mana elemen >= target
2. **Upper bound**: indeks pertama di mana elemen > target

Gunakan pendekatan Binary Search dengan kompleksitas O(log n).

---

### Soal 13 (Sulit)
Analisis kompleksitas dari recurrence relation berikut menggunakan metode **substitusi**:
```
T(n) = T(n-1) + n
T(1) = 1
```
Buktikan bahwa T(n) = O(n²).

---

### Soal 14 (Sulit)
Implementasikan fungsi untuk menghitung **pangkat** a^n dengan kompleksitas O(log n) menggunakan teknik **divide-and-conquer**. Tangani juga kasus n negatif.

---

### Soal 15 (Sulit)
Jelaskan bagaimana **Tail Call Optimization (TCO)** bekerja pada level compiler. Mengapa tidak semua compiler C++ mengimplementasikan TCO secara default?

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Pencarian Log Keamanan

**Latar Belakang:**
Pusat Operasi Keamanan Siber (SOC) menyimpan log aktivitas jaringan dalam array terurut berdasarkan timestamp. Setiap log memiliki struktur:

```cpp
struct LogEntry {
    long long timestamp;    // Unix timestamp (detik)
    string severity;        // "LOW", "MEDIUM", "HIGH", "CRITICAL"
    string source_ip;       // IP address sumber
    string event_type;      // Jenis event
};
```

**Data Contoh:**
Array berisi 1.000.000 log entries dari 24 jam terakhir.

**Tugas:**

1. **Implementasikan fungsi pencarian range waktu** menggunakan Binary Search untuk menemukan semua log dalam rentang waktu tertentu (misalnya: semua log antara 14:00 - 15:00).

2. **Implementasikan fungsi pencarian log CRITICAL** yang menggunakan teknik divide-and-conquer untuk menghitung jumlah log dengan severity "CRITICAL" dalam range waktu tertentu.

3. **Analisis kompleksitas** dari kedua fungsi yang Anda implementasikan.

4. **Optimasi dengan memoization**: Jika query yang sama sering diulang, bagaimana Anda akan menggunakan memoization untuk mempercepat pencarian?

**Template Kode:**
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
using namespace std;

struct LogEntry {
    long long timestamp;
    string severity;
    string source_ip;
    string event_type;
};

// TODO: Implementasikan fungsi-fungsi berikut

// 1. Cari index pertama dengan timestamp >= target
int lowerBoundTimestamp(vector<LogEntry>& logs, long long target) {
    // Implementasi Anda
}

// 2. Cari index pertama dengan timestamp > target
int upperBoundTimestamp(vector<LogEntry>& logs, long long target) {
    // Implementasi Anda
}

// 3. Hitung jumlah log CRITICAL dalam range waktu
int countCriticalInRange(vector<LogEntry>& logs, long long start, long long end) {
    // Implementasi Anda
}

// 4. Versi dengan memoization
unordered_map<string, int> queryCache;
int countCriticalMemoized(vector<LogEntry>& logs, long long start, long long end) {
    // Implementasi Anda
}

int main() {
    // Test dengan data contoh
    vector<LogEntry> logs = {
        {1704067200, "LOW", "192.168.1.10", "LOGIN"},
        {1704070800, "MEDIUM", "192.168.1.15", "FILE_ACCESS"},
        {1704074400, "CRITICAL", "10.0.0.5", "INTRUSION_ATTEMPT"},
        {1704078000, "HIGH", "192.168.1.20", "MALWARE_DETECTED"},
        {1704081600, "CRITICAL", "10.0.0.8", "DATA_EXFILTRATION"},
        {1704085200, "LOW", "192.168.1.25", "LOGOUT"},
        {1704088800, "CRITICAL", "172.16.0.100", "DDOS_ATTACK"}
    };
    
    // Test pencarian range
    long long startTime = 1704070800;  // 14:00
    long long endTime = 1704085200;    // 18:00
    
    cout << "Log dalam range: " << endl;
    int startIdx = lowerBoundTimestamp(logs, startTime);
    int endIdx = upperBoundTimestamp(logs, endTime);
    
    for (int i = startIdx; i < endIdx; i++) {
        cout << "  " << logs[i].timestamp << " - " 
             << logs[i].severity << " - " 
             << logs[i].event_type << endl;
    }
    
    cout << "\nJumlah CRITICAL: " << countCriticalInRange(logs, startTime, endTime) << endl;
    
    return 0;
}
```

---

### Studi Kasus 2: Optimasi Jalur Patroli dengan Memoization

**Latar Belakang:**
Sistem perencanaan patroli perbatasan perlu menghitung jumlah rute berbeda dari pos A (pojok kiri atas) ke pos B (pojok kanan bawah) pada grid m × n. Setiap langkah hanya boleh bergerak ke **kanan** atau ke **bawah**.

**Tantangan Tambahan:**
Beberapa sel pada grid adalah **zona terlarang** (obstacle) yang tidak bisa dilewati.

**Tugas:**

1. **Implementasikan fungsi rekursif** untuk menghitung jumlah rute unik pada grid m × n tanpa obstacle.

2. **Optimasi dengan memoization** untuk menghindari perhitungan berulang.

3. **Modifikasi fungsi** untuk menangani grid dengan obstacle. Obstacle ditandai dengan nilai 1 pada matriks, sedangkan sel yang bisa dilewati ditandai dengan 0.

4. **Analisis kompleksitas** sebelum dan sesudah memoization.

5. **Bandingkan performa** untuk grid 15×15 antara versi naive dan memoization.

**Template Kode:**
```cpp
#include <iostream>
#include <vector>
#include <map>
#include <chrono>
using namespace std;

// 1. Versi rekursif naive (tanpa obstacle)
long long countPathsNaive(int m, int n) {
    // Base case
    if (m == 1 || n == 1) return 1;
    // Recursive case
    return countPathsNaive(m - 1, n) + countPathsNaive(m, n - 1);
}

// 2. Versi dengan memoization
map<pair<int,int>, long long> memo;

long long countPathsMemo(int m, int n) {
    // TODO: Implementasikan
}

// 3. Versi dengan obstacle
long long countPathsWithObstacles(vector<vector<int>>& grid, int row, int col,
                                   map<pair<int,int>, long long>& memo) {
    // TODO: Implementasikan
}

// Fungsi helper untuk mengukur waktu eksekusi
template<typename Func>
double measureTime(Func f) {
    auto start = chrono::high_resolution_clock::now();
    f();
    auto end = chrono::high_resolution_clock::now();
    chrono::duration<double, milli> duration = end - start;
    return duration.count();
}

int main() {
    // Test 1: Grid kecil
    cout << "=== Grid 5x5 ===" << endl;
    cout << "Jumlah rute: " << countPathsMemo(5, 5) << endl;
    
    // Test 2: Perbandingan performa
    cout << "\n=== Perbandingan Performa (Grid 15x15) ===" << endl;
    
    memo.clear();
    double timeMemo = measureTime([]() {
        countPathsMemo(15, 15);
    });
    cout << "Memoization: " << timeMemo << " ms" << endl;
    
    // Warning: naive version sangat lambat untuk grid besar!
    // double timeNaive = measureTime([]() {
    //     countPathsNaive(15, 15);
    // });
    // cout << "Naive: " << timeNaive << " ms" << endl;
    
    // Test 3: Grid dengan obstacle
    cout << "\n=== Grid dengan Obstacle ===" << endl;
    vector<vector<int>> gridWithObstacle = {
        {0, 0, 0, 0},
        {0, 1, 0, 0},  // 1 = obstacle
        {0, 0, 1, 0},
        {0, 0, 0, 0}
    };
    
    map<pair<int,int>, long long> obstacleMemo;
    int rows = gridWithObstacle.size();
    int cols = gridWithObstacle[0].size();
    
    cout << "Jumlah rute (dengan obstacle): " 
         << countPathsWithObstacles(gridWithObstacle, 0, 0, obstacleMemo) 
         << endl;
    
    return 0;
}
```

**Pertanyaan Analisis:**

1. Jelaskan mengapa versi naive memiliki kompleksitas eksponensial.
2. Bagaimana memoization mengubah kompleksitas menjadi O(m × n)?
3. Dalam konteks pertahanan, berikan 3 contoh aplikasi nyata dari algoritma path counting ini.
4. Jika grid sangat besar (1000 × 1000), teknik optimasi apa lagi yang bisa digunakan selain memoization?

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan |
|----|---------|------------|
| 1 | **B** | Base case adalah kondisi penghenti yang mencegah rekursi tak terbatas |
| 2 | **C** | mystery(5) = 5+4+3+2+1+0 = 15 |
| 3 | **B** | Binary Search membagi array menjadi setengah dengan cost O(1) per level |
| 4 | **D** | Master Theorem Kasus 2: a=2, b=2, log₂2=1, f(n)=n=Θ(n¹), T(n)=Θ(n log n) |
| 5 | **B** | Tower of Hanoi: 2⁸ - 1 = 256 - 1 = 255 langkah |
| 6 | **C** | Tail recursion: pemanggilan rekursif adalah operasi terakhir sebelum return |
| 7 | **E** | Fibonacci naive memiliki overlapping subproblems, T(n) ≈ O(2ⁿ) |
| 8 | **B** | Memoization menyimpan hasil untuk menghindari rekomputasi |
| 9 | **C** | Divide: langkah memecah masalah menjadi sub-masalah lebih kecil |
| 10 | **B** | Master Theorem Kasus 1: f(n) polynomially smaller, T(n) = Θ(n^(log_b(a))) |
| 11 | **B** | log₂(4) = log₂(2²) = 2 |
| 12 | **B** | Opsi B: pemanggilan rekursif `f(n-1, n*acc)` adalah operasi terakhir |
| 13 | **D** | log₂(1024) = 10, ditambah 1 untuk base case = 11 perbandingan |
| 14 | **B** | Memoization menghilangkan perhitungan berulang (overlapping subproblems) |
| 15 | **C** | Fast exponentiation: T(n) = T(n/2) + O(1) = O(log n) |
| 16 | **B** | a=9, b=3, log₃9=2, f(n)=n=O(n^(2-1)), Kasus 1: Θ(n²) |
| 17 | **C** | Tanpa base case valid, rekursi terus berjalan hingga stack overflow |
| 18 | **C** | Stack digunakan untuk mensimulasikan call stack sistem |
| 19 | **D** | Bubble Sort menggunakan iterasi, bukan D&C |
| 20 | **B** | a=2, b=4, log₄2=0.5, f(n)=√n=n^0.5=Θ(n^0.5), Kasus 2: Θ(√n · log n) |

---

### Bagian B: Uraian

#### Jawaban Soal 1

**Base Case:**
- Kondisi yang menghentikan rekursi
- Mengembalikan nilai langsung tanpa pemanggilan rekursif
- Pada faktorial: `if (n <= 1) return 1;`

**Recursive Case:**
- Kondisi yang melakukan pemanggilan rekursif
- Memecah masalah menjadi sub-masalah lebih kecil
- Pada faktorial: `return n * faktorial(n - 1);`

---

#### Jawaban Soal 2

**Tracing sumDigits(1234):**

![Tracing sumDigits(1234)](images/p07-08-tracing-sumdigits.png)

*Gambar: Tracing rekursi sumDigits(1234)*


**Hasil: 10** (= 1 + 2 + 3 + 4)

---

#### Jawaban Soal 3

**Recurrence Relations:**

1. **Linear Search:**
   ```
   T(n) = T(n-1) + O(1), T(1) = O(1)
   Solusi: T(n) = O(n)
   ```

2. **Faktorial:**
   ```
   T(n) = T(n-1) + O(1), T(1) = O(1)
   Solusi: T(n) = O(n)
   ```

3. **Merge Sort:**
   ```
   T(n) = 2T(n/2) + O(n), T(1) = O(1)
   Solusi: T(n) = O(n log n)
   ```

---

#### Jawaban Soal 4

**Master Theorem untuk T(n) = 3T(n/3) + n:**

**Langkah 1:** Identifikasi parameter
- a = 3 (jumlah subproblem)
- b = 3 (faktor pembagi)
- f(n) = n

**Langkah 2:** Hitung log_b(a)
- log₃(3) = 1
- n^(log_b(a)) = n¹ = n

**Langkah 3:** Bandingkan f(n) dengan n^(log_b(a))
- f(n) = n
- n^(log_b(a)) = n
- f(n) = Θ(n¹) = Θ(n^(log_b(a)))

**Langkah 4:** Kasus 2 berlaku
- T(n) = **Θ(n log n)**

---

#### Jawaban Soal 5

**Tail Recursive Faktorial:**

```cpp
// Versi tail recursive
int faktorialTail(int n, int accumulator = 1) {
    if (n <= 1) return accumulator;
    return faktorialTail(n - 1, n * accumulator);
}
```

**Mengapa lebih efisien:**
- Pada tail recursion, tidak ada operasi setelah pemanggilan rekursif
- Compiler dapat mengoptimasi dengan TCO (Tail Call Optimization)
- Stack frame dapat di-reuse karena tidak perlu menyimpan state
- Kompleksitas ruang: O(1) dengan TCO vs O(n) tanpa TCO

---

#### Jawaban Soal 6

**Mengapa Memoization Efektif untuk Fibonacci:**
- Fibonacci memiliki **overlapping subproblems**: fib(n-1) dan fib(n-2) berbagi banyak subproblem yang sama
- Contoh: fib(5) memanggil fib(3) dua kali, fib(2) tiga kali
- Memoization menyimpan hasil sehingga setiap subproblem hanya dihitung sekali
- Kompleksitas berubah dari O(2ⁿ) menjadi O(n)

**Mengapa Tidak Efektif untuk Faktorial:**
- Faktorial **tidak memiliki** overlapping subproblems
- Setiap nilai faktorial(k) hanya dihitung sekali dalam proses faktorial(n)
- Call tree berbentuk linear: faktorial(5) → faktorial(4) → faktorial(3) → ...
- Memoization tidak memberikan keuntungan karena tidak ada perhitungan berulang

---

#### Jawaban Soal 7

**Pohon Rekursi T(n) = 2T(n/2) + n dengan n = 8:**

![Pohon Rekursi T(n)=2T(n/2)+n](images/p07-09-recursion-tree-n8.png)

*Gambar: Pohon rekursi untuk T(n) = 2T(n/2) + n dengan n = 8*

**Analisis:**
- Jumlah level = log₂(8) + 1 = 4
- Total cost = 8 + 8 + 8 + 8 = 32 = 8 × 4 = n × log n
- **Kompleksitas: O(n log n)**

---

#### Jawaban Soal 8

**Binary Search Rekursif:**

```cpp
int binarySearch(int arr[], int left, int right, int target) {
    // Base case: tidak ditemukan
    if (left > right) return -1;
    
    // Hitung mid (hindari overflow)
    int mid = left + (right - left) / 2;
    
    // Ditemukan
    if (arr[mid] == target) return mid;
    
    // Cari di subarray yang sesuai
    if (target < arr[mid])
        return binarySearch(arr, left, mid - 1, target);
    else
        return binarySearch(arr, mid + 1, right, target);
}
```

**Analisis Kompleksitas:**
- **Waktu:** O(log n) - setiap rekursi membagi search space menjadi setengah
- **Ruang:** O(log n) - kedalaman rekursi maksimum adalah log n

---

#### Jawaban Soal 9

**1. Strategi Divide-and-Conquer:**
- **Divide:** Pecah masalah n disk menjadi: pindahkan n-1 disk
- **Conquer:** Pindahkan 1 disk (disk terbesar)
- **Combine:** Pindahkan n-1 disk ke tujuan akhir

**2. Bukti jumlah langkah = 2ⁿ - 1:**

Recurrence: T(n) = 2T(n-1) + 1, T(1) = 1

Substitusi:
- T(1) = 1 = 2¹ - 1 ✓
- T(2) = 2(1) + 1 = 3 = 2² - 1 ✓
- T(3) = 2(3) + 1 = 7 = 2³ - 1 ✓

Induksi: Asumsikan T(k) = 2^k - 1
T(k+1) = 2T(k) + 1 = 2(2^k - 1) + 1 = 2^(k+1) - 2 + 1 = 2^(k+1) - 1 ✓

**3. Waktu untuk 10 disk:**
- Langkah = 2¹⁰ - 1 = 1023
- Waktu = 1023 × 2 detik = 2046 detik = **34 menit 6 detik**

---

#### Jawaban Soal 10

```cpp
#include <iostream>
#include <unordered_map>
#include <chrono>
using namespace std;

// Versi naive
long long fibNaive(int n) {
    if (n <= 1) return n;
    return fibNaive(n-1) + fibNaive(n-2);
}

// Versi memoization
unordered_map<int, long long> memo;
long long fibMemo(int n) {
    if (n <= 1) return n;
    if (memo.find(n) != memo.end()) return memo[n];
    memo[n] = fibMemo(n-1) + fibMemo(n-2);
    return memo[n];
}

int main() {
    int n = 40;
    
    // Memoization
    auto start1 = chrono::high_resolution_clock::now();
    cout << "fibMemo(" << n << ") = " << fibMemo(n) << endl;
    auto end1 = chrono::high_resolution_clock::now();
    chrono::duration<double, milli> dur1 = end1 - start1;
    cout << "Waktu: " << dur1.count() << " ms" << endl;
    
    // Naive (warning: sangat lambat!)
    auto start2 = chrono::high_resolution_clock::now();
    cout << "fibNaive(" << n << ") = " << fibNaive(n) << endl;
    auto end2 = chrono::high_resolution_clock::now();
    chrono::duration<double, milli> dur2 = end2 - start2;
    cout << "Waktu: " << dur2.count() << " ms" << endl;
    
    return 0;
}
```

**Hasil perkiraan:**
- Memoization: < 1 ms
- Naive: ~30-60 detik untuk n=40

---

#### Jawaban Soal 11

```cpp
#include <iostream>
#include <stack>
using namespace std;

struct HanoiState {
    int n;
    char src, dest, aux;
    int stage;  // 0, 1, 2
};

void hanoiIterative(int n, char src, char dest, char aux) {
    stack<HanoiState> s;
    s.push({n, src, dest, aux, 0});
    
    while (!s.empty()) {
        HanoiState& state = s.top();
        
        if (state.n == 1) {
            cout << "Move disk 1 from " << state.src 
                 << " to " << state.dest << endl;
            s.pop();
            continue;
        }
        
        switch (state.stage) {
            case 0:
                state.stage = 1;
                s.push({state.n-1, state.src, state.aux, state.dest, 0});
                break;
            case 1:
                cout << "Move disk " << state.n << " from " 
                     << state.src << " to " << state.dest << endl;
                state.stage = 2;
                s.push({state.n-1, state.aux, state.dest, state.src, 0});
                break;
            case 2:
                s.pop();
                break;
        }
    }
}
```

**Struktur data:** HanoiState menyimpan parameter fungsi (n, src, dest, aux) dan stage untuk melacak progress dalam "fungsi".

---

#### Jawaban Soal 12

```cpp
// Lower bound: index pertama dengan arr[i] >= target
int lowerBound(int arr[], int n, int target) {
    int left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] < target)
            left = mid + 1;
        else
            right = mid;
    }
    return left;
}

// Upper bound: index pertama dengan arr[i] > target
int upperBound(int arr[], int n, int target) {
    int left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] <= target)
            left = mid + 1;
        else
            right = mid;
    }
    return left;
}
```

Kompleksitas: O(log n) untuk keduanya.

---

#### Jawaban Soal 13

**Metode Substitusi untuk T(n) = T(n-1) + n:**

T(n) = T(n-1) + n
     = [T(n-2) + (n-1)] + n
     = T(n-2) + (n-1) + n
     = T(n-3) + (n-2) + (n-1) + n
     ...
     = T(1) + 2 + 3 + ... + n
     = 1 + (2 + 3 + ... + n)
     = n(n+1)/2
     = **O(n²)**

---

#### Jawaban Soal 14

```cpp
double power(double a, int n) {
    // Handle negative exponent
    if (n < 0) {
        a = 1.0 / a;
        n = -n;
    }
    
    // Base cases
    if (n == 0) return 1;
    if (n == 1) return a;
    
    // Divide and conquer
    if (n % 2 == 0) {
        double half = power(a, n / 2);
        return half * half;
    } else {
        return a * power(a, n - 1);
    }
}
```

Kompleksitas: O(log n)

---

#### Jawaban Soal 15

**Cara Kerja TCO:**
1. Compiler mendeteksi bahwa pemanggilan rekursif adalah operasi terakhir
2. Alih-alih membuat stack frame baru, compiler me-reuse frame yang ada
3. Parameter diupdate dan program "jump" ke awal fungsi
4. Efeknya seperti loop, menghindari pertumbuhan stack

**Mengapa tidak semua compiler mengimplementasikan TCO:**
1. **Debugging sulit:** Stack trace tidak menunjukkan history pemanggilan
2. **ABI compatibility:** Beberapa calling convention tidak mendukung
3. **Standard C++:** Tidak mewajibkan TCO
4. **Overhead analisis:** Compiler perlu mendeteksi tail call
5. **Exception handling:** Interaksi kompleks dengan unwinding

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Pencarian Log Keamanan

```cpp
#include <iostream>
#include <vector>
#include <string>
#include <unordered_map>
using namespace std;

struct LogEntry {
    long long timestamp;
    string severity;
    string source_ip;
    string event_type;
};

// 1. Lower bound - O(log n)
int lowerBoundTimestamp(vector<LogEntry>& logs, long long target) {
    int left = 0, right = logs.size();
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (logs[mid].timestamp < target)
            left = mid + 1;
        else
            right = mid;
    }
    return left;
}

// 2. Upper bound - O(log n)
int upperBoundTimestamp(vector<LogEntry>& logs, long long target) {
    int left = 0, right = logs.size();
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (logs[mid].timestamp <= target)
            left = mid + 1;
        else
            right = mid;
    }
    return left;
}

// 3. Count CRITICAL in range - O(log n + k) dimana k = jumlah log dalam range
int countCriticalInRange(vector<LogEntry>& logs, long long start, long long end) {
    int startIdx = lowerBoundTimestamp(logs, start);
    int endIdx = upperBoundTimestamp(logs, end);
    
    int count = 0;
    for (int i = startIdx; i < endIdx; i++) {
        if (logs[i].severity == "CRITICAL") {
            count++;
        }
    }
    return count;
}

// 4. Dengan memoization - O(1) untuk query yang sama
unordered_map<string, int> queryCache;

string makeKey(long long start, long long end) {
    return to_string(start) + "_" + to_string(end);
}

int countCriticalMemoized(vector<LogEntry>& logs, long long start, long long end) {
    string key = makeKey(start, end);
    
    if (queryCache.find(key) != queryCache.end()) {
        cout << "  [Cache hit]" << endl;
        return queryCache[key];
    }
    
    int result = countCriticalInRange(logs, start, end);
    queryCache[key] = result;
    return result;
}
```

**Analisis Kompleksitas:**
- `lowerBoundTimestamp`: O(log n)
- `upperBoundTimestamp`: O(log n)
- `countCriticalInRange`: O(log n + k), k = jumlah log dalam range
- `countCriticalMemoized`: O(1) untuk repeated query, O(log n + k) untuk query baru

---

#### Studi Kasus 2: Optimasi Jalur Patroli

```cpp
#include <iostream>
#include <vector>
#include <map>
using namespace std;

// 1. Naive - O(2^(m+n))
long long countPathsNaive(int m, int n) {
    if (m == 1 || n == 1) return 1;
    return countPathsNaive(m - 1, n) + countPathsNaive(m, n - 1);
}

// 2. Memoization - O(m × n)
map<pair<int,int>, long long> memo;

long long countPathsMemo(int m, int n) {
    if (m == 1 || n == 1) return 1;
    
    pair<int,int> key = {m, n};
    if (memo.find(key) != memo.end()) return memo[key];
    
    memo[key] = countPathsMemo(m - 1, n) + countPathsMemo(m, n - 1);
    return memo[key];
}

// 3. Dengan obstacle - O(m × n)
long long countPathsWithObstacles(vector<vector<int>>& grid, int row, int col,
                                   map<pair<int,int>, long long>& memo) {
    int rows = grid.size();
    int cols = grid[0].size();
    
    // Out of bounds atau obstacle
    if (row >= rows || col >= cols || grid[row][col] == 1) return 0;
    
    // Reached destination
    if (row == rows - 1 && col == cols - 1) return 1;
    
    pair<int,int> key = {row, col};
    if (memo.find(key) != memo.end()) return memo[key];
    
    // Hanya bisa ke kanan atau ke bawah
    memo[key] = countPathsWithObstacles(grid, row + 1, col, memo) +
                countPathsWithObstacles(grid, row, col + 1, memo);
    return memo[key];
}
```

**Jawaban Pertanyaan Analisis:**

1. **Kompleksitas Eksponensial Naive:**
   - Setiap sel memiliki 2 pilihan (kanan/bawah)
   - Total kedalaman rekursi = m + n - 2
   - Pohon rekursi hampir penuh → O(2^(m+n))

2. **Memoization → O(m × n):**
   - Setiap sel (i, j) hanya dihitung sekali
   - Total sel = m × n
   - Setiap perhitungan = O(1)

3. **Aplikasi Pertahanan:**
   - Perencanaan rute patroli perbatasan
   - Analisis jalur evakuasi pada krisis
   - Optimasi pergerakan pasukan dalam operasi

4. **Optimasi untuk Grid Besar:**
   - Dynamic Programming iteratif (bottom-up)
   - Optimasi ruang: hanya simpan 2 baris
   - Formula kombinatorik: C(m+n-2, m-1)

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
