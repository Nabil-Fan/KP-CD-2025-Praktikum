[<< Silabus](../silabus.md)

# 6.1 - Pengenalan Pointer

## Apa itu Pointer?

**Pointer** adalah **variabel spesial** yang isinya bukan nilai data langsung, melainkan **alamat memori** tempat data tersebut disimpan.  
Dengan kata lain, pointer digunakan untuk **menunjuk ke lokasi** sebuah variabel di memori komputer.

Misalnya, jika variabel `health` menyimpan nilai `100`, maka pointer bisa menyimpan **alamat memori** tempat nilai `100` itu berada.

---

## Kenapa Harus Belajar Pointer?

Pointer sangat penting karena memungkinkan kita **mengubah nilai suatu variabel dari luar fungsinya (scope berbeda)**.  
Biasanya, variabel di dalam fungsi hanya bisa digunakan di fungsi itu sendiri. Pointer membantu agar fungsi lain tetap bisa mengakses variabel tersebut.

Contoh:

```c
#include <stdio.h>

void kurangi_health(int jumlah);

int main() {
    int health = 100;

    printf("Health awal: %d\n", health);

    // Coba kurangi health lewat function
    kurangi_health(20);

    printf("Health akhir: %d\n", health);

    return 0;
}

void kurangi_health(int jumlah) {
    // ERROR! Variabel 'health' tidak dikenal di sini karena scopenya berbeda
    health = health - jumlah;
}
