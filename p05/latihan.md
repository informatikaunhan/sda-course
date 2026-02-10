# Latihan Mandiri 05: Stack

**Mata Kuliah:** Struktur Data dan Algoritma  
**Pertemuan:** 05  
**Topik:** Stack  
**Waktu:** 150 menit  
**Sifat:** Open Book

---

## Petunjuk Pengerjaan

1. Kerjakan semua soal dengan teliti
2. Bagian A: Pilihan ganda (2 poin per soal)
3. Bagian B: Essay dan implementasi (10-15 poin per soal)
4. Bagian C: Studi kasus pertahanan (50 poin per kasus)
5. Tuliskan langkah-langkah penyelesaian dengan jelas
6. Perhatikan kompleksitas waktu dan ruang dalam implementasi

---

## Bagian A: Soal Pilihan Ganda (20 Soal)

**Instruksi:** Pilih satu jawaban yang paling tepat.

### Soal 1
Stack adalah struktur data yang mengikuti prinsip:
- A. FIFO (First-In-First-Out)
- B. LIFO (Last-In-First-Out)
- C. Random Access
- D. Priority-based

### Soal 2
Pada stack, operasi untuk menambahkan elemen disebut:
- A. enqueue
- B. insert
- C. push
- D. append

### Soal 3
Operasi `peek()` pada stack berfungsi untuk:
- A. Menghapus elemen top
- B. Melihat elemen top tanpa menghapus
- C. Menghitung jumlah elemen
- D. Memeriksa apakah stack kosong

### Soal 4
Pada implementasi stack dengan array, jika `topIndex = -1`, maka:
- A. Stack penuh
- B. Stack berisi satu elemen
- C. Stack kosong
- D. Stack overflow

### Soal 5
Diberikan stack kosong S. Setelah operasi: `push(1), push(2), push(3), pop(), push(4)`, elemen top adalah:
- A. 1
- B. 2
- C. 3
- D. 4

### Soal 6
Kompleksitas waktu operasi `push()` pada stack yang diimplementasikan dengan linked list adalah:
- A. O(n)
- B. O(log n)
- C. O(1)
- D. O(n²)

### Soal 7
Mengapa operasi push dan pop pada stack menggunakan linked list dilakukan di head (bukan tail)?
- A. Karena linked list tidak memiliki tail
- B. Karena head lebih mudah diakses
- C. Karena operasi di head O(1), sedangkan pop di tail O(n)
- D. Tidak ada perbedaan

### Soal 8
Dalam algoritma balanced parentheses, ketika menemukan kurung tutup `)`, aksi yang dilakukan adalah:
- A. Push ke stack
- B. Pop dan cek matching
- C. Abaikan
- D. Clear stack

### Soal 9
String mana yang balanced?
- A. `([)]`
- B. `{[()]}`
- C. `((())`
- D. `{[}`

### Soal 10
Dalam konversi infix ke postfix, operator dengan prioritas lebih tinggi akan:
- A. Selalu di-push langsung
- B. Menunggu operator prioritas rendah keluar
- C. Menyebabkan operator prioritas lebih rendah di-pop
- D. Diabaikan

### Soal 11
Ekspresi infix `A + B * C` dalam notasi postfix adalah:
- A. `+ A * B C`
- B. `A B C * +`
- C. `A B + C *`
- D. `A B C + *`

### Soal 12
Dalam evaluasi postfix `3 4 + 5 *`, urutan operasi yang benar adalah:
- A. 3 + 4, lalu hasil * 5
- B. 4 + 5, lalu hasil * 3
- C. 3 * 5, lalu hasil + 4
- D. 4 * 5, lalu hasil + 3

### Soal 13
Hasil evaluasi postfix `8 2 / 3 -` adalah:
- A. -1
- B. 1
- C. 4
- D. 6

### Soal 14
Dalam doubling strategy untuk dynamic array stack, kapan resize dilakukan?
- A. Setiap operasi push
- B. Ketika stack 50% penuh
- C. Ketika stack penuh
- D. Setiap 10 operasi

### Soal 15
Amortized time complexity dari operasi push pada dynamic array stack dengan doubling strategy adalah:
- A. O(n)
- B. O(log n)
- C. O(1)
- D. O(n²)

### Soal 16
Apa yang menyebabkan "stack overflow" pada rekursi?
- A. Base case terlalu cepat tercapai
- B. Tidak ada base case atau base case tidak tercapai
- C. Return value terlalu besar
- D. Parameter fungsi terlalu banyak

### Soal 17
Dalam sistem undo/redo, ketika user melakukan aksi baru setelah undo, apa yang terjadi dengan redo stack?
- A. Tetap tidak berubah
- B. Ditambahkan aksi baru
- C. Di-clear/dikosongkan
- D. Dipindahkan ke undo stack

### Soal 18
Untuk mengimplementasikan queue menggunakan stack, minimal diperlukan berapa stack?
- A. 1 stack
- B. 2 stack
- C. 3 stack
- D. 4 stack

### Soal 19
Operator `^` (pangkat) berbeda dari `+`, `-`, `*`, `/` dalam hal:
- A. Prioritas lebih rendah
- B. Right-to-left associativity
- C. Tidak bisa digunakan dalam postfix
- D. Memerlukan 3 operand

### Soal 20
Dalam implementasi MinStack (stack dengan operasi getMin O(1)), struktur data tambahan yang dibutuhkan adalah:
- A. Array biasa
- B. Stack tambahan untuk menyimpan minimum
- C. Linked list
- D. Binary tree

---

## Bagian B: Soal Uraian (15 Soal)

### Soal 1 (Mudah)
**Trace Operasi Stack**

Diberikan stack kosong. Trace operasi berikut dan tuliskan:
- Isi stack setelah setiap operasi
- Nilai yang dikembalikan oleh setiap operasi pop

```
push(10), push(20), pop(), push(30), push(40), pop(), pop(), push(50)
```

---

### Soal 2 (Mudah)
**Perbandingan Implementasi**

Jelaskan kelebihan dan kekurangan implementasi stack menggunakan:
a) Array statis
b) Array dinamis
c) Linked list

Dalam kondisi apa masing-masing implementasi paling cocok digunakan?

---

### Soal 3 (Mudah)
**Balanced Parentheses Trace**

Trace algoritma balanced parentheses untuk string berikut. Tunjukkan isi stack pada setiap langkah dan tentukan apakah balanced atau tidak:

a) `{[()()]}`
b) `[({}])`

---

### Soal 4 (Sedang)
**Konversi Infix ke Postfix**

Konversi ekspresi infix berikut ke postfix menggunakan algoritma Shunting-Yard. Tunjukkan trace lengkap (token, action, stack, output):

```
A * (B + C) - D / E
```

---

### Soal 5 (Sedang)
**Evaluasi Postfix**

Evaluasi ekspresi postfix berikut. Tunjukkan trace lengkap (token, action, stack, calculation):

```
6 2 3 + - 3 8 2 / + *
```

---

### Soal 6 (Mudah)
**Implementasi peek() dan isEmpty()**

Implementasikan method `peek()` dan `isEmpty()` untuk stack menggunakan array dalam C++. Sertakan penanganan error yang tepat.

---

### Soal 7 (Sedang)
**Implementasi Stack dengan Linked List**

Implementasikan class `StackLinkedList` dalam C++ dengan operasi:
- `push(int value)`
- `pop()`
- `peek()`
- `isEmpty()`
- `size()`

Sertakan destructor untuk mencegah memory leak.

---

### Soal 8 (Sedang)
**Analisis Kompleksitas**

Analisis kompleksitas waktu (best, worst, average case) dan ruang untuk operasi berikut pada stack yang diimplementasikan dengan array dinamis:

a) push() saat array belum penuh
b) push() saat array penuh (perlu resize)
c) 100 operasi push berturut-turut (amortized)

---

### Soal 9 (Sedang)
**Konversi Rekursi ke Iterasi**

Fungsi rekursif berikut menghitung jumlah digit suatu bilangan:

```cpp
int sumDigits(int n) {
    if (n == 0) return 0;
    return (n % 10) + sumDigits(n / 10);
}
```

Ubah fungsi ini menjadi versi iteratif menggunakan stack eksplisit.

---

### Soal 10 (Sedang)
**String Reversal dengan Stack**

Implementasikan fungsi untuk membalik string menggunakan stack. Fungsi harus:
- Menerima string input
- Mengembalikan string yang sudah dibalik
- Hanya menggunakan operasi stack (push, pop)

---

### Soal 11 (Sedang)
**Validasi Ekspresi Matematika**

Modifikasi algoritma balanced parentheses untuk memvalidasi ekspresi matematika yang mengandung:
- Tanda kurung: `()`, `[]`, `{}`
- Operator: `+`, `-`, `*`, `/`
- Operand: angka dan variabel (huruf)

Fungsi harus mengembalikan `true` jika ekspresi valid (kurung balanced dan operator/operand benar).

---

### Soal 12 (Sedang)
**Next Greater Element**

Jelaskan algoritma untuk menemukan Next Greater Element (NGE) untuk setiap elemen dalam array menggunakan stack dengan kompleksitas O(n). Berikan contoh untuk array `[4, 5, 2, 10, 8]`.

---

### Soal 13 (Mudah)
**Browser History**

Jelaskan bagaimana browser history (back/forward) dapat diimplementasikan menggunakan dua stack. Gambarkan state kedua stack setelah operasi berikut:

1. Kunjungi: google.com
2. Kunjungi: youtube.com
3. Kunjungi: facebook.com
4. Back
5. Back
6. Forward
7. Kunjungi: twitter.com

---

### Soal 14 (Sulit)
**Sort Stack**

Implementasikan fungsi untuk mengurutkan stack secara ascending (elemen terkecil di top) menggunakan hanya satu stack tambahan sebagai tempat sementara. Tidak boleh menggunakan struktur data lain.

---

### Soal 15 (Sulit)
**Stock Span Problem**

Stock span adalah jumlah hari berturut-turut sebelum hari ini di mana harga saham ≤ harga hari ini. Implementasikan fungsi untuk menghitung span menggunakan stack dengan kompleksitas O(n).

Contoh:
```
Harga: [100, 80, 60, 70, 60, 75, 85]
Span:  [1,   1,  1,  2,  1,  4,  6]
```

---

## Bagian C: Studi Kasus Pertahanan (2 Kasus)

### Studi Kasus 1: Sistem Manajemen Perintah Militer (50 poin)

**Latar Belakang:**
Dalam operasi militer, sistem command & control harus mampu mengelola perintah dengan fitur undo/redo untuk mengantisipasi perubahan situasi di lapangan. Setiap perintah memiliki ID, deskripsi, unit pelaksana, dan timestamp.

**Tugas:**
Rancang dan implementasikan `MilitaryCommandSystem` dengan spesifikasi:

1. **Struktur Data Command:**
```cpp
struct Command {
    int id;
    string description;
    string unit;
    time_t timestamp;
    int priority;  // 1-5, 5 tertinggi
};
```

2. **Operasi yang harus didukung:**
   - `issueCommand(description, unit, priority)`: Mengeluarkan perintah baru
   - `cancelLastCommand()`: Membatalkan perintah terakhir
   - `reinstateCommand()`: Mengembalikan perintah yang dibatalkan
   - `getActiveCommands()`: Menampilkan semua perintah aktif
   - `getHighPriorityCommand()`: Mengembalikan perintah dengan prioritas tertinggi

3. **Constraint:**
   - Maksimum 20 perintah dalam undo history
   - Perintah dengan priority 5 tidak bisa di-cancel tanpa konfirmasi khusus
   - Log semua operasi dengan timestamp

4. **Deliverable:**
   - Desain class dengan penjelasan struktur data yang digunakan
   - Implementasi lengkap dalam C++
   - Analisis kompleksitas setiap operasi
   - Contoh skenario penggunaan dengan output

---

### Studi Kasus 2: Sistem Analisis Sinyal Radar (50 poin)

**Latar Belakang:**
Sistem radar pertahanan udara menerima data sinyal secara real-time. Untuk mendeteksi anomali, sistem perlu menganalisis pola kenaikan dan penurunan kekuatan sinyal menggunakan konsep sliding window maximum.

**Tugas:**
Implementasikan `RadarSignalAnalyzer` yang dapat:

1. **Input:**
   - Stream data kekuatan sinyal (array integer)
   - Window size k untuk analisis

2. **Operasi yang harus didukung:**
   - `processSignal(int strength)`: Memproses sinyal baru
   - `getMaxInWindow()`: Mendapatkan nilai maksimum dalam window terakhir
   - `detectAnomalies()`: Mendeteksi lonjakan sinyal yang mencurigakan
   - `getSignalHistory(int n)`: Mendapatkan n sinyal terakhir

3. **Algoritma Sliding Window Maximum:**
   Gunakan struktur data berbasis stack/deque untuk mencapai kompleksitas O(n) untuk memproses n sinyal.

4. **Kriteria Anomali:**
   - Lonjakan > 50% dari rata-rata window sebelumnya
   - Penurunan > 30% secara tiba-tiba
   - Pola berulang yang mencurigakan

5. **Deliverable:**
   - Implementasi lengkap dalam C++
   - Penggunaan stack/deque untuk optimasi
   - Analisis kompleksitas
   - Simulasi dengan data contoh:
   ```
   Sinyal: [10, 15, 12, 20, 18, 50, 25, 30, 28, 35]
   Window size: 3
   ```
   - Identifikasi anomali dalam data tersebut

---

## Kunci Jawaban

### Bagian A: Pilihan Ganda

| No | Jawaban | Penjelasan Singkat |
|----|---------|-------------------|
| 1 | B | LIFO - Last-In-First-Out |
| 2 | C | push adalah operasi menambah elemen |
| 3 | B | peek melihat tanpa menghapus |
| 4 | C | topIndex = -1 berarti kosong |
| 5 | D | Stack: [1,2,4], top = 4 |
| 6 | C | O(1) karena selalu di head |
| 7 | C | Pop di tail perlu traverse O(n) |
| 8 | B | Pop dan cek apakah match |
| 9 | B | {[()]} adalah balanced |
| 10 | C | Prioritas tinggi menyebabkan pop rendah |
| 11 | B | A B C * + (B*C dulu, lalu +A) |
| 12 | A | 3+4=7, lalu 7*5=35 |
| 13 | B | 8/2=4, 4-3=1 |
| 14 | C | Resize saat penuh |
| 15 | C | O(1) amortized |
| 16 | B | Tidak ada/tidak tercapai base case |
| 17 | C | Redo stack di-clear |
| 18 | B | Minimal 2 stack |
| 19 | B | ^ adalah right-to-left |
| 20 | B | Stack tambahan untuk minimum |

---

### Bagian B: Jawaban Essay

#### Soal 1: Trace Operasi Stack

| Operasi | Stack | Return |
|---------|-------|--------|
| push(10) | [10] | - |
| push(20) | [10, 20] | - |
| pop() | [10] | 20 |
| push(30) | [10, 30] | - |
| push(40) | [10, 30, 40] | - |
| pop() | [10, 30] | 40 |
| pop() | [10] | 30 |
| push(50) | [10, 50] | - |

**Hasil akhir:** Stack = [10, 50], Return values: 20, 40, 30

---

#### Soal 2: Perbandingan Implementasi

**a) Array Statis:**
- Kelebihan: Sederhana, O(1), cache-friendly
- Kekurangan: Ukuran tetap, waste memory
- Cocok untuk: Ukuran maksimum diketahui, embedded systems

**b) Array Dinamis:**
- Kelebihan: Fleksibel, O(1) amortized, cache-friendly
- Kekurangan: Resize memerlukan waktu O(n)
- Cocok untuk: General purpose, ukuran tidak diketahui

**c) Linked List:**
- Kelebihan: Sangat fleksibel, O(1) murni
- Kekurangan: Overhead pointer, tidak cache-friendly
- Cocok untuk: Ukuran sangat bervariasi, memory terbatas

---

#### Soal 3: Balanced Parentheses Trace

**a) `{[()()]}`**

| Char | Action | Stack | Status |
|------|--------|-------|--------|
| { | Push | [{] | - |
| [ | Push | [{, [] | - |
| ( | Push | [{, [, (] | - |
| ) | Pop, match | [{, [] | ✓ |
| ( | Push | [{, [, (] | - |
| ) | Pop, match | [{, [] | ✓ |
| ] | Pop, match | [{] | ✓ |
| } | Pop, match | [] | ✓ |

**Hasil: BALANCED ✓**

**b) `[({}])`**

| Char | Action | Stack | Status |
|------|--------|-------|--------|
| [ | Push | [[] | - |
| ( | Push | [[, (] | - |
| { | Push | [[, (, {] | - |
| } | Pop, match | [[, (] | ✓ |
| ] | Pop | [[, (] | ( ≠ ] ✗ |

**Hasil: NOT BALANCED ✗**

---

#### Soal 4: Konversi Infix ke Postfix

**Infix:** `A * (B + C) - D / E`

| Token | Action | Stack | Output |
|-------|--------|-------|--------|
| A | Output | [] | A |
| * | Push | [*] | A |
| ( | Push | [*, (] | A |
| B | Output | [*, (] | AB |
| + | Push | [*, (, +] | AB |
| C | Output | [*, (, +] | ABC |
| ) | Pop sampai ( | [*] | ABC+ |
| - | Pop *, Push - | [-] | ABC+* |
| D | Output | [-] | ABC+*D |
| / | Push (/ > -) | [-, /] | ABC+*D |
| E | Output | [-, /] | ABC+*DE |
| END | Pop all | [] | ABC+*DE/- |

**Hasil Postfix:** `ABC+*DE/-`

---

#### Soal 5: Evaluasi Postfix

**Postfix:** `6 2 3 + - 3 8 2 / + *`

| Token | Action | Stack | Calculation |
|-------|--------|-------|-------------|
| 6 | Push | [6] | - |
| 2 | Push | [6, 2] | - |
| 3 | Push | [6, 2, 3] | - |
| + | Pop, calc, push | [6, 5] | 2+3=5 |
| - | Pop, calc, push | [1] | 6-5=1 |
| 3 | Push | [1, 3] | - |
| 8 | Push | [1, 3, 8] | - |
| 2 | Push | [1, 3, 8, 2] | - |
| / | Pop, calc, push | [1, 3, 4] | 8/2=4 |
| + | Pop, calc, push | [1, 7] | 3+4=7 |
| * | Pop, calc, push | [7] | 1*7=7 |

**Hasil:** 7

---

#### Soal 6: Implementasi peek() dan isEmpty()

```cpp
class StackArray {
private:
    static const int MAX_SIZE = 100;
    int data[MAX_SIZE];
    int topIndex;
    
public:
    StackArray() : topIndex(-1) {}
    
    bool isEmpty() {
        return topIndex == -1;
    }
    
    int peek() {
        if (isEmpty()) {
            throw runtime_error("Stack is empty - cannot peek");
            // atau: cout << "Error: Stack kosong!" << endl; return -1;
        }
        return data[topIndex];
    }
};
```

---

#### Soal 7: Implementasi Stack dengan Linked List

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class StackLinkedList {
private:
    Node* topNode;
    int count;
    
public:
    StackLinkedList() : topNode(nullptr), count(0) {}
    
    ~StackLinkedList() {
        while (!isEmpty()) {
            pop();
        }
    }
    
    void push(int value) {
        Node* newNode = new Node(value);
        newNode->next = topNode;
        topNode = newNode;
        count++;
    }
    
    int pop() {
        if (isEmpty()) {
            cout << "Error: Stack Underflow!" << endl;
            return -1;
        }
        Node* temp = topNode;
        int value = temp->data;
        topNode = topNode->next;
        delete temp;
        count--;
        return value;
    }
    
    int peek() {
        if (isEmpty()) {
            cout << "Error: Stack kosong!" << endl;
            return -1;
        }
        return topNode->data;
    }
    
    bool isEmpty() {
        return topNode == nullptr;
    }
    
    int size() {
        return count;
    }
};
```

---

#### Soal 8: Analisis Kompleksitas

**a) push() saat array belum penuh:**
- Time: O(1)
- Space: O(1)

**b) push() saat array penuh (resize):**
- Time: O(n) untuk copy n elemen
- Space: O(n) untuk array baru (lalu array lama di-delete)

**c) 100 operasi push (amortized):**
- Jika mulai dari kapasitas 1: resize di 1, 2, 4, 8, 16, 32, 64, 128
- Total copy: 1+2+4+8+16+32+64 = 127
- Amortized per operasi: 127/100 ≈ 1.27 = O(1)

---

#### Soal 9: Konversi Rekursi ke Iterasi

```cpp
int sumDigitsIterative(int n) {
    stack<int> s;
    
    // Push semua digit ke stack
    while (n > 0) {
        s.push(n % 10);
        n = n / 10;
    }
    
    // Pop dan jumlahkan
    int sum = 0;
    while (!s.empty()) {
        sum += s.top();
        s.pop();
    }
    
    return sum;
}
```

---

#### Soal 10: String Reversal

```cpp
#include <stack>
#include <string>
using namespace std;

string reverseString(string str) {
    stack<char> s;
    
    // Push semua karakter
    for (char c : str) {
        s.push(c);
    }
    
    // Pop untuk mendapatkan reversed string
    string reversed = "";
    while (!s.empty()) {
        reversed += s.top();
        s.pop();
    }
    
    return reversed;
}
```

---

#### Soal 11: Validasi Ekspresi Matematika

```cpp
bool isValidExpression(string expr) {
    stack<char> s;
    bool expectOperand = true;  // Mulai dengan expecting operand
    
    for (char c : expr) {
        if (c == ' ') continue;
        
        // Kurung buka
        if (c == '(' || c == '[' || c == '{') {
            s.push(c);
            expectOperand = true;
        }
        // Kurung tutup
        else if (c == ')' || c == ']' || c == '}') {
            if (s.empty()) return false;
            char top = s.top(); s.pop();
            if (!isMatchingPair(top, c)) return false;
            expectOperand = false;
        }
        // Operator
        else if (c == '+' || c == '-' || c == '*' || c == '/') {
            if (expectOperand) return false;  // Operator tanpa operand
            expectOperand = true;
        }
        // Operand (angka atau huruf)
        else if (isalnum(c)) {
            expectOperand = false;
        }
    }
    
    return s.empty() && !expectOperand;
}
```

---

#### Soal 12: Next Greater Element

**Algoritma:**
1. Traverse array dari kanan ke kiri
2. Untuk setiap elemen, pop semua elemen stack yang ≤ elemen saat ini
3. Jika stack tidak kosong, top adalah NGE; jika kosong, NGE = -1
4. Push elemen saat ini ke stack

**Contoh: `[4, 5, 2, 10, 8]`**

| Index | Element | Stack Before | Action | NGE | Stack After |
|-------|---------|--------------|--------|-----|-------------|
| 4 | 8 | [] | Push | -1 | [8] |
| 3 | 10 | [8] | Pop 8, Push | -1 | [10] |
| 2 | 2 | [10] | Push | 10 | [10, 2] |
| 1 | 5 | [10, 2] | Pop 2, Push | 10 | [10, 5] |
| 0 | 4 | [10, 5] | Push | 5 | [10, 5, 4] |

**Hasil NGE: [5, 10, 10, -1, -1]**

---

#### Soal 13: Browser History

| Operasi | Current | Back Stack | Forward Stack |
|---------|---------|------------|---------------|
| Initial | - | [] | [] |
| Visit google | google | [] | [] |
| Visit youtube | youtube | [google] | [] |
| Visit facebook | facebook | [google, youtube] | [] |
| Back | youtube | [google] | [facebook] |
| Back | google | [] | [facebook, youtube] |
| Forward | youtube | [google] | [facebook] |
| Visit twitter | twitter | [google, youtube] | [] |

**State Akhir:**
- Current: twitter
- Back: [google, youtube]
- Forward: [] (di-clear karena visit baru)

---

#### Soal 14: Sort Stack

```cpp
void sortStack(stack<int>& input) {
    stack<int> tempStack;
    
    while (!input.empty()) {
        int temp = input.top();
        input.pop();
        
        // Pindahkan elemen dari tempStack yang > temp kembali ke input
        while (!tempStack.empty() && tempStack.top() > temp) {
            input.push(tempStack.top());
            tempStack.pop();
        }
        
        tempStack.push(temp);
    }
    
    // Pindahkan kembali ke input (sekarang terurut descending)
    while (!tempStack.empty()) {
        input.push(tempStack.top());
        tempStack.pop();
    }
}
```

**Kompleksitas:** O(n²) worst case

---

#### Soal 15: Stock Span

```cpp
vector<int> calculateSpan(vector<int>& prices) {
    int n = prices.size();
    vector<int> span(n);
    stack<int> s;  // Stack menyimpan indeks
    
    for (int i = 0; i < n; i++) {
        // Pop semua elemen dengan harga <= harga saat ini
        while (!s.empty() && prices[s.top()] <= prices[i]) {
            s.pop();
        }
        
        // Hitung span
        span[i] = s.empty() ? (i + 1) : (i - s.top());
        
        s.push(i);
    }
    
    return span;
}

// Untuk: [100, 80, 60, 70, 60, 75, 85]
// Hasil: [1, 1, 1, 2, 1, 4, 6]
```

**Kompleksitas:** O(n) - setiap elemen di-push dan di-pop maksimal sekali

---

### Bagian C: Panduan Jawaban Studi Kasus

#### Studi Kasus 1: Sistem Manajemen Perintah Militer

**Struktur Utama:**
```cpp
class MilitaryCommandSystem {
private:
    stack<Command> activeCommands;
    stack<Command> cancelledCommands;
    vector<string> operationLog;
    int nextId;
    const int MAX_UNDO_HISTORY = 20;
    
public:
    void issueCommand(string desc, string unit, int priority);
    bool cancelLastCommand(bool forceCancel = false);
    void reinstateCommand();
    void getActiveCommands();
    Command getHighPriorityCommand();
    void logOperation(string operation);
};
```

**Kompleksitas:**
- issueCommand: O(1)
- cancelLastCommand: O(1)
- reinstateCommand: O(1)
- getActiveCommands: O(n)
- getHighPriorityCommand: O(n) atau O(1) dengan auxiliary data structure

---

#### Studi Kasus 2: Sistem Analisis Sinyal Radar

**Algoritma Sliding Window Maximum menggunakan Deque:**
```cpp
class RadarSignalAnalyzer {
private:
    deque<pair<int, int>> window;  // (value, index)
    vector<int> signalHistory;
    int windowSize;
    int currentIndex;
    
public:
    int processSignal(int strength) {
        currentIndex++;
        
        // Hapus elemen yang keluar dari window
        while (!window.empty() && 
               window.front().second <= currentIndex - windowSize) {
            window.pop_front();
        }
        
        // Hapus elemen yang lebih kecil dari strength baru
        while (!window.empty() && window.back().first <= strength) {
            window.pop_back();
        }
        
        window.push_back({strength, currentIndex});
        signalHistory.push_back(strength);
        
        return window.front().first;  // Maximum in window
    }
};
```

**Analisis untuk data [10, 15, 12, 20, 18, 50, 25, 30, 28, 35], window=3:**

| Signal | Window | Max | Anomaly |
|--------|--------|-----|---------|
| 10 | [10] | 10 | - |
| 15 | [10,15] | 15 | - |
| 12 | [10,15,12] | 15 | - |
| 20 | [15,12,20] | 20 | - |
| 18 | [12,20,18] | 20 | - |
| 50 | [20,18,50] | 50 | **⚠️ Lonjakan 150%** |
| 25 | [18,50,25] | 50 | - |
| 30 | [50,25,30] | 50 | - |
| 28 | [25,30,28] | 30 | **⚠️ Penurunan 44%** |
| 35 | [30,28,35] | 35 | - |

**Anomali terdeteksi:** Index 5 (lonjakan), Index 8 (penurunan setelah puncak)

---

## Rubrik Penilaian

| Komponen | Poin | Kriteria |
|----------|------|----------|
| Bagian A | 40 | 2 poin per jawaban benar |
| Bagian B | 160 | Sesuai bobot per soal |
| Bagian C | 100 | 50 poin per studi kasus |
| **Total** | **300** | |

### Konversi Nilai

| Rentang | Nilai |
|---------|-------|
| 255-300 | A |
| 240-254 | A- |
| 225-239 | B+ |
| 210-224 | B |
| 195-209 | B- |
| 180-194 | C+ |
| 165-179 | C |
| 120-164 | D |
| 0-119 | E |

---

## Referensi

1. Cormen, T.H., Leiserson, C.E., Rivest, R.L., & Stein, C. (2022). *Introduction to Algorithms* (4th Ed.). MIT Press. Chapter 10.1
2. Weiss, M.A. (2014). *Data Structures and Algorithm Analysis in C++* (4th Ed.). Pearson. Chapter 3.6
3. Hubbard, J.R. (2000). *Data Structures with C++ (Schaum's Outlines)*. McGraw-Hill. Chapter 5

---

## License

This repository is licensed under the **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Commercial use is permitted, provided attribution is given to the author.

© 2026 Anindito
