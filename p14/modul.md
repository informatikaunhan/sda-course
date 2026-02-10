# Modul 14: Hash Table

**Mata Kuliah:** Struktur Data dan Algoritma  
**Kode:** SDA201  
**SKS:** 3 SKS (2 Teori + 1 Praktikum)  
**Pertemuan:** 14  
**Topik:** Hash Table

> **Capaian Pembelajaran:** Sub-CPMK-6.1, Sub-CPMK-6.2 — Mampu memahami konsep hashing, merancang fungsi hash, dan menerapkan teknik collision handling

**Estimasi Waktu Belajar:** 7 jam

**Referensi Utama:** Cormen Ch.11; Weiss Ch.5; Hubbard Ch.8

---

## Tujuan Pembelajaran

Setelah menyelesaikan modul ini, mahasiswa diharapkan mampu:

1. **Menjelaskan** konsep hashing dan keunggulannya dibanding struktur data lain
2. **Merancang** fungsi hash yang baik menggunakan berbagai metode
3. **Mengidentifikasi** penyebab collision dan dampaknya terhadap performa
4. **Mengimplementasikan** hash table dengan teknik separate chaining
5. **Mengimplementasikan** hash table dengan teknik open addressing
6. **Menganalisis** kompleksitas waktu operasi hash table
7. **Menerapkan** hash table untuk menyelesaikan permasalahan nyata

---

## 1. Pengantar Hash Table

### 1.1 Motivasi: Mengapa Perlu Hash Table?

Bayangkan sebuah sistem pertahanan yang harus menyimpan dan mengakses data ribuan personel militer berdasarkan NIK (Nomor Induk Kependudukan). Dengan struktur data yang telah dipelajari:

| Struktur Data | Operasi Search | Masalah |
|---------------|----------------|---------|
| Array tidak terurut | O(n) | Terlalu lambat untuk data besar |
| Array terurut | O(log n) | Insert/Delete lambat O(n) |
| Binary Search Tree | O(log n) rata-rata | Bisa menjadi O(n) jika tidak seimbang |

**Pertanyaan:** Bisakah kita mencapai **O(1)** untuk search, insert, dan delete?

**Jawaban:** Ya, dengan **Hash Table**!

### 1.2 Konsep Direct Addressing

Ide paling sederhana adalah **direct addressing**: gunakan key sebagai index array secara langsung.

```cpp
// Direct addressing table untuk key 0-999
int table[1000];

// Insert
table[key] = value;

// Search
return table[key];

// Delete
table[key] = -1;  // atau nilai sentinel
```

**Keuntungan:** Semua operasi O(1)

**Kelemahan:** 
- Jika key adalah NIK 16 digit, perlu array berukuran 10^16 — tidak mungkin!
- Memboroskan memori jika key tersebar (sparse)

### 1.3 Konsep Hashing

> **Definisi:** **Hashing** adalah teknik memetakan key dari domain yang besar ke domain yang lebih kecil menggunakan **fungsi hash** h(k).

![Konsep Hashing](images/gambar-14-1.png)

*Gambar 14.1: Konsep dasar hashing — memetakan key ke index array*

**Komponen Hash Table:**
1. **Array** berukuran m (disebut **bucket** atau **slot**)
2. **Fungsi hash** h: U → {0, 1, ..., m-1}
3. **Collision handling** untuk menangani h(k1) = h(k2)

---

### SOLVED PROBLEM 1 ⭐

**Soal:** Jelaskan mengapa direct addressing tidak praktis untuk menyimpan data dengan NIK sebagai key!

**Penyelesaian:**

NIK Indonesia terdiri dari 16 digit, dengan format:
- 6 digit kode wilayah
- 6 digit tanggal lahir (DDMMYY, dengan DD+40 untuk perempuan)
- 4 digit nomor urut

**Masalah Direct Addressing:**

1. **Ukuran Array:** Jika menggunakan NIK langsung sebagai index:
   - Kemungkinan nilai: 10^16 = 10.000.000.000.000.000
   - Jika setiap slot 8 byte: 80.000 Terabyte!
   - Tidak ada komputer yang mampu menyediakan memori sebesar itu

2. **Ketersebaran (Sparsity):**
   - Populasi Indonesia ~275 juta
   - Hanya 275.000.000 dari 10^16 slot yang terpakai
   - Utilisasi: 0.00000275% — sangat boros!

**Solusi:** Gunakan fungsi hash untuk memetakan NIK ke array berukuran wajar (misalnya 1 juta slot), dengan mekanisme collision handling.

---

### SOLVED PROBLEM 2 ⭐

**Soal:** Apa perbedaan antara key, value, dan hash value dalam konteks hash table?

**Penyelesaian:**

| Istilah | Definisi | Contoh |
|---------|----------|--------|
| **Key** | Identifier unik untuk data | NIK: "3201234567890001" |
| **Value** | Data yang disimpan | {nama: "Budi", pangkat: "Lettu"} |
| **Hash Value** | Hasil fungsi hash, menjadi index | h("3201234567890001") = 42 |

**Ilustrasi:**
```
Key: "3201234567890001" --[h(k)]--> Hash Value: 42 --[table[42]]--> Value: {Budi, Lettu}
```

**Hubungan:**
- Key digunakan untuk **mengidentifikasi** data
- Hash value digunakan untuk **menentukan lokasi** penyimpanan
- Value adalah **data aktual** yang disimpan

---

## 2. Fungsi Hash

### 2.1 Karakteristik Fungsi Hash yang Baik

Fungsi hash yang baik harus memiliki karakteristik:

1. **Deterministic:** Key yang sama selalu menghasilkan hash value yang sama
2. **Uniform Distribution:** Menyebarkan key secara merata ke seluruh slot
3. **Efficient:** Dapat dihitung dengan cepat O(1)
4. **Minimize Collision:** Meminimalkan key berbeda yang menghasilkan hash value sama

### 2.2 Division Method

> **Definisi:** **Division Method** menghitung hash value dengan mengambil sisa pembagian key dengan ukuran tabel m.

```
h(k) = k mod m
```

**Contoh:**
```cpp
int hashDivision(int key, int m) {
    return key % m;
}

// Untuk key = 12345, m = 100
// h(12345) = 12345 % 100 = 45
```

**Pemilihan m:**
- **Hindari** m = 2^p (power of 2) — hanya menggunakan p bit terakhir
- **Pilih** m = bilangan prima yang tidak dekat dengan power of 2
- **Contoh bagus:** m = 97, 193, 389, 769, 1543, 3079

### 2.3 Multiplication Method

> **Definisi:** **Multiplication Method** mengalikan key dengan konstanta A (0 < A < 1), mengambil bagian fraksional, lalu mengalikan dengan m.

```
h(k) = floor(m × (k × A mod 1))
```

di mana `(k × A mod 1)` adalah bagian fraksional dari k × A.

**Konstanta Knuth:** A ≈ (√5 - 1) / 2 ≈ 0.6180339887 (golden ratio)

```cpp
int hashMultiplication(int key, int m) {
    const double A = 0.6180339887;
    double temp = key * A;
    temp = temp - (int)temp;  // Ambil bagian fraksional
    return (int)(m * temp);
}
```

**Keuntungan:** Nilai m tidak kritis, bisa menggunakan power of 2.

### 2.4 Fungsi Hash untuk String

Untuk string, kita perlu mengkonversi karakter menjadi nilai numerik:

```cpp
// Polynomial Rolling Hash
unsigned long hashString(const string& key, int m) {
    unsigned long hash = 0;
    unsigned long base = 31;  // Basis (bilangan prima)
    
    for (char c : key) {
        hash = (hash * base + c) % m;
    }
    
    return hash;
}

// Contoh: hash("abc") dengan m = 100
// = ((0*31 + 'a') * 31 + 'b') * 31 + 'c') % 100
// = ((97 * 31 + 98) * 31 + 99) % 100
// = (3105 * 31 + 99) % 100
// = 96354 % 100 = 54
```

### 2.5 Universal Hashing

> **Definisi:** **Universal Hashing** memilih fungsi hash secara acak dari keluarga fungsi hash H pada saat runtime untuk menghindari worst-case collision yang disengaja.

Keluarga universal:
```
h_{a,b}(k) = ((a × k + b) mod p) mod m
```

di mana:
- p = bilangan prima lebih besar dari semua key
- a ∈ {1, 2, ..., p-1} dipilih acak
- b ∈ {0, 1, ..., p-1} dipilih acak

---

### SOLVED PROBLEM 3 ⭐

**Soal:** Hitung h(k) untuk k = 1234 menggunakan division method dengan m = 97!

**Penyelesaian:**

```
h(k) = k mod m
h(1234) = 1234 mod 97
```

Langkah perhitungan:
```
1234 ÷ 97 = 12.72... 
1234 = 97 × 12 + r
1234 = 1164 + r
r = 1234 - 1164 = 70
```

**Jawaban:** h(1234) = **70**

---

### SOLVED PROBLEM 4 ⭐

**Soal:** Mengapa m = 100 bukan pilihan yang baik untuk division method?

**Penyelesaian:**

Jika m = 100 = 10^2:

```
h(k) = k mod 100
```

Ini hanya menggunakan **2 digit terakhir** dari key:
- h(123456) = 56
- h(789456) = 56
- h(000056) = 56

**Masalah:**
1. **Tidak memanfaatkan seluruh key** — Informasi dari digit lain diabaikan
2. **Pola collision mudah diprediksi** — Semua key dengan 2 digit terakhir sama akan collision
3. **Distribusi tidak merata** jika key memiliki pola tertentu (misalnya semua diakhiri 00)

**Solusi:** Gunakan bilangan prima seperti m = 97 atau m = 101.

---

### SOLVED PROBLEM 5 ⭐⭐

**Soal:** Implementasikan fungsi hash untuk string NIP PNS menggunakan polynomial rolling hash!

**Penyelesaian:**

NIP PNS format: 18 digit (contoh: "199012312020011001")

```cpp
#include <iostream>
#include <string>
using namespace std;

unsigned long hashNIP(const string& nip, int m) {
    if (nip.length() != 18) {
        throw invalid_argument("NIP harus 18 digit!");
    }
    
    unsigned long hash = 0;
    unsigned long base = 31;
    unsigned long power = 1;
    
    // Polynomial rolling hash
    for (int i = nip.length() - 1; i >= 0; i--) {
        // Konversi karakter digit ke nilai 0-9
        int digit = nip[i] - '0';
        
        // Tambahkan kontribusi digit ini
        hash = (hash + digit * power) % m;
        power = (power * base) % m;
    }
    
    return hash;
}

int main() {
    string nip1 = "199012312020011001";
    string nip2 = "198507152015031002";
    int m = 1009;  // Bilangan prima
    
    cout << "Hash NIP " << nip1 << " = " << hashNIP(nip1, m) << endl;
    cout << "Hash NIP " << nip2 << " = " << hashNIP(nip2, m) << endl;
    
    return 0;
}
```

**Output:**
```
Hash NIP 199012312020011001 = 847
Hash NIP 198507152015031002 = 312
```

**Analisis Kompleksitas:**
- Waktu: O(L) dimana L = panjang string (18 untuk NIP)
- Ruang: O(1)

---

### SOLVED PROBLEM 6 ⭐⭐

**Soal:** Hitung hash value menggunakan multiplication method untuk k = 123456 dengan m = 1000 dan A = 0.6180339887!

**Penyelesaian:**

Formula: h(k) = floor(m × (k × A mod 1))

**Langkah 1:** Hitung k × A
```
k × A = 123456 × 0.6180339887
     = 76299.9137...
```

**Langkah 2:** Ambil bagian fraksional (mod 1)
```
76299.9137... mod 1 = 0.9137...
```

**Langkah 3:** Kalikan dengan m dan floor
```
m × 0.9137... = 1000 × 0.9137...
              = 913.7...
floor(913.7) = 913
```

**Jawaban:** h(123456) = **913**

**Verifikasi dengan kode:**
```cpp
int hashMult(int key, int m) {
    const double A = 0.6180339887;
    double temp = key * A;
    temp = temp - (int)temp;  // fraksional
    return (int)(m * temp);
}

// hashMult(123456, 1000) = 913
```

---

## 3. Collision dan Teknik Penanganan

### 3.1 Apa itu Collision?

> **Definisi:** **Collision** terjadi ketika dua key berbeda k1 ≠ k2 menghasilkan hash value yang sama: h(k1) = h(k2).

![Collision pada Hash Table](images/gambar-14-2.png)

*Gambar 14.2: Ilustrasi collision — dua key berbeda dipetakan ke slot yang sama*

**Mengapa Collision Pasti Terjadi?**

Menurut **Pigeonhole Principle**: Jika n item dimasukkan ke m slot (n > m), minimal satu slot berisi lebih dari satu item.

Untuk hash table dengan m slot dan n key dari universe U (|U| > m):
- Collision **pasti** terjadi jika n > m
- Collision **mungkin** terjadi bahkan jika n < m (Birthday Paradox)

### 3.2 Birthday Paradox

> **Birthday Paradox:** Dalam grup 23 orang, probabilitas dua orang memiliki tanggal lahir sama > 50%.

Implikasi untuk hash table: Collision lebih sering terjadi dari yang kita perkirakan!

Probabilitas collision untuk n key dalam m slot:

```
P(collision) ≈ 1 - e^(-n²/2m)
```

| n (key) | m (slot) | P(collision) |
|---------|----------|--------------|
| 10 | 365 | 11.7% |
| 23 | 365 | 50.7% |
| 50 | 365 | 97.0% |
| 10 | 1000 | 4.4% |
| 45 | 1000 | 63.3% |

### 3.3 Dua Pendekatan Utama Collision Handling

| Pendekatan | Teknik | Ide Dasar |
|------------|--------|-----------|
| **Separate Chaining** | Linked List di setiap slot | Slot menyimpan daftar semua key dengan hash sama |
| **Open Addressing** | Probing | Cari slot kosong lain dalam array |

---

### SOLVED PROBLEM 7 ⭐

**Soal:** Berikan contoh 5 key yang menyebabkan collision pada hash table dengan h(k) = k mod 7!

**Penyelesaian:**

Untuk h(k) = k mod 7, key yang memberikan hash value sama adalah key dengan sisa bagi 7 yang sama.

**Contoh key dengan h(k) = 3:**

| Key | Perhitungan | Hash Value |
|-----|-------------|------------|
| 3 | 3 mod 7 = 3 | 3 |
| 10 | 10 mod 7 = 3 | 3 |
| 17 | 17 mod 7 = 3 | 3 |
| 24 | 24 mod 7 = 3 | 3 |
| 31 | 31 mod 7 = 3 | 3 |

**Pola:** Semua key dengan bentuk 7k + 3 akan collision di slot 3.

**Contoh lain dengan h(k) = 0:**
- 0, 7, 14, 21, 28, 35, ...

---

### SOLVED PROBLEM 8 ⭐⭐

**Soal:** Dalam sistem database personel dengan 10.000 record dan hash table berukuran 10.000 slot, berapa probabilitas terjadinya setidaknya satu collision?

**Penyelesaian:**

Menggunakan approximasi Birthday Paradox:

```
P(collision) ≈ 1 - e^(-n²/2m)
```

Dengan n = 10.000 dan m = 10.000:

```
P(collision) ≈ 1 - e^(-(10000)²/(2×10000))
             ≈ 1 - e^(-100000000/20000)
             ≈ 1 - e^(-5000)
             ≈ 1 - 0
             ≈ 1 (praktis 100%)
```

**Kesimpulan:** Bahkan dengan jumlah slot sama dengan jumlah key, collision **hampir pasti** terjadi.

**Implikasi desain:**
- Collision handling **wajib** diimplementasikan
- Load factor harus dipertimbangkan (idealnya < 0.75)
- Untuk mengurangi collision signifikan, m >> n (misalnya m = 2n)

---

## 4. Separate Chaining

### 4.1 Konsep Separate Chaining

> **Definisi:** **Separate Chaining** menyimpan semua key yang memetakan ke slot yang sama dalam linked list di slot tersebut.

![Separate Chaining](images/gambar-14-3.png)

*Gambar 14.3: Hash table dengan separate chaining*

### 4.2 Implementasi Separate Chaining

```cpp
#include <iostream>
#include <list>
#include <vector>
using namespace std;

class HashTableChaining {
private:
    int size;
    vector<list<pair<int, string>>> table;
    
    int hash(int key) {
        return key % size;
    }
    
public:
    HashTableChaining(int m) : size(m), table(m) {}
    
    // Insert key-value pair
    void insert(int key, const string& value) {
        int index = hash(key);
        
        // Cek apakah key sudah ada
        for (auto& pair : table[index]) {
            if (pair.first == key) {
                pair.second = value;  // Update value
                return;
            }
        }
        
        // Key belum ada, tambahkan
        table[index].push_back({key, value});
    }
    
    // Search by key
    string* search(int key) {
        int index = hash(key);
        
        for (auto& pair : table[index]) {
            if (pair.first == key) {
                return &pair.second;
            }
        }
        
        return nullptr;  // Not found
    }
    
    // Delete by key
    bool remove(int key) {
        int index = hash(key);
        
        for (auto it = table[index].begin(); it != table[index].end(); ++it) {
            if (it->first == key) {
                table[index].erase(it);
                return true;
            }
        }
        
        return false;  // Not found
    }
    
    // Display hash table
    void display() {
        for (int i = 0; i < size; i++) {
            cout << "Slot " << i << ": ";
            for (auto& pair : table[i]) {
                cout << "[" << pair.first << ":" << pair.second << "] -> ";
            }
            cout << "NULL" << endl;
        }
    }
};

int main() {
    HashTableChaining ht(7);
    
    // Insert data personel (NRP sebagai key)
    ht.insert(12345, "Kapten Budi");
    ht.insert(12352, "Lettu Andi");    // 12352 % 7 = 5 (sama dengan 12345 % 7 = 5)
    ht.insert(12359, "Mayor Siti");     // collision di slot 5
    ht.insert(12348, "Serma Dodi");
    
    cout << "=== Hash Table Contents ===" << endl;
    ht.display();
    
    cout << "\n=== Search Test ===" << endl;
    string* result = ht.search(12352);
    if (result) {
        cout << "NRP 12352: " << *result << endl;
    }
    
    return 0;
}
```

**Output:**
```
=== Hash Table Contents ===
Slot 0: NULL
Slot 1: [12348:Serma Dodi] -> NULL
Slot 2: NULL
Slot 3: NULL
Slot 4: NULL
Slot 5: [12345:Kapten Budi] -> [12352:Lettu Andi] -> [12359:Mayor Siti] -> NULL
Slot 6: NULL

=== Search Test ===
NRP 12352: Lettu Andi
```

### 4.3 Kompleksitas Separate Chaining

| Operasi | Average Case | Worst Case |
|---------|--------------|------------|
| Insert | O(1) | O(n) |
| Search | O(1 + α) | O(n) |
| Delete | O(1 + α) | O(n) |

Di mana **α = n/m** adalah **load factor** (rasio jumlah elemen terhadap ukuran tabel).

**Worst case** terjadi ketika semua key memetakan ke satu slot (semua collision).

---

### SOLVED PROBLEM 9 ⭐

**Soal:** Pada hash table dengan separate chaining, m = 10, masukkan key: 5, 15, 25, 35, 45. Gambarkan hash table setelah semua insert!

**Penyelesaian:**

Fungsi hash: h(k) = k mod 10

| Key | Hash Value |
|-----|------------|
| 5 | 5 mod 10 = 5 |
| 15 | 15 mod 10 = 5 |
| 25 | 25 mod 10 = 5 |
| 35 | 35 mod 10 = 5 |
| 45 | 45 mod 10 = 5 |

Semua key memetakan ke **slot 5** — worst case scenario!

**Hash Table setelah insert:**

```
Slot 0: NULL
Slot 1: NULL
Slot 2: NULL
Slot 3: NULL
Slot 4: NULL
Slot 5: [5] -> [15] -> [25] -> [35] -> [45] -> NULL
Slot 6: NULL
Slot 7: NULL
Slot 8: NULL
Slot 9: NULL
```

**Analisis:** Ini adalah contoh **bad hash function** untuk dataset ini. Search untuk key 45 memerlukan traversal 5 node.

---

### SOLVED PROBLEM 10 ⭐⭐

**Soal:** Implementasikan method `getLoadFactor()` dan `getChainLengths()` untuk menganalisis distribusi hash table!

**Penyelesaian:**

```cpp
class HashTableChaining {
    // ... (kode sebelumnya)
    
public:
    // Hitung load factor
    double getLoadFactor() {
        int totalElements = 0;
        for (int i = 0; i < size; i++) {
            totalElements += table[i].size();
        }
        return (double)totalElements / size;
    }
    
    // Dapatkan statistik panjang chain
    void getChainLengths() {
        int totalElements = 0;
        int maxLength = 0;
        int nonEmptySlots = 0;
        
        cout << "Chain lengths per slot:" << endl;
        for (int i = 0; i < size; i++) {
            int len = table[i].size();
            totalElements += len;
            
            if (len > maxLength) maxLength = len;
            if (len > 0) nonEmptySlots++;
            
            cout << "  Slot " << i << ": " << len << " elements" << endl;
        }
        
        cout << "\nStatistics:" << endl;
        cout << "  Total elements: " << totalElements << endl;
        cout << "  Table size: " << size << endl;
        cout << "  Load factor: " << getLoadFactor() << endl;
        cout << "  Max chain length: " << maxLength << endl;
        cout << "  Non-empty slots: " << nonEmptySlots << "/" << size << endl;
        cout << "  Avg chain length (non-empty): " 
             << (nonEmptySlots > 0 ? (double)totalElements/nonEmptySlots : 0) 
             << endl;
    }
};
```

**Contoh penggunaan:**
```cpp
HashTableChaining ht(7);
ht.insert(10, "A");
ht.insert(20, "B");
ht.insert(15, "C");
ht.insert(25, "D");
ht.insert(35, "E");

ht.getChainLengths();
```

**Output:**
```
Chain lengths per slot:
  Slot 0: 1 elements
  Slot 1: 2 elements
  Slot 2: 0 elements
  Slot 3: 1 elements
  Slot 4: 0 elements
  Slot 5: 0 elements
  Slot 6: 1 elements

Statistics:
  Total elements: 5
  Table size: 7
  Load factor: 0.714286
  Max chain length: 2
  Non-empty slots: 4/7
  Avg chain length (non-empty): 1.25
```

---

### SOLVED PROBLEM 11 ⭐⭐

**Soal:** Untuk hash table dengan n = 1000 elemen dan target average search time O(1), berapa ukuran tabel minimum yang diperlukan?

**Penyelesaian:**

Untuk separate chaining, average search time = O(1 + α) dimana α = n/m.

Agar mendekati O(1), kita ingin α kecil, idealnya α ≤ 1.

**Analisis:**
- Jika α = 1: m = n = 1000, average search = O(2) ≈ O(1)
- Jika α = 0.5: m = 2n = 2000, average search = O(1.5) ≈ O(1)
- Jika α = 0.75: m = n/0.75 ≈ 1333, average search = O(1.75) ≈ O(1)

**Rekomendasi praktis:**
- Minimum: **m = 1000** (α = 1)
- Lebih baik: **m = 1333** (α ≈ 0.75) — standar industri
- Ideal: **m = 2000** (α = 0.5)

**Catatan:** m sebaiknya bilangan prima untuk distribusi lebih merata:
- 1009 (prima dekat 1000)
- 1361 (prima dekat 1333)
- 2003 (prima dekat 2000)

---

## 5. Open Addressing

### 5.1 Konsep Open Addressing

> **Definisi:** **Open Addressing** menyimpan semua elemen dalam array hash table itu sendiri. Jika slot tujuan sudah terisi, cari slot kosong lain menggunakan **probe sequence**.

**Perbedaan dengan Separate Chaining:**

| Aspek | Separate Chaining | Open Addressing |
|-------|-------------------|-----------------|
| Struktur tambahan | Linked list | Tidak ada |
| Memori per elemen | Lebih besar (node + pointer) | Lebih efisien |
| Load factor max | > 1 (chain bisa panjang) | ≤ 1 (tabel bisa penuh) |
| Cache performance | Buruk (pointer chasing) | Baik (locality) |

### 5.2 Linear Probing

> **Definisi:** **Linear Probing** mencari slot kosong dengan mengecek slot berikutnya secara berurutan.

**Probe sequence:**
```
h(k, i) = (h'(k) + i) mod m
```

di mana i = 0, 1, 2, 3, ... (nomor percobaan)

![Linear Probing](images/gambar-14-4.png)

*Gambar 14.4: Linear probing — mencari slot kosong secara sekuensial*

**Implementasi Linear Probing:**

```cpp
class HashTableLinearProbing {
private:
    int size;
    int* keys;
    string* values;
    bool* occupied;
    bool* deleted;  // Untuk lazy deletion
    
    int hash(int key) {
        return key % size;
    }
    
public:
    HashTableLinearProbing(int m) : size(m) {
        keys = new int[size];
        values = new string[size];
        occupied = new bool[size]();
        deleted = new bool[size]();
    }
    
    ~HashTableLinearProbing() {
        delete[] keys;
        delete[] values;
        delete[] occupied;
        delete[] deleted;
    }
    
    // Insert dengan linear probing
    bool insert(int key, const string& value) {
        int index = hash(key);
        int startIndex = index;
        int i = 0;
        
        do {
            // Slot kosong atau deleted - bisa insert
            if (!occupied[index] || deleted[index]) {
                keys[index] = key;
                values[index] = value;
                occupied[index] = true;
                deleted[index] = false;
                return true;
            }
            
            // Key sudah ada - update value
            if (keys[index] == key && !deleted[index]) {
                values[index] = value;
                return true;
            }
            
            // Linear probe: cek slot berikutnya
            i++;
            index = (startIndex + i) % size;
            
        } while (index != startIndex);  // Full circle = table penuh
        
        return false;  // Table penuh
    }
    
    // Search dengan linear probing
    string* search(int key) {
        int index = hash(key);
        int startIndex = index;
        int i = 0;
        
        do {
            // Slot belum pernah diisi - key tidak ada
            if (!occupied[index] && !deleted[index]) {
                return nullptr;
            }
            
            // Key ditemukan
            if (occupied[index] && !deleted[index] && keys[index] == key) {
                return &values[index];
            }
            
            // Linear probe
            i++;
            index = (startIndex + i) % size;
            
        } while (index != startIndex);
        
        return nullptr;
    }
    
    // Delete dengan lazy deletion
    bool remove(int key) {
        int index = hash(key);
        int startIndex = index;
        int i = 0;
        
        do {
            if (!occupied[index] && !deleted[index]) {
                return false;  // Not found
            }
            
            if (occupied[index] && !deleted[index] && keys[index] == key) {
                deleted[index] = true;  // Lazy delete
                return true;
            }
            
            i++;
            index = (startIndex + i) % size;
            
        } while (index != startIndex);
        
        return false;
    }
    
    void display() {
        for (int i = 0; i < size; i++) {
            cout << "Slot " << i << ": ";
            if (occupied[i] && !deleted[i]) {
                cout << "[" << keys[i] << ":" << values[i] << "]";
            } else if (deleted[i]) {
                cout << "[DELETED]";
            } else {
                cout << "[EMPTY]";
            }
            cout << endl;
        }
    }
};
```

### 5.3 Primary Clustering

> **Definisi:** **Primary Clustering** adalah fenomena terbentuknya cluster (kelompok slot terisi berurutan) yang semakin besar, memperlambat operasi.

**Masalah:** Jika ada cluster panjang k, key baru yang hash ke salah satu dari k slot tersebut akan menambah cluster menjadi k+1.

### 5.4 Quadratic Probing

> **Definisi:** **Quadratic Probing** menggunakan fungsi kuadrat untuk menentukan probe sequence, mengurangi primary clustering.

**Probe sequence:**
```
h(k, i) = (h'(k) + c₁·i + c₂·i²) mod m
```

Bentuk sederhana (c₁ = 0, c₂ = 1):
```
h(k, i) = (h'(k) + i²) mod m
```

**Probe sequence untuk h'(k) = 5, m = 11:**
- i=0: (5 + 0) mod 11 = 5
- i=1: (5 + 1) mod 11 = 6
- i=2: (5 + 4) mod 11 = 9
- i=3: (5 + 9) mod 11 = 3
- i=4: (5 + 16) mod 11 = 10

### 5.5 Double Hashing

> **Definisi:** **Double Hashing** menggunakan dua fungsi hash: satu untuk posisi awal, satu untuk step size.

**Probe sequence:**
```
h(k, i) = (h₁(k) + i · h₂(k)) mod m
```

**Syarat:**
- h₂(k) ≠ 0 untuk semua k
- h₂(k) dan m harus relatively prime (GCD = 1)

**Contoh umum:**
```
h₁(k) = k mod m
h₂(k) = 1 + (k mod (m-1))
```

**Keuntungan:** Menghindari clustering, distribusi probe lebih merata.

---

### SOLVED PROBLEM 12 ⭐

**Soal:** Insert key 10, 22, 31, 4, 15 ke hash table dengan m = 11 menggunakan linear probing. h(k) = k mod 11.

**Penyelesaian:**

| Step | Key | h(k) | Probes | Final Position |
|------|-----|------|--------|----------------|
| 1 | 10 | 10 mod 11 = 10 | 10 (kosong) | 10 |
| 2 | 22 | 22 mod 11 = 0 | 0 (kosong) | 0 |
| 3 | 31 | 31 mod 11 = 9 | 9 (kosong) | 9 |
| 4 | 4 | 4 mod 11 = 4 | 4 (kosong) | 4 |
| 5 | 15 | 15 mod 11 = 4 | 4 (terisi), 5 (kosong) | 5 |

**Hash Table akhir:**

```
Index:  0    1    2    3    4    5    6    7    8    9   10
      [22] [ ] [ ] [ ] [4] [15] [ ] [ ] [ ] [31] [10]
```

---

### SOLVED PROBLEM 13 ⭐⭐

**Soal:** Untuk soal sebelumnya, sekarang gunakan quadratic probing h(k,i) = (h(k) + i²) mod 11. Bandingkan hasilnya!

**Penyelesaian:**

| Step | Key | h(k) | Probes (slot, formula) | Final Position |
|------|-----|------|------------------------|----------------|
| 1 | 10 | 10 | (10+0²)%11 = 10 (kosong) | 10 |
| 2 | 22 | 0 | (0+0²)%11 = 0 (kosong) | 0 |
| 3 | 31 | 9 | (9+0²)%11 = 9 (kosong) | 9 |
| 4 | 4 | 4 | (4+0²)%11 = 4 (kosong) | 4 |
| 5 | 15 | 4 | (4+0²)%11 = 4 (terisi), (4+1²)%11 = 5 (kosong) | 5 |

**Hash Table akhir:** Sama dengan linear probing untuk kasus ini.

```
Index:  0    1    2    3    4    5    6    7    8    9   10
      [22] [ ] [ ] [ ] [4] [15] [ ] [ ] [ ] [31] [10]
```

**Catatan:** Perbedaan terlihat saat cluster lebih panjang. Quadratic probing akan "melompat" lebih jauh.

---

### SOLVED PROBLEM 14 ⭐⭐

**Soal:** Implementasikan double hashing dengan h₁(k) = k mod 13 dan h₂(k) = 7 - (k mod 7). Insert key 18, 41, 22, 44, 59, 32.

**Penyelesaian:**

```cpp
int h1(int k) { return k % 13; }
int h2(int k) { return 7 - (k % 7); }  // Selalu 1-7, tidak pernah 0

int doubleHash(int k, int i, int m) {
    return (h1(k) + i * h2(k)) % m;
}
```

**Proses insert (m = 13):**

| Key | h₁(k) | h₂(k) | Probes | Position |
|-----|-------|-------|--------|----------|
| 18 | 5 | 7-(18%7)=7-4=3 | 5 | 5 |
| 41 | 2 | 7-(41%7)=7-6=1 | 2 | 2 |
| 22 | 9 | 7-(22%7)=7-1=6 | 9 | 9 |
| 44 | 5 | 7-(44%7)=7-2=5 | 5→10 | 10 |
| 59 | 7 | 7-(59%7)=7-3=4 | 7 | 7 |
| 32 | 6 | 7-(32%7)=7-4=3 | 6 | 6 |

**Detail collision untuk key 44:**
- h₁(44) = 5 (terisi oleh 18)
- i=1: (5 + 1×5) % 13 = 10 (kosong) ✓

**Hash Table akhir:**
```
Index:  0    1    2    3    4    5    6    7    8    9   10   11   12
      [ ] [ ] [41] [ ] [ ] [18] [32] [59] [ ] [22] [44] [ ] [ ]
```

---

### SOLVED PROBLEM 15 ⭐⭐⭐

**Soal:** Analisis mengapa lazy deletion diperlukan pada open addressing dan apa dampaknya terhadap performa!

**Penyelesaian:**

**Masalah dengan "Hard Deletion":**

Misalkan hash table dengan linear probing:
```
Insert 10 (h=3): slot 3
Insert 20 (h=3): collision, slot 4
Insert 30 (h=3): collision, slot 5
```

```
Index: 0    1    2    3    4    5
      [ ] [ ] [ ] [10] [20] [30]
```

Jika kita "hard delete" 20 (mengosongkan slot 4):
```
Index: 0    1    2    3    4    5
      [ ] [ ] [ ] [10] [ ] [30]
```

**Masalah:** Search untuk 30 akan:
1. h(30) = 3 → terisi oleh 10, bukan 30, lanjut
2. Slot 4 → kosong → **berhenti, return not found!** ❌

Padahal 30 ada di slot 5!

**Solusi: Lazy Deletion**

Tandai slot sebagai "DELETED" bukan "EMPTY":
```
Index: 0    1    2    3    4        5
      [ ] [ ] [ ] [10] [DELETED] [30]
```

Search untuk 30:
1. h(30) = 3 → terisi, bukan 30
2. Slot 4 → DELETED → **lanjut probing**
3. Slot 5 → 30 ditemukan! ✓

**Dampak Performa:**

| Aspek | Dampak |
|-------|--------|
| Search | Harus melewati DELETED slots → probe lebih lama |
| Insert | Bisa reuse DELETED slots → OK |
| Space | DELETED slots tidak benar-benar kosong |
| Load factor | Perlu dihitung termasuk DELETED |

**Mitigasi:**
1. **Periodic rehashing:** Rebuild table tanpa DELETED slots
2. **Threshold:** Rehash jika DELETED > threshold (misal 25%)

---

## 6. Load Factor dan Rehashing

### 6.1 Load Factor

> **Definisi:** **Load Factor (α)** adalah rasio jumlah elemen terhadap ukuran tabel: α = n/m

| α | Interpretasi | Performa |
|---|--------------|----------|
| 0.25 | 25% terisi | Sangat baik, boros memori |
| 0.50 | 50% terisi | Baik |
| 0.75 | 75% terisi | Acceptable, standar threshold |
| 0.90 | 90% terisi | Degradasi signifikan |
| 1.00 | Penuh (open addr.) | Tidak bisa insert lagi |

### 6.2 Kapan Rehashing?

> **Definisi:** **Rehashing** adalah proses membuat hash table baru dengan ukuran lebih besar dan memindahkan semua elemen.

**Trigger rehashing:**
- Load factor melebihi threshold (biasanya 0.75)
- Terlalu banyak slot DELETED (untuk open addressing)

### 6.3 Implementasi Rehashing

```cpp
class HashTableWithRehash {
private:
    static constexpr double LOAD_THRESHOLD = 0.75;
    static constexpr double SHRINK_THRESHOLD = 0.25;
    
    int size;
    int count;
    vector<pair<int, string>*> table;
    
    int hash(int key) { return key % size; }
    
    // Cari bilangan prima berikutnya
    int nextPrime(int n) {
        while (!isPrime(n)) n++;
        return n;
    }
    
    bool isPrime(int n) {
        if (n < 2) return false;
        for (int i = 2; i * i <= n; i++) {
            if (n % i == 0) return false;
        }
        return true;
    }
    
    void rehash(int newSize) {
        newSize = nextPrime(newSize);
        vector<pair<int, string>*> oldTable = table;
        int oldSize = size;
        
        // Buat table baru
        size = newSize;
        count = 0;
        table = vector<pair<int, string>*>(size, nullptr);
        
        // Pindahkan semua elemen
        for (int i = 0; i < oldSize; i++) {
            if (oldTable[i] != nullptr) {
                insert(oldTable[i]->first, oldTable[i]->second);
                delete oldTable[i];
            }
        }
        
        cout << "[Rehash] Size: " << oldSize << " -> " << size << endl;
    }
    
public:
    HashTableWithRehash(int initialSize = 11) 
        : size(nextPrime(initialSize)), count(0), table(size, nullptr) {}
    
    void insert(int key, const string& value) {
        // Check load factor
        if ((double)(count + 1) / size > LOAD_THRESHOLD) {
            rehash(size * 2);
        }
        
        int index = hash(key);
        int i = 0;
        
        while (table[(index + i) % size] != nullptr) {
            if (table[(index + i) % size]->first == key) {
                table[(index + i) % size]->second = value;
                return;
            }
            i++;
        }
        
        table[(index + i) % size] = new pair<int, string>(key, value);
        count++;
    }
    
    double getLoadFactor() {
        return (double)count / size;
    }
};
```

---

### SOLVED PROBLEM 16 ⭐

**Soal:** Hash table dengan m = 10 berisi 7 elemen. Hitung load factor dan tentukan apakah perlu rehashing (threshold 0.75)!

**Penyelesaian:**

```
α = n / m = 7 / 10 = 0.7
```

**Load factor = 0.7 = 70%**

Karena 0.7 < 0.75, **belum perlu rehashing**.

Namun, insert 1 elemen lagi:
```
α = 8 / 10 = 0.8 > 0.75
```

Insert berikutnya akan **trigger rehashing**.

---

### SOLVED PROBLEM 17 ⭐⭐

**Soal:** Jika hash table dengan α = 0.8 di-rehash menjadi ukuran 2× lebih besar, berapa load factor baru?

**Penyelesaian:**

Misalkan:
- Ukuran lama: m
- Jumlah elemen: n
- α lama = n/m = 0.8 → n = 0.8m

Setelah rehash:
- Ukuran baru: 2m
- Jumlah elemen: tetap n = 0.8m

```
α baru = n / (2m) = 0.8m / 2m = 0.4
```

**Load factor baru = 0.4 = 40%**

**Analisis:**
- Performa membaik (lebih sedikit collision)
- Memori penggunaan meningkat 2×
- Trade-off antara speed dan space

---

### SOLVED PROBLEM 18 ⭐⭐⭐

**Soal:** Desain strategi resize untuk hash table yang meminimalkan total waktu amortized untuk n insert operations!

**Penyelesaian:**

**Strategi: Doubling dengan Threshold 0.5**

**Analisis Amortized:**

Mulai dengan tabel ukuran 1:
- Insert 1-1: O(1), rehash ke ukuran 2, copy 1 elemen
- Insert 2: O(1)
- Insert 3: rehash ke ukuran 4, copy 2 elemen
- Insert 4: O(1)
- Insert 5: rehash ke ukuran 8, copy 4 elemen
- ...

**Total cost untuk n insert:**

```
Cost = n × O(1) + (1 + 2 + 4 + 8 + ... + n/2)
     = n + (n - 1)
     = O(n)
```

**Amortized cost per insert = O(n)/n = O(1)**

**Mengapa doubling?**
- Jika +k (konstanta): Rehash setiap k insert → total O(n²/k)
- Jika ×1.5: Rehash lebih sering tapi hemat memori
- Jika ×2: Balance antara frequency dan waste

**Rekomendasi praktis:**
- Grow factor: 2 (doubling)
- Grow threshold: 0.75
- Shrink factor: 0.5
- Shrink threshold: 0.25

---

## 7. Analisis Kompleksitas

### 7.1 Ringkasan Kompleksitas

| Operasi | Separate Chaining | Open Addressing (sukses) | Open Addressing (gagal) |
|---------|-------------------|--------------------------|-------------------------|
| **Insert** | O(1) average | O(1/(1-α)) | O(1/(1-α)) |
| **Search** | O(1+α) average | O(1/α × ln(1/(1-α))) | O(1/(1-α)) |
| **Delete** | O(1+α) average | O(1/α × ln(1/(1-α))) | O(1/(1-α)) |
| **Worst case** | O(n) | O(n) | O(n) |

### 7.2 Expected Probes untuk Open Addressing

Dengan asumsi uniform hashing:

**Unsuccessful search (key tidak ada):**
```
E[probes] ≈ 1/(1-α)
```

**Successful search (key ada):**
```
E[probes] ≈ (1/α) × ln(1/(1-α))
```

| α | Unsuccessful | Successful |
|---|--------------|------------|
| 0.50 | 2 | 1.39 |
| 0.75 | 4 | 1.85 |
| 0.90 | 10 | 2.56 |
| 0.95 | 20 | 3.15 |

### 7.3 Perbandingan dengan Struktur Data Lain

| Struktur Data | Search | Insert | Delete | Space |
|---------------|--------|--------|--------|-------|
| Array (unsorted) | O(n) | O(1)* | O(n) | O(n) |
| Array (sorted) | O(log n) | O(n) | O(n) | O(n) |
| BST (balanced) | O(log n) | O(log n) | O(log n) | O(n) |
| Hash Table | O(1) avg | O(1) avg | O(1) avg | O(n) |

*Insert di akhir array

---

### SOLVED PROBLEM 19 ⭐⭐

**Soal:** Hitung expected number of probes untuk search di hash table dengan open addressing dan α = 0.8!

**Penyelesaian:**

**Untuk unsuccessful search:**
```
E[probes] = 1/(1-α) = 1/(1-0.8) = 1/0.2 = 5
```

**Untuk successful search:**
```
E[probes] = (1/α) × ln(1/(1-α))
          = (1/0.8) × ln(1/0.2)
          = 1.25 × ln(5)
          = 1.25 × 1.609
          ≈ 2.01
```

**Interpretasi:**
- Rata-rata 5 probes untuk key yang tidak ada
- Rata-rata 2 probes untuk key yang ada
- Load factor 0.8 masih acceptable tapi mendekati batas

---

### SOLVED PROBLEM 20 ⭐⭐⭐

**Soal:** Desain hash table untuk sistem cache dengan requirement: 100.000 entries, 95% search adalah hit (successful), target average probe ≤ 2. Tentukan ukuran tabel dan metode yang tepat!

**Penyelesaian:**

**Requirement Analysis:**
- n = 100.000 entries
- Target: E[probes] ≤ 2 untuk successful search

**Untuk Open Addressing (linear probing):**

Dari formula E[probes] = (1/α) × ln(1/(1-α)):

Coba α = 0.5:
```
E = (1/0.5) × ln(1/0.5) = 2 × 0.693 = 1.39 ✓
```

Coba α = 0.6:
```
E = (1/0.6) × ln(1/0.4) = 1.67 × 0.916 = 1.53 ✓
```

Coba α = 0.7:
```
E = (1/0.7) × ln(1/0.3) = 1.43 × 1.204 = 1.72 ✓
```

**Rekomendasi:**

| Parameter | Value | Alasan |
|-----------|-------|--------|
| **Metode** | Double Hashing | Distribusi probe lebih baik |
| **α target** | 0.65 | Balance speed & space |
| **m** | 154.000 | n/α = 100K/0.65, dibulatkan ke prima |
| **m (prima)** | **154.001** | Prima terdekat |
| **Expected probe** | ~1.6 | < 2 requirement ✓ |

**Kode:**
```cpp
// Ukuran tabel
const int TABLE_SIZE = 154001;  // Prima

// Fungsi hash
int h1(int key) { return key % TABLE_SIZE; }
int h2(int key) { return 1 + (key % (TABLE_SIZE - 2)); }
```

---

## 8. Aplikasi Hash Table

### 8.1 Dictionary / Map

Hash table adalah implementasi umum untuk ADT Dictionary/Map yang menyimpan pasangan key-value.

```cpp
#include <unordered_map>

unordered_map<string, int> wordCount;
wordCount["hello"] = 1;
wordCount["world"] = 2;

// Access
cout << wordCount["hello"];  // 1

// Check existence
if (wordCount.find("test") != wordCount.end()) {
    // key exists
}
```

### 8.2 Set

Hash table juga digunakan untuk mengimplementasikan Set (kumpulan elemen unik).

```cpp
#include <unordered_set>

unordered_set<int> uniqueNumbers;
uniqueNumbers.insert(10);
uniqueNumbers.insert(20);
uniqueNumbers.insert(10);  // Tidak ditambahkan (sudah ada)

cout << uniqueNumbers.size();  // 2
```

### 8.3 Counting / Frequency

```cpp
// Menghitung frekuensi karakter
string text = "hello world";
unordered_map<char, int> freq;

for (char c : text) {
    freq[c]++;
}

// freq['l'] = 3, freq['o'] = 2, ...
```

### 8.4 Caching (LRU Cache)

Hash table + Doubly Linked List untuk implementasi LRU Cache dengan O(1) access dan eviction.

### 8.5 Aplikasi Pertahanan

1. **Database Personel:** Key = NRP/NIP, Value = data personel
2. **Tracking Aset:** Key = nomor inventaris, Value = lokasi & status
3. **Authentication:** Key = username, Value = hashed password
4. **Logging:** Key = timestamp, Value = log entry
5. **Network Packet Routing:** Key = destination IP, Value = next hop

---

### SOLVED PROBLEM 21 ⭐⭐

**Soal:** Implementasikan fungsi untuk mendeteksi apakah dua array memiliki elemen yang sama (intersection) menggunakan hash table!

**Penyelesaian:**

```cpp
#include <iostream>
#include <vector>
#include <unordered_set>
using namespace std;

vector<int> findIntersection(const vector<int>& arr1, 
                             const vector<int>& arr2) {
    // Masukkan elemen arr1 ke hash set
    unordered_set<int> set1(arr1.begin(), arr1.end());
    
    // Cek elemen arr2 yang ada di set1
    unordered_set<int> resultSet;
    for (int num : arr2) {
        if (set1.find(num) != set1.end()) {
            resultSet.insert(num);
        }
    }
    
    // Convert to vector
    return vector<int>(resultSet.begin(), resultSet.end());
}

int main() {
    vector<int> arr1 = {1, 2, 3, 4, 5};
    vector<int> arr2 = {4, 5, 6, 7, 8};
    
    vector<int> intersection = findIntersection(arr1, arr2);
    
    cout << "Intersection: ";
    for (int num : intersection) {
        cout << num << " ";
    }
    cout << endl;
    
    return 0;
}
```

**Output:**
```
Intersection: 4 5
```

**Kompleksitas:**
- Waktu: O(n + m) dimana n = |arr1|, m = |arr2|
- Ruang: O(n) untuk hash set

**Tanpa hash table:** O(n × m) dengan nested loop

---

### SOLVED PROBLEM 22 ⭐⭐⭐

**Soal:** Dalam sistem pertahanan, implementasikan hash table untuk menyimpan log aktivitas dengan fitur:
1. Insert log dengan timestamp sebagai key
2. Search log berdasarkan timestamp range
3. Delete log yang sudah kadaluarsa

**Penyelesaian:**

```cpp
#include <iostream>
#include <unordered_map>
#include <vector>
#include <ctime>
using namespace std;

struct LogEntry {
    time_t timestamp;
    string severity;    // INFO, WARNING, CRITICAL
    string source;      // Unit/sistem asal
    string message;
    
    void display() const {
        char buffer[26];
        ctime_r(&timestamp, buffer);
        buffer[24] = '\0';  // Remove newline
        cout << "[" << buffer << "] [" << severity << "] " 
             << source << ": " << message << endl;
    }
};

class ActivityLogger {
private:
    unordered_map<time_t, LogEntry> logs;
    time_t retentionPeriod;  // Dalam detik
    
public:
    ActivityLogger(int retentionDays = 30) {
        retentionPeriod = retentionDays * 24 * 60 * 60;
    }
    
    // Insert new log
    void addLog(const string& severity, const string& source, 
                const string& message) {
        time_t now = time(nullptr);
        
        LogEntry entry;
        entry.timestamp = now;
        entry.severity = severity;
        entry.source = source;
        entry.message = message;
        
        logs[now] = entry;
        
        // Auto-cleanup expired logs
        cleanupExpired();
    }
    
    // Search logs dalam range waktu
    vector<LogEntry> searchByTimeRange(time_t start, time_t end) {
        vector<LogEntry> result;
        
        for (auto& pair : logs) {
            if (pair.first >= start && pair.first <= end) {
                result.push_back(pair.second);
            }
        }
        
        // Sort by timestamp
        sort(result.begin(), result.end(), 
             [](const LogEntry& a, const LogEntry& b) {
                 return a.timestamp < b.timestamp;
             });
        
        return result;
    }
    
    // Search logs berdasarkan severity
    vector<LogEntry> searchBySeverity(const string& severity) {
        vector<LogEntry> result;
        
        for (auto& pair : logs) {
            if (pair.second.severity == severity) {
                result.push_back(pair.second);
            }
        }
        
        return result;
    }
    
    // Delete expired logs
    void cleanupExpired() {
        time_t cutoff = time(nullptr) - retentionPeriod;
        
        vector<time_t> toDelete;
        for (auto& pair : logs) {
            if (pair.first < cutoff) {
                toDelete.push_back(pair.first);
            }
        }
        
        for (time_t ts : toDelete) {
            logs.erase(ts);
        }
        
        if (!toDelete.empty()) {
            cout << "[Cleanup] Deleted " << toDelete.size() 
                 << " expired logs" << endl;
        }
    }
    
    // Manual delete
    bool deleteLog(time_t timestamp) {
        return logs.erase(timestamp) > 0;
    }
    
    // Statistics
    void showStats() {
        int infoCount = 0, warnCount = 0, critCount = 0;
        
        for (auto& pair : logs) {
            if (pair.second.severity == "INFO") infoCount++;
            else if (pair.second.severity == "WARNING") warnCount++;
            else if (pair.second.severity == "CRITICAL") critCount++;
        }
        
        cout << "=== Log Statistics ===" << endl;
        cout << "Total logs: " << logs.size() << endl;
        cout << "INFO: " << infoCount << endl;
        cout << "WARNING: " << warnCount << endl;
        cout << "CRITICAL: " << critCount << endl;
    }
    
    // Display all logs
    void displayAll() {
        vector<LogEntry> sorted;
        for (auto& pair : logs) {
            sorted.push_back(pair.second);
        }
        
        sort(sorted.begin(), sorted.end(),
             [](const LogEntry& a, const LogEntry& b) {
                 return a.timestamp < b.timestamp;
             });
        
        cout << "=== Activity Logs ===" << endl;
        for (auto& entry : sorted) {
            entry.display();
        }
    }
};

int main() {
    ActivityLogger logger(7);  // Retention 7 hari
    
    // Simulasi log entries
    logger.addLog("INFO", "RADAR-01", "Sistem aktif");
    logger.addLog("WARNING", "COMM-02", "Signal degradation detected");
    logger.addLog("CRITICAL", "SEC-01", "Unauthorized access attempt");
    logger.addLog("INFO", "RADAR-01", "Target terdeteksi: bearing 045");
    
    logger.displayAll();
    cout << endl;
    logger.showStats();
    
    // Search by severity
    cout << "\n=== Critical Alerts ===" << endl;
    auto critical = logger.searchBySeverity("CRITICAL");
    for (auto& entry : critical) {
        entry.display();
    }
    
    return 0;
}
```

**Analisis:**
- Insert: O(1) average
- Search by timestamp: O(1) untuk single, O(n) untuk range
- Search by severity: O(n) - bisa dioptimasi dengan secondary index
- Delete: O(1)
- Cleanup: O(n) tapi dilakukan periodik

**Optimasi lanjutan:**
- Secondary hash table untuk index by severity
- B-tree untuk range queries yang lebih efisien

---

## Supplementary Problems

Kerjakan soal-soal berikut untuk latihan tambahan. Jawaban singkat tersedia di bagian akhir.

### Problem S1 ⭐
Untuk hash table dengan h(k) = k mod 13, key mana yang akan collision dengan key 5?
a) 18, 31, 44
b) 19, 32, 45
c) 17, 30, 43
d) 20, 33, 46

### Problem S2 ⭐
Apa keuntungan utama double hashing dibanding linear probing?

### Problem S3 ⭐⭐
Hash table dengan m = 7 dan separate chaining. Setelah insert key 8, 15, 22, 1, 29, berapa panjang chain terpanjang?

### Problem S4 ⭐⭐
Jika hash table memiliki n = 500 elemen dan α = 0.8, berapa ukuran tabel m?

### Problem S5 ⭐⭐⭐
Desain fungsi hash untuk plat nomor kendaraan Indonesia (format: B 1234 ABC) yang meminimalkan collision!

---

## Ringkasan

| Konsep | Deskripsi | Kompleksitas |
|--------|-----------|--------------|
| **Hash Table** | Struktur data dengan O(1) average access | O(1) avg, O(n) worst |
| **Fungsi Hash** | Memetakan key ke index (division, multiplication, universal) | O(1) atau O(L) untuk string |
| **Collision** | Dua key berbeda menghasilkan hash sama | Pasti terjadi (Pigeonhole) |
| **Separate Chaining** | Linked list di setiap slot | Space: O(n + m) |
| **Open Addressing** | Probing dalam array (linear, quadratic, double) | Space: O(m) |
| **Load Factor** | α = n/m, threshold umumnya 0.75 | Mempengaruhi performa |
| **Rehashing** | Resize table saat α melebihi threshold | Amortized O(1) insert |

---

## Jawaban Supplementary Problems

**S1:** a) 18, 31, 44
- 18 mod 13 = 5 ✓
- 31 mod 13 = 5 ✓
- 44 mod 13 = 5 ✓

**S2:** Double hashing menghindari primary dan secondary clustering karena step size berbeda untuk setiap key, menghasilkan distribusi probe yang lebih merata.

**S3:** Panjang chain = 3
- h(8) = 8 mod 7 = 1
- h(15) = 15 mod 7 = 1 → chain di slot 1
- h(22) = 22 mod 7 = 1 → chain di slot 1
- h(1) = 1 mod 7 = 1 → chain di slot 1
- h(29) = 29 mod 7 = 1 → chain di slot 1 (total 5 elemen!)

Koreksi: Semua collision di slot 1, chain length = **5**

**S4:** m = n/α = 500/0.8 = **625**

**S5:** Contoh fungsi hash untuk plat nomor:
```cpp
int hashPlatNomor(const string& plat, int m) {
    // B 1234 ABC
    unsigned long hash = 0;
    
    // Huruf wilayah (B, D, F, dll)
    hash = plat[0] * 31;
    
    // Angka (1234)
    for (int i = 2; i <= 5; i++) {
        if (isdigit(plat[i])) {
            hash = hash * 31 + (plat[i] - '0');
        }
    }
    
    // Huruf seri (ABC)
    for (int i = 7; i < plat.length(); i++) {
        hash = hash * 31 + plat[i];
    }
    
    return hash % m;
}
```

---

## Referensi

1. Cormen, T.H., et al. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 11.
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 5.
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 8.

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
