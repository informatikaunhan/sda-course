# Modul 07: Rekursi Lanjut dan Divide-and-Conquer

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 07  
**Topik:** Rekursi Lanjut dan Divide-and-Conquer

> **Capaian Pembelajaran:** Sub-CPMK-3.1, Sub-CPMK-3.2 — Mampu menganalisis dan mengoptimalkan algoritma rekursif serta menerapkan paradigma divide-and-conquer dalam penyelesaian masalah

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.4; Weiss Ch.1.3; Hubbard Ch.4

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menganalisis** algoritma rekursif dengan mengidentifikasi base case dan recursive case secara tepat
2. **Menghitung** kompleksitas algoritma rekursif menggunakan recurrence relation
3. **Menerapkan** Master Theorem untuk menentukan kompleksitas algoritma divide-and-conquer
4. **Mengidentifikasi** dan mengoptimalkan tail recursion pada algoritma
5. **Mengimplementasikan** teknik memoization untuk mengoptimalkan algoritma rekursif
6. **Menerapkan** paradigma divide-and-conquer dalam menyelesaikan berbagai permasalahan
7. **Mengkonversi** algoritma rekursif menjadi iteratif menggunakan stack eksplisit

---

## 1. Review Rekursi

### 1.1 Konsep Dasar Rekursi

> **Definisi:** Rekursi adalah teknik pemrograman di mana sebuah fungsi memanggil dirinya sendiri untuk menyelesaikan masalah dengan memecahnya menjadi sub-masalah yang lebih kecil.

Setiap fungsi rekursif memiliki dua komponen penting:

| Komponen | Deskripsi | Fungsi |
|----------|-----------|--------|
| **Base Case** | Kondisi penghenti rekursi | Mencegah pemanggilan tak terbatas |
| **Recursive Case** | Pemanggilan fungsi ke dirinya sendiri | Memecah masalah menjadi lebih kecil |

#### Anatomi Fungsi Rekursif

```cpp
returnType fungsiRekursif(parameter) {
    // Base case: kondisi berhenti
    if (kondisiBerhenti) {
        return nilaiDasar;
    }
    
    // Recursive case: pemanggilan diri sendiri
    return fungsiRekursif(parameterYangLebihKecil);
}
```

### 1.2 Contoh Klasik: Faktorial

```cpp
#include <iostream>
using namespace std;

// Fungsi faktorial rekursif
int faktorial(int n) {
    // Base case
    if (n <= 1) {
        return 1;
    }
    // Recursive case
    return n * faktorial(n - 1);
}

int main() {
    cout << "5! = " << faktorial(5) << endl;  // Output: 120
    return 0;
}
```

### 1.3 Tracing Rekursi

Tracing adalah teknik untuk memahami alur eksekusi fungsi rekursif dengan melacak setiap pemanggilan.

![Tracing Faktorial](images/p07-01-factorial-tracing.png)

*Gambar 1.1: Visualisasi tracing rekursi faktorial(5)*


**Tabel Tracing faktorial(5):**

| Call | n | Kondisi | Aksi | Return |
|------|---|---------|------|--------|
| faktorial(5) | 5 | n > 1 | 5 * faktorial(4) | 5 * 24 = 120 |
| faktorial(4) | 4 | n > 1 | 4 * faktorial(3) | 4 * 6 = 24 |
| faktorial(3) | 3 | n > 1 | 3 * faktorial(2) | 3 * 2 = 6 |
| faktorial(2) | 2 | n > 1 | 2 * faktorial(1) | 2 * 1 = 2 |
| faktorial(1) | 1 | n ≤ 1 | Base case | 1 |

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Tuliskan fungsi rekursif untuk menghitung jumlah digit dari sebuah bilangan positif.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

int jumlahDigit(int n) {
    // Base case: satu digit tersisa
    if (n < 10) {
        return n;
    }
    // Recursive case: digit terakhir + jumlah digit sisanya
    return (n % 10) + jumlahDigit(n / 10);
}

int main() {
    cout << "Jumlah digit 12345 = " << jumlahDigit(12345) << endl;
    // Output: 15 (1+2+3+4+5)
    return 0;
}
```

**Analisis:**
- Base case: n < 10 (hanya satu digit)
- Recursive case: ambil digit terakhir (n % 10), tambahkan dengan hasil rekursi sisanya (n / 10)
- Tracing: 12345 → 5 + jumlahDigit(1234) → 5 + 4 + jumlahDigit(123) → ... → 15

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Implementasikan fungsi rekursif untuk menghitung pangkat a^n.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

// Versi sederhana: O(n)
int pangkat(int a, int n) {
    if (n == 0) return 1;           // Base case
    return a * pangkat(a, n - 1);    // Recursive case
}

// Versi efisien menggunakan divide-and-conquer: O(log n)
int pangkatCepat(int a, int n) {
    if (n == 0) return 1;
    if (n % 2 == 0) {
        int half = pangkatCepat(a, n / 2);
        return half * half;
    } else {
        return a * pangkatCepat(a, n - 1);
    }
}

int main() {
    cout << "2^10 = " << pangkat(2, 10) << endl;        // 1024
    cout << "2^10 = " << pangkatCepat(2, 10) << endl;   // 1024
    return 0;
}
```

---

## 2. Analisis Kompleksitas Rekursi

### 2.1 Recurrence Relation

> **Definisi:** Recurrence relation adalah persamaan yang mendefinisikan kompleksitas waktu fungsi rekursif dalam bentuk kompleksitas untuk input yang lebih kecil.

#### Bentuk Umum Recurrence Relation

```
T(n) = a·T(n/b) + f(n)
```

Di mana:
- `T(n)` = waktu untuk menyelesaikan masalah berukuran n
- `a` = jumlah subproblem
- `n/b` = ukuran setiap subproblem
- `f(n)` = waktu untuk membagi dan menggabungkan

### 2.2 Metode Substitusi

Langkah-langkah:
1. **Tebak** bentuk solusi
2. **Substitusi** ke recurrence relation
3. **Buktikan** dengan induksi matematika

**Contoh: Faktorial**
- Recurrence: T(n) = T(n-1) + c, T(1) = c
- Tebakan: T(n) = O(n)
- Substitusi: T(n) = T(n-1) + c = cn
- Bukti: T(n) = cn untuk semua n ≥ 1 ✓

### 2.3 Metode Pohon Rekursi (Recursion Tree)

![Recursion Tree](images/p07-02-recursion-tree.png)

*Gambar 2.1: Pohon rekursi untuk T(n) = 2T(n/2) + n*


---

### SOLVED PROBLEM 3 ⭐⭐

**Soal:** Tentukan kompleksitas waktu dari recurrence relation: T(n) = 2T(n/2) + n menggunakan metode pohon rekursi.

**Penyelesaian:**

**Langkah 1:** Gambar pohon rekursi
- Level 0: 1 node dengan cost n
- Level 1: 2 node, masing-masing cost n/2, total = n
- Level 2: 4 node, masing-masing cost n/4, total = n
- Level k: 2^k node, masing-masing cost n/2^k, total = n

**Langkah 2:** Hitung jumlah level
- Berhenti ketika n/2^k = 1, yaitu k = log₂n
- Jumlah level = log₂n + 1

**Langkah 3:** Hitung total cost
- Total = n × (log₂n + 1) = n log n + n
- T(n) = **O(n log n)**

---

## 3. Master Theorem

### 3.1 Pernyataan Master Theorem

> **Master Theorem:** Untuk recurrence relation berbentuk T(n) = aT(n/b) + f(n), di mana a ≥ 1 dan b > 1:

| Kasus | Kondisi | Kompleksitas |
|-------|---------|--------------|
| **Kasus 1** | f(n) = O(n^(log_b(a) - ε)) untuk ε > 0 | T(n) = Θ(n^(log_b(a))) |
| **Kasus 2** | f(n) = Θ(n^(log_b(a))) | T(n) = Θ(n^(log_b(a)) · log n) |
| **Kasus 3** | f(n) = Ω(n^(log_b(a) + ε)) untuk ε > 0 | T(n) = Θ(f(n)) |

### 3.2 Cara Menggunakan Master Theorem

**Langkah-langkah:**
1. Identifikasi nilai a, b, dan f(n)
2. Hitung log_b(a)
3. Bandingkan f(n) dengan n^(log_b(a))
4. Tentukan kasus yang berlaku
5. Tulis kompleksitasnya

![Master Theorem Flowchart](images/p07-03-master-theorem.png)

*Gambar 3.1: Flowchart penggunaan Master Theorem*


---

### SOLVED PROBLEM 4 ⭐⭐

**Soal:** Gunakan Master Theorem untuk menentukan kompleksitas T(n) = 4T(n/2) + n.

**Penyelesaian:**

**Langkah 1:** Identifikasi parameter
- a = 4 (jumlah subproblem)
- b = 2 (faktor pembagi)
- f(n) = n

**Langkah 2:** Hitung log_b(a)
- log₂(4) = 2
- Jadi n^(log_b(a)) = n²

**Langkah 3:** Bandingkan f(n) dengan n²
- f(n) = n = n¹
- n¹ vs n² → n¹ lebih kecil secara polinomial
- f(n) = O(n^(2-ε)) dengan ε = 1

**Langkah 4:** Kasus 1 berlaku
- T(n) = **Θ(n²)**

---

### SOLVED PROBLEM 5 ⭐⭐

**Soal:** Tentukan kompleksitas T(n) = 2T(n/2) + n menggunakan Master Theorem.

**Penyelesaian:**

- a = 2, b = 2, f(n) = n
- log₂(2) = 1, jadi n^(log_b(a)) = n¹ = n
- f(n) = n = Θ(n^1)
- Kasus 2: f(n) = Θ(n^(log_b(a)))
- T(n) = **Θ(n log n)**

---

### SOLVED PROBLEM 6 ⭐⭐⭐

**Soal:** Tentukan kompleksitas T(n) = 3T(n/4) + n log n.

**Penyelesaian:**

**Langkah 1:** Identifikasi
- a = 3, b = 4, f(n) = n log n

**Langkah 2:** Hitung log_b(a)
- log₄(3) = log(3)/log(4) ≈ 0.793
- n^(log_b(a)) ≈ n^0.793

**Langkah 3:** Bandingkan
- f(n) = n log n = n¹ · log n
- n^0.793 vs n¹ · log n
- n log n lebih besar secara polinomial dari n^0.793 (dengan ε ≈ 0.2)

**Langkah 4:** Kasus 3 berlaku
- Verifikasi regularity condition: 3·(n/4)log(n/4) ≤ c·n log n untuk c < 1 ✓
- T(n) = **Θ(n log n)**

---

## 4. Tail Recursion dan Optimasi

### 4.1 Pengertian Tail Recursion

> **Definisi:** Tail recursion adalah bentuk rekursi di mana pemanggilan rekursif adalah operasi terakhir yang dilakukan oleh fungsi sebelum mengembalikan nilai.

#### Perbandingan Regular vs Tail Recursion

**Regular Recursion (Non-tail):**
```cpp
int faktorial(int n) {
    if (n <= 1) return 1;
    return n * faktorial(n - 1);  // Operasi * setelah rekursi
}
```

**Tail Recursion:**
```cpp
int faktorialTail(int n, int accumulator = 1) {
    if (n <= 1) return accumulator;
    return faktorialTail(n - 1, n * accumulator);  // Rekursi terakhir
}
```

### 4.2 Keuntungan Tail Recursion

| Aspek | Regular Recursion | Tail Recursion |
|-------|-------------------|----------------|
| Stack Frame | Menumpuk | Dapat di-reuse |
| Memory | O(n) | O(1) dengan TCO |
| Stack Overflow | Mungkin | Dihindari |
| Compiler Optimization | Terbatas | TCO applicable |

> **Catatan:** TCO (Tail Call Optimization) adalah optimasi compiler yang mengubah tail recursion menjadi loop, menghindari penumpukan stack frame.

![Tail Recursion Comparison](images/p07-04-tail-recursion.png)

*Gambar 4.1: Perbandingan stack usage antara regular dan tail recursion*


---

### SOLVED PROBLEM 7 ⭐⭐

**Soal:** Konversi fungsi sum array rekursif menjadi tail recursive.

**Penyelesaian:**

**Versi Non-tail:**
```cpp
int sumArray(int arr[], int n) {
    if (n <= 0) return 0;
    return arr[n-1] + sumArray(arr, n-1);
}
```

**Versi Tail Recursive:**
```cpp
int sumArrayTail(int arr[], int n, int accumulator = 0) {
    if (n <= 0) return accumulator;
    return sumArrayTail(arr, n - 1, accumulator + arr[n-1]);
}

// Penggunaan
int main() {
    int data[] = {1, 2, 3, 4, 5};
    cout << "Sum = " << sumArrayTail(data, 5) << endl;  // Output: 15
    return 0;
}
```

**Penjelasan:**
- Parameter `accumulator` menyimpan hasil perhitungan parsial
- Tidak ada operasi setelah pemanggilan rekursif
- Compiler dapat mengoptimasi menjadi loop

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Implementasikan fungsi Fibonacci dengan tail recursion.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

// Versi non-tail: O(2^n) waktu, O(n) space
int fibNonTail(int n) {
    if (n <= 1) return n;
    return fibNonTail(n-1) + fibNonTail(n-2);
}

// Versi tail recursive: O(n) waktu, O(1) space dengan TCO
int fibTailHelper(int n, int a = 0, int b = 1) {
    if (n == 0) return a;
    if (n == 1) return b;
    return fibTailHelper(n - 1, b, a + b);
}

int fibTail(int n) {
    return fibTailHelper(n);
}

int main() {
    cout << "Fib(10) Non-tail: " << fibNonTail(10) << endl;  // 55
    cout << "Fib(10) Tail: " << fibTail(10) << endl;         // 55
    return 0;
}
```

**Tracing fibTailHelper(5, 0, 1):**

| Call | n | a | b | Action |
|------|---|---|---|--------|
| 1 | 5 | 0 | 1 | Continue |
| 2 | 4 | 1 | 1 | Continue |
| 3 | 3 | 1 | 2 | Continue |
| 4 | 2 | 2 | 3 | Continue |
| 5 | 1 | 3 | 5 | Return b = 5 |

---

## 5. Memoization dan Dynamic Programming

### 5.1 Konsep Memoization

> **Definisi:** Memoization adalah teknik optimasi yang menyimpan hasil komputasi yang sudah dilakukan untuk menghindari perhitungan berulang.

#### Masalah dengan Rekursi Naive (Fibonacci)

```cpp
// O(2^n) - sangat lambat!
int fibNaive(int n) {
    if (n <= 1) return n;
    return fibNaive(n-1) + fibNaive(n-2);
}
```

Permasalahan: Perhitungan berulang yang sama!

![Fibonacci Overlapping Subproblems](images/p07-05-fibonacci-overlap.png)

*Gambar 5.1: Overlapping subproblems pada Fibonacci rekursif*


### 5.2 Implementasi Memoization

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

unordered_map<int, long long> memo;

// O(n) waktu, O(n) space
long long fibMemo(int n) {
    // Base case
    if (n <= 1) return n;
    
    // Cek apakah sudah pernah dihitung
    if (memo.find(n) != memo.end()) {
        return memo[n];  // Kembalikan hasil yang tersimpan
    }
    
    // Hitung dan simpan
    memo[n] = fibMemo(n-1) + fibMemo(n-2);
    return memo[n];
}

int main() {
    cout << "Fib(50) = " << fibMemo(50) << endl;  // Cepat!
    return 0;
}
```

### 5.3 Perbandingan Performa

| Metode | Kompleksitas Waktu | Kompleksitas Ruang | Fib(40) Time |
|--------|-------------------|-------------------|--------------|
| Naive Recursion | O(2^n) | O(n) | ~1 menit |
| Memoization | O(n) | O(n) | < 1 ms |
| Tail Recursion | O(n) | O(1)* | < 1 ms |
| Iteratif | O(n) | O(1) | < 1 ms |

*dengan TCO

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Implementasikan fungsi untuk menghitung jumlah cara naik tangga n anak tangga, di mana setiap langkah bisa naik 1 atau 2 anak tangga, menggunakan memoization.

**Penyelesaian:**

```cpp
#include <iostream>
#include <unordered_map>
using namespace std;

unordered_map<int, long long> memo;

// Jumlah cara naik n anak tangga
long long climbStairs(int n) {
    // Base cases
    if (n <= 0) return 0;
    if (n == 1) return 1;
    if (n == 2) return 2;
    
    // Check memo
    if (memo.find(n) != memo.end()) {
        return memo[n];
    }
    
    // Rekursi dengan memoization
    memo[n] = climbStairs(n-1) + climbStairs(n-2);
    return memo[n];
}

int main() {
    cout << "Cara naik 5 tangga: " << climbStairs(5) << endl;   // 8
    cout << "Cara naik 10 tangga: " << climbStairs(10) << endl; // 89
    return 0;
}
```

**Analisis:**
- Ini mirip dengan deret Fibonacci!
- climbStairs(n) = climbStairs(n-1) + climbStairs(n-2)
- Tanpa memoization: O(2^n), dengan memoization: O(n)

---

### SOLVED PROBLEM 10 ⭐⭐⭐

**Soal:** Dalam sistem pertahanan, perlu dihitung jumlah rute berbeda dari pojok kiri atas ke pojok kanan bawah pada grid m×n, di mana hanya bisa bergerak ke kanan atau ke bawah. Implementasikan dengan memoization.

**Penyelesaian:**

```cpp
#include <iostream>
#include <map>
using namespace std;

map<pair<int,int>, long long> memo;

// Menghitung jumlah rute unik pada grid m x n
long long uniquePaths(int m, int n) {
    // Base cases
    if (m == 1 || n == 1) return 1;
    if (m == 0 || n == 0) return 0;
    
    // Check memo
    pair<int,int> key = {m, n};
    if (memo.find(key) != memo.end()) {
        return memo[key];
    }
    
    // Jumlah rute = rute dari atas + rute dari kiri
    memo[key] = uniquePaths(m-1, n) + uniquePaths(m, n-1);
    return memo[key];
}

int main() {
    // Contoh: Grid patroli 3x7
    cout << "Jumlah rute 3x7: " << uniquePaths(3, 7) << endl;  // 28
    cout << "Jumlah rute 10x10: " << uniquePaths(10, 10) << endl;  // 48620
    return 0;
}
```

**Aplikasi Pertahanan:**
- Perencanaan rute patroli
- Analisis jalur evakuasi
- Optimasi pergerakan unit

---

## 6. Paradigma Divide-and-Conquer

### 6.1 Pengertian Divide-and-Conquer

> **Definisi:** Divide-and-conquer adalah paradigma algoritma yang memecah masalah menjadi sub-masalah yang lebih kecil, menyelesaikan setiap sub-masalah secara rekursif, lalu menggabungkan solusinya.

**Tiga Langkah Divide-and-Conquer:**

| Langkah | Deskripsi | Contoh (Merge Sort) |
|---------|-----------|---------------------|
| **Divide** | Bagi masalah menjadi sub-masalah | Bagi array menjadi 2 bagian |
| **Conquer** | Selesaikan sub-masalah secara rekursif | Sort setiap bagian |
| **Combine** | Gabungkan solusi sub-masalah | Merge 2 array terurut |

![Divide and Conquer Paradigm](images/p07-06-divide-conquer.png)

*Gambar 6.1: Paradigma Divide-and-Conquer*


### 6.2 Algoritma Divide-and-Conquer Klasik

| Algoritma | Divide | Conquer | Combine | Kompleksitas |
|-----------|--------|---------|---------|--------------|
| Binary Search | Bagi 2 | Search di separuh | - | O(log n) |
| Merge Sort | Bagi 2 | Sort keduanya | Merge | O(n log n) |
| Quick Sort | Partition | Sort keduanya | - | O(n log n)* |
| Tower of Hanoi | n-1 disk | Pindah 1 disk | n-1 disk | O(2^n) |

*average case

---

## 7. Binary Search sebagai Divide-and-Conquer

### 7.1 Konsep Binary Search

> **Definisi:** Binary search adalah algoritma pencarian pada array terurut yang membagi search space menjadi setengah pada setiap iterasi.

**Prasyarat:** Array harus sudah terurut (sorted)!

### 7.2 Implementasi Rekursif

```cpp
#include <iostream>
using namespace std;

int binarySearch(int arr[], int left, int right, int target) {
    // Base case: tidak ditemukan
    if (left > right) return -1;
    
    // Divide: hitung titik tengah
    int mid = left + (right - left) / 2;  // Hindari overflow
    
    // Conquer
    if (arr[mid] == target) {
        return mid;  // Ditemukan!
    }
    else if (target < arr[mid]) {
        return binarySearch(arr, left, mid - 1, target);  // Cari di kiri
    }
    else {
        return binarySearch(arr, mid + 1, right, target);  // Cari di kanan
    }
}

int main() {
    int data[] = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
    int n = 10;
    int target = 23;
    
    int result = binarySearch(data, 0, n-1, target);
    if (result != -1) {
        cout << "Ditemukan di index " << result << endl;
    } else {
        cout << "Tidak ditemukan" << endl;
    }
    return 0;
}
```

### 7.3 Analisis Kompleksitas Binary Search

**Recurrence Relation:** T(n) = T(n/2) + O(1)

Menggunakan Master Theorem:
- a = 1, b = 2, f(n) = O(1)
- log₂(1) = 0, jadi n^(log_b(a)) = n^0 = 1
- f(n) = Θ(1) = Θ(n^0)
- Kasus 2: T(n) = **Θ(log n)**

---

### SOLVED PROBLEM 11 ⭐

**Soal:** Implementasikan binary search iteratif.

**Penyelesaian:**

```cpp
int binarySearchIterative(int arr[], int n, int target) {
    int left = 0, right = n - 1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            return mid;
        }
        else if (target < arr[mid]) {
            right = mid - 1;
        }
        else {
            left = mid + 1;
        }
    }
    
    return -1;  // Tidak ditemukan
}
```

---

### SOLVED PROBLEM 12 ⭐⭐

**Soal:** Implementasikan fungsi untuk mencari posisi pertama dan terakhir dari elemen target dalam array terurut menggunakan binary search.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

// Cari posisi pertama (leftmost)
int findFirst(int arr[], int n, int target) {
    int left = 0, right = n - 1, result = -1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            result = mid;
            right = mid - 1;  // Terus cari ke kiri
        }
        else if (target < arr[mid]) {
            right = mid - 1;
        }
        else {
            left = mid + 1;
        }
    }
    return result;
}

// Cari posisi terakhir (rightmost)
int findLast(int arr[], int n, int target) {
    int left = 0, right = n - 1, result = -1;
    
    while (left <= right) {
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            result = mid;
            left = mid + 1;  // Terus cari ke kanan
        }
        else if (target < arr[mid]) {
            right = mid - 1;
        }
        else {
            left = mid + 1;
        }
    }
    return result;
}

int main() {
    int arr[] = {2, 4, 4, 4, 4, 6, 8, 10};
    int n = 8;
    int target = 4;
    
    cout << "First occurrence: " << findFirst(arr, n, target) << endl;  // 1
    cout << "Last occurrence: " << findLast(arr, n, target) << endl;    // 4
    
    return 0;
}
```

---

## 8. Tower of Hanoi

### 8.1 Deskripsi Masalah

> **Tower of Hanoi:** Pindahkan n disk dari tiang sumber (A) ke tiang tujuan (C) dengan aturan:
> 1. Hanya boleh memindahkan satu disk pada satu waktu
> 2. Disk yang lebih besar tidak boleh diletakkan di atas disk yang lebih kecil
> 3. Gunakan tiang bantu (B) sebagai tempat sementara

![Tower of Hanoi](images/p07-07-tower-of-hanoi.png)

*Gambar 8.1: Ilustrasi Tower of Hanoi dengan 3 disk*


### 8.2 Solusi Rekursif

**Strategi Divide-and-Conquer:**
1. **Divide:** Pindahkan n-1 disk dari A ke B (menggunakan C)
2. **Conquer:** Pindahkan disk terbesar dari A ke C
3. **Combine:** Pindahkan n-1 disk dari B ke C (menggunakan A)

```cpp
#include <iostream>
using namespace std;

int moveCount = 0;

void hanoi(int n, char source, char destination, char auxiliary) {
    if (n == 1) {
        // Base case: pindahkan disk terkecil
        cout << "Pindahkan disk 1 dari " << source 
             << " ke " << destination << endl;
        moveCount++;
        return;
    }
    
    // Langkah 1: Pindahkan n-1 disk dari source ke auxiliary
    hanoi(n - 1, source, auxiliary, destination);
    
    // Langkah 2: Pindahkan disk terbesar dari source ke destination
    cout << "Pindahkan disk " << n << " dari " << source 
         << " ke " << destination << endl;
    moveCount++;
    
    // Langkah 3: Pindahkan n-1 disk dari auxiliary ke destination
    hanoi(n - 1, auxiliary, destination, source);
}

int main() {
    int n = 3;
    cout << "Tower of Hanoi dengan " << n << " disk:\n" << endl;
    hanoi(n, 'A', 'C', 'B');
    cout << "\nTotal langkah: " << moveCount << endl;
    return 0;
}
```

**Output untuk n=3:**
```
Pindahkan disk 1 dari A ke C
Pindahkan disk 2 dari A ke B
Pindahkan disk 1 dari C ke B
Pindahkan disk 3 dari A ke C
Pindahkan disk 1 dari B ke A
Pindahkan disk 2 dari B ke C
Pindahkan disk 1 dari A ke C

Total langkah: 7
```

### 8.3 Analisis Kompleksitas Tower of Hanoi

**Recurrence Relation:** T(n) = 2T(n-1) + 1

**Solusi:**
- T(1) = 1
- T(2) = 2(1) + 1 = 3
- T(3) = 2(3) + 1 = 7
- T(n) = **2^n - 1**

Kompleksitas: **O(2^n)** - eksponensial!

| n (disk) | Langkah | Waktu (1 langkah/detik) |
|----------|---------|-------------------------|
| 5 | 31 | 31 detik |
| 10 | 1.023 | ~17 menit |
| 20 | 1.048.575 | ~12 hari |
| 64* | ~1.8 × 10^19 | ~585 miliar tahun |

*Legenda: para biksu di Hanoi memindahkan 64 disk emas

---

### SOLVED PROBLEM 13 ⭐

**Soal:** Berapa langkah minimum yang diperlukan untuk menyelesaikan Tower of Hanoi dengan 5 disk?

**Penyelesaian:**

Rumus: Langkah = 2^n - 1

Untuk n = 5:
- Langkah = 2^5 - 1 = 32 - 1 = **31 langkah**

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Modifikasi fungsi Tower of Hanoi untuk menghitung jumlah langkah tanpa mencetak setiap langkah.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

long long hanoiCount(int n) {
    if (n == 1) return 1;
    return 2 * hanoiCount(n - 1) + 1;
}

// Versi dengan rumus langsung (lebih efisien)
long long hanoiFormula(int n) {
    return (1LL << n) - 1;  // 2^n - 1
}

int main() {
    for (int n = 1; n <= 20; n++) {
        cout << "Disk " << n << ": " << hanoiFormula(n) << " langkah" << endl;
    }
    return 0;
}
```

---

### SOLVED PROBLEM 15 ⭐⭐⭐

**Soal:** Dalam latihan logistik militer, ada 4 kontainer yang harus dipindahkan mengikuti aturan Tower of Hanoi. Berapa total waktu yang diperlukan jika setiap pemindahan membutuhkan 15 menit?

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

int main() {
    int n = 4;                    // Jumlah kontainer
    int waktuPerPindah = 15;      // menit
    
    // Hitung jumlah langkah
    long long langkah = (1LL << n) - 1;  // 2^4 - 1 = 15
    
    // Hitung total waktu
    long long totalMenit = langkah * waktuPerPindah;
    int jam = totalMenit / 60;
    int menit = totalMenit % 60;
    
    cout << "Jumlah kontainer: " << n << endl;
    cout << "Jumlah pemindahan: " << langkah << endl;
    cout << "Waktu per pemindahan: " << waktuPerPindah << " menit" << endl;
    cout << "Total waktu: " << jam << " jam " << menit << " menit" << endl;
    
    return 0;
}
```

**Output:**
```
Jumlah kontainer: 4
Jumlah pemindahan: 15
Waktu per pemindahan: 15 menit
Total waktu: 3 jam 45 menit
```

---

## 9. Konversi Rekursi ke Iterasi dengan Stack

### 9.1 Mengapa Mengkonversi?

| Rekursi | Iterasi dengan Stack |
|---------|---------------------|
| Kode lebih sederhana | Kode lebih kompleks |
| Stack implisit (call stack) | Stack eksplisit |
| Risiko stack overflow | Kontrol ukuran stack |
| Overhead function call | Lebih efisien |

### 9.2 Teknik Konversi

**Langkah-langkah:**
1. Identifikasi parameter yang perlu disimpan
2. Buat stack untuk menyimpan state
3. Gunakan loop untuk menggantikan pemanggilan rekursif
4. Pop state dari stack dan proses

### 9.3 Contoh: Faktorial

```cpp
#include <iostream>
#include <stack>
using namespace std;

// Versi rekursif
int faktorialRekursif(int n) {
    if (n <= 1) return 1;
    return n * faktorialRekursif(n - 1);
}

// Versi iteratif dengan stack eksplisit
int faktorialStack(int n) {
    stack<int> s;
    
    // Push semua nilai ke stack (simulasi rekursi turun)
    while (n > 1) {
        s.push(n);
        n--;
    }
    
    // Pop dan kalikan (simulasi rekursi naik)
    int result = 1;
    while (!s.empty()) {
        result *= s.top();
        s.pop();
    }
    
    return result;
}

int main() {
    cout << "Rekursif: 5! = " << faktorialRekursif(5) << endl;
    cout << "Stack: 5! = " << faktorialStack(5) << endl;
    return 0;
}
```

### 9.4 Contoh: Tree Traversal (Preview)

> **Catatan:** Struktur data tree akan dibahas pada Pertemuan 11. Contoh ini diberikan sebagai preview aplikasi konversi rekursi ke iterasi.

```cpp
#include <iostream>
#include <stack>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(nullptr), right(nullptr) {}
};

// Inorder rekursif
void inorderRekursif(Node* root) {
    if (root == nullptr) return;
    inorderRekursif(root->left);
    cout << root->data << " ";
    inorderRekursif(root->right);
}

// Inorder iteratif dengan stack
void inorderIteratif(Node* root) {
    stack<Node*> s;
    Node* current = root;
    
    while (current != nullptr || !s.empty()) {
        // Traverse ke kiri sebanyak mungkin
        while (current != nullptr) {
            s.push(current);
            current = current->left;
        }
        
        // Pop dan proses
        current = s.top();
        s.pop();
        cout << current->data << " ";
        
        // Pindah ke subtree kanan
        current = current->right;
    }
}
```

---

### SOLVED PROBLEM 16 ⭐⭐

**Soal:** Konversi fungsi binary search rekursif menjadi iteratif dengan stack eksplisit.

**Penyelesaian:**

```cpp
#include <iostream>
#include <stack>
using namespace std;

struct SearchState {
    int left;
    int right;
};

int binarySearchWithStack(int arr[], int n, int target) {
    stack<SearchState> s;
    s.push({0, n - 1});
    
    while (!s.empty()) {
        SearchState state = s.top();
        s.pop();
        
        int left = state.left;
        int right = state.right;
        
        if (left > right) continue;
        
        int mid = left + (right - left) / 2;
        
        if (arr[mid] == target) {
            return mid;  // Ditemukan
        }
        else if (target < arr[mid]) {
            s.push({left, mid - 1});  // Cari di kiri
        }
        else {
            s.push({mid + 1, right});  // Cari di kanan
        }
    }
    
    return -1;  // Tidak ditemukan
}

int main() {
    int data[] = {2, 5, 8, 12, 16, 23, 38, 56, 72, 91};
    int target = 23;
    
    int result = binarySearchWithStack(data, 10, target);
    cout << "Index: " << result << endl;  // Output: 5
    
    return 0;
}
```

---

### SOLVED PROBLEM 17 ⭐⭐⭐

**Soal:** Konversi Tower of Hanoi rekursif menjadi iteratif dengan stack.

**Penyelesaian:**

```cpp
#include <iostream>
#include <stack>
using namespace std;

struct HanoiState {
    int n;
    char source;
    char destination;
    char auxiliary;
    int stage;  // 0 = sebelum rekursi pertama, 1 = sebelum move, 2 = sebelum rekursi kedua
};

void hanoiIteratif(int n, char source, char destination, char auxiliary) {
    stack<HanoiState> s;
    s.push({n, source, destination, auxiliary, 0});
    
    while (!s.empty()) {
        HanoiState& state = s.top();
        
        if (state.n == 1) {
            cout << "Pindahkan disk 1 dari " << state.source 
                 << " ke " << state.destination << endl;
            s.pop();
            continue;
        }
        
        switch (state.stage) {
            case 0:
                // Push rekursi pertama
                state.stage = 1;
                s.push({state.n - 1, state.source, state.auxiliary, 
                        state.destination, 0});
                break;
                
            case 1:
                // Pindahkan disk terbesar
                cout << "Pindahkan disk " << state.n << " dari " 
                     << state.source << " ke " << state.destination << endl;
                state.stage = 2;
                // Push rekursi kedua
                s.push({state.n - 1, state.auxiliary, state.destination, 
                        state.source, 0});
                break;
                
            case 2:
                s.pop();
                break;
        }
    }
}

int main() {
    cout << "Tower of Hanoi Iteratif (3 disk):\n" << endl;
    hanoiIteratif(3, 'A', 'C', 'B');
    return 0;
}
```

---

### SOLVED PROBLEM 18 ⭐⭐

**Soal:** Implementasikan fungsi untuk menghitung GCD (Greatest Common Divisor) menggunakan algoritma Euclidean dengan rekursi dan konversi ke iteratif.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

// Rekursif
int gcdRekursif(int a, int b) {
    if (b == 0) return a;
    return gcdRekursif(b, a % b);
}

// Iteratif (tanpa stack karena tail recursive)
int gcdIteratif(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

int main() {
    cout << "GCD(48, 18) rekursif: " << gcdRekursif(48, 18) << endl;   // 6
    cout << "GCD(48, 18) iteratif: " << gcdIteratif(48, 18) << endl;   // 6
    return 0;
}
```

**Analisis:**
- Algoritma Euclidean adalah contoh tail recursion
- Konversi ke iteratif sangat straightforward
- Kompleksitas: O(log(min(a, b)))

---

### SOLVED PROBLEM 19 ⭐⭐

**Soal:** Implementasikan fungsi rekursif untuk mencetak semua substring dari sebuah string.

**Penyelesaian:**

```cpp
#include <iostream>
#include <string>
using namespace std;

void printSubstrings(const string& str, int start, int end) {
    // Base case: sudah melewati semua posisi awal
    if (start >= str.length()) return;
    
    // Base case: end melewati panjang string, pindah ke start berikutnya
    if (end > str.length()) {
        printSubstrings(str, start + 1, start + 2);
        return;
    }
    
    // Print substring dari start ke end
    cout << str.substr(start, end - start) << endl;
    
    // Recursive case: perpanjang end
    printSubstrings(str, start, end + 1);
}

int main() {
    string s = "ABC";
    cout << "Semua substring dari \"" << s << "\":" << endl;
    printSubstrings(s, 0, 1);
    return 0;
}
```

**Output:**
```
A
AB
ABC
B
BC
C
```

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Implementasikan algoritma Merge Sort rekursif (preview untuk Pertemuan 10).

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

// Fungsi untuk merge dua subarray yang sudah terurut
void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    // Array sementara
    int* L = new int[n1];
    int* R = new int[n2];
    
    // Copy data ke array sementara
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    // Merge kembali ke arr[]
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    // Copy sisa elemen
    while (i < n1) {
        arr[k] = L[i];
        i++; k++;
    }
    while (j < n2) {
        arr[k] = R[j];
        j++; k++;
    }
    
    delete[] L;
    delete[] R;
}

// Fungsi rekursif Merge Sort
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        // Divide: cari titik tengah
        int mid = left + (right - left) / 2;
        
        // Conquer: sort kedua bagian
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        
        // Combine: merge hasil
        merge(arr, left, mid, right);
    }
}

void printArray(int arr[], int n) {
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
}

int main() {
    int arr[] = {38, 27, 43, 3, 9, 82, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    cout << "Array awal: ";
    printArray(arr, n);
    
    mergeSort(arr, 0, n - 1);
    
    cout << "Array setelah sort: ";
    printArray(arr, n);
    
    return 0;
}
```

**Output:**
```
Array awal: 38 27 43 3 9 82 10 
Array setelah sort: 3 9 10 27 38 43 82 
```

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Soal:** Dalam sistem radar pertahanan, data deteksi disimpan dalam array terurut berdasarkan waktu. Implementasikan fungsi untuk mencari range waktu tertentu menggunakan binary search.

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Deteksi {
    int waktu;      // timestamp dalam detik
    string objek;   // jenis objek terdeteksi
};

// Cari index pertama >= target
int lowerBound(Deteksi arr[], int n, int target) {
    int left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid].waktu < target)
            left = mid + 1;
        else
            right = mid;
    }
    return left;
}

// Cari index pertama > target
int upperBound(Deteksi arr[], int n, int target) {
    int left = 0, right = n;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (arr[mid].waktu <= target)
            left = mid + 1;
        else
            right = mid;
    }
    return left;
}

// Cetak deteksi dalam range waktu
void cariDalamRange(Deteksi arr[], int n, int waktuMulai, int waktuAkhir) {
    int start = lowerBound(arr, n, waktuMulai);
    int end = upperBound(arr, n, waktuAkhir);
    
    cout << "Deteksi dari waktu " << waktuMulai << " sampai " << waktuAkhir << ":" << endl;
    for (int i = start; i < end; i++) {
        cout << "  Waktu: " << arr[i].waktu << ", Objek: " << arr[i].objek << endl;
    }
    cout << "Total: " << (end - start) << " deteksi" << endl;
}

int main() {
    Deteksi data[] = {
        {100, "Pesawat"},
        {150, "Drone"},
        {200, "Pesawat"},
        {250, "Helikopter"},
        {300, "Drone"},
        {350, "Pesawat"},
        {400, "Drone"}
    };
    int n = 7;
    
    // Cari deteksi antara waktu 150 dan 300
    cariDalamRange(data, n, 150, 300);
    
    return 0;
}
```

**Output:**
```
Deteksi dari waktu 150 sampai 300:
  Waktu: 150, Objek: Drone
  Waktu: 200, Objek: Pesawat
  Waktu: 250, Objek: Helikopter
  Waktu: 300, Objek: Drone
Total: 4 deteksi
```

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Implementasikan fungsi untuk menghasilkan semua kombinasi elemen dari sebuah array menggunakan rekursi.

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
using namespace std;

void generateCombinations(int arr[], int n, int start, vector<int>& current) {
    // Cetak kombinasi saat ini (jika tidak kosong)
    if (!current.empty()) {
        cout << "{ ";
        for (int i = 0; i < current.size(); i++) {
            cout << current[i];
            if (i < current.size() - 1) cout << ", ";
        }
        cout << " }" << endl;
    }
    
    // Generate kombinasi dengan menambahkan setiap elemen yang tersisa
    for (int i = start; i < n; i++) {
        current.push_back(arr[i]);
        generateCombinations(arr, n, i + 1, current);
        current.pop_back();  // Backtrack
    }
}

int main() {
    int arr[] = {1, 2, 3};
    int n = 3;
    vector<int> current;
    
    cout << "Semua kombinasi dari {1, 2, 3}:" << endl;
    generateCombinations(arr, n, 0, current);
    
    return 0;
}
```

**Output:**
```
Semua kombinasi dari {1, 2, 3}:
{ 1 }
{ 1, 2 }
{ 1, 2, 3 }
{ 1, 3 }
{ 2 }
{ 2, 3 }
{ 3 }
```

---

## 10. Supplementary Problems

### Problem S1 ⭐
Tuliskan fungsi rekursif untuk membalik sebuah string. Apa kompleksitasnya?

**Jawaban:**
```cpp
string reverseString(string s, int left, int right) {
    if (left >= right) return s;
    swap(s[left], s[right]);
    return reverseString(s, left + 1, right - 1);
}
```
Kompleksitas: O(n) waktu, O(n) space untuk call stack.

### Problem S2 ⭐
Gunakan Master Theorem untuk menentukan kompleksitas T(n) = 9T(n/3) + n.

**Jawaban:**
- a = 9, b = 3, f(n) = n
- log₃(9) = 2, jadi n^(log_b(a)) = n²
- f(n) = n = O(n^(2-1)), Kasus 1
- T(n) = Θ(n²)

### Problem S3 ⭐⭐
Berapa langkah minimum untuk Tower of Hanoi dengan 10 disk?

**Jawaban:**
- Langkah = 2^n - 1 = 2^10 - 1 = 1024 - 1 = **1023 langkah**

### Problem S4 ⭐⭐
Konversikan fungsi sum 1 sampai n dari rekursif menjadi tail recursive.

**Jawaban:**
```cpp
// Non-tail
int sumN(int n) {
    if (n == 0) return 0;
    return n + sumN(n - 1);
}

// Tail recursive
int sumNTail(int n, int acc = 0) {
    if (n == 0) return acc;
    return sumNTail(n - 1, acc + n);
}
```

### Problem S5 ⭐⭐⭐
Jelaskan mengapa memoization efektif untuk Fibonacci tapi tidak untuk faktorial?

**Jawaban:**
- Fibonacci memiliki **overlapping subproblems**: fib(n-1) dan fib(n-2) berbagi banyak subproblem yang sama
- Faktorial **tidak memiliki** overlapping subproblems: faktorial(n-1) hanya dipanggil sekali dan tidak ada nilai yang dihitung ulang
- Memoization hanya bermanfaat jika ada perhitungan berulang yang bisa dihindari

---

## Ringkasan

| Topik | Konsep Kunci | Kompleksitas |
|-------|--------------|--------------|
| **Rekursi** | Base case + Recursive case | Tergantung algoritma |
| **Recurrence Relation** | T(n) = aT(n/b) + f(n) | - |
| **Master Theorem** | 3 kasus berdasarkan perbandingan | - |
| **Tail Recursion** | Rekursi sebagai operasi terakhir | O(1) space dengan TCO |
| **Memoization** | Simpan hasil yang sudah dihitung | Reduce dari O(2^n) ke O(n) |
| **Divide-and-Conquer** | Divide → Conquer → Combine | Biasanya O(n log n) |
| **Binary Search** | Bagi search space menjadi setengah | O(log n) |
| **Tower of Hanoi** | Pindahkan n-1, pindah 1, pindahkan n-1 | O(2^n) |
| **Rekursi → Iterasi** | Gunakan stack eksplisit | Sama, tapi efisien |

### Tabel Perbandingan Kompleksitas

| Algoritma | Waktu | Ruang (Rekursif) | Ruang (Iteratif) |
|-----------|-------|------------------|------------------|
| Fibonacci Naive | O(2^n) | O(n) | - |
| Fibonacci Memo | O(n) | O(n) | O(n) |
| Fibonacci Tail | O(n) | O(1)* | O(1) |
| Binary Search | O(log n) | O(log n) | O(1) |
| Merge Sort | O(n log n) | O(n + log n) | O(n) |
| Tower of Hanoi | O(2^n) | O(n) | O(n) |

*dengan Tail Call Optimization

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 4.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 1.3.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 4.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
