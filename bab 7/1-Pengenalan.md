6.1 - Pengenalan Pointer
Apa Itu Pointer?
Pointer adalah variabel khusus yang menyimpan alamat memori dari variabel lain. Bayangkan pointer seperti alamat rumah - alamatnya bukan rumah itu sendiri, tapi menunjukkan lokasi rumah tersebut.

c
int angka = 10;      // Variabel biasa (isi: 10)
int *pointer_angka;  // Pointer ke integer (isi: alamat memori)
Mengapa Belajar Pointer?
Pointer memungkinkan kita mengubah nilai variabel dari luar scope function. Perhatikan masalah berikut:

c
#include <stdio.h>

void kurangi_health(int jumlah);

int main() {
    int health = 100;
    
    printf("Health awal: %d\n", health);  // Output: 100
    
    kurangi_health(20);  // Ingin mengurangi health sebesar 20
    
    printf("Health akhir: %d\n", health); // Masih 100! Tidak berubah!
    
    return 0;
}

void kurangi_health(int jumlah) {
    /* PROBLEM: Di sini tidak bisa mengakses variabel `health` 
       karena berada di scope yang berbeda */
    
    health = health - jumlah;  // ERROR! Variabel `health` tidak dikenal
}
Solusi: Dengan pointer, kita bisa mengatasi masalah ini!

Cara Mendeklarasikan Pointer
c
// Format: <tipe_data> *<nama_variabel>
int *pointer_int;        // Pointer ke integer
float *pointer_float;    // Pointer ke float
char *pointer_char;      // Pointer ke character
Contoh Deklarasi:
c
int *health_ptr;     // Style 1
int* ammo_ptr;       // Style 2 - sama saja
Deklarasi Multiple Pointer:
c
// BENAR: kedua variabel adalah pointer
int *health_ptr, *ammo_ptr;

// SALAH: hanya health_ptr yang pointer, ammo_ptr adalah integer biasa
int* health_ptr, ammo_ptr;
Cara Menggunakan Pointer
1. Inisialisasi Pointer
c
int health = 100;
int *health_ptr;

// Buat health_ptr menunjuk ke variabel health
health_ptr = &health;  // & = operator "address of"
2. Membaca Nilai dari Pointer (Dereferencing)
c
int health = 100;
int *health_ptr = &health;

printf("Health: %d\n", *health_ptr);  // Output: 100
// * = operator "value of" (ambil nilai dari alamat yang ditunjuk)

health = 50;  // Ubah nilai asli
printf("Health sekarang: %d\n", *health_ptr);  // Output: 50
3. Mengubah Nilai melalui Pointer
c
int health = 100;
int *health_ptr = &health;

printf("Health awal: %d\n", health);  // Output: 100

*health_ptr = 75;  // Ubah nilai melalui pointer

printf("Health akhir: %d\n", health);  // Output: 75
NULL Pointer
Pointer yang belum siap digunakan sebaiknya di-set ke NULL:

c
#include <stddef.h>  // Untuk definisi NULL

int main() {
    int health = 100;
    int *health_ptr = NULL;  // Pointer kosong
    
    int pilihan;
    printf("Masukkan 1 untuk bertarung, 0 untuk keluar: ");
    scanf("%d", &pilihan);
    
    if (pilihan == 1) {
        health_ptr = &health;  // Sekarang menunjuk ke health
        printf("Siap bertarung!\n");
    }
    
    if (health_ptr != NULL) {
        // Hanya dijalankan jika pointer tidak NULL
        *health_ptr = 85;
        printf("Health setelah bertarung: %d\n", health);
    } else {
        printf("Anda keluar dari permainan\n");
    }
    
    return 0;
}
Constant Pointer (Pointer Baca-Saja)
Membuat pointer yang hanya bisa membaca, tidak bisa mengubah nilai:

c
int health = 100;
const int *health_ptr = &health;  // Read-only pointer

// BISA: Membaca nilai
printf("Health: %d\n", *health_ptr);  // Output: 100

// TIDAK BISA: Mengubah nilai
*health_ptr = 50;  // ERROR! Compiler akan menolak

// Catatan: variabel asli masih bisa diubah
health = 50;  // Ini boleh
Ringkasan Operator Pointer
Operator	Contoh	Arti
*	*ptr	Ambil nilai dari alamat yang ditunjuk
&	&var	Ambil alamat memori dari variabel
Contoh Lengkap
c
#include <stdio.h>

int main() {
    int health = 100;
    int *health_ptr = &health;
    
    printf("Nilai health: %d\n", health);
    printf("Alamat health: %p\n", &health);
    printf("Isi health_ptr: %p\n", health_ptr);
    printf("Nilai melalui health_ptr: %d\n", *health_ptr);
    
    // Ubah nilai melalui pointer
    *health_ptr = 75;
    printf("Health setelah diubah: %d\n", health);
    
    return 0;
}
Output:

text
Nilai health: 100
Alamat health: 0x7ffd42a8b5ac
Isi health_ptr: 0x7ffd42a8b5ac
Nilai melalui health_ptr: 100
Health setelah diubah: 75
Tips Penting
Selalu inisialisasi pointer - set ke NULL jika belum digunakan

Hati-hati dengan dereferencing - pastikan pointer menunjuk ke alamat yang valid

Pahami perbedaan * dan & - * untuk nilai, & untuk alamat

Selanjutnya: Pass By Reference >>
