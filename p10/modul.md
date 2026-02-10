# Modul 10: Algoritma Sorting Lanjut

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 10  
**Topik:** Algoritma Sorting (Bagian 2) - Sorting Lanjut

> **Capaian Pembelajaran:** Sub-CPMK-4.2, Sub-CPMK-4.3 — Mampu mengimplementasikan algoritma sorting lanjut (merge sort, quick sort) dan membandingkan serta memilih algoritma sorting berdasarkan karakteristik data

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.7-8; Weiss Ch.7.4-7.7; Hubbard Ch.13

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** prinsip divide-and-conquer dalam konteks algoritma sorting
2. **Mengimplementasikan** algoritma merge sort dengan benar
3. **Menganalisis** kompleksitas waktu dan ruang merge sort
4. **Mengimplementasikan** algoritma quick sort dengan berbagai strategi pemilihan pivot
5. **Membandingkan** performa merge sort dan quick sort dalam berbagai skenario
6. **Memahami** lower bound Ω(n log n) untuk comparison-based sorting
7. **Memilih** algoritma sorting yang tepat berdasarkan karakteristik data dan kebutuhan aplikasi

---

## 1. Pendahuluan Sorting Lanjut

### 1.1 Keterbatasan Sorting Dasar

Pada Pertemuan 9, kita telah mempelajari algoritma sorting dasar: bubble sort, selection sort, dan insertion sort. Ketiga algoritma tersebut memiliki kompleksitas waktu **O(n²)** pada kasus rata-rata dan terburuk.

Untuk dataset yang besar (misalnya jutaan elemen), kompleksitas O(n²) menjadi tidak praktis:

| Jumlah Elemen (n) | O(n²) Operasi | O(n log n) Operasi | Rasio |
|-------------------|---------------|---------------------|-------|
| 1,000 | 1,000,000 | ~10,000 | 100× |
| 10,000 | 100,000,000 | ~133,000 | 750× |
| 1,000,000 | 1,000,000,000,000 | ~20,000,000 | 50,000× |

Dalam konteks sistem pertahanan, bayangkan mengurutkan data radar yang mendeteksi ribuan objek terbang. Algoritma O(n²) akan terlalu lambat untuk pengolahan real-time.

### 1.2 Paradigma Divide-and-Conquer

> **Definisi:** Divide-and-conquer adalah paradigma desain algoritma yang memecah masalah besar menjadi sub-masalah yang lebih kecil, menyelesaikan sub-masalah secara rekursif, kemudian menggabungkan solusi sub-masalah menjadi solusi masalah asal.

Tiga langkah utama divide-and-conquer:

1. **Divide (Bagi)**: Pecah masalah menjadi sub-masalah yang lebih kecil
2. **Conquer (Taklukkan)**: Selesaikan sub-masalah secara rekursif
3. **Combine (Gabung)**: Gabungkan solusi sub-masalah menjadi solusi akhir

![Paradigma Divide-and-Conquer](images/gambar-10-1.png)

*Gambar 10.1: Ilustrasi paradigma divide-and-conquer*

### 1.3 Algoritma Sorting O(n log n)

Dengan paradigma divide-and-conquer, kita dapat mencapai kompleksitas **O(n log n)**, yang jauh lebih efisien untuk dataset besar. Dua algoritma utama yang akan kita pelajari:

| Algoritma | Kompleksitas Waktu | Kompleksitas Ruang | Stable | In-place |
|-----------|-------------------|-------------------|--------|----------|
| **Merge Sort** | O(n log n) selalu | O(n) | Ya | Tidak |
| **Quick Sort** | O(n log n) rata-rata | O(log n) | Tidak | Ya |

---

## 2. Merge Sort

### 2.1 Konsep Merge Sort

> **Definisi:** Merge sort adalah algoritma sorting yang menggunakan strategi divide-and-conquer dengan membagi array menjadi dua bagian, mengurutkan masing-masing bagian secara rekursif, kemudian menggabungkan (merge) kedua bagian yang sudah terurut.

**Langkah-langkah Merge Sort:**

1. **Divide**: Bagi array menjadi dua bagian yang sama besar
2. **Conquer**: Urutkan kedua bagian secara rekursif dengan merge sort
3. **Combine**: Gabungkan (merge) kedua bagian yang sudah terurut

![Proses Merge Sort](images/gambar-10-2.png)

*Gambar 10.2: Visualisasi proses merge sort pada array [38, 27, 43, 3, 9, 82, 10]*

### 2.2 Algoritma Merge

Operasi **merge** adalah inti dari merge sort. Fungsi ini menggabungkan dua array yang sudah terurut menjadi satu array terurut.

```cpp
void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;  // Ukuran subarray kiri
    int n2 = right - mid;      // Ukuran subarray kanan
    
    // Buat array temporary
    int* L = new int[n1];
    int* R = new int[n2];
    
    // Copy data ke array temporary
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    // Merge kembali ke arr[left..right]
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
    
    // Copy sisa elemen L[] jika ada
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    
    // Copy sisa elemen R[] jika ada
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
    
    delete[] L;
    delete[] R;
}
```

### 2.3 Implementasi Merge Sort

```cpp
void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        // Cari titik tengah untuk membagi array
        int mid = left + (right - left) / 2;
        
        // Urutkan kedua bagian secara rekursif
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        
        // Gabungkan kedua bagian yang sudah terurut
        merge(arr, left, mid, right);
    }
}

// Fungsi wrapper untuk kemudahan penggunaan
void mergeSort(int arr[], int n) {
    mergeSort(arr, 0, n - 1);
}
```

### 2.4 Analisis Kompleksitas Merge Sort

**Kompleksitas Waktu:**

Recurrence relation untuk merge sort:
```
T(n) = 2T(n/2) + O(n)
```

Menggunakan Master Theorem:
- a = 2, b = 2, f(n) = O(n)
- n^(log_b(a)) = n^(log_2(2)) = n^1 = n
- Karena f(n) = Θ(n^(log_b(a))), maka **T(n) = O(n log n)**

| Kasus | Kompleksitas |
|-------|-------------|
| Best Case | O(n log n) |
| Average Case | O(n log n) |
| Worst Case | O(n log n) |

**Kompleksitas Ruang:** O(n) untuk array temporary dalam proses merge.

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Tunjukkan langkah-langkah merge sort untuk array [5, 2, 8, 1]!

**Penyelesaian:**

**Langkah 1 - Divide:**
```
[5, 2, 8, 1]
    ↓
[5, 2] dan [8, 1]
    ↓
[5] [2] dan [8] [1]  ← Base case tercapai
```

**Langkah 2 - Merge (bottom-up):**
```
Merge [5] dan [2]:
- Bandingkan 5 dan 2 → pilih 2
- Sisa 5
- Hasil: [2, 5]

Merge [8] dan [1]:
- Bandingkan 8 dan 1 → pilih 1
- Sisa 8
- Hasil: [1, 8]

Merge [2, 5] dan [1, 8]:
- Bandingkan 2 dan 1 → pilih 1
- Bandingkan 2 dan 8 → pilih 2
- Bandingkan 5 dan 8 → pilih 5
- Sisa 8
- Hasil: [1, 2, 5, 8] ✓
```

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Berapa jumlah perbandingan yang dilakukan saat merge dua subarray [1, 3, 5] dan [2, 4, 6]?

**Penyelesaian:**

Proses merge:
```
L = [1, 3, 5], R = [2, 4, 6]
i = 0, j = 0

Perbandingan 1: L[0]=1 vs R[0]=2 → pilih 1, i++
Perbandingan 2: L[1]=3 vs R[0]=2 → pilih 2, j++
Perbandingan 3: L[1]=3 vs R[1]=4 → pilih 3, i++
Perbandingan 4: L[2]=5 vs R[1]=4 → pilih 4, j++
Perbandingan 5: L[2]=5 vs R[2]=6 → pilih 5, i++
(L habis, copy sisa R)
```

**Jawaban:** 5 perbandingan

**Catatan:** Untuk merge dua array dengan ukuran n1 dan n2, jumlah perbandingan maksimum adalah n1 + n2 - 1.

---

### SOLVED PROBLEM 3 ⭐

**Soal:** Apa yang terjadi jika kita mengganti kondisi `L[i] <= R[j]` menjadi `L[i] < R[j]` dalam fungsi merge?

**Penyelesaian:**

Dengan mengubah `<=` menjadi `<`, algoritma tetap benar (menghasilkan array terurut), **tetapi merge sort akan menjadi tidak stable**.

**Stable sort** berarti elemen dengan nilai sama mempertahankan urutan relatif aslinya.

Contoh:
```
Array asal: [(A,5), (B,3), (C,5)]  // (nama, nilai)
L = [(A,5)], R = [(C,5)]

Dengan <=: A diambil dulu → [(A,5), (C,5)] ✓ Stable
Dengan <:  C diambil dulu → [(C,5), (A,5)] ✗ Tidak stable
```

Dalam aplikasi seperti mengurutkan data mahasiswa berdasarkan nilai, stabilitas penting untuk mempertahankan urutan alfabet jika nilai sama.

---

### SOLVED PROBLEM 4 ⭐⭐

**Soal:** Implementasikan merge sort untuk mengurutkan array dalam urutan menurun (descending)!

**Penyelesaian:**

```cpp
void mergeDescending(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    
    int* L = new int[n1];
    int* R = new int[n2];
    
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    
    int i = 0, j = 0, k = left;
    
    while (i < n1 && j < n2) {
        // Ubah kondisi: ambil yang LEBIH BESAR
        if (L[i] >= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
    
    delete[] L;
    delete[] R;
}

void mergeSortDescending(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSortDescending(arr, left, mid);
        mergeSortDescending(arr, mid + 1, right);
        mergeDescending(arr, left, mid, right);
    }
}
```

**Perubahan kunci:** Pada fungsi merge, kondisi `L[i] <= R[j]` diubah menjadi `L[i] >= R[j]` agar elemen yang lebih besar dipilih terlebih dahulu.

---

### SOLVED PROBLEM 5 ⭐⭐

**Soal:** Hitunglah jumlah rekursi dan operasi merge yang terjadi saat merge sort memproses array dengan 8 elemen!

**Penyelesaian:**

Untuk n = 8 elemen:

**Struktur rekursi (pohon rekursi):**
```
Level 0: mergeSort(0-7)                    → 1 panggilan
Level 1: mergeSort(0-3), mergeSort(4-7)    → 2 panggilan
Level 2: mergeSort(0-1), (2-3), (4-5), (6-7) → 4 panggilan
Level 3: 8 panggilan untuk single element    → 8 panggilan
```

**Total panggilan rekursif:** 1 + 2 + 4 + 8 = **15 panggilan**

**Jumlah operasi merge:**
- Level 2→1: 4 merge (masing-masing 2 elemen) = 4 operasi merge
- Level 1→0: 2 merge (masing-masing 4 elemen) = 2 operasi merge
- Level 0: 1 merge (8 elemen) = 1 operasi merge

**Total operasi merge:** 4 + 2 + 1 = **7 operasi merge**

**Formula umum:**
- Total panggilan rekursif: 2n - 1
- Total operasi merge: n - 1

---

## 3. Quick Sort

### 3.1 Konsep Quick Sort

> **Definisi:** Quick sort adalah algoritma sorting divide-and-conquer yang memilih sebuah elemen sebagai pivot, kemudian mempartisi array sehingga elemen yang lebih kecil dari pivot berada di kiri dan yang lebih besar di kanan.

**Langkah-langkah Quick Sort:**

1. **Pilih Pivot**: Pilih satu elemen sebagai pivot
2. **Partition**: Susun ulang array sehingga:
   - Semua elemen < pivot berada di kiri pivot
   - Semua elemen > pivot berada di kanan pivot
3. **Rekursi**: Terapkan quick sort pada subarray kiri dan kanan

![Proses Quick Sort](images/gambar-10-3.png)

*Gambar 10.3: Visualisasi proses quick sort dengan pivot terakhir*

### 3.2 Algoritma Partition

Fungsi partition adalah jantung dari quick sort. Berikut implementasi dengan skema Lomuto (pivot di akhir):

```cpp
int partition(int arr[], int low, int high) {
    int pivot = arr[high];  // Pilih elemen terakhir sebagai pivot
    int i = low - 1;        // Index elemen terkecil
    
    for (int j = low; j < high; j++) {
        // Jika elemen saat ini lebih kecil dari pivot
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    
    // Letakkan pivot di posisi yang benar
    swap(arr[i + 1], arr[high]);
    return i + 1;  // Return posisi pivot
}
```

**Ilustrasi proses partition:**

![Proses Partition](images/gambar-10-4.png)

*Gambar 10.4: Langkah-langkah proses partition dengan skema Lomuto*

### 3.3 Implementasi Quick Sort

```cpp
void quickSort(int arr[], int low, int high) {
    if (low < high) {
        // Partition dan dapatkan posisi pivot
        int pi = partition(arr, low, high);
        
        // Rekursif pada subarray kiri dan kanan
        quickSort(arr, low, pi - 1);   // Elemen sebelum pivot
        quickSort(arr, pi + 1, high);  // Elemen setelah pivot
    }
}

// Fungsi wrapper
void quickSort(int arr[], int n) {
    quickSort(arr, 0, n - 1);
}
```

### 3.4 Strategi Pemilihan Pivot

Pemilihan pivot sangat mempengaruhi performa quick sort:

| Strategi | Deskripsi | Kelebihan | Kekurangan |
|----------|-----------|-----------|------------|
| **First** | Pilih elemen pertama | Simpel | Buruk untuk data terurut |
| **Last** | Pilih elemen terakhir | Simpel | Buruk untuk data terurut |
| **Random** | Pilih elemen acak | Rata-rata baik | Overhead random |
| **Median-of-Three** | Median dari first, middle, last | Hindari worst case | Sedikit lebih kompleks |

**Implementasi Median-of-Three:**

```cpp
int medianOfThree(int arr[], int low, int high) {
    int mid = low + (high - low) / 2;
    
    // Urutkan arr[low], arr[mid], arr[high]
    if (arr[low] > arr[mid])
        swap(arr[low], arr[mid]);
    if (arr[low] > arr[high])
        swap(arr[low], arr[high]);
    if (arr[mid] > arr[high])
        swap(arr[mid], arr[high]);
    
    // Pindahkan median ke posisi high-1
    swap(arr[mid], arr[high - 1]);
    return arr[high - 1];
}

int partitionMedian(int arr[], int low, int high) {
    int pivot = medianOfThree(arr, low, high);
    int i = low;
    int j = high - 1;
    
    while (true) {
        while (arr[++i] < pivot);
        while (arr[--j] > pivot);
        if (i >= j) break;
        swap(arr[i], arr[j]);
    }
    swap(arr[i], arr[high - 1]);
    return i;
}
```

### 3.5 Analisis Kompleksitas Quick Sort

**Kompleksitas Waktu:**

| Kasus | Kondisi | Kompleksitas |
|-------|---------|--------------|
| Best Case | Pivot selalu membagi array menjadi dua bagian sama | O(n log n) |
| Average Case | Pivot membagi secara "cukup baik" | O(n log n) |
| Worst Case | Pivot selalu terkecil/terbesar (array sudah terurut) | O(n²) |

**Recurrence untuk kasus terbaik:**
```
T(n) = 2T(n/2) + O(n) = O(n log n)
```

**Recurrence untuk kasus terburuk:**
```
T(n) = T(n-1) + O(n) = O(n²)
```

**Kompleksitas Ruang:** O(log n) untuk call stack dalam kasus rata-rata.

---

### SOLVED PROBLEM 6 ⭐

**Soal:** Lakukan partition pada array [7, 2, 1, 6, 8, 5, 3, 4] dengan pivot = 4 (elemen terakhir)!

**Penyelesaian:**

```
Array awal: [7, 2, 1, 6, 8, 5, 3, 4]
pivot = 4, i = -1

j=0: arr[0]=7 > 4, tidak swap
     [7, 2, 1, 6, 8, 5, 3, 4], i=-1

j=1: arr[1]=2 < 4, i++, swap(arr[0], arr[1])
     [2, 7, 1, 6, 8, 5, 3, 4], i=0

j=2: arr[2]=1 < 4, i++, swap(arr[1], arr[2])
     [2, 1, 7, 6, 8, 5, 3, 4], i=1

j=3: arr[3]=6 > 4, tidak swap
     [2, 1, 7, 6, 8, 5, 3, 4], i=1

j=4: arr[4]=8 > 4, tidak swap
     [2, 1, 7, 6, 8, 5, 3, 4], i=1

j=5: arr[5]=5 > 4, tidak swap
     [2, 1, 7, 6, 8, 5, 3, 4], i=1

j=6: arr[6]=3 < 4, i++, swap(arr[2], arr[6])
     [2, 1, 3, 6, 8, 5, 7, 4], i=2

Akhir: swap(arr[i+1], arr[high]) = swap(arr[3], arr[7])
       [2, 1, 3, 4, 8, 5, 7, 6]
                 ↑
              pivot di posisi 3
```

**Hasil:** Array setelah partition: [2, 1, 3, 4, 8, 5, 7, 6], pivot index = 3

---

### SOLVED PROBLEM 7 ⭐

**Soal:** Mengapa quick sort memiliki worst case O(n²) pada array yang sudah terurut jika menggunakan pivot pertama atau terakhir?

**Penyelesaian:**

Misalkan array [1, 2, 3, 4, 5] dengan pivot terakhir:

**Iterasi 1:**
- pivot = 5, semua elemen < 5
- Hasil partition: [1, 2, 3, 4, 5] dengan pivot di posisi 4
- Subarray kiri: [1, 2, 3, 4] (4 elemen)
- Subarray kanan: kosong

**Iterasi 2:**
- pivot = 4, semua elemen < 4
- Hasil: [1, 2, 3, 4]
- Subarray kiri: [1, 2, 3] (3 elemen)
- Subarray kanan: kosong

**Pola:** Setiap kali, hanya 1 elemen yang "diproses" (pivot), sisanya masuk ke satu subarray.

**Total perbandingan:**
- Partition 1: n-1 perbandingan
- Partition 2: n-2 perbandingan
- ...
- Partition n-1: 1 perbandingan

Total = (n-1) + (n-2) + ... + 1 = **n(n-1)/2 = O(n²)**

**Solusi:** Gunakan random pivot atau median-of-three untuk menghindari kasus ini.

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Implementasikan quick sort dengan random pivot selection!

**Penyelesaian:**

```cpp
#include <cstdlib>
#include <ctime>

int randomPartition(int arr[], int low, int high) {
    // Generate random index antara low dan high
    int randomIndex = low + rand() % (high - low + 1);
    
    // Tukar elemen random dengan elemen terakhir
    swap(arr[randomIndex], arr[high]);
    
    // Lakukan partition biasa dengan pivot di akhir
    return partition(arr, low, high);
}

void quickSortRandom(int arr[], int low, int high) {
    if (low < high) {
        int pi = randomPartition(arr, low, high);
        quickSortRandom(arr, low, pi - 1);
        quickSortRandom(arr, pi + 1, high);
    }
}

int main() {
    srand(time(0));  // Seed random number generator
    
    int arr[] = {10, 7, 8, 9, 1, 5};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    quickSortRandom(arr, 0, n - 1);
    
    cout << "Array terurut: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    
    return 0;
}
```

**Output:**
```
Array terurut: 1 5 7 8 9 10
```

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Hitunglah kedalaman rekursi maksimum quick sort untuk array dengan n=16 elemen dalam kasus terbaik dan terburuk!

**Penyelesaian:**

**Kasus Terbaik (partition selalu di tengah):**
```
Level 0: 16 elemen
Level 1: 2 × 8 elemen
Level 2: 4 × 4 elemen
Level 3: 8 × 2 elemen
Level 4: 16 × 1 elemen (base case)
```
Kedalaman maksimum = log₂(16) = **4 level**

**Kasus Terburuk (partition selalu di ujung):**
```
Level 0: 16 elemen → pivot di posisi 0 atau 15
Level 1: 15 elemen
Level 2: 14 elemen
...
Level 15: 1 elemen (base case)
```
Kedalaman maksimum = 16 - 1 = **15 level**

**Implikasi:**
- Kasus terbaik: Stack depth O(log n) → efisien
- Kasus terburuk: Stack depth O(n) → bisa menyebabkan stack overflow untuk n besar

---

### SOLVED PROBLEM 10 ⭐⭐

**Soal:** Modifikasi quick sort agar menggunakan insertion sort untuk subarray yang ukurannya kurang dari threshold tertentu (hybrid sorting)!

**Penyelesaian:**

```cpp
const int THRESHOLD = 10;  // Threshold untuk switch ke insertion sort

void insertionSort(int arr[], int low, int high) {
    for (int i = low + 1; i <= high; i++) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= low && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

void hybridQuickSort(int arr[], int low, int high) {
    // Jika subarray kecil, gunakan insertion sort
    if (high - low + 1 <= THRESHOLD) {
        insertionSort(arr, low, high);
        return;
    }
    
    if (low < high) {
        int pi = partition(arr, low, high);
        hybridQuickSort(arr, low, pi - 1);
        hybridQuickSort(arr, pi + 1, high);
    }
}
```

**Alasan efektif:**
1. Insertion sort sangat efisien untuk array kecil (overhead rendah)
2. Mengurangi jumlah panggilan rekursif
3. Memanfaatkan cache locality yang lebih baik untuk array kecil

Teknik ini digunakan dalam implementasi quick sort di library standar seperti `std::sort` di C++.

---

## 4. Perbandingan Merge Sort dan Quick Sort

### 4.1 Perbandingan Karakteristik

| Aspek | Merge Sort | Quick Sort |
|-------|------------|------------|
| **Kompleksitas Waktu (Worst)** | O(n log n) | O(n²) |
| **Kompleksitas Waktu (Average)** | O(n log n) | O(n log n) |
| **Kompleksitas Ruang** | O(n) | O(log n) |
| **Stable** | Ya | Tidak |
| **In-place** | Tidak | Ya |
| **Cache Efficiency** | Kurang baik | Lebih baik |
| **Parallelizable** | Sangat baik | Cukup baik |

### 4.2 Kapan Menggunakan Masing-masing

**Gunakan Merge Sort ketika:**
- Stabilitas diperlukan
- Data diakses secara sequential (linked list, external sort)
- Worst case yang terjamin O(n log n) diperlukan
- Memori bukan masalah
- Sorting data di external storage (disk)

**Gunakan Quick Sort ketika:**
- Memori terbatas (in-place sorting)
- Data di internal memory (RAM)
- Performa rata-rata yang baik lebih penting
- Cache efficiency penting
- Random access tersedia

![Perbandingan Merge Sort vs Quick Sort](images/gambar-10-5.png)

*Gambar 10.5: Perbandingan karakteristik merge sort dan quick sort*

### 4.3 Performa Empiris

Dalam praktik, quick sort sering **lebih cepat** dari merge sort meskipun keduanya O(n log n) karena:

1. **Faktor konstan lebih kecil**: Quick sort melakukan lebih sedikit operasi per elemen
2. **Cache locality**: Quick sort bekerja pada segmen array yang berdekatan
3. **In-place**: Tidak perlu alokasi memori tambahan

---

### SOLVED PROBLEM 11 ⭐

**Soal:** Sebuah sistem radar perlu mengurutkan 10.000 objek berdasarkan jarak. Objek dengan jarak sama harus mempertahankan urutan waktu deteksi. Algoritma mana yang lebih tepat?

**Penyelesaian:**

**Merge Sort** adalah pilihan yang tepat karena:

1. **Stabilitas diperlukan**: Objek dengan jarak sama harus mempertahankan urutan waktu deteksi → merge sort adalah stable sort

2. **Kompleksitas terjamin**: Dalam sistem radar real-time, kita tidak bisa mentolerir worst case O(n²) → merge sort menjamin O(n log n)

3. **Ukuran data**: 10.000 objek × misalnya 32 byte per objek = 320 KB, masih manageable untuk overhead memori O(n)

Quick sort tidak cocok karena:
- Tidak stable → objek dengan jarak sama bisa berubah urutannya
- Worst case O(n²) bisa terjadi pada kondisi tertentu

---

### SOLVED PROBLEM 12 ⭐⭐

**Soal:** Bandingkan jumlah operasi swap antara merge sort dan quick sort untuk array [3, 1, 4, 1, 5, 9, 2, 6]!

**Penyelesaian:**

**Merge Sort:**
Merge sort tidak menggunakan swap secara langsung, melainkan copy ke array temporary dan copy kembali.

Total "move" operations:
- Setiap level memproses n elemen
- Ada log₂(8) = 3 level merge
- Total: 8 × 3 × 2 = **48 operasi copy** (ke temp dan kembali)

**Quick Sort (pivot terakhir):**
Mari trace:
```
[3, 1, 4, 1, 5, 9, 2, 6], pivot=6
Partition: [3, 1, 4, 1, 5, 2, 6, 9] → 2 swaps (2↔9, 6↔di posisi)

[3, 1, 4, 1, 5, 2], pivot=2
Partition: [1, 1, 2, 4, 5, 3] → 3 swaps

[1, 1], pivot=1: 1 swap
[4, 5, 3], pivot=3: 2 swaps
```

Total swaps (approximate): **8-10 swaps**

**Kesimpulan:** Quick sort melakukan lebih sedikit data movement, yang menjelaskan kenapa sering lebih cepat dalam praktik.

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Implementasikan versi iteratif dari quick sort menggunakan stack eksplisit!

**Penyelesaian:**

```cpp
#include <stack>
using namespace std;

void quickSortIterative(int arr[], int n) {
    // Stack untuk menyimpan pasangan (low, high)
    stack<pair<int, int>> stk;
    
    // Push range awal
    stk.push({0, n - 1});
    
    while (!stk.empty()) {
        // Pop range dari stack
        int low = stk.top().first;
        int high = stk.top().second;
        stk.pop();
        
        if (low < high) {
            // Partition
            int pi = partition(arr, low, high);
            
            // Push subarray yang lebih besar dulu (untuk efisiensi stack)
            // Ini memastikan subarray yang lebih kecil diproses dulu
            if (pi - low < high - pi) {
                // Subarray kiri lebih kecil
                stk.push({pi + 1, high});  // Push kanan dulu
                stk.push({low, pi - 1});   // Push kiri (diproses dulu)
            } else {
                // Subarray kanan lebih kecil
                stk.push({low, pi - 1});   // Push kiri dulu
                stk.push({pi + 1, high});  // Push kanan (diproses dulu)
            }
        }
    }
}
```

**Keuntungan versi iteratif:**
1. Menghindari stack overflow untuk array sangat besar
2. Optimasi: selalu proses subarray lebih kecil dulu → menjaga kedalaman stack minimal

---

## 5. Lower Bound untuk Comparison-Based Sorting

### 5.1 Decision Tree Model

> **Teorema:** Setiap algoritma comparison-based sorting memerlukan minimal **Ω(n log n)** perbandingan dalam kasus terburuk.

**Penjelasan:**
- Untuk n elemen, ada n! kemungkinan permutasi
- Setiap perbandingan membagi kemungkinan menjadi dua
- Decision tree dengan n! daun memerlukan kedalaman minimal log₂(n!)
- Menggunakan Stirling's approximation: log₂(n!) ≈ n log₂(n) - n log₂(e) = **Ω(n log n)**

![Decision Tree untuk Sorting](images/gambar-10-6.png)

*Gambar 10.6: Decision tree untuk sorting 3 elemen [a, b, c]*

### 5.2 Implikasi

| Algoritma | Mencapai Lower Bound? |
|-----------|----------------------|
| Bubble Sort | Tidak (O(n²)) |
| Selection Sort | Tidak (O(n²)) |
| Insertion Sort | Tidak (O(n²) worst) |
| **Merge Sort** | Ya (O(n log n)) |
| **Quick Sort** | Ya (O(n log n) average) |
| **Heap Sort** | Ya (O(n log n)) |

**Catatan:** Heap Sort akan dipelajari pada Pertemuan 13.

---

### SOLVED PROBLEM 14 ⭐

**Soal:** Berapa jumlah perbandingan minimum yang diperlukan untuk mengurutkan 5 elemen menggunakan comparison-based sorting?

**Penyelesaian:**

Untuk n = 5 elemen:
- Jumlah permutasi: 5! = 120
- Lower bound perbandingan: ⌈log₂(120)⌉ = ⌈6.9⌉ = **7 perbandingan**

**Verifikasi:**
- Dengan 7 perbandingan, kita bisa membedakan 2⁷ = 128 kemungkinan
- 128 ≥ 120 ✓
- Dengan 6 perbandingan: 2⁶ = 64 < 120 ✗

**Jawaban:** Minimal **7 perbandingan** diperlukan untuk mengurutkan 5 elemen.

---

### SOLVED PROBLEM 15 ⭐⭐

**Soal:** Jelaskan mengapa counting sort, radix sort, dan bucket sort dapat mencapai O(n) meskipun lower bound adalah Ω(n log n)!

**Penyelesaian:**

Lower bound Ω(n log n) berlaku **hanya untuk comparison-based sorting** — algoritma yang hanya menggunakan perbandingan antar elemen untuk menentukan urutan.

**Counting Sort, Radix Sort, Bucket Sort** bukan comparison-based:

1. **Counting Sort**: 
   - Tidak membandingkan elemen
   - Menghitung frekuensi setiap nilai
   - Memerlukan range nilai terbatas (k)
   - Kompleksitas: O(n + k)

2. **Radix Sort**:
   - Mengurutkan digit per digit
   - Menggunakan counting sort sebagai subroutine
   - Kompleksitas: O(d × (n + k)) dimana d = jumlah digit

3. **Bucket Sort**:
   - Mendistribusikan elemen ke bucket berdasarkan nilai
   - Mengurutkan setiap bucket
   - Kompleksitas: O(n) average dengan distribusi uniform

**Trade-off:** Algoritma non-comparison memerlukan asumsi tambahan tentang data (range terbatas, distribusi tertentu, dll).

---

## 6. Pemilihan Algoritma Sorting

### 6.1 Kriteria Pemilihan

Faktor yang perlu dipertimbangkan:

1. **Ukuran data (n)**: 
   - n kecil (< 50): Insertion sort sering lebih cepat
   - n besar: Quick sort atau merge sort

2. **Karakteristik data**:
   - Hampir terurut: Insertion sort
   - Random: Quick sort
   - Banyak duplikat: 3-way quick sort

3. **Kebutuhan stabilitas**:
   - Perlu stable: Merge sort
   - Tidak perlu: Quick sort

4. **Keterbatasan memori**:
   - Memori terbatas: Quick sort (in-place)
   - Memori cukup: Merge sort

5. **External vs Internal**:
   - Eksternal (disk): Merge sort
   - Internal (RAM): Quick sort

### 6.2 Flowchart Pemilihan

![Flowchart Pemilihan Algoritma](images/gambar-10-7.png)

*Gambar 10.7: Flowchart pemilihan algoritma sorting*

---

### SOLVED PROBLEM 16 ⭐

**Soal:** Sistem database militer perlu mengurutkan 10 juta record berdasarkan timestamp. Data disimpan di hard disk karena terlalu besar untuk RAM. Algoritma apa yang paling tepat?

**Penyelesaian:**

**Merge Sort** adalah pilihan terbaik untuk external sorting karena:

1. **Sequential access pattern**: Merge sort membaca dan menulis data secara berurutan, yang sangat efisien untuk disk (minimize seek time)

2. **Predictable I/O**: Pola akses dapat diprediksi, memungkinkan optimasi I/O

3. **Divide naturally**: Data dapat dibagi menjadi chunk yang fit di RAM, diurutkan di RAM, kemudian di-merge

**Proses External Merge Sort:**
```
1. Baca chunk data yang muat di RAM (misalnya 100MB)
2. Urutkan chunk di RAM dengan quick sort
3. Tulis sorted chunk ke disk (run)
4. Ulangi untuk semua data
5. Merge semua run secara bertahap
```

Quick sort tidak cocok karena memerlukan random access, yang sangat lambat pada disk.

---

### SOLVED PROBLEM 17 ⭐⭐

**Soal:** Implementasikan fungsi yang memilih algoritma sorting optimal berdasarkan karakteristik data!

**Penyelesaian:**

```cpp
#include <algorithm>
#include <cstdlib>

enum SortType { INSERTION, MERGE, QUICK };

// Hitung tingkat "keterurutan" data
double calculateSortedness(int arr[], int n) {
    int inversions = 0;
    for (int i = 0; i < n - 1; i++) {
        if (arr[i] > arr[i + 1]) {
            inversions++;
        }
    }
    return 1.0 - (double)inversions / (n - 1);
}

SortType selectSortingAlgorithm(int arr[], int n, 
                                 bool needStable, 
                                 bool memoryLimited) {
    // Kriteria 1: Ukuran kecil → insertion sort
    if (n < 50) {
        return INSERTION;
    }
    
    // Kriteria 2: Perlu stabilitas → merge sort
    if (needStable) {
        return MERGE;
    }
    
    // Kriteria 3: Data hampir terurut → insertion sort
    double sortedness = calculateSortedness(arr, n);
    if (sortedness > 0.9) {  // 90% terurut
        return INSERTION;
    }
    
    // Kriteria 4: Memori terbatas → quick sort
    if (memoryLimited) {
        return QUICK;
    }
    
    // Default: quick sort (biasanya tercepat)
    return QUICK;
}

void adaptiveSort(int arr[], int n, bool needStable = false, 
                  bool memoryLimited = false) {
    SortType type = selectSortingAlgorithm(arr, n, needStable, 
                                            memoryLimited);
    
    switch (type) {
        case INSERTION:
            insertionSort(arr, n);
            break;
        case MERGE:
            mergeSort(arr, 0, n - 1);
            break;
        case QUICK:
            quickSort(arr, 0, n - 1);
            break;
    }
}
```

---

### SOLVED PROBLEM 18 ⭐⭐⭐

**Soal:** Implementasikan 3-way quick sort untuk menangani array dengan banyak elemen duplikat secara efisien!

**Penyelesaian:**

3-way quick sort (Dutch National Flag) mempartisi array menjadi tiga bagian: < pivot, = pivot, > pivot.

```cpp
void threeWayPartition(int arr[], int low, int high, 
                       int& lt, int& gt) {
    int pivot = arr[low];  // Pilih pivot
    lt = low;              // arr[low..lt-1] < pivot
    gt = high;             // arr[gt+1..high] > pivot
    int i = low;           // arr[lt..i-1] = pivot
    
    while (i <= gt) {
        if (arr[i] < pivot) {
            swap(arr[lt], arr[i]);
            lt++;
            i++;
        } else if (arr[i] > pivot) {
            swap(arr[i], arr[gt]);
            gt--;
            // i tidak di-increment karena arr[i] baru perlu dicek
        } else {
            // arr[i] == pivot
            i++;
        }
    }
}

void quickSort3Way(int arr[], int low, int high) {
    if (low >= high) return;
    
    int lt, gt;
    threeWayPartition(arr, low, high, lt, gt);
    
    // arr[low..lt-1] < pivot
    // arr[lt..gt] = pivot (sudah di posisi benar)
    // arr[gt+1..high] > pivot
    
    quickSort3Way(arr, low, lt - 1);
    quickSort3Way(arr, gt + 1, high);
}
```

**Keunggulan untuk data dengan banyak duplikat:**
- Standard quick sort: semua duplikat pivot masuk ke satu sisi → tidak efisien
- 3-way: semua duplikat pivot langsung di posisi final → sangat efisien

**Contoh:** Array [4, 4, 4, 4, 4, 4, 4]
- Standard: O(n²) karena partition selalu tidak seimbang
- 3-way: O(n) karena semua elemen = pivot, langsung selesai

---

### SOLVED PROBLEM 19 ⭐⭐⭐

**Soal:** Analisis kompleksitas space untuk rekursi quick sort dan jelaskan teknik tail call optimization!

**Penyelesaian:**

**Kompleksitas Space Quick Sort:**

Standard recursive quick sort memerlukan O(n) space dalam worst case karena call stack.

```
Worst case (partition sangat tidak seimbang):
quickSort([1,2,3,...,n])
  └─ quickSort([1,2,3,...,n-1])
       └─ quickSort([1,2,3,...,n-2])
            └─ ...
                 └─ quickSort([1])
```

Stack depth: n-1 → **O(n) space**

**Tail Call Optimization:**

Kita bisa mengoptimasi dengan selalu melakukan rekursi pada subarray yang lebih kecil terlebih dahulu, dan menggunakan iterasi untuk yang lebih besar:

```cpp
void quickSortOptimized(int arr[], int low, int high) {
    while (low < high) {
        int pi = partition(arr, low, high);
        
        // Rekursi pada bagian yang lebih kecil
        // Iterasi (tail call) pada bagian yang lebih besar
        if (pi - low < high - pi) {
            // Subarray kiri lebih kecil
            quickSortOptimized(arr, low, pi - 1);
            low = pi + 1;  // "Tail call" menjadi iterasi
        } else {
            // Subarray kanan lebih kecil
            quickSortOptimized(arr, pi + 1, high);
            high = pi - 1;  // "Tail call" menjadi iterasi
        }
    }
}
```

**Hasil optimasi:**
- Selalu rekursi pada bagian ≤ n/2 elemen
- Stack depth maksimum: log₂(n)
- **Space complexity: O(log n)** bahkan dalam worst case partitioning

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Implementasikan parallel merge sort menggunakan threading untuk mempercepat sorting pada sistem multi-core!

**Penyelesaian:**

```cpp
#include <thread>
#include <vector>

const int PARALLEL_THRESHOLD = 10000;  // Minimum untuk paralel

void parallelMergeSort(int arr[], int left, int right, int depth = 0) {
    if (left >= right) return;
    
    int mid = left + (right - left) / 2;
    
    // Batasi kedalaman paralel untuk menghindari terlalu banyak thread
    // dan untuk array yang cukup besar
    if (depth < 3 && (right - left) > PARALLEL_THRESHOLD) {
        // Buat thread untuk subarray kiri
        thread leftThread(parallelMergeSort, arr, left, mid, depth + 1);
        
        // Proses subarray kanan di thread saat ini
        parallelMergeSort(arr, mid + 1, right, depth + 1);
        
        // Tunggu thread kiri selesai
        leftThread.join();
    } else {
        // Sequential untuk array kecil atau kedalaman sudah cukup
        parallelMergeSort(arr, left, mid, depth + 1);
        parallelMergeSort(arr, mid + 1, right, depth + 1);
    }
    
    // Merge (bisa juga diparalelkan untuk array sangat besar)
    merge(arr, left, mid, right);
}

int main() {
    const int n = 1000000;
    int* arr = new int[n];
    
    // Isi dengan data random
    for (int i = 0; i < n; i++) {
        arr[i] = rand();
    }
    
    auto start = chrono::high_resolution_clock::now();
    parallelMergeSort(arr, 0, n - 1);
    auto end = chrono::high_resolution_clock::now();
    
    auto duration = chrono::duration_cast<chrono::milliseconds>(end - start);
    cout << "Waktu: " << duration.count() << " ms" << endl;
    
    delete[] arr;
    return 0;
}
```

**Catatan penting:**
1. Hanya paralelkan untuk array cukup besar (overhead thread creation)
2. Batasi kedalaman paralel (2^depth thread)
3. Merge masih sequential dalam implementasi ini
4. Performa tergantung jumlah core CPU

---

### SOLVED PROBLEM 21 ⭐⭐

**Soal:** Sebuah sistem pertahanan udara perlu mengurutkan objek radar berdasarkan prioritas ancaman. Data meliputi: ID, jarak, kecepatan, jenis objek. Desain struktur data dan algoritma sorting yang optimal!

**Penyelesaian:**

```cpp
#include <iostream>
#include <cstring>
using namespace std;

struct ObjekRadar {
    int id;
    double jarak;        // km
    double kecepatan;    // km/jam
    char jenis[20];      // pesawat, rudal, drone, dll
    int prioritas;       // Dihitung berdasarkan faktor lain
    
    // Hitung prioritas ancaman
    void hitungPrioritas() {
        // Semakin dekat dan cepat = semakin berbahaya
        double timeToImpact = jarak / kecepatan;  // jam
        
        // Base priority dari waktu hingga impact
        prioritas = (int)(1000 / (timeToImpact + 0.001));
        
        // Modifier berdasarkan jenis
        if (strcmp(jenis, "rudal") == 0) {
            prioritas *= 3;
        } else if (strcmp(jenis, "jet_tempur") == 0) {
            prioritas *= 2;
        } else if (strcmp(jenis, "drone") == 0) {
            prioritas = (int)(prioritas * 1.5);
        }
    }
};

// Comparator untuk sorting descending (prioritas tinggi dulu)
bool comparePrioritas(const ObjekRadar& a, const ObjekRadar& b) {
    return a.prioritas > b.prioritas;
}

// Quick sort khusus untuk ObjekRadar
int partitionRadar(ObjekRadar arr[], int low, int high) {
    int pivot = arr[high].prioritas;
    int i = low - 1;
    
    for (int j = low; j < high; j++) {
        if (arr[j].prioritas > pivot) {  // Descending
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return i + 1;
}

void sortObjekRadar(ObjekRadar arr[], int low, int high) {
    if (low < high) {
        int pi = partitionRadar(arr, low, high);
        sortObjekRadar(arr, low, pi - 1);
        sortObjekRadar(arr, pi + 1, high);
    }
}

int main() {
    ObjekRadar objek[5] = {
        {1001, 50, 800, "rudal", 0},
        {1002, 100, 300, "pesawat", 0},
        {1003, 30, 600, "drone", 0},
        {1004, 80, 1200, "jet_tempur", 0},
        {1005, 150, 400, "helikopter", 0}
    };
    
    // Hitung prioritas
    for (int i = 0; i < 5; i++) {
        objek[i].hitungPrioritas();
    }
    
    // Urutkan berdasarkan prioritas
    sortObjekRadar(objek, 0, 4);
    
    // Tampilkan hasil
    cout << "=== PRIORITAS ANCAMAN ===" << endl;
    for (int i = 0; i < 5; i++) {
        cout << "Rank " << (i+1) << ": ID " << objek[i].id 
             << " | " << objek[i].jenis 
             << " | Jarak: " << objek[i].jarak << " km"
             << " | Kecepatan: " << objek[i].kecepatan << " km/jam"
             << " | Prioritas: " << objek[i].prioritas << endl;
    }
    
    return 0;
}
```

**Output (contoh):**
```
=== PRIORITAS ANCAMAN ===
Rank 1: ID 1001 | rudal | Jarak: 50 km | Kecepatan: 800 km/jam | Prioritas: 48000
Rank 2: ID 1004 | jet_tempur | Jarak: 80 km | Kecepatan: 1200 km/jam | Prioritas: 30000
Rank 3: ID 1003 | drone | Jarak: 30 km | Kecepatan: 600 km/jam | Prioritas: 30000
Rank 4: ID 1002 | pesawat | Jarak: 100 km | Kecepatan: 300 km/jam | Prioritas: 3000
Rank 5: ID 1005 | helikopter | Jarak: 150 km | Kecepatan: 400 km/jam | Prioritas: 2666
```

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Implementasikan Introsort (introspective sort) yang menggabungkan quick sort, heap sort, dan insertion sort untuk performa optimal di semua kasus!

**Penyelesaian:**

Introsort adalah algoritma yang digunakan dalam `std::sort` C++:

```cpp
#include <cmath>
#include <algorithm>

// Insertion sort untuk array kecil
void insertionSortRange(int arr[], int low, int high) {
    for (int i = low + 1; i <= high; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= low && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// Heapify untuk heap sort
void heapify(int arr[], int n, int i, int offset) {
    int largest = i;
    int left = 2 * i + 1;
    int right = 2 * i + 2;
    
    if (left < n && arr[offset + left] > arr[offset + largest])
        largest = left;
    if (right < n && arr[offset + right] > arr[offset + largest])
        largest = right;
    
    if (largest != i) {
        swap(arr[offset + i], arr[offset + largest]);
        heapify(arr, n, largest, offset);
    }
}

// Heap sort untuk subarray
void heapSortRange(int arr[], int low, int high) {
    int n = high - low + 1;
    
    // Build heap
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(arr, n, i, low);
    
    // Extract elements
    for (int i = n - 1; i > 0; i--) {
        swap(arr[low], arr[low + i]);
        heapify(arr, i, 0, low);
    }
}

// Median of three
int medianOfThreeIntro(int arr[], int low, int high) {
    int mid = low + (high - low) / 2;
    
    if (arr[mid] < arr[low])
        swap(arr[mid], arr[low]);
    if (arr[high] < arr[low])
        swap(arr[high], arr[low]);
    if (arr[high] < arr[mid])
        swap(arr[high], arr[mid]);
    
    return arr[mid];
}

// Partition untuk introsort
int partitionIntro(int arr[], int low, int high) {
    int pivot = medianOfThreeIntro(arr, low, high);
    int i = low - 1;
    int j = high + 1;
    
    while (true) {
        do { i++; } while (arr[i] < pivot);
        do { j--; } while (arr[j] > pivot);
        
        if (i >= j) return j;
        swap(arr[i], arr[j]);
    }
}

const int SIZE_THRESHOLD = 16;  // Threshold untuk insertion sort

void introsortUtil(int arr[], int low, int high, int depthLimit) {
    int size = high - low + 1;
    
    // Gunakan insertion sort untuk array kecil
    if (size < SIZE_THRESHOLD) {
        insertionSortRange(arr, low, high);
        return;
    }
    
    // Jika kedalaman rekursi melebihi limit, gunakan heap sort
    // Ini mencegah worst case O(n²) dari quick sort
    if (depthLimit == 0) {
        heapSortRange(arr, low, high);
        return;
    }
    
    // Gunakan quick sort dengan median-of-three
    int pi = partitionIntro(arr, low, high);
    introsortUtil(arr, low, pi, depthLimit - 1);
    introsortUtil(arr, pi + 1, high, depthLimit - 1);
}

void introsort(int arr[], int n) {
    // Depth limit = 2 * floor(log2(n))
    int depthLimit = 2 * (int)floor(log2(n));
    introsortUtil(arr, 0, n - 1, depthLimit);
}

int main() {
    int arr[] = {10, 7, 8, 9, 1, 5, 3, 4, 2, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    introsort(arr, n);
    
    cout << "Hasil introsort: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    
    return 0;
}
```

**Komponen Introsort:**

| Situasi | Algoritma | Alasan |
|---------|-----------|--------|
| Array kecil (< 16) | Insertion Sort | Overhead rendah, cache efficient |
| Kedalaman normal | Quick Sort | Cepat rata-rata |
| Kedalaman berlebihan | Heap Sort | Menjamin O(n log n) |

**Keuntungan Introsort:**
- Best case: O(n log n) seperti quick sort
- Worst case: O(n log n) karena fallback ke heap sort
- Sangat efisien untuk array kecil

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan.

### Problem S1 ⭐
Apa output dari merge sort berikut jika kita trace langkah per langkah?
```cpp
int arr[] = {9, 3, 7, 5, 6, 4, 8, 2};
mergeSort(arr, 0, 7);
```

### Problem S2 ⭐⭐
Hitunglah jumlah perbandingan yang dilakukan quick sort untuk array [1, 2, 3, 4, 5] dengan pivot terakhir!

### Problem S3 ⭐⭐
Implementasikan fungsi untuk menghitung jumlah inversion dalam array menggunakan modifikasi merge sort!

### Problem S4 ⭐⭐⭐
Jelaskan bagaimana cara memodifikasi quick sort agar worst case space complexity-nya menjadi O(log n)!

### Problem S5 ⭐⭐⭐
Buatlah implementasi merge sort untuk mengurutkan linked list!

---

## Ringkasan

| Konsep | Deskripsi | Kompleksitas |
|--------|-----------|--------------|
| **Merge Sort** | Divide-and-conquer: bagi, urutkan rekursif, merge | O(n log n) selalu, O(n) space |
| **Quick Sort** | Pilih pivot, partition, rekursi | O(n log n) avg, O(n²) worst |
| **Partition** | Susun elemen relatif terhadap pivot | O(n) |
| **Pivot Selection** | First, last, random, median-of-three | Mempengaruhi performa |
| **Lower Bound** | Comparison-based sorting minimal Ω(n log n) | Teorema decision tree |
| **Stable Sort** | Mempertahankan urutan relatif elemen sama | Merge sort stable, quick sort tidak |
| **In-place** | Tidak memerlukan memori tambahan signifikan | Quick sort in-place, merge sort tidak |
| **3-way Quick Sort** | Tiga partisi untuk data dengan banyak duplikat | Efisien untuk duplikat |
| **Introsort** | Hybrid: quick sort + heap sort + insertion sort | O(n log n) terjamin |

---

## Jawaban Supplementary Problems

**S1:** 
Array diurutkan melalui 7 operasi merge menghasilkan [2, 3, 4, 5, 6, 7, 8, 9]

**S2:** 
Dengan pivot terakhir pada array sudah terurut: 4+3+2+1 = 10 perbandingan

**S3:** 
Hitung inversion saat merge: jika L[i] > R[j], semua L[i..n1] membentuk inversion dengan R[j]

**S4:** 
Gunakan tail call optimization: selalu rekursi pada subarray lebih kecil, iterasi pada yang lebih besar

**S5:** 
Gunakan slow-fast pointer untuk menemukan tengah linked list, merge dua sorted list dengan membandingkan node

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapters 7-8.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapters 7.4-7.7.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 13.
4. Sedgewick, R. & Wayne, K. (2011). *Algorithms* (4th Ed.). Addison-Wesley.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
