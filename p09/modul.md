# Modul 09: Algoritma Sorting (Bagian 1) - Sorting Dasar

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 09  
**Topik:** Algoritma Sorting Dasar (Bubble Sort, Selection Sort, Insertion Sort)

> **Capaian Pembelajaran:** Sub-CPMK-4.1 — Mampu mengimplementasikan algoritma sorting dasar dan menganalisis kompleksitasnya

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.2; Weiss Ch.7.2; Hubbard Ch.13

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** konsep dasar pengurutan (sorting) dan pentingnya dalam pemrograman
2. **Mengidentifikasi** kriteria pemilihan algoritma sorting yang tepat
3. **Mengimplementasikan** algoritma Bubble Sort beserta optimasinya
4. **Mengimplementasikan** algoritma Selection Sort dengan benar
5. **Mengimplementasikan** algoritma Insertion Sort dan memahami keunggulannya
6. **Menganalisis** kompleksitas waktu dan ruang masing-masing algoritma
7. **Membedakan** konsep stable sort dan unstable sort serta implikasinya

---

## 1. Pengantar Sorting

### 1.1 Apa itu Sorting?

> **Definisi:** Sorting (pengurutan) adalah proses menyusun ulang elemen-elemen dalam suatu koleksi data berdasarkan kriteria tertentu, biasanya dalam urutan ascending (menaik) atau descending (menurun).

Sorting merupakan salah satu operasi fundamental dalam ilmu komputer. Diperkirakan 25-50% waktu komputasi di banyak sistem dihabiskan untuk proses sorting. Mengapa? Karena data yang terurut memungkinkan:

- **Pencarian lebih cepat**: Binary search (O(log n)) hanya bekerja pada data terurut
- **Penggabungan efisien**: Merge dua list terurut jauh lebih cepat
- **Deteksi duplikat**: Elemen duplikat akan bersebelahan
- **Analisis data**: Median, percentile, dan statistik lain lebih mudah dihitung

### 1.2 Kriteria Algoritma Sorting

Dalam memilih algoritma sorting, kita perlu mempertimbangkan beberapa kriteria:

| Kriteria | Deskripsi | Pertimbangan |
|----------|-----------|--------------|
| **Kompleksitas Waktu** | Jumlah operasi yang dilakukan | Best, average, worst case |
| **Kompleksitas Ruang** | Memori tambahan yang dibutuhkan | In-place vs membutuhkan array tambahan |
| **Stabilitas** | Mempertahankan urutan elemen dengan nilai sama | Penting untuk sorting multi-key |
| **Adaptivitas** | Performa pada data yang hampir terurut | Beberapa algoritma lebih adaptif |
| **Kesederhanaan** | Kemudahan implementasi dan debugging | Trade-off dengan performa |

### 1.3 Klasifikasi Algoritma Sorting

![Klasifikasi Algoritma Sorting](images/gambar-9-1.png)

*Gambar 9.1: Klasifikasi algoritma sorting berdasarkan berbagai kriteria*

Algoritma sorting dapat diklasifikasikan berdasarkan:

**Berdasarkan Metode:**
- **Comparison-based**: Membandingkan pasangan elemen (Bubble, Selection, Insertion, Merge, Quick Sort)
- **Non-comparison**: Menggunakan informasi tambahan tentang data (Counting, Radix, Bucket Sort)

**Berdasarkan Kompleksitas:**
- **O(n²)**: Bubble, Selection, Insertion Sort — cocok untuk data kecil
- **O(n log n)**: Merge, Quick, Heap Sort — efisien untuk data besar

**Berdasarkan Memori:**
- **In-place**: Membutuhkan O(1) memori tambahan
- **Out-of-place**: Membutuhkan memori tambahan proporsional dengan input

### 1.4 Konteks Pertahanan: Pentingnya Sorting

Dalam sistem pertahanan, sorting digunakan secara ekstensif:

- **Prioritas Target Radar**: Mengurutkan objek berdasarkan jarak atau tingkat ancaman
- **Manajemen Logistik**: Mengurutkan inventory berdasarkan tanggal kadaluarsa atau prioritas
- **Penjadwalan Misi**: Mengurutkan tugas berdasarkan deadline atau tingkat urgensi
- **Analisis Intelijen**: Mengurutkan data berdasarkan relevansi atau timestamp

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Jelaskan mengapa algoritma sorting penting dalam operasi sistem C4ISR (Command, Control, Communications, Computers, Intelligence, Surveillance, Reconnaissance)!

**Penyelesaian:**

Sistem C4ISR memproses data dalam jumlah besar dari berbagai sumber secara real-time. Sorting menjadi krusial karena:

1. **Intelligence Processing**
   - Data dari berbagai sumber perlu diurutkan berdasarkan timestamp untuk analisis kronologis
   - Laporan intelijen diurutkan berdasarkan tingkat kepercayaan (reliability)

2. **Surveillance**
   - Objek terdeteksi radar diurutkan berdasarkan jarak untuk prioritas tracking
   - Ancaman diurutkan berdasarkan threat level untuk response yang tepat

3. **Decision Making**
   - Opsi taktis diurutkan berdasarkan probability of success
   - Resource allocation berdasarkan prioritas misi

4. **Communication**
   - Message queue diurutkan berdasarkan priority level
   - Data packets diurutkan untuk reassembly

Dengan sorting yang efisien, decision maker dapat mengakses informasi kritis lebih cepat, yang bisa menjadi perbedaan antara keberhasilan dan kegagalan misi.

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Apa perbedaan antara comparison-based sorting dan non-comparison sorting? Berikan masing-masing satu contoh!

**Penyelesaian:**

| Aspek | Comparison-Based | Non-Comparison |
|-------|------------------|----------------|
| **Mekanisme** | Membandingkan pasangan elemen untuk menentukan urutan | Menggunakan informasi struktural tentang data |
| **Lower Bound** | Ω(n log n) untuk worst case | Dapat mencapai O(n) |
| **Fleksibilitas** | Bekerja dengan data apapun yang bisa dibandingkan | Membutuhkan asumsi tentang data |
| **Contoh** | Quick Sort, Merge Sort | Counting Sort, Radix Sort |

**Contoh Comparison-Based (Bubble Sort):**
```cpp
// Membandingkan arr[j] dengan arr[j+1]
if (arr[j] > arr[j+1]) {
    swap(arr[j], arr[j+1]);
}
```

**Contoh Non-Comparison (Counting Sort):**
```cpp
// Menghitung kemunculan setiap nilai, tanpa perbandingan langsung
count[arr[i]]++;
```

Comparison-based sorting lebih umum digunakan karena fleksibilitasnya, sedangkan non-comparison sorting sangat efisien untuk kasus khusus dengan range nilai terbatas.

---

## 2. Bubble Sort

### 2.1 Konsep Dasar

> **Definisi:** Bubble Sort adalah algoritma sorting sederhana yang bekerja dengan berulang kali menukar elemen bersebelahan jika urutannya salah. Elemen terbesar "menggelembung" (bubble) ke posisi akhir array pada setiap iterasi.

Bubble Sort mendapatkan namanya dari cara elemen terbesar bergerak ke akhir array seperti gelembung yang naik ke permukaan air.

### 2.2 Algoritma Bubble Sort

**Langkah-langkah:**
1. Mulai dari elemen pertama
2. Bandingkan elemen saat ini dengan elemen berikutnya
3. Jika elemen saat ini lebih besar, tukar keduanya
4. Lanjutkan ke pasangan berikutnya
5. Setelah satu pass, elemen terbesar sudah di posisi akhir
6. Ulangi proses untuk elemen yang tersisa

![Proses Bubble Sort](images/gambar-9-2.png)

*Gambar 9.2: Visualisasi proses Bubble Sort pada array [64, 34, 25, 12, 22]*

### 2.3 Implementasi Bubble Sort Dasar

```cpp
#include <iostream>
using namespace std;

void bubbleSort(int arr[], int n) {
    // Outer loop: jumlah pass
    for (int i = 0; i < n - 1; i++) {
        // Inner loop: membandingkan pasangan bersebelahan
        for (int j = 0; j < n - i - 1; j++) {
            // Bandingkan dan tukar jika perlu
            if (arr[j] > arr[j + 1]) {
                // Swap menggunakan variabel temporary
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

void cetakArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

int main() {
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);
    
    cout << "Array sebelum sorting: ";
    cetakArray(arr, n);
    
    bubbleSort(arr, n);
    
    cout << "Array setelah sorting: ";
    cetakArray(arr, n);
    
    return 0;
}
```

**Output:**
```
Array sebelum sorting: 64 34 25 12 22 11 90 
Array setelah sorting: 11 12 22 25 34 64 90 
```

### 2.4 Optimasi Bubble Sort dengan Early Termination

Bubble Sort dasar selalu melakukan n-1 pass, meskipun array sudah terurut. Kita dapat mengoptimasi dengan mendeteksi jika tidak ada swap yang terjadi dalam satu pass:

```cpp
void bubbleSortOptimized(int arr[], int n) {
    bool swapped;
    
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        
        // Jika tidak ada swap dalam pass ini, array sudah terurut
        if (!swapped) {
            cout << "Early termination at pass " << (i + 1) << endl;
            break;
        }
    }
}
```

**Keuntungan optimasi:**
- Best case menjadi O(n) untuk array yang sudah terurut
- Mengurangi operasi tidak perlu pada array yang hampir terurut

### 2.5 Analisis Kompleksitas Bubble Sort

| Kasus | Kompleksitas Waktu | Kondisi |
|-------|-------------------|---------|
| **Best Case** | O(n) | Array sudah terurut (dengan optimasi) |
| **Average Case** | O(n²) | Elemen tersebar acak |
| **Worst Case** | O(n²) | Array terurut terbalik |

**Kompleksitas Ruang:** O(1) — In-place algorithm

**Analisis matematis:**
- Pass 1: n-1 perbandingan
- Pass 2: n-2 perbandingan
- ...
- Pass n-1: 1 perbandingan
- Total: (n-1) + (n-2) + ... + 1 = n(n-1)/2 = O(n²)

---

### SOLVED PROBLEM 3 ⭐

**Soal:** Trace eksekusi Bubble Sort pada array [5, 3, 8, 4, 2] dan hitung jumlah perbandingan serta swap!

**Penyelesaian:**

**Array awal:** [5, 3, 8, 4, 2]

**Pass 1:**
| Langkah | Perbandingan | Aksi | Array |
|---------|--------------|------|-------|
| 1 | 5 > 3? Ya | Swap | [3, 5, 8, 4, 2] |
| 2 | 5 > 8? Tidak | - | [3, 5, 8, 4, 2] |
| 3 | 8 > 4? Ya | Swap | [3, 5, 4, 8, 2] |
| 4 | 8 > 2? Ya | Swap | [3, 5, 4, 2, 8] |

Perbandingan: 4, Swap: 3

**Pass 2:**
| Langkah | Perbandingan | Aksi | Array |
|---------|--------------|------|-------|
| 1 | 3 > 5? Tidak | - | [3, 5, 4, 2, 8] |
| 2 | 5 > 4? Ya | Swap | [3, 4, 5, 2, 8] |
| 3 | 5 > 2? Ya | Swap | [3, 4, 2, 5, 8] |

Perbandingan: 3, Swap: 2

**Pass 3:**
| Langkah | Perbandingan | Aksi | Array |
|---------|--------------|------|-------|
| 1 | 3 > 4? Tidak | - | [3, 4, 2, 5, 8] |
| 2 | 4 > 2? Ya | Swap | [3, 2, 4, 5, 8] |

Perbandingan: 2, Swap: 1

**Pass 4:**
| Langkah | Perbandingan | Aksi | Array |
|---------|--------------|------|-------|
| 1 | 3 > 2? Ya | Swap | [2, 3, 4, 5, 8] |

Perbandingan: 1, Swap: 1

**Hasil Akhir:** [2, 3, 4, 5, 8]

**Ringkasan:**
- Total perbandingan: 4 + 3 + 2 + 1 = **10**
- Total swap: 3 + 2 + 1 + 1 = **7**

---

### SOLVED PROBLEM 4 ⭐

**Soal:** Apa output dari kode berikut?

```cpp
int arr[] = {1, 2, 3, 4, 5};
int n = 5;
bool swapped = false;

for (int j = 0; j < n - 1; j++) {
    if (arr[j] > arr[j + 1]) {
        swap(arr[j], arr[j + 1]);
        swapped = true;
    }
}

cout << "Swapped: " << (swapped ? "Yes" : "No");
```

**Penyelesaian:**

**Output:** `Swapped: No`

**Penjelasan:**
- Array [1, 2, 3, 4, 5] sudah terurut ascending
- Setiap perbandingan: 1<2, 2<3, 3<4, 4<5 → tidak ada yang memenuhi kondisi `arr[j] > arr[j+1]`
- Variabel `swapped` tetap `false`
- Ini adalah kasus best case untuk Bubble Sort dengan optimasi

---

### SOLVED PROBLEM 5 ⭐⭐

**Soal:** Modifikasi Bubble Sort untuk mengurutkan array dalam urutan descending!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

void bubbleSortDescending(int arr[], int n) {
    bool swapped;
    
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        
        for (int j = 0; j < n - i - 1; j++) {
            // Ubah kondisi dari > menjadi <
            if (arr[j] < arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                swapped = true;
            }
        }
        
        if (!swapped) break;
    }
}

int main() {
    int arr[] = {64, 34, 25, 12, 22};
    int n = 5;
    
    cout << "Sebelum: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    
    bubbleSortDescending(arr, n);
    
    cout << "Sesudah (Descending): ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    
    return 0;
}
```

**Output:**
```
Sebelum: 64 34 25 12 22 
Sesudah (Descending): 64 34 25 22 12 
```

**Perubahan yang dilakukan:**
- Kondisi perbandingan diubah dari `arr[j] > arr[j + 1]` menjadi `arr[j] < arr[j + 1]`
- Elemen terkecil akan "bubble" ke akhir array, sehingga elemen terbesar tetap di depan

---

### SOLVED PROBLEM 6 ⭐⭐

**Soal:** Berapa jumlah perbandingan minimum dan maksimum untuk Bubble Sort dengan optimasi pada array berukuran n=10?

**Penyelesaian:**

**Minimum (Best Case):**
- Terjadi ketika array sudah terurut
- Hanya butuh 1 pass untuk memverifikasi
- Perbandingan: n - 1 = 10 - 1 = **9 perbandingan**

**Maksimum (Worst Case):**
- Terjadi ketika array terurut terbalik
- Butuh n-1 pass lengkap
- Total perbandingan:
  - Pass 1: 9 perbandingan
  - Pass 2: 8 perbandingan
  - Pass 3: 7 perbandingan
  - ...
  - Pass 9: 1 perbandingan
  - Total: 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 = **45 perbandingan**

**Formula umum:**
- Minimum: n - 1
- Maksimum: n(n-1)/2 = 10(9)/2 = 45

---

## 3. Selection Sort

### 3.1 Konsep Dasar

> **Definisi:** Selection Sort adalah algoritma sorting yang bekerja dengan memilih elemen minimum (atau maksimum) dari bagian yang belum terurut dan menukarnya dengan elemen di posisi yang sesuai.

Selection Sort membagi array menjadi dua bagian:
- **Bagian terurut** (di awal array)
- **Bagian belum terurut** (sisanya)

### 3.2 Algoritma Selection Sort

**Langkah-langkah:**
1. Temukan elemen minimum dalam bagian yang belum terurut
2. Tukar dengan elemen pertama dari bagian yang belum terurut
3. Pindahkan batas bagian terurut satu posisi ke kanan
4. Ulangi sampai seluruh array terurut

![Proses Selection Sort](images/gambar-9-3.png)

*Gambar 9.3: Visualisasi proses Selection Sort pada array [64, 25, 12, 22, 11]*

### 3.3 Implementasi Selection Sort

```cpp
#include <iostream>
using namespace std;

void selectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        // Asumsikan elemen pertama dari bagian unsorted adalah minimum
        int minIndex = i;
        
        // Cari elemen minimum di bagian unsorted
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        
        // Tukar minimum dengan elemen pertama bagian unsorted
        if (minIndex != i) {
            swap(arr[i], arr[minIndex]);
        }
    }
}

int main() {
    int arr[] = {64, 25, 12, 22, 11};
    int n = 5;
    
    cout << "Array sebelum sorting: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    
    selectionSort(arr, n);
    
    cout << "Array setelah sorting: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    
    return 0;
}
```

**Output:**
```
Array sebelum sorting: 64 25 12 22 11 
Array setelah sorting: 11 12 22 25 64 
```

### 3.4 Analisis Kompleksitas Selection Sort

| Kasus | Kompleksitas Waktu | Penjelasan |
|-------|-------------------|------------|
| **Best Case** | O(n²) | Tetap harus mencari minimum |
| **Average Case** | O(n²) | Sama untuk semua kasus |
| **Worst Case** | O(n²) | Sama untuk semua kasus |

**Kompleksitas Ruang:** O(1) — In-place algorithm

**Karakteristik penting:**
- Jumlah perbandingan selalu sama: n(n-1)/2
- Jumlah swap maksimal: n-1 (jauh lebih sedikit dari Bubble Sort)
- Tidak adaptif terhadap data yang hampir terurut

---

### SOLVED PROBLEM 7 ⭐

**Soal:** Trace eksekusi Selection Sort pada array [29, 10, 14, 37, 13]!

**Penyelesaian:**

**Array awal:** [29, 10, 14, 37, 13]

**Iterasi 1 (i=0):**
- Cari minimum dari index 0 sampai 4
- Minimum: 10 di index 1
- Swap arr[0] dengan arr[1]
- **Hasil:** [10, 29, 14, 37, 13]

**Iterasi 2 (i=1):**
- Cari minimum dari index 1 sampai 4
- Minimum: 13 di index 4
- Swap arr[1] dengan arr[4]
- **Hasil:** [10, 13, 14, 37, 29]

**Iterasi 3 (i=2):**
- Cari minimum dari index 2 sampai 4
- Minimum: 14 di index 2 (sudah di posisi)
- Tidak perlu swap
- **Hasil:** [10, 13, 14, 37, 29]

**Iterasi 4 (i=3):**
- Cari minimum dari index 3 sampai 4
- Minimum: 29 di index 4
- Swap arr[3] dengan arr[4]
- **Hasil:** [10, 13, 14, 29, 37]

**Array terurut:** [10, 13, 14, 29, 37]

**Statistik:**
- Perbandingan: 4 + 3 + 2 + 1 = 10
- Swap: 3

---

### SOLVED PROBLEM 8 ⭐

**Soal:** Mengapa Selection Sort melakukan jumlah swap yang lebih sedikit dibandingkan Bubble Sort?

**Penyelesaian:**

**Perbandingan jumlah swap:**

| Algoritma | Swap per Iterasi | Total Swap (Worst Case) |
|-----------|------------------|------------------------|
| Bubble Sort | Bisa banyak (setiap pasangan tidak terurut) | O(n²) |
| Selection Sort | Maksimal 1 per iterasi | O(n) |

**Alasan:**
1. **Selection Sort** hanya melakukan satu swap per iterasi outer loop. Setelah menemukan minimum, langsung ditukar ke posisi final.

2. **Bubble Sort** melakukan swap setiap kali menemukan pasangan yang tidak terurut, yang bisa terjadi banyak kali dalam satu pass.

**Contoh dengan array [5, 4, 3, 2, 1]:**
- Selection Sort: 4 swap (n-1)
- Bubble Sort: 10 swap (setiap pasangan bersebelahan ditukar)

**Implikasi praktis:**
- Selection Sort lebih baik ketika operasi swap mahal (misalnya, menukar objek besar)
- Bubble Sort lebih baik untuk mendeteksi data yang hampir terurut (dengan optimasi)

---

### SOLVED PROBLEM 9 ⭐⭐

**Soal:** Implementasikan Selection Sort untuk mengurutkan array of struct berdasarkan field tertentu!

**Penyelesaian:**

```cpp
#include <iostream>
#include <cstring>
using namespace std;

struct Personel {
    int id;
    char nama[50];
    int pangkat;  // 1=Prajurit, 2=Kopral, 3=Sersan, dst
};

void selectionSortByPangkat(Personel arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        int maxIndex = i;
        
        // Cari pangkat tertinggi (descending order)
        for (int j = i + 1; j < n; j++) {
            if (arr[j].pangkat > arr[maxIndex].pangkat) {
                maxIndex = j;
            }
        }
        
        if (maxIndex != i) {
            swap(arr[i], arr[maxIndex]);
        }
    }
}

void cetakPersonel(Personel arr[], int n) {
    cout << "ID\tNama\t\tPangkat" << endl;
    cout << "--------------------------------" << endl;
    for (int i = 0; i < n; i++) {
        cout << arr[i].id << "\t" << arr[i].nama << "\t\t" << arr[i].pangkat << endl;
    }
}

int main() {
    Personel tim[] = {
        {101, "Ahmad", 2},
        {102, "Budi", 4},
        {103, "Citra", 1},
        {104, "Dewi", 3}
    };
    int n = 4;
    
    cout << "Sebelum sorting:" << endl;
    cetakPersonel(tim, n);
    
    selectionSortByPangkat(tim, n);
    
    cout << "\nSetelah sorting (by pangkat, descending):" << endl;
    cetakPersonel(tim, n);
    
    return 0;
}
```

**Output:**
```
Sebelum sorting:
ID	Nama		Pangkat
--------------------------------
101	Ahmad		2
102	Budi		4
103	Citra		1
104	Dewi		3

Setelah sorting (by pangkat, descending):
ID	Nama		Pangkat
--------------------------------
102	Budi		4
104	Dewi		3
101	Ahmad		2
103	Citra		1
```

---

## 4. Insertion Sort

### 4.1 Konsep Dasar

> **Definisi:** Insertion Sort adalah algoritma sorting yang membangun array terurut satu elemen pada satu waktu, dengan menyisipkan setiap elemen baru ke posisi yang tepat dalam bagian yang sudah terurut.

Insertion Sort bekerja seperti cara kita mengurutkan kartu di tangan:
- Ambil satu kartu
- Sisipkan ke posisi yang tepat di antara kartu yang sudah terurut
- Ulangi untuk setiap kartu

### 4.2 Algoritma Insertion Sort

**Langkah-langkah:**
1. Mulai dari elemen kedua (index 1)
2. Simpan elemen tersebut sebagai "key"
3. Bandingkan key dengan elemen-elemen di sebelah kiri
4. Geser elemen yang lebih besar ke kanan
5. Sisipkan key di posisi yang tepat
6. Ulangi untuk elemen berikutnya

![Proses Insertion Sort](images/gambar-9-4.png)

*Gambar 9.4: Visualisasi proses Insertion Sort pada array [12, 11, 13, 5, 6]*

### 4.3 Implementasi Insertion Sort

```cpp
#include <iostream>
using namespace std;

void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];  // Elemen yang akan disisipkan
        int j = i - 1;
        
        // Geser elemen yang lebih besar dari key ke kanan
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        
        // Sisipkan key di posisi yang tepat
        arr[j + 1] = key;
    }
}

int main() {
    int arr[] = {12, 11, 13, 5, 6};
    int n = 5;
    
    cout << "Array sebelum sorting: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    
    insertionSort(arr, n);
    
    cout << "Array setelah sorting: ";
    for (int i = 0; i < n; i++) cout << arr[i] << " ";
    cout << endl;
    
    return 0;
}
```

**Output:**
```
Array sebelum sorting: 12 11 13 5 6 
Array setelah sorting: 5 6 11 12 13 
```

### 4.4 Analisis Kompleksitas Insertion Sort

| Kasus | Kompleksitas Waktu | Kondisi |
|-------|-------------------|---------|
| **Best Case** | O(n) | Array sudah terurut |
| **Average Case** | O(n²) | Elemen tersebar acak |
| **Worst Case** | O(n²) | Array terurut terbalik |

**Kompleksitas Ruang:** O(1) — In-place algorithm

### 4.5 Keunggulan Insertion Sort

1. **Adaptif**: Sangat efisien untuk data yang hampir terurut (nearly sorted)
2. **Stabil**: Mempertahankan urutan relatif elemen dengan nilai sama
3. **Online**: Dapat mengurutkan data saat data masih diterima
4. **Efisien untuk data kecil**: Overhead minimal dibanding algoritma kompleks
5. **In-place**: Tidak membutuhkan memori tambahan

---

### SOLVED PROBLEM 10 ⭐

**Soal:** Trace eksekusi Insertion Sort pada array [7, 3, 5, 2]!

**Penyelesaian:**

**Array awal:** [7, 3, 5, 2]

**Iterasi 1 (i=1):**
- key = 3
- Bandingkan dengan arr[0]=7: 7 > 3, geser 7 ke kanan
- Array sementara: [7, 7, 5, 2]
- j = -1, sisipkan key di j+1=0
- **Hasil:** [3, 7, 5, 2]

**Iterasi 2 (i=2):**
- key = 5
- Bandingkan dengan arr[1]=7: 7 > 5, geser 7 ke kanan
- Array sementara: [3, 7, 7, 2]
- Bandingkan dengan arr[0]=3: 3 < 5, berhenti
- Sisipkan key di j+1=1
- **Hasil:** [3, 5, 7, 2]

**Iterasi 3 (i=3):**
- key = 2
- Bandingkan dengan arr[2]=7: 7 > 2, geser ke kanan
- Array sementara: [3, 5, 7, 7]
- Bandingkan dengan arr[1]=5: 5 > 2, geser ke kanan
- Array sementara: [3, 5, 5, 7]
- Bandingkan dengan arr[0]=3: 3 > 2, geser ke kanan
- Array sementara: [3, 3, 5, 7]
- j = -1, sisipkan key di j+1=0
- **Hasil:** [2, 3, 5, 7]

**Array terurut:** [2, 3, 5, 7]

---

### SOLVED PROBLEM 11 ⭐

**Soal:** Mengapa Insertion Sort sangat efisien untuk data yang hampir terurut?

**Penyelesaian:**

**Analisis Best Case (Array Terurut):**

Untuk array [1, 2, 3, 4, 5]:
```
i=1: key=2, bandingkan dengan 1, 1<2, tidak geser, O(1)
i=2: key=3, bandingkan dengan 2, 2<3, tidak geser, O(1)
i=3: key=4, bandingkan dengan 3, 3<4, tidak geser, O(1)
i=4: key=5, bandingkan dengan 4, 4<5, tidak geser, O(1)
```
Total: n-1 perbandingan = **O(n)**

**Analisis pada Data Hampir Terurut:**

Untuk array [1, 2, 4, 3, 5] (hanya 3 dan 4 tertukar):
```
i=1: key=2, 1 perbandingan
i=2: key=4, 1 perbandingan
i=3: key=3, 2 perbandingan + 1 shift (hanya ini yang butuh kerja ekstra)
i=4: key=5, 1 perbandingan
```
Total: 5 perbandingan, mendekati O(n)

**Kesimpulan:**
- Inner loop `while` hanya berjalan jika ada elemen yang lebih besar
- Pada data hampir terurut, sangat sedikit elemen yang perlu digeser
- Kompleksitas mendekati O(n) dengan konstanta kecil

Ini berbeda dengan Selection Sort yang selalu O(n²) karena harus selalu mencari minimum di seluruh bagian unsorted.

---

### SOLVED PROBLEM 12 ⭐⭐

**Soal:** Implementasikan Insertion Sort untuk mengurutkan linked list!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

// Fungsi untuk menyisipkan node ke posisi yang tepat dalam list terurut
Node* sortedInsert(Node* sorted, Node* newNode) {
    // Kasus khusus: list kosong atau node baru lebih kecil dari head
    if (sorted == nullptr || sorted->data >= newNode->data) {
        newNode->next = sorted;
        return newNode;
    }
    
    // Cari posisi yang tepat
    Node* current = sorted;
    while (current->next != nullptr && current->next->data < newNode->data) {
        current = current->next;
    }
    
    // Sisipkan node
    newNode->next = current->next;
    current->next = newNode;
    
    return sorted;
}

Node* insertionSortLinkedList(Node* head) {
    Node* sorted = nullptr;
    Node* current = head;
    
    while (current != nullptr) {
        // Simpan next sebelum dimodifikasi
        Node* next = current->next;
        
        // Sisipkan current ke sorted list
        sorted = sortedInsert(sorted, current);
        
        // Lanjut ke node berikutnya
        current = next;
    }
    
    return sorted;
}

// Fungsi helper untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

// Fungsi untuk mencetak linked list
void printList(Node* head) {
    Node* temp = head;
    while (temp != nullptr) {
        cout << temp->data;
        if (temp->next != nullptr) cout << " -> ";
        temp = temp->next;
    }
    cout << " -> NULL" << endl;
}

int main() {
    // Buat linked list: 12 -> 11 -> 13 -> 5 -> 6
    Node* head = createNode(12);
    head->next = createNode(11);
    head->next->next = createNode(13);
    head->next->next->next = createNode(5);
    head->next->next->next->next = createNode(6);
    
    cout << "Linked List sebelum sorting:" << endl;
    printList(head);
    
    head = insertionSortLinkedList(head);
    
    cout << "Linked List setelah sorting:" << endl;
    printList(head);
    
    return 0;
}
```

**Output:**
```
Linked List sebelum sorting:
12 -> 11 -> 13 -> 5 -> 6 -> NULL
Linked List setelah sorting:
5 -> 6 -> 11 -> 12 -> 13 -> NULL
```

**Penjelasan:**
- Buat list baru `sorted` yang awalnya kosong
- Ambil setiap node dari list asli dan sisipkan ke posisi yang tepat di `sorted`
- Kompleksitas tetap O(n²), tapi tidak ada operasi shift karena menggunakan linked list

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Bandingkan jumlah operasi geser (shift) pada Insertion Sort untuk array yang terurut, terurut terbalik, dan acak dengan 5 elemen!

**Penyelesaian:**

**Array terurut [1, 2, 3, 4, 5]:**
```
i=1: key=2, 2>1, tidak geser
i=2: key=3, 3>2, tidak geser
i=3: key=4, 4>3, tidak geser
i=4: key=5, 5>4, tidak geser
Total shift: 0
```

**Array terurut terbalik [5, 4, 3, 2, 1]:**
```
i=1: key=4, 4<5, geser 5 → 1 shift
i=2: key=3, 3<5, 3<4, geser 5,4 → 2 shifts
i=3: key=2, 2<5, 2<4, 2<3, geser 5,4,3 → 3 shifts
i=4: key=1, 1<5, 1<4, 1<3, 1<2, geser 5,4,3,2 → 4 shifts
Total shift: 1+2+3+4 = 10
```

**Array acak [3, 1, 4, 5, 2]:**
```
i=1: key=1, 1<3, geser 3 → 1 shift
i=2: key=4, 4>3, tidak geser → 0 shifts
i=3: key=5, 5>4, tidak geser → 0 shifts
i=4: key=2, 2<5, 2<4, 2<3, geser 5,4,3 → 3 shifts
Total shift: 1+0+0+3 = 4
```

**Ringkasan:**

| Kondisi Array | Jumlah Shift |
|---------------|--------------|
| Terurut | 0 |
| Acak | 4 |
| Terurut Terbalik | 10 (maksimum) |

Jumlah shift maksimum = n(n-1)/2 = 5(4)/2 = 10

---

## 5. Stable vs Unstable Sort

### 5.1 Definisi Stabilitas

> **Definisi:** Algoritma sorting dikatakan **stable** jika mempertahankan urutan relatif dari elemen-elemen yang memiliki nilai (key) yang sama.

![Stable vs Unstable Sort](images/gambar-9-5.png)

*Gambar 9.5: Perbandingan hasil stable sort dan unstable sort*

### 5.2 Contoh Pentingnya Stabilitas

Bayangkan database personel militer dengan data:

| Nama | Pangkat | Tahun Masuk |
|------|---------|-------------|
| Ahmad | Sersan | 2020 |
| Budi | Kopral | 2019 |
| Citra | Sersan | 2018 |
| Dewi | Kopral | 2021 |

Jika sudah diurutkan berdasarkan tahun masuk, lalu diurutkan lagi berdasarkan pangkat:

**Dengan Stable Sort:**
```
Kopral: Budi (2019), Dewi (2021)  -- urutan tahun dipertahankan
Sersan: Citra (2018), Ahmad (2020)  -- urutan tahun dipertahankan
```

**Dengan Unstable Sort:**
```
Kopral: Dewi (2021), Budi (2019)  -- urutan tahun BISA berubah
Sersan: Ahmad (2020), Citra (2018)  -- urutan tahun BISA berubah
```

### 5.3 Stabilitas Algoritma Sorting Dasar

| Algoritma | Stabilitas | Alasan |
|-----------|------------|--------|
| **Bubble Sort** | Stable ✓ | Hanya menukar jika `>`, bukan `>=` |
| **Selection Sort** | Unstable ✗ | Swap jarak jauh dapat mengubah urutan |
| **Insertion Sort** | Stable ✓ | Hanya menggeser jika `>`, bukan `>=` |

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Buktikan dengan contoh bahwa Selection Sort tidak stable!

**Penyelesaian:**

**Array input dengan elemen bertanda:**
- Elemen: nilai[index asli]
- Input: [5₀, 3, 5₁, 2]
- (5₀ dan 5₁ adalah dua elemen berbeda dengan nilai sama = 5)

**Trace Selection Sort:**

**Iterasi 1 (i=0):**
- Cari minimum dari [5₀, 3, 5₁, 2]: minimum = 2 di index 3
- Swap arr[0] dengan arr[3]
- [5₀, 3, 5₁, 2] → [2, 3, 5₁, 5₀]
- **Perhatikan:** 5₀ dan 5₁ sudah BERTUKAR posisi!

**Iterasi 2 (i=1):**
- Cari minimum dari [3, 5₁, 5₀]: minimum = 3 di index 1
- Tidak perlu swap
- [2, 3, 5₁, 5₀]

**Iterasi 3 (i=2):**
- Cari minimum dari [5₁, 5₀]: minimum = 5₁ di index 2
- Tidak perlu swap
- [2, 3, 5₁, 5₀]

**Hasil akhir:** [2, 3, 5₁, 5₀]

**Bukti ketidakstabilan:**
- Urutan awal: 5₀ sebelum 5₁
- Urutan akhir: 5₁ sebelum 5₀
- Urutan relatif BERUBAH → **Selection Sort TIDAK STABLE**

---

### SOLVED PROBLEM 15 ⭐⭐

**Soal:** Bagaimana membuat Selection Sort menjadi stable?

**Penyelesaian:**

**Masalah utama:** Swap jarak jauh dapat melewati elemen dengan nilai yang sama.

**Solusi:** Gunakan **insert** (seperti Insertion Sort) alih-alih **swap**.

```cpp
void stableSelectionSort(int arr[], int n) {
    for (int i = 0; i < n - 1; i++) {
        // Cari indeks minimum
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        
        // Jika minimum bukan di posisi i
        if (minIndex != i) {
            // Simpan nilai minimum
            int minVal = arr[minIndex];
            
            // Geser semua elemen dari i sampai minIndex-1 ke kanan
            // (seperti operasi insert pada Insertion Sort)
            for (int k = minIndex; k > i; k--) {
                arr[k] = arr[k - 1];
            }
            
            // Letakkan minimum di posisi i
            arr[i] = minVal;
        }
    }
}
```

**Trade-off:**
- Menjadi stable ✓
- Kompleksitas waktu tetap O(n²)
- Jumlah operasi shift meningkat (seperti Insertion Sort)
- Kehilangan keuntungan utama Selection Sort (jumlah swap sedikit)

**Kesimpulan:** Lebih baik gunakan Insertion Sort jika butuh stable sort dengan O(n²).

---

### SOLVED PROBLEM 16 ⭐⭐⭐

**Soal:** Implementasikan fungsi sorting untuk mengurutkan array personel berdasarkan pangkat (primary key) dan tahun masuk (secondary key) menggunakan stable sort!

**Penyelesaian:**

```cpp
#include <iostream>
#include <cstring>
using namespace std;

struct Personel {
    int id;
    char nama[50];
    int pangkat;      // 1=Prajurit, 2=Kopral, 3=Sersan, 4=Serma
    int tahunMasuk;
};

// Insertion Sort berdasarkan tahunMasuk (stable)
void sortByTahun(Personel arr[], int n) {
    for (int i = 1; i < n; i++) {
        Personel key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && arr[j].tahunMasuk > key.tahunMasuk) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

// Insertion Sort berdasarkan pangkat (stable)
void sortByPangkat(Personel arr[], int n) {
    for (int i = 1; i < n; i++) {
        Personel key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && arr[j].pangkat < key.pangkat) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

void cetakPersonel(Personel arr[], int n) {
    cout << "ID\tNama\t\tPangkat\tTahun" << endl;
    cout << "----------------------------------------" << endl;
    for (int i = 0; i < n; i++) {
        cout << arr[i].id << "\t" << arr[i].nama << "\t\t" 
             << arr[i].pangkat << "\t" << arr[i].tahunMasuk << endl;
    }
}

int main() {
    Personel tim[] = {
        {101, "Ahmad", 3, 2020},
        {102, "Budi", 2, 2019},
        {103, "Citra", 3, 2018},
        {104, "Dewi", 2, 2021},
        {105, "Eko", 4, 2017},
        {106, "Fani", 3, 2019}
    };
    int n = 6;
    
    cout << "Data Awal:" << endl;
    cetakPersonel(tim, n);
    
    // Langkah 1: Sort by secondary key (tahun masuk)
    sortByTahun(tim, n);
    cout << "\nSetelah sort by Tahun Masuk:" << endl;
    cetakPersonel(tim, n);
    
    // Langkah 2: Sort by primary key (pangkat) - stable sort
    // Ini akan mempertahankan urutan tahun untuk pangkat yang sama
    sortByPangkat(tim, n);
    cout << "\nSetelah sort by Pangkat (mempertahankan urutan tahun):" << endl;
    cetakPersonel(tim, n);
    
    return 0;
}
```

**Output:**
```
Data Awal:
ID	Nama		Pangkat	Tahun
----------------------------------------
101	Ahmad		3	2020
102	Budi		2	2019
103	Citra		3	2018
104	Dewi		2	2021
105	Eko		4	2017
106	Fani		3	2019

Setelah sort by Tahun Masuk:
ID	Nama		Pangkat	Tahun
----------------------------------------
105	Eko		4	2017
103	Citra		3	2018
102	Budi		2	2019
106	Fani		3	2019
101	Ahmad		3	2020
104	Dewi		2	2021

Setelah sort by Pangkat (mempertahankan urutan tahun):
ID	Nama		Pangkat	Tahun
----------------------------------------
105	Eko		4	2017
103	Citra		3	2018
106	Fani		3	2019
101	Ahmad		3	2020
102	Budi		2	2019
104	Dewi		2	2021
```

**Verifikasi:**
- Pangkat 4 (Eko): hanya satu, di posisi pertama ✓
- Pangkat 3 (Citra, Fani, Ahmad): urutan tahun 2018, 2019, 2020 ✓
- Pangkat 2 (Budi, Dewi): urutan tahun 2019, 2021 ✓

---

## 6. Perbandingan Ketiga Algoritma

### 6.1 Tabel Perbandingan Komprehensif

| Kriteria | Bubble Sort | Selection Sort | Insertion Sort |
|----------|-------------|----------------|----------------|
| **Best Case** | O(n)* | O(n²) | O(n) |
| **Average Case** | O(n²) | O(n²) | O(n²) |
| **Worst Case** | O(n²) | O(n²) | O(n²) |
| **Space** | O(1) | O(1) | O(1) |
| **Stable** | ✓ Yes | ✗ No | ✓ Yes |
| **Adaptive** | ✓ Yes* | ✗ No | ✓ Yes |
| **# Comparisons** | n(n-1)/2 | n(n-1)/2 | n-1 to n(n-1)/2 |
| **# Swaps** | 0 to n(n-1)/2 | 0 to n-1 | 0 |

*dengan optimasi early termination

### 6.2 Kapan Menggunakan Masing-masing

![Panduan Pemilihan Algoritma](images/gambar-9-6.png)

*Gambar 9.6: Flowchart pemilihan algoritma sorting dasar*

**Rekomendasi penggunaan:**

1. **Insertion Sort** — Pilihan terbaik di antara ketiganya
   - Data kecil (n < 50)
   - Data hampir terurut
   - Butuh stable sort
   - Online sorting (data streaming)

2. **Selection Sort** — Kasus khusus
   - Operasi swap sangat mahal
   - Memori terbatas dan perlu meminimalkan penulisan

3. **Bubble Sort** — Jarang digunakan dalam praktik
   - Hanya untuk pembelajaran
   - Implementasi sederhana untuk prototipe cepat

---

### SOLVED PROBLEM 17 ⭐

**Soal:** Untuk array dengan 1000 elemen yang hampir terurut (hanya 5 elemen tidak pada tempatnya), algoritma mana yang paling efisien? Jelaskan!

**Penyelesaian:**

**Jawaban:** Insertion Sort

**Analisis:**

| Algoritma | Performa pada Data Hampir Terurut |
|-----------|-----------------------------------|
| Bubble Sort | O(n) dengan optimasi, tapi banyak perbandingan tidak perlu |
| Selection Sort | Tetap O(n²), harus mencari minimum setiap iterasi |
| Insertion Sort | Mendekati O(n), hanya 5 elemen perlu digeser jauh |

**Perhitungan untuk Insertion Sort:**
- 995 elemen sudah di posisi yang benar: ~995 perbandingan, 0 shift
- 5 elemen tidak pada tempatnya: maksimal 5 × 1000 = 5000 operasi shift
- Total: ~6000 operasi = **O(n)**

**Perhitungan untuk Selection Sort:**
- Tetap harus melakukan n(n-1)/2 = 1000(999)/2 ≈ 500,000 perbandingan
- Tidak peduli apakah data hampir terurut atau tidak

**Kesimpulan:**
Insertion Sort sekitar 100× lebih cepat dari Selection Sort untuk kasus ini.

---

### SOLVED PROBLEM 18 ⭐⭐

**Soal:** Implementasikan program yang membandingkan jumlah operasi ketiga algoritma sorting!

**Penyelesaian:**

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <cstring>
using namespace std;

// Struktur untuk menyimpan statistik
struct SortStats {
    long long comparisons;
    long long swaps;
    long long shifts;
};

// Bubble Sort dengan statistik
SortStats bubbleSortWithStats(int arr[], int n) {
    SortStats stats = {0, 0, 0};
    bool swapped;
    
    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        for (int j = 0; j < n - i - 1; j++) {
            stats.comparisons++;
            if (arr[j] > arr[j + 1]) {
                swap(arr[j], arr[j + 1]);
                stats.swaps++;
                swapped = true;
            }
        }
        if (!swapped) break;
    }
    return stats;
}

// Selection Sort dengan statistik
SortStats selectionSortWithStats(int arr[], int n) {
    SortStats stats = {0, 0, 0};
    
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            stats.comparisons++;
            if (arr[j] < arr[minIndex]) {
                minIndex = j;
            }
        }
        if (minIndex != i) {
            swap(arr[i], arr[minIndex]);
            stats.swaps++;
        }
    }
    return stats;
}

// Insertion Sort dengan statistik
SortStats insertionSortWithStats(int arr[], int n) {
    SortStats stats = {0, 0, 0};
    
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0) {
            stats.comparisons++;
            if (arr[j] > key) {
                arr[j + 1] = arr[j];
                stats.shifts++;
                j--;
            } else {
                break;
            }
        }
        arr[j + 1] = key;
    }
    return stats;
}

void generateRandomArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        arr[i] = rand() % 1000;
    }
}

void generateSortedArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        arr[i] = i;
    }
}

void generateReversedArray(int arr[], int n) {
    for (int i = 0; i < n; i++) {
        arr[i] = n - i;
    }
}

int main() {
    srand(time(0));
    const int N = 100;
    int arr1[N], arr2[N], arr3[N];
    
    cout << "=== PERBANDINGAN ALGORITMA SORTING (n=" << N << ") ===" << endl;
    
    // Test 1: Random Array
    generateRandomArray(arr1, N);
    memcpy(arr2, arr1, sizeof(arr1));
    memcpy(arr3, arr1, sizeof(arr1));
    
    cout << "\n1. Array Random:" << endl;
    SortStats bs = bubbleSortWithStats(arr1, N);
    SortStats ss = selectionSortWithStats(arr2, N);
    SortStats is = insertionSortWithStats(arr3, N);
    
    cout << "   Bubble Sort    - Comparisons: " << bs.comparisons 
         << ", Swaps: " << bs.swaps << endl;
    cout << "   Selection Sort - Comparisons: " << ss.comparisons 
         << ", Swaps: " << ss.swaps << endl;
    cout << "   Insertion Sort - Comparisons: " << is.comparisons 
         << ", Shifts: " << is.shifts << endl;
    
    // Test 2: Already Sorted Array
    generateSortedArray(arr1, N);
    memcpy(arr2, arr1, sizeof(arr1));
    memcpy(arr3, arr1, sizeof(arr1));
    
    cout << "\n2. Array Terurut:" << endl;
    bs = bubbleSortWithStats(arr1, N);
    ss = selectionSortWithStats(arr2, N);
    is = insertionSortWithStats(arr3, N);
    
    cout << "   Bubble Sort    - Comparisons: " << bs.comparisons 
         << ", Swaps: " << bs.swaps << endl;
    cout << "   Selection Sort - Comparisons: " << ss.comparisons 
         << ", Swaps: " << ss.swaps << endl;
    cout << "   Insertion Sort - Comparisons: " << is.comparisons 
         << ", Shifts: " << is.shifts << endl;
    
    // Test 3: Reversed Array
    generateReversedArray(arr1, N);
    memcpy(arr2, arr1, sizeof(arr1));
    memcpy(arr3, arr1, sizeof(arr1));
    
    cout << "\n3. Array Terbalik:" << endl;
    bs = bubbleSortWithStats(arr1, N);
    ss = selectionSortWithStats(arr2, N);
    is = insertionSortWithStats(arr3, N);
    
    cout << "   Bubble Sort    - Comparisons: " << bs.comparisons 
         << ", Swaps: " << bs.swaps << endl;
    cout << "   Selection Sort - Comparisons: " << ss.comparisons 
         << ", Swaps: " << ss.swaps << endl;
    cout << "   Insertion Sort - Comparisons: " << is.comparisons 
         << ", Shifts: " << is.shifts << endl;
    
    return 0;
}
```

**Contoh Output:**
```
=== PERBANDINGAN ALGORITMA SORTING (n=100) ===

1. Array Random:
   Bubble Sort    - Comparisons: 4950, Swaps: 2387
   Selection Sort - Comparisons: 4950, Swaps: 99
   Insertion Sort - Comparisons: 2486, Shifts: 2387

2. Array Terurut:
   Bubble Sort    - Comparisons: 99, Swaps: 0
   Selection Sort - Comparisons: 4950, Swaps: 0
   Insertion Sort - Comparisons: 99, Shifts: 0

3. Array Terbalik:
   Bubble Sort    - Comparisons: 4950, Swaps: 4950
   Selection Sort - Comparisons: 4950, Swaps: 50
   Insertion Sort - Comparisons: 4950, Shifts: 4950
```

---

### SOLVED PROBLEM 19 ⭐⭐⭐

**Soal:** Dalam sistem radar pertahanan, objek terdeteksi diurutkan berdasarkan jarak untuk prioritas tracking. Data update setiap 0.1 detik dengan perubahan minimal. Algoritma sorting mana yang paling cocok dan mengapa? Implementasikan!

**Penyelesaian:**

**Analisis:**
- Data update sangat sering (10× per detik)
- Perubahan minimal antar update (objek bergerak sedikit)
- Artinya data hampir selalu "hampir terurut"

**Jawaban: Insertion Sort** adalah pilihan terbaik karena:
1. O(n) untuk data hampir terurut
2. Adaptif terhadap perubahan kecil
3. Overhead minimal
4. Stabil (penting jika ada tie-breaker lain)

**Implementasi:**

```cpp
#include <iostream>
#include <cmath>
#include <cstdlib>
using namespace std;

struct ObjekRadar {
    int id;
    double jarak;      // km dari radar
    double azimuth;    // derajat (0-360)
    double kecepatan;  // km/jam
    char jenis[20];
    int threatLevel;   // 1-5
};

// Insertion Sort berdasarkan jarak (ascending)
// Dioptimasi untuk data hampir terurut
void sortByJarak(ObjekRadar arr[], int n) {
    for (int i = 1; i < n; i++) {
        ObjekRadar key = arr[i];
        int j = i - 1;
        
        // Hanya geser jika benar-benar perlu
        while (j >= 0 && arr[j].jarak > key.jarak) {
            arr[j + 1] = arr[j];
            j--;
        }
        
        // Hanya assignment jika ada pergerakan
        if (j + 1 != i) {
            arr[j + 1] = key;
        }
    }
}

// Simulasi update posisi (objek bergerak sedikit)
void updatePosisi(ObjekRadar arr[], int n) {
    for (int i = 0; i < n; i++) {
        // Random movement: -2 to +2 km (kecil)
        double delta = (rand() % 500 - 250) / 100.0;
        arr[i].jarak += delta;
        if (arr[i].jarak < 0) arr[i].jarak = 0;
    }
}

void cetakRadar(ObjekRadar arr[], int n) {
    cout << "ID\tJarak(km)\tAzimuth\tThreat" << endl;
    cout << "----------------------------------------" << endl;
    for (int i = 0; i < n; i++) {
        cout << arr[i].id << "\t" 
             << fixed << arr[i].jarak << "\t\t"
             << arr[i].azimuth << "\t"
             << arr[i].threatLevel << endl;
    }
}

int main() {
    srand(42);  // Seed untuk reproducibility
    
    // Inisialisasi objek radar
    ObjekRadar radar[] = {
        {1001, 50.5, 45, 200, "Pesawat", 2},
        {1002, 75.2, 120, 150, "Helikopter", 1},
        {1003, 120.8, 200, 400, "Jet", 3},
        {1004, 35.1, 90, 100, "Drone", 4},
        {1005, 200.0, 270, 500, "Rudal", 5}
    };
    int n = 5;
    
    cout << "=== SISTEM TRACKING RADAR ===" << endl;
    
    // Initial sort
    sortByJarak(radar, n);
    cout << "\nPosisi Awal (sorted by jarak):" << endl;
    cetakRadar(radar, n);
    
    // Simulasi 3 cycle update
    for (int cycle = 1; cycle <= 3; cycle++) {
        cout << "\n--- Update Cycle " << cycle << " ---" << endl;
        
        // Update posisi (perubahan kecil)
        updatePosisi(radar, n);
        
        // Re-sort (sangat cepat karena hampir terurut)
        sortByJarak(radar, n);
        
        cetakRadar(radar, n);
    }
    
    return 0;
}
```

**Output:**
```
=== SISTEM TRACKING RADAR ===

Posisi Awal (sorted by jarak):
ID	Jarak(km)	Azimuth	Threat
----------------------------------------
1004	35.100000		90	4
1001	50.500000		45	2
1002	75.200000		120	1
1003	120.800000		200	3
1005	200.000000		270	5

--- Update Cycle 1 ---
ID	Jarak(km)	Azimuth	Threat
----------------------------------------
1004	35.380000		90	4
1001	49.730000		45	2
1002	73.380000		120	1
1003	122.290000		200	3
1005	199.510000		270	5

--- Update Cycle 2 ---
...
```

**Keuntungan pendekatan ini:**
- Setiap re-sort hanya membutuhkan O(n) karena data hampir terurut
- Sistem dapat memproses update dengan latensi minimal
- Prioritas tracking selalu akurat

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Implementasikan generic sorting function menggunakan function pointer agar dapat mengurutkan berbagai tipe data!

**Penyelesaian:**

```cpp
#include <iostream>
#include <cstring>
using namespace std;

// Tipe function pointer untuk fungsi perbandingan
// Return: negative jika a < b, 0 jika a == b, positive jika a > b
typedef int (*CompareFunc)(const void*, const void*);

// Generic Insertion Sort
void genericInsertionSort(void* arr, int n, int size, CompareFunc compare) {
    char* base = (char*)arr;
    char* temp = new char[size];  // Temporary storage
    
    for (int i = 1; i < n; i++) {
        // Copy current element to temp
        memcpy(temp, base + i * size, size);
        
        int j = i - 1;
        while (j >= 0 && compare(base + j * size, temp) > 0) {
            // Shift element to the right
            memcpy(base + (j + 1) * size, base + j * size, size);
            j--;
        }
        
        // Insert temp at correct position
        memcpy(base + (j + 1) * size, temp, size);
    }
    
    delete[] temp;
}

// === Fungsi Perbandingan untuk Integer ===
int compareIntAsc(const void* a, const void* b) {
    return (*(int*)a - *(int*)b);
}

int compareIntDesc(const void* a, const void* b) {
    return (*(int*)b - *(int*)a);
}

// === Fungsi Perbandingan untuk String ===
int compareStrAsc(const void* a, const void* b) {
    return strcmp((char*)a, (char*)b);
}

// === Struct dan fungsi perbandingannya ===
struct Mahasiswa {
    int nim;
    char nama[50];
    double ipk;
};

int compareMhsByNIM(const void* a, const void* b) {
    return ((Mahasiswa*)a)->nim - ((Mahasiswa*)b)->nim;
}

int compareMhsByIPK(const void* a, const void* b) {
    double diff = ((Mahasiswa*)b)->ipk - ((Mahasiswa*)a)->ipk;
    if (diff > 0) return 1;
    if (diff < 0) return -1;
    return 0;
}

int main() {
    // Test 1: Sort integer array (ascending)
    cout << "=== Test 1: Integer Ascending ===" << endl;
    int nums[] = {64, 34, 25, 12, 22, 11, 90};
    int n = 7;
    
    cout << "Before: ";
    for (int i = 0; i < n; i++) cout << nums[i] << " ";
    cout << endl;
    
    genericInsertionSort(nums, n, sizeof(int), compareIntAsc);
    
    cout << "After:  ";
    for (int i = 0; i < n; i++) cout << nums[i] << " ";
    cout << endl;
    
    // Test 2: Sort integer array (descending)
    cout << "\n=== Test 2: Integer Descending ===" << endl;
    int nums2[] = {64, 34, 25, 12, 22, 11, 90};
    
    genericInsertionSort(nums2, n, sizeof(int), compareIntDesc);
    
    cout << "Result: ";
    for (int i = 0; i < n; i++) cout << nums2[i] << " ";
    cout << endl;
    
    // Test 3: Sort struct by different fields
    cout << "\n=== Test 3: Struct Mahasiswa ===" << endl;
    Mahasiswa mhs[] = {
        {103, "Citra", 3.75},
        {101, "Ahmad", 3.50},
        {104, "Dewi", 3.90},
        {102, "Budi", 3.25}
    };
    int m = 4;
    
    cout << "By NIM:" << endl;
    genericInsertionSort(mhs, m, sizeof(Mahasiswa), compareMhsByNIM);
    for (int i = 0; i < m; i++) {
        cout << mhs[i].nim << " - " << mhs[i].nama 
             << " (IPK: " << mhs[i].ipk << ")" << endl;
    }
    
    cout << "\nBy IPK (descending):" << endl;
    genericInsertionSort(mhs, m, sizeof(Mahasiswa), compareMhsByIPK);
    for (int i = 0; i < m; i++) {
        cout << mhs[i].nim << " - " << mhs[i].nama 
             << " (IPK: " << mhs[i].ipk << ")" << endl;
    }
    
    return 0;
}
```

**Output:**
```
=== Test 1: Integer Ascending ===
Before: 64 34 25 12 22 11 90 
After:  11 12 22 25 34 64 90 

=== Test 2: Integer Descending ===
Result: 90 64 34 25 22 12 11 

=== Test 3: Struct Mahasiswa ===
By NIM:
101 - Ahmad (IPK: 3.5)
102 - Budi (IPK: 3.25)
103 - Citra (IPK: 3.75)
104 - Dewi (IPK: 3.9)

By IPK (descending):
104 - Dewi (IPK: 3.9)
103 - Citra (IPK: 3.75)
101 - Ahmad (IPK: 3.5)
102 - Budi (IPK: 3.25)
```

---

### SOLVED PROBLEM 21 ⭐⭐⭐

**Soal:** Implementasikan Binary Insertion Sort yang menggunakan binary search untuk menemukan posisi insert!

**Penyelesaian:**

```cpp
#include <iostream>
using namespace std;

// Binary search untuk menemukan posisi insert
int binarySearch(int arr[], int item, int low, int high) {
    while (low <= high) {
        int mid = low + (high - low) / 2;
        
        if (item == arr[mid])
            return mid + 1;  // Insert setelah elemen yang sama (stable)
        
        if (item > arr[mid])
            low = mid + 1;
        else
            high = mid - 1;
    }
    
    return low;  // Posisi insert
}

void binaryInsertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        // Gunakan binary search untuk mencari posisi insert
        // Hanya di bagian yang sudah terurut [0..i-1]
        int pos = binarySearch(arr, key, 0, j);
        
        // Geser semua elemen dari pos sampai i-1 ke kanan
        while (j >= pos) {
            arr[j + 1] = arr[j];
            j--;
        }
        
        // Insert key di posisi yang tepat
        arr[pos] = key;
    }
}

// Standard Insertion Sort untuk perbandingan
void standardInsertionSort(int arr[], int n, int& comparisons) {
    comparisons = 0;
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        
        while (j >= 0) {
            comparisons++;
            if (arr[j] > key) {
                arr[j + 1] = arr[j];
                j--;
            } else {
                break;
            }
        }
        arr[j + 1] = key;
    }
}

// Binary Insertion Sort dengan counting
void binaryInsertionSortWithCount(int arr[], int n, int& comparisons) {
    comparisons = 0;
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        int low = 0, high = j;
        
        // Binary search dengan counting
        while (low <= high) {
            comparisons++;
            int mid = low + (high - low) / 2;
            if (key >= arr[mid])
                low = mid + 1;
            else
                high = mid - 1;
        }
        
        int pos = low;
        
        while (j >= pos) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[pos] = key;
    }
}

int main() {
    const int N = 20;
    int arr1[N], arr2[N];
    
    // Generate random array
    srand(42);
    for (int i = 0; i < N; i++) {
        arr1[i] = rand() % 100;
        arr2[i] = arr1[i];
    }
    
    cout << "Array awal: ";
    for (int i = 0; i < N; i++) cout << arr1[i] << " ";
    cout << endl;
    
    int comp1, comp2;
    
    standardInsertionSort(arr1, N, comp1);
    binaryInsertionSortWithCount(arr2, N, comp2);
    
    cout << "\nHasil Standard Insertion Sort: ";
    for (int i = 0; i < N; i++) cout << arr1[i] << " ";
    cout << endl;
    cout << "Jumlah perbandingan: " << comp1 << endl;
    
    cout << "\nHasil Binary Insertion Sort: ";
    for (int i = 0; i < N; i++) cout << arr2[i] << " ";
    cout << endl;
    cout << "Jumlah perbandingan: " << comp2 << endl;
    
    cout << "\n=== ANALISIS ===" << endl;
    cout << "Standard: O(n^2) comparisons dalam worst case" << endl;
    cout << "Binary:   O(n log n) comparisons" << endl;
    cout << "Catatan:  Keduanya tetap O(n^2) karena shift masih O(n) per elemen" << endl;
    
    return 0;
}
```

**Output:**
```
Array awal: 67 93 49 38 74 36 15 44 22 71 63 52 13 59 41 88 50 29 96 24 

Hasil Standard Insertion Sort: 13 15 22 24 29 36 38 41 44 49 50 52 59 63 67 71 74 88 93 96 
Jumlah perbandingan: 107

Hasil Binary Insertion Sort: 13 15 22 24 29 36 38 41 44 49 50 52 59 63 67 71 74 88 93 96 
Jumlah perbandingan: 66

=== ANALISIS ===
Standard: O(n^2) comparisons dalam worst case
Binary:   O(n log n) comparisons
Catatan:  Keduanya tetap O(n^2) karena shift masih O(n) per elemen
```

**Analisis:**
- Binary Insertion Sort mengurangi jumlah perbandingan dari O(n²) menjadi O(n log n)
- Namun jumlah operasi shift tetap O(n²) dalam worst case
- Total kompleksitas tetap O(n²)
- Berguna ketika operasi perbandingan mahal (misalnya membandingkan string panjang)

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Sistem komunikasi militer menerima pesan dengan timestamp dan priority. Implementasikan sorting yang mengurutkan berdasarkan priority (primary) dan timestamp (secondary) dengan efisien!

**Penyelesaian:**

```cpp
#include <iostream>
#include <cstring>
#include <ctime>
using namespace std;

struct MilitaryMessage {
    int id;
    int priority;       // 1=LOW, 2=NORMAL, 3=HIGH, 4=URGENT, 5=FLASH
    long timestamp;     // Unix timestamp
    char sender[50];
    char content[200];
    bool encrypted;
};

// Comparator: Sort by priority DESC, then timestamp ASC
bool shouldSwap(const MilitaryMessage& a, const MilitaryMessage& b) {
    // Primary key: priority (descending - higher priority first)
    if (a.priority != b.priority) {
        return a.priority < b.priority;  // Swap jika a priority lebih rendah
    }
    // Secondary key: timestamp (ascending - older messages first within same priority)
    return a.timestamp > b.timestamp;  // Swap jika a lebih baru
}

// Insertion Sort - stable dan adaptif
void sortMessages(MilitaryMessage arr[], int n) {
    for (int i = 1; i < n; i++) {
        MilitaryMessage key = arr[i];
        int j = i - 1;
        
        while (j >= 0 && shouldSwap(arr[j], key)) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}

const char* getPriorityName(int p) {
    switch(p) {
        case 1: return "LOW";
        case 2: return "NORMAL";
        case 3: return "HIGH";
        case 4: return "URGENT";
        case 5: return "FLASH";
        default: return "UNKNOWN";
    }
}

void printMessages(MilitaryMessage arr[], int n) {
    cout << "ID\tPriority\tTimestamp\tSender\t\tEncrypted" << endl;
    cout << "================================================================" << endl;
    for (int i = 0; i < n; i++) {
        cout << arr[i].id << "\t" 
             << getPriorityName(arr[i].priority) << "\t\t"
             << arr[i].timestamp << "\t"
             << arr[i].sender << "\t\t"
             << (arr[i].encrypted ? "Yes" : "No") << endl;
    }
}

int main() {
    // Simulasi message queue
    MilitaryMessage messages[] = {
        {1001, 2, 1700000100, "Alpha-1", "Status report", true},
        {1002, 4, 1700000050, "Bravo-2", "Enemy spotted", true},
        {1003, 3, 1700000200, "Charlie-3", "Request backup", false},
        {1004, 5, 1700000150, "HQ", "FLASH message", true},
        {1005, 4, 1700000080, "Delta-4", "Position update", true},
        {1006, 2, 1700000020, "Echo-5", "Routine check", false},
        {1007, 5, 1700000120, "HQ", "Priority intel", true},
        {1008, 3, 1700000180, "Alpha-1", "Mission complete", true}
    };
    int n = 8;
    
    cout << "=== MILITARY MESSAGE QUEUE ===" << endl;
    cout << "\nBefore Sorting (arrival order):" << endl;
    printMessages(messages, n);
    
    sortMessages(messages, n);
    
    cout << "\nAfter Sorting (by Priority DESC, Timestamp ASC):" << endl;
    printMessages(messages, n);
    
    cout << "\n=== PROCESSING ORDER ===" << endl;
    cout << "Messages will be processed in this order:" << endl;
    for (int i = 0; i < n; i++) {
        cout << (i+1) << ". [" << getPriorityName(messages[i].priority) 
             << "] " << messages[i].sender << ": " << messages[i].content << endl;
    }
    
    return 0;
}
```

**Output:**
```
=== MILITARY MESSAGE QUEUE ===

Before Sorting (arrival order):
ID	Priority	Timestamp	Sender		Encrypted
================================================================
1001	NORMAL		1700000100	Alpha-1		Yes
1002	URGENT		1700000050	Bravo-2		Yes
1003	HIGH		1700000200	Charlie-3	No
1004	FLASH		1700000150	HQ		Yes
1005	URGENT		1700000080	Delta-4		Yes
1006	NORMAL		1700000020	Echo-5		No
1007	FLASH		1700000120	HQ		Yes
1008	HIGH		1700000180	Alpha-1		Yes

After Sorting (by Priority DESC, Timestamp ASC):
ID	Priority	Timestamp	Sender		Encrypted
================================================================
1007	FLASH		1700000120	HQ		Yes
1004	FLASH		1700000150	HQ		Yes
1002	URGENT		1700000050	Bravo-2		Yes
1005	URGENT		1700000080	Delta-4		Yes
1008	HIGH		1700000180	Alpha-1		Yes
1003	HIGH		1700000200	Charlie-3	No
1006	NORMAL		1700000020	Echo-5		No
1001	NORMAL		1700000100	Alpha-1		Yes

=== PROCESSING ORDER ===
Messages will be processed in this order:
1. [FLASH] HQ: Priority intel
2. [FLASH] HQ: FLASH message
3. [URGENT] Bravo-2: Enemy spotted
4. [URGENT] Delta-4: Position update
5. [HIGH] Alpha-1: Mission complete
6. [HIGH] Charlie-3: Request backup
7. [NORMAL] Echo-5: Routine check
8. [NORMAL] Alpha-1: Status report
```

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan. Jawaban singkat tersedia di bagian akhir.

### Problem S1 ⭐
Apa output Bubble Sort optimized pada array [1, 2, 3, 5, 4]? Berapa jumlah pass yang dilakukan?

### Problem S2 ⭐⭐
Implementasikan Cocktail Shaker Sort (variasi Bubble Sort yang maju-mundur)!

### Problem S3 ⭐⭐
Untuk n=1000, berapa perbandingan yang dilakukan Selection Sort? Apakah berbeda untuk best, average, dan worst case?

### Problem S4 ⭐⭐⭐
Modifikasi Insertion Sort agar dapat menangani data yang masuk secara streaming (satu per satu) dengan efisien!

### Problem S5 ⭐⭐⭐
Buktikan secara matematis bahwa lower bound untuk comparison-based sorting adalah Ω(n log n)!

---

## Ringkasan

| Konsep | Deskripsi | Catatan Penting |
|--------|-----------|-----------------|
| **Sorting** | Proses menyusun ulang elemen berdasarkan kriteria | Fundamental dalam ilmu komputer |
| **Bubble Sort** | Menukar elemen bersebelahan yang tidak terurut | O(n) best case dengan optimasi |
| **Selection Sort** | Memilih minimum dan swap ke posisi yang tepat | Jumlah swap minimum: O(n) |
| **Insertion Sort** | Menyisipkan elemen ke posisi yang tepat | Terbaik untuk data hampir terurut |
| **Stable Sort** | Mempertahankan urutan relatif elemen dengan nilai sama | Bubble & Insertion stable |
| **Adaptive Sort** | Performa lebih baik pada data hampir terurut | Bubble (optimized) & Insertion |
| **In-place Sort** | Membutuhkan O(1) memori tambahan | Ketiga algoritma in-place |
| **Kompleksitas** | Ketiga algoritma O(n²) average/worst case | Tidak cocok untuk data besar |

---

## Jawaban Supplementary Problems

**S1:** 
- Output: [1, 2, 3, 4, 5]
- Jumlah pass: 2 (pass 1 untuk swap 5↔4, pass 2 untuk verifikasi tidak ada swap)

**S2:**
```cpp
void cocktailShakerSort(int arr[], int n) {
    bool swapped = true;
    int start = 0, end = n - 1;
    
    while (swapped) {
        swapped = false;
        
        // Left to right pass
        for (int i = start; i < end; i++) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                swapped = true;
            }
        }
        if (!swapped) break;
        end--;
        
        swapped = false;
        
        // Right to left pass
        for (int i = end - 1; i >= start; i--) {
            if (arr[i] > arr[i + 1]) {
                swap(arr[i], arr[i + 1]);
                swapped = true;
            }
        }
        start++;
    }
}
```

**S3:**
- Perbandingan = n(n-1)/2 = 1000(999)/2 = 499,500
- **Sama untuk semua kasus** karena Selection Sort tidak adaptif

**S4:**
```cpp
// Maintain sorted array, insert new element
void insertSorted(int arr[], int& n, int newVal) {
    int i = n - 1;
    while (i >= 0 && arr[i] > newVal) {
        arr[i + 1] = arr[i];
        i--;
    }
    arr[i + 1] = newVal;
    n++;
}
```

**S5:**
- Setiap comparison-based sort membuat decision tree
- Tree dengan n! leaves (semua permutasi) memiliki height minimal log₂(n!)
- Menggunakan Stirling's approximation: log₂(n!) ≈ n log₂(n) - n log₂(e)
- Jadi minimal Ω(n log n) perbandingan diperlukan

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 2.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 7.2.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 13.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
