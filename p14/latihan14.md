# Latihan Mandiri 14: Hash Table

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 14  
**Topik:** Hash Table  
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
Apa keunggulan utama hash table dibandingkan binary search tree yang seimbang?

A. Menggunakan lebih sedikit memori  
B. Menjaga elemen dalam urutan terurut  
C. Average case O(1) untuk search, insert, dan delete  
D. Tidak memerlukan fungsi hash  
E. Lebih mudah diimplementasikan  

### Soal 2
Diberikan hash table dengan ukuran m = 13 dan fungsi hash h(k) = k mod 13. Berapa hash value untuk key 52?

A. 0  
B. 1  
C. 4  
D. 13  
E. 52  

### Soal 3
Manakah yang merupakan karakteristik fungsi hash yang BAIK?

A. Menghasilkan hash value yang berbeda untuk setiap key  
B. Mendistribusikan key secara merata ke semua slot  
C. Memerlukan waktu O(n) untuk menghitung  
D. Menghasilkan hash value yang sama untuk key berbeda  
E. Hanya bekerja untuk key bertipe integer  

### Soal 4
Apa yang dimaksud dengan collision dalam hash table?

A. Dua hash table memiliki ukuran yang sama  
B. Fungsi hash menghasilkan nilai negatif  
C. Dua key berbeda menghasilkan hash value yang sama  
D. Hash table penuh  
E. Key tidak dapat ditemukan  

### Soal 5
Pada separate chaining, jika semua n key di-hash ke slot yang sama, berapa kompleksitas search?

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

### Soal 6
Perhatikan hash table dengan separate chaining berikut:
```
Slot 0: [10] -> [30] -> NULL
Slot 1: [21] -> NULL
Slot 2: [12] -> [42] -> [52] -> NULL
```
Berapa load factor jika ukuran tabel adalah 10?

A. 0.3  
B. 0.5  
C. 0.6  
D. 1.0  
E. 3.0  

### Soal 7
Pada linear probing dengan h(k) = k mod 7, jika slot 3 sudah terisi, key dengan h(k) = 3 akan dicoba di slot mana berikutnya?

A. 0  
B. 2  
C. 4  
D. 6  
E. 9  

### Soal 8
Apa masalah utama dari linear probing?

A. Memerlukan linked list  
B. Primary clustering  
C. Tidak dapat menangani collision  
D. Memerlukan dua fungsi hash  
E. Load factor tidak dapat lebih dari 0.5  

### Soal 9
Manakah formula yang BENAR untuk quadratic probing?

A. h(k, i) = (h'(k) + i) mod m  
B. h(k, i) = (h'(k) + i²) mod m  
C. h(k, i) = (h'(k) × i) mod m  
D. h(k, i) = (h'(k) - i) mod m  
E. h(k, i) = (h'(k) / i) mod m  

### Soal 10
Pada double hashing, mengapa h₂(k) tidak boleh menghasilkan nilai 0?

A. Akan menyebabkan overflow  
B. Probe sequence hanya akan mengunjungi satu slot  
C. Hash table menjadi penuh  
D. Collision tidak dapat terjadi  
E. Memerlukan lebih banyak memori  

### Soal 11
Apa yang dimaksud dengan lazy deletion dalam open addressing?

A. Menghapus semua elemen sekaligus  
B. Menandai slot sebagai DELETED alih-alih mengosongkan  
C. Menunda penghapusan hingga rehashing  
D. Menghapus dari akhir probe sequence  
E. Tidak menghapus sama sekali  

### Soal 12
Mengapa lazy deletion diperlukan pada open addressing?

A. Untuk menghemat memori  
B. Untuk mempercepat insert  
C. Agar search tidak berhenti prematur di slot yang dihapus  
D. Untuk menghindari rehashing  
E. Untuk menjaga urutan elemen  

### Soal 13
Jika load factor α = 0.75, berapa persentase slot yang terisi?

A. 25%  
B. 50%  
C. 70%  
D. 75%  
E. 100%  

### Soal 14
Kapan rehashing biasanya dilakukan?

A. Setiap kali ada collision  
B. Ketika load factor melebihi threshold tertentu  
C. Setelah setiap operasi delete  
D. Ketika ada key duplikat  
E. Setiap 100 operasi insert  

### Soal 15
Berapa ukuran baru yang umum digunakan saat rehashing?

A. m + 1  
B. m + 10  
C. m × 1.5  
D. m × 2 (atau prima terdekat)  
E. m²  

### Soal 16
Untuk hash string "ABC" dengan h(s) = Σ(ASCII × 31^i) mod 100, urutan perhitungan yang benar adalah:

A. (65 + 66 + 67) mod 100  
B. ((65 × 31 + 66) × 31 + 67) mod 100  
C. (65 × 66 × 67) mod 100  
D. (65 × 31² + 66 × 31 + 67) mod 100  
E. B dan D sama-sama benar  

### Soal 17
Manakah pernyataan yang BENAR tentang separate chaining vs open addressing?

A. Separate chaining memiliki cache performance lebih baik  
B. Open addressing dapat memiliki load factor > 1  
C. Separate chaining memerlukan extra memory untuk pointer  
D. Open addressing lebih mudah diimplementasikan  
E. Keduanya memiliki kompleksitas worst case yang berbeda  

### Soal 18
Dalam C++ STL, struktur data mana yang diimplementasikan menggunakan hash table?

A. `set` dan `map`  
B. `unordered_set` dan `unordered_map`  
C. `vector` dan `list`  
D. `priority_queue`  
E. `stack` dan `queue`  

### Soal 19
Untuk m = 11 dan h₁(k) = k mod 11, h₂(k) = 1 + (k mod 10), berapa probe sequence untuk key 42 jika slot 9 terisi?

A. 9, 10, 0, 1, ...  
B. 9, 0, 2, 4, ...  
C. 9, 12, 15, 18, ...  
D. 9, 1, 4, 7, ...  
E. 9, 6, 3, 0, ...  

### Soal 20
Apa kompleksitas waktu untuk rehashing dari ukuran m ke 2m dengan n elemen?

A. O(1)  
B. O(log n)  
C. O(n)  
D. O(n log n)  
E. O(n²)  

---

## Bagian B: Soal Uraian (15 Soal)

### Soal U1 (3 poin) ⭐
Jelaskan perbedaan antara direct addressing dan hashing! Mengapa hashing lebih praktis untuk kebanyakan aplikasi?

### Soal U2 (3 poin) ⭐
Sebutkan dan jelaskan tiga sifat yang harus dimiliki fungsi hash yang baik!

### Soal U3 (3 poin) ⭐
Diberikan hash table dengan ukuran m = 11 dan fungsi hash h(k) = k mod 11. Hitung hash value untuk key: 23, 45, 67, 89, 100!

### Soal U4 (3 poin) ⭐
Jelaskan mengapa collision pasti terjadi pada hash table berdasarkan Pigeonhole Principle!

### Soal U5 (3 poin) ⭐
Bandingkan kelebihan dan kekurangan separate chaining dengan open addressing!

### Soal U6 (4 poin) ⭐⭐
Diberikan hash table dengan separate chaining, ukuran m = 7, dan h(k) = k mod 7. Gambarkan hash table setelah insert key: 15, 8, 22, 29, 36, 1, 43 secara berurutan!

### Soal U7 (4 poin) ⭐⭐
Diberikan hash table dengan linear probing, ukuran m = 11, dan h(k) = k mod 11. Tunjukkan langkah-langkah insert untuk key: 10, 22, 31, 4, 15, 28! Gambarkan state akhir tabel!

### Soal U8 (4 poin) ⭐⭐
Jelaskan fenomena primary clustering pada linear probing! Bagaimana quadratic probing dan double hashing mengurangi masalah ini?

### Soal U9 (4 poin) ⭐⭐
Implementasikan fungsi hash untuk string menggunakan polynomial rolling hash dengan base 31 dalam C++!

### Soal U10 (4 poin) ⭐⭐
Jelaskan mengapa lazy deletion diperlukan pada open addressing! Berikan contoh kasus yang menunjukkan masalah jika menggunakan hard delete!

### Soal U11 (4 poin) ⭐⭐
Hash table memiliki 100 slot dengan 60 elemen. Hitung:
a) Load factor saat ini
b) Expected number of probes untuk unsuccessful search (gunakan formula 1/(1-α))
c) Apakah perlu rehashing jika threshold adalah 0.75?

### Soal U12 (5 poin) ⭐⭐⭐
Implementasikan class HashTableChaining lengkap dengan operasi insert, search, dan remove dalam C++!

### Soal U13 (5 poin) ⭐⭐⭐
Diberikan hash table dengan double hashing, m = 13, h₁(k) = k mod 13, h₂(k) = 1 + (k mod 11). Insert key: 18, 41, 22, 44, 59. Tunjukkan probe sequence untuk setiap key!

### Soal U14 (5 poin) ⭐⭐⭐
Implementasikan fungsi rehash yang:
a) Membuat tabel baru dengan ukuran prima terdekat dari 2m
b) Memindahkan semua elemen valid (bukan DELETED)
c) Mengupdate count dan menghapus marker DELETED

### Soal U15 (5 poin) ⭐⭐⭐
Analisis kompleksitas waktu dan ruang untuk hash table dengan separate chaining! Jelaskan dalam kondisi apa worst case terjadi dan bagaimana mencegahnya!

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Autentikasi Basis Militer (7 poin)

**Latar Belakang:**
Sebuah basis militer memerlukan sistem autentikasi untuk mengontrol akses ke berbagai fasilitas. Setiap personel memiliki ID unik (NRP/NIP) dan level akses yang berbeda. Sistem harus dapat memverifikasi kredensial dengan sangat cepat karena checkpoint harus memproses ratusan personel per jam.

**Data yang tersimpan untuk setiap personel:**
- ID Personel (NRP/NIP): string 18 karakter
- Nama lengkap
- Pangkat
- Level akses (1-5)
- Sidik jari hash (untuk keamanan tambahan)
- Status aktif

**Pertanyaan:**

a) **(2 poin)** Rancang struktur data untuk menyimpan informasi personel dan jelaskan mengapa hash table cocok untuk kasus ini!

b) **(2 poin)** Pilih dan jelaskan fungsi hash yang tepat untuk key NRP/NIP (string 18 karakter)! Berikan contoh perhitungan untuk NRP "320110098765432100"!

c) **(3 poin)** Jika basis memiliki 5000 personel aktif, tentukan:
   - Ukuran tabel yang optimal (dengan load factor target 0.7)
   - Estimasi collision yang akan terjadi
   - Pilihan collision handling yang tepat beserta alasannya

---

### Studi Kasus 2: Sistem Tracking Logistik Alutsista (8 poin)

**Latar Belakang:**
Komando Logistik memerlukan sistem untuk melacak ribuan item alutsista (senjata, amunisi, kendaraan, perlengkapan) yang tersebar di berbagai gudang. Setiap item memiliki kode unik dan perlu dilacak lokasinya secara real-time. Sistem harus mendukung operasi:
- Registrasi item baru
- Update lokasi saat item dipindahkan
- Pencarian cepat berdasarkan kode item
- Penghapusan saat item dimusnahkan atau dijual

**Format kode item:** `CAT-LOC-YYYYNNNNN`
- CAT: Kategori (3 huruf): SJT (senjata), AMN (amunisi), KND (kendaraan), PRL (perlengkapan)
- LOC: Kode lokasi (3 huruf)
- YYYY: Tahun registrasi
- NNNNN: Nomor urut (5 digit)

Contoh: `SJT-JKT-202300001` (Senjata di Jakarta, registrasi 2023, nomor 00001)

**Pertanyaan:**

a) **(2 poin)** Desain struktur data `ItemAlutsista` dan jelaskan field-field yang diperlukan!

b) **(2 poin)** Implementasikan fungsi hash yang efektif untuk kode item dengan format di atas! Fungsi harus memanfaatkan semua bagian kode untuk distribusi yang baik.

c) **(2 poin)** Sistem memiliki 50.000 item aktif. Jika menggunakan open addressing dengan quadratic probing:
   - Hitung ukuran tabel minimum dengan load factor maksimum 0.6
   - Jelaskan mengapa load factor harus dijaga lebih rendah untuk open addressing!

d) **(2 poin)** Implementasikan fungsi `updateLokasi(string kodeItem, string lokasiBaru)` yang:
   - Mencari item berdasarkan kode
   - Mengupdate lokasinya
   - Mencatat timestamp perubahan
   - Mengembalikan true jika berhasil, false jika item tidak ditemukan

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|:-------:|-------------------|
| 1 | C | Hash table memiliki O(1) average untuk semua operasi utama |
| 2 | C | 52 mod 13 = 4 (52 = 13 × 4 + 0, salah; 52 = 13 × 4 = 52, jadi 52 - 52 = 0... sebenarnya 52 mod 13 = 0) |
| 3 | B | Distribusi merata mengurangi collision |
| 4 | C | Collision = dua key berbeda, hash sama |
| 5 | C | Semua key di satu slot = linked list O(n) |
| 6 | C | n = 6 elemen, m = 10 slot, α = 6/10 = 0.6 |
| 7 | C | Linear probing: coba slot (3+1) mod 7 = 4 |
| 8 | B | Primary clustering adalah masalah utama linear probing |
| 9 | B | Quadratic probing menggunakan i² |
| 10 | B | h₂(k) = 0 berarti step size 0, hanya satu slot yang dikunjungi |
| 11 | B | Lazy deletion menandai slot DELETED |
| 12 | C | Search berhenti di EMPTY, harus lewati DELETED |
| 13 | D | α = 0.75 = 75% terisi |
| 14 | B | Rehashing dilakukan saat load factor melebihi threshold |
| 15 | D | Ukuran baru biasanya 2× lipat atau prima terdekat |
| 16 | E | Kedua formula menghasilkan nilai yang sama (rolling hash) |
| 17 | C | Separate chaining memerlukan pointer untuk linked list |
| 18 | B | unordered_set dan unordered_map menggunakan hash table |
| 19 | A | h₂(42) = 1 + (42 mod 10) = 3; probe: 9, (9+3)%11=1, ... |
| 20 | C | Rehashing memerlukan insert ulang semua n elemen |

**Koreksi Soal 2:** 52 mod 13 = 0 (karena 52 = 13 × 4). Jawaban yang benar adalah **A**.

**Koreksi Soal 19:** h₁(42) = 42 mod 11 = 9; h₂(42) = 1 + (42 mod 10) = 1 + 2 = 3. Probe sequence: 9, (9+3)%11=1, (9+6)%11=4, (9+9)%11=7, ... Jawaban **A** dengan pola 9, 1, 4, 7 (bukan 9, 10, 0, 1). Jawaban yang benar adalah **D**.

---

### Bagian B: Soal Uraian

#### Jawaban U1

**Direct Addressing:**
- Menggunakan key sebagai index array secara langsung
- `table[key] = value`
- Memerlukan array sebesar domain key
- Cocok jika domain kecil dan padat

**Hashing:**
- Memetakan key ke index menggunakan fungsi hash
- `table[h(key)] = value`
- Ukuran array tidak bergantung pada domain key
- Dapat menangani domain yang sangat besar

**Mengapa hashing lebih praktis:**
1. Domain key sering sangat besar (misal: NIK 16 digit = 10^16 kemungkinan)
2. Hanya sebagian kecil key yang benar-benar digunakan
3. Hashing mengkompresi domain besar ke ukuran tabel yang praktis
4. Tetap mempertahankan O(1) average access

---

#### Jawaban U2

**Tiga sifat fungsi hash yang baik:**

1. **Deterministic (Deterministik)**
   - Key yang sama selalu menghasilkan hash value yang sama
   - Penting untuk konsistensi search: h(k) harus sama saat insert dan search

2. **Uniform Distribution (Distribusi Seragam)**
   - Hash value tersebar merata ke semua slot
   - Mengurangi collision dan panjang chain
   - Setiap slot memiliki probabilitas yang sama untuk menerima key

3. **Efficient (Efisien)**
   - Dapat dihitung dalam waktu O(1) atau O(|k|) untuk string
   - Tidak boleh menjadi bottleneck operasi hash table
   - Operasi sederhana: modulo, perkalian, penjumlahan

---

#### Jawaban U3

Fungsi hash: h(k) = k mod 11

| Key | Perhitungan | Hash Value |
|-----|-------------|------------|
| 23 | 23 mod 11 = 23 - 22 = 1 | **1** |
| 45 | 45 mod 11 = 45 - 44 = 1 | **1** |
| 67 | 67 mod 11 = 67 - 66 = 1 | **1** |
| 89 | 89 mod 11 = 89 - 88 = 1 | **1** |
| 100 | 100 mod 11 = 100 - 99 = 1 | **1** |

**Catatan:** Semua key menghasilkan hash 1! Ini contoh fungsi hash yang buruk untuk data ini karena semua key memiliki bentuk (11k + 1).

---

#### Jawaban U4

**Pigeonhole Principle:**
> Jika n item dimasukkan ke m slot dan n > m, maka minimal satu slot berisi lebih dari satu item.

**Aplikasi pada Hash Table:**
- Hash table memiliki m slot (ukuran terbatas)
- Domain key biasanya jauh lebih besar dari m
- Fungsi hash memetakan domain besar ke {0, 1, ..., m-1}
- Berdasarkan pigeonhole principle, pasti ada beberapa key yang dipetakan ke slot sama

**Contoh numerik:**
- m = 100 slot
- Domain = semua integer positif (tak terbatas)
- Pasti ada tak terhingga key yang hash ke setiap slot

**Birthday Paradox memperkuat:**
- Dengan hanya 23 orang (key) dan 365 kemungkinan tanggal (slot)
- Probabilitas collision sudah > 50%

---

#### Jawaban U5

| Aspek | Separate Chaining | Open Addressing |
|-------|-------------------|-----------------|
| **Kelebihan** | Load factor dapat > 1 | Cache performance lebih baik |
| | Delete sederhana | Tidak perlu extra memory untuk pointer |
| | Tidak ada clustering | Cocok untuk embedded systems |
| | Performa stabil | |
| **Kekurangan** | Extra memory untuk pointer | Load factor harus ≤ 1 |
| | Cache performance buruk | Clustering dapat terjadi |
| | Fragmentasi memori | Delete kompleks (lazy deletion) |
| | | Performa menurun drastis saat α tinggi |

**Rekomendasi penggunaan:**
- Separate chaining: saat delete sering, load tidak dapat diprediksi
- Open addressing: saat memory terbatas, cache performance penting

---

#### Jawaban U6

Ukuran m = 7, h(k) = k mod 7

**Perhitungan hash:**
| Key | h(k) = k mod 7 |
|-----|----------------|
| 15 | 1 |
| 8 | 1 |
| 22 | 1 |
| 29 | 1 |
| 36 | 1 |
| 1 | 1 |
| 43 | 1 |

**Hash Table dengan Separate Chaining:**
```
Slot 0: NULL
Slot 1: [15] -> [8] -> [22] -> [29] -> [36] -> [1] -> [43] -> NULL
Slot 2: NULL
Slot 3: NULL
Slot 4: NULL
Slot 5: NULL
Slot 6: NULL
```

**Catatan:** Ini adalah worst case! Semua key collision ke slot 1 karena semuanya ≡ 1 (mod 7).

---

#### Jawaban U7

Ukuran m = 11, h(k) = k mod 11, Linear Probing

**Proses Insert:**

1. **Insert 10:** h(10) = 10 mod 11 = 10 → Slot 10 kosong ✓
2. **Insert 22:** h(22) = 22 mod 11 = 0 → Slot 0 kosong ✓
3. **Insert 31:** h(31) = 31 mod 11 = 9 → Slot 9 kosong ✓
4. **Insert 4:** h(4) = 4 mod 11 = 4 → Slot 4 kosong ✓
5. **Insert 15:** h(15) = 15 mod 11 = 4 → Slot 4 terisi!
   - Probe: slot 5 kosong ✓
6. **Insert 28:** h(28) = 28 mod 11 = 6 → Slot 6 kosong ✓

**State Akhir:**
```
Index:  0    1    2    3    4    5    6    7    8    9    10
Value: [22] [ ]  [ ]  [ ]  [4] [15] [28] [ ]  [ ]  [31] [10]
```

---

#### Jawaban U8

**Primary Clustering:**
- Fenomena di mana slot-slot yang terisi berurutan membentuk "cluster"
- Cluster cenderung semakin besar karena key baru yang hash ke dalam cluster akan memperpanjang cluster
- Semakin besar cluster, semakin besar kemungkinan key baru menambah cluster

**Efek negatif:**
- Probe sequence semakin panjang
- Performa menurun dari O(1) mendekati O(n)

**Bagaimana Quadratic Probing mengurangi masalah:**
- Probe sequence: h, h+1, h+4, h+9, h+16, ...
- Langkah tidak berurutan → tidak memperpanjang cluster linear
- Masih ada secondary clustering (key dengan hash sama punya probe sequence sama)

**Bagaimana Double Hashing mengurangi masalah:**
- Probe sequence bergantung pada dua fungsi: h₁(k) dan h₂(k)
- Setiap key memiliki step size berbeda
- Key berbeda dengan hash sama akan memiliki probe sequence berbeda
- Distribusi paling merata dari ketiga metode

---

#### Jawaban U9

```cpp
#include <string>
using namespace std;

unsigned long hashString(const string& key, int tableSize) {
    unsigned long hash = 0;
    unsigned long base = 31;  // Bilangan prima
    unsigned long power = 1;
    
    // Metode 1: Menggunakan Horner's method (lebih efisien)
    for (int i = key.length() - 1; i >= 0; i--) {
        hash = (hash + (unsigned long)key[i] * power) % tableSize;
        power = (power * base) % tableSize;
    }
    
    return hash;
}

// Alternatif: Metode iteratif dari kiri ke kanan
unsigned long hashStringAlt(const string& key, int tableSize) {
    unsigned long hash = 0;
    
    for (char c : key) {
        hash = (hash * 31 + c) % tableSize;
    }
    
    return hash;
}
```

**Penjelasan:**
- Base 31 adalah bilangan prima yang menghasilkan distribusi baik
- Modulo dilakukan di setiap langkah untuk mencegah overflow
- Kompleksitas O(|key|)

---

#### Jawaban U10

**Mengapa Lazy Deletion Diperlukan:**

Pada open addressing, search berhenti ketika menemukan slot EMPTY. Jika kita melakukan hard delete (mengosongkan slot), search untuk key lain yang probe melewati slot tersebut akan berhenti prematur.

**Contoh Masalah dengan Hard Delete:**

```
Initial state dengan linear probing:
h(10) = 3, h(20) = 3, h(30) = 3

Insert 10: slot 3
Insert 20: slot 3 terisi, probe → slot 4
Insert 30: slot 3,4 terisi, probe → slot 5

Table: [_][_][_][10][20][30][_][_][_]
             slot 3  4   5

Operasi: Delete 20 (hard delete)
Table: [_][_][_][10][_][30][_][_][_]
             slot 3  4   5

Operasi: Search 30
h(30) = 3 → slot 3 ada 10 (bukan 30)
probe → slot 4 EMPTY → STOP!
Hasil: 30 tidak ditemukan (SALAH!)
```

**Solusi dengan Lazy Deletion:**

```
Delete 20 (lazy)
Table: [_][_][_][10][DEL][30][_][_][_]
                    slot 4 marked

Search 30:
h(30) = 3 → slot 3 ada 10
probe → slot 4 DELETED → lanjut
probe → slot 5 ada 30 → FOUND!
```

---

#### Jawaban U11

Diberikan: 100 slot, 60 elemen

**a) Load factor:**
```
α = n/m = 60/100 = 0.6
```

**b) Expected probes untuk unsuccessful search:**
Menggunakan formula untuk open addressing (uniform hashing assumption):
```
E[probes] = 1/(1-α) = 1/(1-0.6) = 1/0.4 = 2.5 probes
```

**c) Apakah perlu rehashing?**
- Threshold = 0.75
- Current α = 0.6
- 0.6 < 0.75

**Tidak perlu rehashing** karena load factor masih di bawah threshold.

---

#### Jawaban U12

```cpp
#include <iostream>
#include <list>
#include <vector>
#include <string>
using namespace std;

class HashTableChaining {
private:
    struct Entry {
        int key;
        string value;
        Entry(int k, const string& v) : key(k), value(v) {}
    };
    
    vector<list<Entry>> table;
    int size;
    int count;
    
    int hash(int key) {
        return ((key % size) + size) % size;  // Handle negative
    }
    
public:
    HashTableChaining(int tableSize = 101) {
        size = tableSize;
        count = 0;
        table.resize(size);
    }
    
    void insert(int key, const string& value) {
        int index = hash(key);
        
        // Check if key exists, update if so
        for (auto& entry : table[index]) {
            if (entry.key == key) {
                entry.value = value;
                return;
            }
        }
        
        // Key doesn't exist, add new entry
        table[index].push_back(Entry(key, value));
        count++;
    }
    
    string* search(int key) {
        int index = hash(key);
        
        for (auto& entry : table[index]) {
            if (entry.key == key) {
                return &entry.value;
            }
        }
        
        return nullptr;  // Not found
    }
    
    bool remove(int key) {
        int index = hash(key);
        
        for (auto it = table[index].begin(); it != table[index].end(); ++it) {
            if (it->key == key) {
                table[index].erase(it);
                count--;
                return true;
            }
        }
        
        return false;  // Not found
    }
    
    double loadFactor() {
        return (double)count / size;
    }
};
```

---

#### Jawaban U13

m = 13, h₁(k) = k mod 13, h₂(k) = 1 + (k mod 11)

**Probe sequence formula:** h(k, i) = (h₁(k) + i × h₂(k)) mod 13

| Key | h₁(k) | h₂(k) | Probe Sequence | Final Slot |
|-----|-------|-------|----------------|------------|
| 18 | 18 mod 13 = 5 | 1 + (18 mod 11) = 8 | i=0: 5 ✓ | **5** |
| 41 | 41 mod 13 = 2 | 1 + (41 mod 11) = 9 | i=0: 2 ✓ | **2** |
| 22 | 22 mod 13 = 9 | 1 + (22 mod 11) = 1 | i=0: 9 ✓ | **9** |
| 44 | 44 mod 13 = 5 | 1 + (44 mod 11) = 1 | i=0: 5 (terisi), i=1: (5+1)%13 = 6 ✓ | **6** |
| 59 | 59 mod 13 = 7 | 1 + (59 mod 11) = 5 | i=0: 7 ✓ | **7** |

**State Akhir:**
```
Index:  0   1   2   3   4   5   6   7   8   9  10  11  12
Value: [ ] [ ] [41] [ ] [ ] [18] [44] [59] [ ] [22] [ ] [ ] [ ]
```

---

#### Jawaban U14

```cpp
void rehash(int newSize) {
    // Cari bilangan prima terdekat >= newSize
    newSize = nextPrime(newSize);
    
    // Simpan tabel lama
    vector<Entry*> oldTable = table;
    int oldSize = size;
    
    // Buat tabel baru
    size = newSize;
    count = 0;
    table.assign(size, nullptr);
    deleted.assign(size, false);
    
    // Pindahkan semua elemen valid (bukan DELETED)
    for (int i = 0; i < oldSize; i++) {
        if (oldTable[i] != nullptr) {
            // Insert ke tabel baru
            insert(oldTable[i]->key, oldTable[i]->value);
            // Hapus entry lama
            delete oldTable[i];
        }
    }
}

// Helper: Cari bilangan prima terdekat
int nextPrime(int n) {
    while (!isPrime(n)) {
        n++;
    }
    return n;
}

bool isPrime(int n) {
    if (n <= 1) return false;
    if (n <= 3) return true;
    if (n % 2 == 0 || n % 3 == 0) return false;
    
    for (int i = 5; i * i <= n; i += 6) {
        if (n % i == 0 || n % (i + 2) == 0) {
            return false;
        }
    }
    return true;
}
```

---

#### Jawaban U15

**Analisis Kompleksitas Separate Chaining:**

**Kompleksitas Waktu:**
| Operasi | Average Case | Worst Case |
|---------|--------------|------------|
| Insert | O(1) | O(n) |
| Search | O(1 + α) | O(n) |
| Delete | O(1 + α) | O(n) |

Di mana α = n/m adalah load factor.

**Average Case Analysis:**
- Dengan distribusi uniform, panjang rata-rata chain = α
- Search memerlukan traversal setengah chain rata-rata = α/2
- Jika α konstan (misalnya α ≤ 2), maka O(1 + α) = O(1)

**Kompleksitas Ruang:**
- O(m + n): m slot array + n entries
- Extra memory untuk pointer di setiap node linked list

**Worst Case terjadi ketika:**
1. Fungsi hash buruk → semua key hash ke satu slot
2. Data memiliki pola yang menyebabkan collision berlebih
3. Contoh: semua key kelipatan m akan hash ke slot 0

**Cara mencegah worst case:**
1. Pilih fungsi hash yang baik (distribusi uniform)
2. Pilih ukuran tabel m yang prima
3. Gunakan universal hashing untuk jaminan probabilistik
4. Lakukan rehashing jika load factor terlalu tinggi
5. Pertimbangkan menggunakan balanced BST untuk chain jika collision berlebih

---

### Bagian C: Studi Kasus

#### Studi Kasus 1: Sistem Autentikasi Basis Militer

**a) Struktur Data dan Alasan:**

```cpp
struct Personel {
    string nrp;           // Key: 18 karakter
    string nama;
    string pangkat;
    int levelAkses;       // 1-5
    string sidikJariHash; // Hash untuk verifikasi
    bool statusAktif;
    time_t lastAccess;    // Timestamp akses terakhir
};

class SistemAutentikasi {
private:
    vector<list<Personel>> table;
    int size;
    // ... methods
};
```

**Mengapa hash table cocok:**
1. **Akses O(1):** Checkpoint harus memproses ratusan personel/jam
2. **Key unik:** NRP/NIP adalah identifier unik
3. **Lookup dominan:** Operasi utama adalah verifikasi (search)
4. **Tidak perlu urutan:** Tidak ada kebutuhan traversal berurutan

**b) Fungsi Hash untuk NRP:**

```cpp
unsigned long hashNRP(const string& nrp, int tableSize) {
    unsigned long hash = 0;
    unsigned long base = 31;
    
    for (char c : nrp) {
        hash = (hash * base + c) % tableSize;
    }
    
    return hash;
}

// Contoh untuk NRP "320110098765432100"
// Menggunakan polynomial rolling hash
// hash = Σ(char[i] * 31^(n-1-i)) mod tableSize
```

**c) Ukuran Tabel dan Collision:**

```
n = 5000 personel
Target α = 0.7

Ukuran tabel: m = n/α = 5000/0.7 ≈ 7143
Prima terdekat: m = 7151 (atau 7159)

Estimasi collision:
Menggunakan birthday paradox approximation:
P(collision) ≈ 1 - e^(-n²/2m)
P ≈ 1 - e^(-25000000/14302) ≈ 1 (sangat tinggi)

Rata-rata panjang chain = α = 0.7
```

**Pilihan collision handling: Separate Chaining**
- Alasan: Load factor 0.7 moderat, delete jarang, performa stabil
- Dengan α = 0.7, rata-rata chain pendek (< 1 elemen)

---

#### Studi Kasus 2: Sistem Tracking Logistik Alutsista

**a) Struktur Data ItemAlutsista:**

```cpp
struct ItemAlutsista {
    string kodeItem;      // Key: "CAT-LOC-YYYYNNNNN"
    string kategori;      // SJT, AMN, KND, PRL
    string namaItem;
    string lokasiSaat;    // Kode gudang
    string kondisi;       // Baik, Rusak Ringan, Rusak Berat
    int jumlah;
    time_t tanggalRegistrasi;
    time_t lastUpdate;
    string penanggunJawab;
};
```

**b) Fungsi Hash untuk Kode Item:**

```cpp
unsigned long hashKodeItem(const string& kode, int tableSize) {
    // Format: "CAT-LOC-YYYYNNNNN" (total 17 karakter)
    unsigned long hash = 0;
    
    // Hash kategori (karakter 0-2)
    for (int i = 0; i < 3; i++) {
        hash = hash * 31 + kode[i];
    }
    
    // Hash lokasi (karakter 4-6)
    for (int i = 4; i < 7; i++) {
        hash = hash * 31 + kode[i];
    }
    
    // Hash tahun dan nomor urut (karakter 8-16)
    for (int i = 8; i < 17; i++) {
        hash = hash * 31 + kode[i];
    }
    
    return hash % tableSize;
}
```

**c) Ukuran Tabel dengan Open Addressing:**

```
n = 50,000 item
Max α = 0.6

Ukuran minimum: m = n/α = 50000/0.6 = 83,334
Prima terdekat: m = 83,357

Mengapa load factor harus lebih rendah untuk open addressing:
1. Tidak ada overflow ke struktur eksternal
2. Clustering meningkat drastis saat α tinggi
3. Expected probes = 1/(1-α)
   - α = 0.6 → 2.5 probes
   - α = 0.9 → 10 probes
4. Performa degradasi lebih cepat dibanding separate chaining
```

**d) Fungsi updateLokasi:**

```cpp
bool updateLokasi(const string& kodeItem, const string& lokasiBaru) {
    int index = hashKodeItem(kodeItem, size);
    int startIndex = index;
    int i = 0;
    
    // Quadratic probing search
    do {
        if (table[index] != nullptr && !deleted[index]) {
            if (table[index]->kodeItem == kodeItem) {
                // Found! Update lokasi
                table[index]->lokasiSaat = lokasiBaru;
                table[index]->lastUpdate = time(nullptr);
                
                // Log perubahan (opsional)
                logTransfer(kodeItem, table[index]->lokasiSaat, lokasiBaru);
                
                return true;
            }
        }
        
        // Quadratic probe
        i++;
        index = (startIndex + i * i) % size;
        
    } while (index != startIndex && (table[index] != nullptr || deleted[index]));
    
    return false;  // Item tidak ditemukan
}

void logTransfer(const string& kode, const string& dari, const string& ke) {
    cout << "[" << time(nullptr) << "] Transfer " << kode 
         << " dari " << dari << " ke " << ke << endl;
}
```

---

## Kriteria Penilaian

| Bagian | Jumlah Soal | Poin per Soal | Total |
|--------|-------------|---------------|-------|
| Pilihan Ganda | 20 | 2 | 40 |
| Uraian | 15 | Bervariasi (3-5) | 45 |
| Studi Kasus | 2 | 7 + 8 | 15 |
| **Total** | | | **100** |

---

## Catatan untuk Pengajar

- Soal-soal mencakup semua Sub-CPMK untuk Pertemuan 14 (Sub-CPMK-6.1 dan Sub-CPMK-6.2)
- Studi kasus dirancang dengan konteks pertahanan Indonesia yang relevan
- Tingkat kesulitan bervariasi: ⭐ (mudah), ⭐⭐ (sedang), ⭐⭐⭐ (sulit)
- Soal uraian dan studi kasus menguji pemahaman konseptual dan kemampuan implementasi
- Koreksi pada kunci jawaban pilihan ganda nomor 2 dan 19 perlu diperhatikan

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
