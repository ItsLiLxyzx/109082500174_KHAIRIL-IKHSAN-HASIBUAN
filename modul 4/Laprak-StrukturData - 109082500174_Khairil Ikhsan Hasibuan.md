# <h1 align="center"> Modul 4 SINGLY LINKED LIST (BAGIAN PERTAMA) </h1>
<p align="center">Khairil Ikhsan Hasibuan - 109082500174</p>

## Dasar Teori

### A. Pengertian Linked List

Linked List atau senarai berantai merupakan struktur data yang tersusun atas beberapa elemen yang saling terhubung. Struktur data tersebut bersifat dinamis sehingga jumlah elemennya dapat bertambah ataupun berkurang sesuai kebutuhan. Berbeda dengan array yang umumnya memiliki ukuran tetap ketika dibuat, linked list memanfaatkan pointer untuk menghubungkan setiap elemen, sehingga lebih fleksibel untuk mengelola data yang jumlahnya belum diketahui.

## B. Singly Linked List

Singly Linked List adalah jenis linked list yang setiap elemennya hanya memiliki satu pointer yang menuju ke elemen berikutnya. Setiap elemen atau node terdiri dari dua bagian yaitu:

- **Data**: Berisi informasi atau nilai yang disimpan.

- **Successor (next)**: Pointer yang menuju ke node berikutnya.

**Karakteristik Singly Linked List:**

1. Setiap node memiliki satu pointer yang menuju ke node selanjutnya.

2. Node terakhir menuju ke Nil karena tidak ada node setelahnya.

3. Penelusuran data hanya bisa dilakukan dari awal ke arah node terakhir.

4. Penambahan dan penghapusan node dapat dilakukan dengan mengatur pointer yang menghubungkan setiap node.

**Istilah Penting:**

| Istilah | Deskripsi |
| :--- | :--- |
| first/head | Pointer yang menuju ke node pertama. |
| next | Pointer yang menuju ke node selanjutnya. |
| Nil/NULL | Penanda pointer tidak menuju ke node mana pun. |
| Node | Bagian yang menyimpan data dan pointer dalam linked list. |


**Alokasi dan Dealokasi Memori**

- **Alokasi (C++):** `P = new elmlist;` digunakan untuk membuat node baru.
- **Dealokasi (C++):** `delete P;` digunakan untuk menghapus node dan membersihkan memori.

**Operasi Dasar Linked List**

Beberapa operasi yang dapat digunakan untuk mengelola linked list.

1. **CreateList:** Membuat linked list dalam keadaan kosong dengan `first = Nil`.
2. **Insert:** Digunakan untuk menambahkan node baru ke dalam list:
   - `insertFirst`, untuk menambahkan node di awal list.
   - `insertLast`, untuk menambahkan node di akhir list.
   - `insertAfter`, untuk menambahkan node setelah node tertentu.
3. **Delete:** Digunakan untuk menghapus node dari list:
   - `deleteFirst`, untuk menghapus node pertama.
   - `deleteLast`, untuk menghapus node terakhir.
   - `deleteAfter`, untuk menghapus node setelah node tertentu.
4. **View (printInfo):** Digunakan untuk menampilkan semua data di dalam list dengan cara menelusuri setiap node.
5. **Update:** Digunakan untuk merubah data setelah node yang ingin diubah ditemukan.

### C. Abstract Data Type (ADT)

Abstract Data Type (ADT) merupakan tipe data yang memiliki beberapa operasi dasar untuk mengolah data. ADT dibagi menjadi tiga bagian, yaitu:

1. **Header (.h):** Berisi deklarasi tipe data dan fungsi yang akan digunakan.

2. **Body (.cpp):** Berisi isi kode dari fungsi-fungsi yang sudah dideklarasikan di header.

3. **Driver (main.cpp):** Berisi program utama untuk menjalankan dan mencoba fungsi-fungsi yang telah dibuat.

## Guided 

### 1. Program list.h

```C++
#ifndef LIST_h
#define LIST_h
#define Nil NULL

#include <iostream>
using namespace std;

struct mahasiswa {
    string nama;
    string nim;
    int umur;
};

typedef mahasiswa datamahasiswa;

typedef struct mode *address;

struct mode {
    datamahasiswa isidata;
    address next;
};

struct linked list {
    address first;
}

bool isEmpty(linkedlist list);
void createList(linkedlist &list);
address alokasi(string nama, string nim, int umur);
void dealokasi(address &node);
void printList(linkedlist list);
void insertFirst(linkedlist &list, address nodeBaru);
void insertAfter(linkedlist &list, address nodeBaru, address Prev);
void insertLast(linkedlist &list, address nodeBaru);

void delFirst(linkedlist &list);
void delLast(linkedlist &list);
void delAfter(linkedlist &list, address nodeHapus, address nodePrev);
int nbList(linkedlist list);
void deleteFirst(linkedlist &list);

#endif
```
File list.h adalah file header yang berfungsi sebagai antarmuka (interface) dari Abstract Data Type (ADT) Linked List. File ini mendeklarasikan struktur data, tipe bentukan, serta prototipe semua fungsi dan prosedur yang akan diimplementasikan di file list.cpp.

### 2. Program list.cpp

```C++
#include "list.h"
#include <iostream>
using namespace std;

// I.S = Initial State / kondisi awal
// F.S = Final State / kondisi akhir

// Fungsi untuk cek apakah list kosong atau tidak
bool isEmpty(LinkedList List) {
    if(List.first == Nil) {
        return true;
    } else {
        return false;
    }
}

// pembuatan linked list kosong
void createList(LinkedList &List) {
    /* I.S. sembarang
       F.S. terbentuk list kosong */
    List.first = Nil;
}

// pembuatan node baru dengan menerapkan manajemen memori
address alokasi(string nama, string nim, int umur) {
    /* I.S. sembarang
       F.S. mengembalikan alamat node baru dengan isidata = sesuai parameter dan next = Nil */
    address nodeBaru = new node;
    nodeBaru->isidata.nama = nama;
    nodeBaru->isidata.nim = nim;
    nodeBaru->isidata.umur = umur;
    nodeBaru->next = Nil;
    return nodeBaru;
}

// penghapusan node dengan menerapkan manajemen memori
void dealokasi(address &node) {
    /* I.S. P terdefinisi
       F.S. memori yang digunakan node dikembalikan ke sistem */
    node->next = Nil;
    delete node;
}

// prosedur-prosedur untuk insert / menambahkan node baru kedalam list
void insertFirst(LinkedList &List, address nodeBaru) {
    /* I.S. sembarang, P sudah dialokasikan
       F.S. menempatkan elemen list (node) pada awal list */
    nodeBaru->next = List.first;
    List.first = nodeBaru;
}

void insertAfter(LinkedList &List, address nodeBaru, address Prev) {
    /* I.S. sembarang, nodeBaru dan Prev alamat salah satu elemen list (node)
       F.S. menempatkan elemen (node) sesudah elemen node Prev */
    if (Prev != Nil) {
        nodeBaru->next = Prev->next;
        Prev->next = nodeBaru;
    } else {
        cout << "Node sebelumnya tidak valid!" << endl;
    }
}

void insertLast(LinkedList &List, address nodeBaru) {
    /* I.S. sembarang, nodeBaru sudah dialokasikan
       F.S. menempatkan elemen nodeBaru pada akhir list */
    if (isEmpty(List)) {
        List.first = nodeBaru;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu->next != Nil) {
            nodeBantu = nodeBantu->next;
        }
        nodeBantu->next = nodeBaru;
    }
}

// prosedur-prosedur untuk delete / menghapus node yang ada didalam list
void delFirst(LinkedList &List) {
    /* I.S. list tidak kosong
       F.S. node pertama di list terhapus */
    address nodeHapus;
    if (isEmpty(List) == false) {
        nodeHapus = List.first;
        List.first = List.first->next;
        nodeHapus->next = Nil;
        dealokasi(nodeHapus);
    } else {
        cout << "List kosong!" << endl;
    }
}

void delLast(LinkedList &List) {
    /* I.S. list tidak kosong
       F.S. node terakhir di list terhapus */
    address nodeHapus, nodePrev;
    if(isEmpty(List) == false) {
        nodeHapus = List.first;
        if(nodeHapus->next == Nil) {
            List.first->next = Nil;
            dealokasi(nodeHapus);
        } else {
            while(nodeHapus->next != Nil) {
                nodePrev = nodeHapus;
                nodeHapus = nodeHapus->next;
            }
            nodePrev->next = Nil;
            dealokasi(nodeHapus);
        }
    } else {
        cout << "List kosong" << endl;
    }
}

void delAfter(LinkedList &List, address nodeHapus, address nodePrev) {
    /* I.S. list tidak kosong, Prev alamat salah satu elemen list
       F.S. nodeBantu adalah alamat dari Prev->next, menghapus Prev->next dari list */
    if(isEmpty(List) == true) {
        cout << "List kosong!" << endl;
    } else { //jika list tidak kosong
        if (nodePrev != Nil && nodePrev->next != Nil) {
            nodeHapus = nodePrev->next;
            nodePrev->next = nodeHapus->next;
            nodeHapus->next = Nil;
            dealokasi(nodeHapus);
        } else {
            cout << "Node sebelumnya (prev) tidak valid!" << endl;
        }
    }
}

// prosedur untuk menampilkan isi list
void printList(LinkedList List) {
    /* I.S. list mungkin kosong
       F.S. jika list tidak kosong menampilkan semua info yang ada pada list */
    if (isEmpty(List)) {
        cout << "List kosong." << endl;
    } else {
        address nodeBantu = List.first;
        while (nodeBantu != Nil) {
            cout << "Nama : " << nodeBantu->isidata.nama << ", NIM : " << nodeBantu->isidata.nim << ", Usia : " << nodeBantu->isidata.umur << endl;
            nodeBantu = nodeBantu->next;
        }
    }
}

// Function untuk menampilkan jumlah node didalam list
int nbList(LinkedList List) {
    /* I.S. list sudah ada
       F.S. menampilkan jumlah node didalam list */
    int count = 0;
    address nodeBantu = List.first;
    while (nodeBantu != Nil) {
        count++;
        nodeBantu = nodeBantu->next;
    }
    return count;
}

// prosedur untuk menghapus list (menghapus semua node didalam list)
void deleteList(LinkedList &List) {
    /* I.S. list sudah ada
       F.S. menghapus semua node didalam list */
    address nodeBantu, nodeHapus;
    nodeBantu = List.first;
    while(nodeBantu != Nil) {
        nodeHapus = nodeBantu;
        nodeBantu = nodeBantu->next;
        dealokasi(nodeHapus);
    }
    List.first = Nil;
    cout << "List sudah terhapus!" << endl;
}
```
File list.cpp adalah bagian implementasi dari Abstract Data Type (ADT) Linked List. File ini berisi definisi semua prosedur dan fungsi yang telah dideklarasikan di file header list.h. Program ini menerapkan manajemen memori dinamis menggunakan operator new dan delete.




### 3. Program Main.cpp

```C++
#include "list.h"
#include <iostream>
using namespace std;

int main(){
    LinkedList List;
    address nodeA, nodeB, nodeC, nodeD, nodeE = Nil;
    createList(List);

    dataMahasiswa mhs;

    nodeA = alokasi("Dhimas", "2311102151", 20);
    nodeB = alokasi("Arvin", "221110014", 21);
    nodeC = alokasi("Rizal", "231110029", 20);
    nodeD = alokasi("Satro", "211102173", 21);
    nodeE = alokasi("Joshua", "2311102133", 21);

    insertFirst(List, nodeA);
    insertLast(List, nodeB);
    insertAfter(List, nodeC, nodeA);
    insertAfter(List, nodeD, nodeC);
    insertLast(List, nodeE);

    cout << "--- ISI LIST SETELAH DILAKUKAN INSERT ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

    delFirst(List);
    delLast(List);
    delAfter(List, nodeD, nodeC);

    cout << "--- ISI LIST SETELAH DILAKUKAN DELETE ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

    deleteList(List);
    cout << "--- ISI LIST SETELAH DILAKUKAN HAPUS LIST ---" << endl;
    printList(List);
    cout << "Jumlah node : " << nbList(List) << endl;
    cout << endl;

    return 0;
}
```
Program ini adalah implementasi struktur data Singly Linked List (Senarai Berantai Tunggal) menggunakan bahasa C++ untuk mengelola data mahasiswa. Program ini menerapkan konsep manajemen memori dinamis (alokasi dan dealokasi) serta Abstract Data Type (ADT) dengan memisahkan file header (list.h), implementasi (list.cpp), dan program utama (main.cpp).




## Unguided 

### 1. Buatlah ADT Singly Linked list sebagai berikut di dalam file “Singlylist.h” 
### Kemudian buatlah implementasi dari procedure-procedure yang digunakan didalam file “Singlylist.cpp” Kemudian buat program utama didalam file “main.cpp” dengan implementasi sebagai berikut : Sehingga linkedlist yang dibuat akan seperti ini : Output yang diharapkan : 9,12,8,0,2 
    

```C++
//singlylist.h
#ifndef SINGLYLIST_H
#define SINGLYLIST_H

#include <iostream>
using namespace std;

// Definisi Type infotype
typedef int infotype;

// Definisi pointer ke ElmList
typedef struct ElmList *address;

// Definisi Struct ElmList
struct ElmList {
    infotype info;
    address next;
};

// Definisi Struct List
struct List {
    address First;
};

// Deklarasi Prosedur dan Fungsi
void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

#endif
```
```C++
//singlylist.cpp
#include "Singlylist.h"

// Prosedur untuk membuat list kosong
void CreateList(List &L) {
    L.First = NULL;
}

// Fungsi untuk mengalokasikan memori untuk elemen baru
address alokasi(infotype x) {
    address P = new ElmList;
    if (P != NULL) {
        P->info = x;
        P->next = NULL;
    }
    return P;
}

// Prosedur untuk menghapus elemen dari memori
void dealokasi(address &P) {
    delete P;
    P = NULL;
}

// Prosedur untuk menampilkan isi list
void printInfo(List L) {
    address P = L.First;
    while (P != NULL) {
        cout << P->info;
        if (P->next != NULL) {
            cout << " ";
        }
        P = P->next;
    }
    cout << endl;
}

// Prosedur untuk menambahkan elemen di awal list
void insertFirst(List &L, address P) {
    if (P != NULL) {
        P->next = L.First;
        L.First = P;
    }
}
```
```C++
//main.cpp
#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5 = NULL;

    CreateList(L);

    P1 = alokasi(2);
    insertFirst(L, P1);

    P2 = alokasi(0);
    insertFirst(L, P2);

    P3 = alokasi(8);
    insertFirst(L, P3);

    P4 = alokasi(12);
    insertFirst(L, P4);

    P5 = alokasi(9);
    insertFirst(L, P5);

    printInfo(L);

    return 0;
}
```

### Output Unguided 1 :

##### Output 1
![Output 1](laprak4-1.jpg)

Pada soal pertama, program Singly Linked List dibuat menggunakan tiga file, yaitu `Singlylist.h`, `Singlylist.cpp`, dan `main.cpp`. File header berisi struktur data dan deklarasi fungsi, sedangkan file `.cpp` berisi implementasi fungsi yang digunakan. File `main.cpp` digunakan untuk menjalankan program. 

Struktur `ElmList` memiliki dua bagian, yaitu `info` untuk menyimpan nilai dan `next` untuk menunjuk ke node berikutnya. Sementara itu, struktur `List` memiliki `First` yang menunjuk ke node pertama. Beberapa fungsi yang digunakan adalah `CreateList()` untuk membuat list kosong, `alokasi()` untuk membuat node baru, `insertFirst()` untuk menambahkan node di awal, `printInfo()` untuk menampilkan isi list, dan `dealokasi()` untuk menghapus node dari memori. 

Pada program utama, angka 2, 0, 8, 12, dan 9 dimasukkan menggunakan fungsi `insertFirst()`. Karena setiap angka ditambahkan di bagian awal, urutan data menjadi terbalik dari urutan input. Hasil akhirnya adalah `9 12 8 0 2`, sesuai dengan output yang diharapkan.

### 2. Dari soal Latihan pertama, lakukan penghapusan node 9 menggunakan deleteFirst(), node 2 menggunakan deleteLast(), dan node 8 menggunakan deleteAfter(). Kemudian tampilkan jumlah node yang tersimpan menggunakan nbList() dan lakukan penghapusan seluruh node menggunakan deleteList(). Output yang diharapkan : 

```C++
//singlylist.h
#ifndef SINGLYLIST_H
#define SINGLYLIST_H

#include <iostream>
using namespace std;

// Definisi Type infotype
typedef int infotype;

// Definisi pointer ke ElmList
typedef struct ElmList *address;

// Definisi Struct ElmList
struct ElmList {
    infotype info;
    address next;
};

// Definisi Struct List
struct List {
    address First;
};

// --- Deklarasi Prosedur dan Fungsi ---

// Fungsi Dasar (Soal 1)
void CreateList(List &L);
address alokasi(infotype x);
void dealokasi(address &P);
void printInfo(List L);
void insertFirst(List &L, address P);

// Fungsi Tambahan (Soal 2)
void deleteFirst(List &L, address &P);
void deleteLast(List &L, address &P);
void deleteAfter(address Prec, address &P);
int nbList(List L);
void deleteList(List &L);

#endif
```

```C++
//singlylist.cpp
#include "Singlylist.h"

// --- Implementasi Fungsi Dasar ---

void CreateList(List &L) {
    L.First = NULL;
}

address alokasi(infotype x) {
    address P = new ElmList;
    if (P != NULL) {
        P->info = x;
        P->next = NULL;
    }
    return P;
}

void dealokasi(address &P) {
    delete P;
    P = NULL;
}

void printInfo(List L) {
    address P = L.First;
    while (P != NULL) {
        cout << P->info;
        if (P->next != NULL) {
            cout << " ";
        }
        P = P->next;
    }
    cout << endl;
}

void insertFirst(List &L, address P) {
    if (P != NULL) {
        P->next = L.First;
        L.First = P;
    }
}

// --- Implementasi Fungsi Tambahan (Soal 2) ---

// Menghapus elemen pertama
void deleteFirst(List &L, address &P) {
    if (L.First != NULL) {
        P = L.First;
        L.First = L.First->next;
        P->next = NULL;
    } else {
        P = NULL;
    }
}

// Menghapus elemen terakhir
void deleteLast(List &L, address &P) {
    if (L.First == NULL) {
        P = NULL;
    } else if (L.First->next == NULL) {
        P = L.First;
        L.First = NULL;
    } else {
        address Q = L.First;
        while (Q->next->next != NULL) {
            Q = Q->next;
        }
        P = Q->next;
        Q->next = NULL;
    }
}

// Menghapus elemen setelah node Prec
void deleteAfter(address Prec, address &P) {
    if (Prec != NULL && Prec->next != NULL) {
        P = Prec->next;
        Prec->next = P->next;
        P->next = NULL;
    } else {
        P = NULL;
    }
}

// Menghitung jumlah elemen (node)
int nbList(List L) {
    int count = 0;
    address P = L.First;
    while (P != NULL) {
        count++;
        P = P->next;
    }
    return count;
}

// Menghapus seluruh elemen di dalam list
void deleteList(List &L) {
    address P;
    while (L.First != NULL) {
        deleteFirst(L, P);
        dealokasi(P);
    }
}
```
```C++
//main.cpp
#include "Singlylist.h"

int main() {
    List L;
    address P1, P2, P3, P4, P5, P;
    address Prec;

    // 1. Inisialisasi List Kosong
    CreateList(L);

    // 2. Membuat List Awal: 9 -> 12 -> 8 -> 0 -> 2
    // (Menggunakan insertFirst, maka input dibalik urutannya)
    P1 = alokasi(2);
    insertFirst(L, P1);
    P2 = alokasi(0);
    insertFirst(L, P2);
    P3 = alokasi(8);
    insertFirst(L, P3);
    P4 = alokasi(12);
    insertFirst(L, P4);
    P5 = alokasi(9);
    insertFirst(L, P5);

    // --- PROSES SOAL 2 ---

    // a. Hapus node 9 (di awal) menggunakan deleteFirst()
    deleteFirst(L, P);
    dealokasi(P); // Hapus dari memori
    // List saat ini: 12 -> 8 -> 0 -> 2

    // b. Hapus node 2 (di akhir) menggunakan deleteLast()
    deleteLast(L, P);
    dealokasi(P); // Hapus dari memori
    // List saat ini: 12 -> 8 -> 0

    // c. Hapus node 8 menggunakan deleteAfter()
    // Node 8 berada setelah node 12. Kita perlu mencari posisi node 12.
    Prec = L.First; // Prec menunjuk ke node 12
    if (Prec != NULL && Prec->next != NULL) {
        deleteAfter(Prec, P); // Hapus node setelah 12 (yaitu 8)
        dealokasi(P); // Hapus dari memori
    }
    // List saat ini: 12 -> 0

    // d. Tampilkan list dan jumlah node
    printInfo(L);
    cout << "Jumlah node : " << nbList(L) << endl;

    // e. Hapus seluruh node menggunakan deleteList()
    deleteList(L);
    
    // Tampilkan output akhir
    cout << endl;
    cout << "- List Berhasil Terhapus -" << endl;
    cout << "Jumlah node : " << nbList(L) << endl;

    return 0;
}
```
### Output Unguided 2 :

##### Output 2
![Output 2](laprak4-2.jpg)

Pada soal kedua, program dikembangkan dengan menambahkan beberapa fungsi untuk menghapus node dan menghitung jumlah data dalam Singly Linked List. Fungsi tambahan yang digunakan adalah `deleteFirst()` untuk menghapus node pertama, `deleteLast()` untuk menghapus node terakhir, `deleteAfter()` untuk menghapus node setelah posisi tertentu, `nbList()` untuk menghitung jumlah node, dan `deleteList()` untuk menghapus seluruh node dalam list.

Awalnya, list berisi data `9 12 8 0 2`. Pertama, node 9 dihapus menggunakan `deleteFirst()`, sehingga list menjadi `12 8 0 2`. Selanjutnya, node 2 dihapus menggunakan `deleteLast()`, sehingga tersisa `12 8 0`. Setelah itu, node 8 dihapus menggunakan `deleteAfter()` dengan node 12 sebagai posisi sebelumnya. Hasilnya, list menjadi `12 0` dengan jumlah dua node. 

Terakhir, fungsi `nbList()` digunakan untuk menampilkan jumlah node yang masih tersimpan. Fungsi `deleteList()` kemudian dipanggil untuk menghapus seluruh node yang tersisa. Setelah proses selesai, jumlah node menjadi 0 karena list sudah kosong.



## Kesimpulan

Pada Modul 4 ini, saya mempelajari Singly Linked List sebagai salah satu struktur data yang menggunakan pointer untuk menghubungkan setiap node. Setiap node memiliki bagian `info` untuk menyimpan data dan `next` untuk menunjuk ke node berikutnya. Node terakhir menunjuk ke `NULL` karena tidak ada node lanjutan. Berbeda dengan array, jumlah node pada Linked List dapat ditambah atau dikurangi sesuai kebutuhan.

Pembuatan ADT Singly Linked List menggunakan tiga file, yaitu header (`.h`), implementasi (`.cpp`), dan program utama (`main.cpp`). File header digunakan untuk mendeklarasikan struktur data dan fungsi, file implementasi berisi kode dari fungsi tersebut, sedangkan `main.cpp` digunakan untuk menjalankan program. Dengan pembagian ini, kode menjadi lebih teratur dan mudah dipahami.

Pada bagian Guided, dipelajari beberapa operasi dasar Linked List, seperti `CreateList()` untuk membuat list kosong, `alokasi()` dan `dealokasi()` untuk mengatur penggunaan memori, serta operasi insert dan delete untuk menambah atau menghapus node. Selain itu, terdapat `printList()` untuk menampilkan data, `nbList()` untuk menghitung jumlah node, dan `deleteList()` untuk menghapus semua node.

Pada bagian Unguided, latihan pertama membuat Singly Linked List yang menyimpan lima angka, yaitu 2, 0, 8, 12, dan 9. Karena penambahan data menggunakan `insertFirst()`, urutan angka pada list menjadi `9 → 12 → 8 → 0 → 2`. Latihan kedua melanjutkan program tersebut dengan menghapus node 9 menggunakan `deleteFirst()`, node 2 menggunakan `deleteLast()`, dan node 8 menggunakan `deleteAfter()`. Setelah penghapusan selesai, data yang tersisa adalah `12 → 0` dengan jumlah dua node. Selanjutnya, `deleteList()` digunakan untuk menghapus semua node sehingga list kembali kosong.

Dari praktikum ini, saya memahami bahwa Singly Linked List dapat digunakan untuk mengelola data secara dinamis. Saya juga mempelajari penggunaan pointer, pengaturan memori dengan `new` dan `delete`, serta pemisahan program ke dalam beberapa file. Materi ini menjadi dasar untuk mempelajari struktur data lainnya, seperti Doubly Linked List dan Circular Linked List.

## Referensi
[1] Malik, D. S. (2010). Data Structures Using C++ (2nd ed.). Boston: Cengage Learning. 

[2] Drozdek, A. (2013). Data Structures and Algorithms in C++ (4th ed.). Boston: Cengage Learning. 
<br>...
