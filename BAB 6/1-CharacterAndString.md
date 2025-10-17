## Fundamental String dan Character

Character merupakan penyusun sebuah kata atau kalimat (string) dengan nilai `int` yang direpresentasikan dengan tanda kutip tunggal `'...'`. Contoh: alphabet, special character, dan lain-lain.

String merupakan sekumpulan character yang dihimpun menjadi satu kesatuan. String direpresentasikan dengan tanda kutip ganda `"..."`. Setiap string harus diakhiri dengan null character `\0`.

## Deklarasi String

```C
char myStr1[] = {'P', 'r', 'a', 'k', 't', 'i', 'k', 'u', 'm', ' ', 'K', 'P', '\0'};
char myStr2[] = "Praktikum KP";
```

## Membaca String

```C
// mendeklarasikan char array
char charArray1[21];
char charArray2[101];

// membaca string dengan `scanf`
scanf("%20s", charArray1);

// membaca string dengan `fgets'
fgets(charArray2, sizeof(charArray2), stdin);
```

## Character Handling Library

Character Handling Library memungkinkan kita untuk memanipulasi atau memproses character lebih lanjut. Library ini menyediakan fungsi-fungsi yang memungkinkan kita untuk memeriksa apakah suatu character adalah digit, huruf, kosong, dan lain-lain. Untuk dapat menggunakan fungsi-fungsi tersebut kita harus menyertakan `<ctype.h>` di dalam program kita.

<table border="1">
  <tr>
    <th style="width:45%; text-align: center;">Prototype</th>
    <th style="width:55%; text-align: center;">Deskripsi Fungsi</th>
  </tr>
  <tr>
    <td><code>int isblank (int c)</code></td>
    <td>Mengembalikan nilai <code>true</code> jika <code>c</code> adalah karakter kosong</td>
  </tr>
  <tr>
    <td><code>int isdigit (int c)</code></td>
    <td>Mengembalikan nilai <code>true</code> jika <code>c</code> adalah karakter digit</td>
  </tr>
  <tr>
    <td><code>int isalpha (int c)</code></td>
    <td>Mengembalikan nilai <code>true</code> jika <code>c</code> adalah karakter huruf</td>
  </tr>
  <tr>
    <td><code>int isalnum (int c)</code></td>
    <td>Mengembalikan nilai <code>true</code> jika <code>c</code> adalah karakter digit atau huruf</td>
  </tr>
  <tr>
    <td><code>int isxdigit (int c)</code></td>
    <td>Mengembalikan nilai <code>true</code> jika <code>c</code> adalah karakter hexadecimal</td>
  </tr>
  <tr>
    <td><code>int islower (int c)</code></td>
    <td>Mengembalikan nilai <code>true</code> jika <code>c</code> adalah karakter lowercase</td>
  </tr>
  <tr>
    <td><code>int isupper (int c)</code></td>
    <td>Mengembalikan nilai <code>true</code> jika <code>c</code> adalah karakter uppercase</td>
  </tr>
  <tr>
    <td><code>int tolower(int c)</code></td>
    <td>Mengubah karakter lowercase menjadi uppercase</td>
  </tr>
  <tr>
    <td><code>int toupper (int c)</code></td>
    <td>Mengubah karakter uppercase menjadi lowercase</td>
  </tr>
</table>

## Standard Input/Output Library

Standard input/output library berisi fungsi-fungsi yang digunakan untuk menangani input/output dari standard input device (seperti keyboard) dan standard output device (seperti layar). Input/output yang dilakukan oleh program dapat berupa text, number, maupun karakter-karakter khusus. Untuk dapat menggunakan fungsi-fungsi tersebut kita harus menyertakan library `<stdio.h>`.

<table border="1">
  <tr>
    <th style="width:45%; text-align: center;">Function</th>
    <th style="width:55%; text-align: center;">Deskripsi</th>
  </tr>
  <tr>
    <td><code>int getchar(void);</code></td>
    <td>Mengambil karakter berikutnya dari input standar sebagai integer.</td>
  </tr>
  <tr>
    <td><code>char *fgets(char *s, int n, FILE *stream);</code></td>
    <td>Membaca karakter dari stream ke array <code>s</code> hingga newline atau akhir file, maksimal <code>n - 1</code> karakter.</td>
  </tr>
  <tr>
    <td><code>int putchar(int c);</code></td>
    <td>Mencetak karakter <code>c</code> dan mengembalikannya sebagai integer.</td>
  </tr>
  <tr>
    <td><code>int puts(const char *s);</code></td>
    <td>Mencetak string <code>s</code> dengan newline. Mengembalikan nilai non-nol jika berhasil.</td>
  </tr>
  <tr>
    <td><code>int sprintf(char *s, const char *format, ...);</code></td>
    <td>Menyimpan output ke array <code>s</code> seperti <code>printf</code>, lalu mengembalikan jumlah karakter yang ditulis.</td>
  </tr>
  <tr>
    <td><code>int sscanf(char *s, const char *format, ...);</code></td>
    <td>Membaca input dari array <code>s</code> seperti <code>scanf</code>, dan mengembalikan jumlah item yang terbaca.</td>
  </tr>
</table>

<details>
<summary>Source Code</summary>

```c
#include <stdio.h>

int main() {
    int c;
    printf("Ketik satu huruf: ");
    c = getchar();   // baca satu karakter
    printf("Karakter yang dibaca: %c\n", c);
    return 0;
}

#include <stdio.h>

int main() {
    char str[50];
    printf("Masukkan teks: ");
    fgets(str, sizeof(str), stdin);  // baca string
    printf("Teks yang dibaca: %s\n", str);
    return 0;
}

#include <stdio.h>

int main() {
    putchar('A');   // cetak satu huruf
    putchar('\n');  // cetak newline
    return 0;
}

#include <stdio.h>

int main() {
    puts("Halo, dunia!");  // langsung ada newline
    return 0;
}

#include <stdio.h>

int main() {
    char buffer[100];
    int umur = 20;
    sprintf(buffer, "Umur saya %d tahun", umur);
    puts(buffer);   // tampilkan hasil sprintf
    return 0;
}

#include <stdio.h>

int main() {
    char data[] = "123 45.67";
    int a;
    float b;
    sscanf(data, "%d %f", &a, &b);
    printf("Hasil parsing: a = %d, b = %.2f\n", a, b);
    return 0;
}
```
</details>

## String Handling Library

String Handling Library memungkinkan kita untuk memanipulasi string-string yang ada dalam program lebih lanjut. Library ini menyediakan fungsi-fungsi yang memungkinkan kita untuk mengcopy string, menggabungkan string, menghitung panjang string, membandingkan string, dan lain-lain. Sebelum menggunakan fungsi-fungsi tersebut kita harus menyertakan `<string.h>` terlebih dahulu di dalam program kita.

### 1. Fungsi Manipulasi dan Perbandingan

<table border="1">
  <tr>
    <th style="width:45%; text-align: center">Prototype</th>
    <th style="width:55%; text-align: center">Deskripsi Fungsi</th>
  </tr>
  <tr>
    <td><code>char *strcpy(char *s1, const char *s2)</code></td>
    <td>Menyalin string <code>s2</code> ke string <code>s1</code> dan mengembalikan string <code>s1</code></td>
  </tr>
  <tr>
    <td><code>char *strncpy(char *s1, const char *s2, size_t n)</code></td>
    <td>Menyalin string <code>s2</code> sebanyak <code>n</code> karakter ke string <code>s1</code> dan mengembalikan string <code>s1</code></td>
  </tr>
  <tr>
    <td><code>char *strcat(char *s1, const char *s2)</code></td>
    <td>Menggabungkan string <code>s2</code> ke string <code>s1</code> dan mengembalikan string <code>s1</code></td>
  </tr>
  <tr>
    <td><code>char *strncat(char *s1, const char *s2, size_t n)</code></td>
    <td>Menggabungkan string <code>s2</code> sebanyak <code>n</code> karakter ke string <code>s1</code> dan mengembalikan string <code>s1</code></td>
  </tr>
  <tr>
    <td><code>int strcmp(const char *s1, const char *s2)</code></td>
    <td>Membandingkan string <code>s1</code> dengan <code>s2</code>, mengembalikan nilai 0 jika string <code>s1</code> dan <code>s2</code> sama</td>
  </tr>
  <tr>
    <td><code>int strncmp(const char *s1, const char *s2, size_t n)</code></td>
    <td>Membandingkan <code>n</code> karakter string <code>s1</code> dengan <code>s2</code>, mengembalikan nilai 0 jika string <code>s1</code> dan <code>s2</code> sama</td>
  </tr>
</table>

### 2. Fungsi Pencarian

<table border="1">
  <tr>
    <th style="width:45%; text-align: center;">Prototipe Fungsi</th>
    <th style="width:55%; text-align: center;">Deskripsi</th>
  </tr>
  <tr>
    <td><code>char *strchr(const char *s, int c);</code></td>
    <td>Menemukan kemunculan pertama karakter <code>c</code> dalam string <code>s</code>. Jika ditemukan, <code>strchr</code> mengembalikan pointer ke <code>c</code> dalam string <code>s</code>. Jika tidak, mengembalikan <code>NULL</code>.</td>
  </tr>
  <tr>
    <td><code>size_t strcspn(const char *s1, const char *s2);</code></td>
    <td>Menentukan dan mengembalikan panjang segmen awal dari string <code>s1</code> yang hanya terdiri dari karakter-karakter yang tidak ada di <code>s2</code>.</td>
  </tr>
  <tr>
    <td><code>size_t strspn(const char *s1, const char *s2);</code></td>
    <td>Menentukan dan mengembalikan panjang segmen awal dari string <code>s1</code> yang hanya terdiri dari karakter-karakter yang terdapat di <code>s2</code>.</td>
  </tr>
  <tr>
    <td><code>char *strpbrk(const char *s1, const char *s2);</code></td>
    <td>Menemukan kemunculan pertama dalam string <code>s1</code> dari karakter apa pun yang ada di string <code>s2</code>. Jika karakter dari <code>s2</code> ditemukan, <code>strpbrk</code> mengembalikan pointer ke karakter tersebut dalam <code>s1</code>. Jika tidak, mengembalikan <code>NULL</code>.</td>
  </tr>
  <tr>
    <td><code>char *strrchr(const char *s, int c);</code></td>
    <td>Menemukan kemunculan terakhir dari karakter <code>c</code> dalam string <code>s</code>. Jika ditemukan, <code>strrchr</code> mengembalikan pointer ke <code>c</code> dalam string <code>s</code>. Jika tidak, mengembalikan <code>NULL</code>.</td>
  </tr>
  <tr>
    <td><code>char *strstr(const char *s1, const char *s2);</code></td>
    <td>Menemukan kemunculan pertama string <code>s2</code> dalam string <code>s1</code>. Jika string ditemukan, <code>strstr</code> mengembalikan pointer ke string di <code>s1</code>. Jika tidak, mengembalikan <code>NULL</code>.</td>
  </tr>
  <tr>
    <td><code>char *strtok(char *s1, const char *s2);</code></td>
    <td>Memecah string <code>s1</code> menjadi token yang dipisahkan oleh karakter yang terkandung dalam <code>s2</code>. <code>strtok</code> mengembalikan pointer ke token saat ini dalam setiap panggilan berurutan. Jika tidak ada token lagi, <code>strtok</code> mengembalikan <code>NULL</code>.</td>
  </tr>
</table>

<details>
<summary>Source Code</summary>

```c
#include <stdio.h>
int main() {

    // MANIP
    char a[20], b[] = "Halo";
    strcpy(a, b); // a = "Halo"

    char a[20];
    strncpy(a, "Praktikum", 5); // a = "Prakt"

    char a[20] = "Hello ";
    char b[] = "World";
    strcat(a, b); // a = "Hello World"

    char a[20] = "Data";
    strncat(a, "Structure", 4); // a = "DataStru"

    // PENCARIAN
    char str[] = "informatika";
    printf("%s", strchr(str, 'm')); // output: "matika"

    char s1[] = "abcdef";
    char s2[] = "xzce";
    printf("%zu", strcspn(s1, s2)); // output: 2 ("ab")

    char s1[] = "abcde321";
    char s2[] = "abcde";
    printf("%zu", strspn(s1, s2)); // output: 5

    char s1[] = "praktikum";
    char s2[] = "xyz";
    printf("%s", strpbrk(s1, s2)); // output: NULL (tidak ada huruf x, y, z)

    char str[] = "informatika";
    printf("%s", strrchr(str, 'a')); // output: "a"

    char str[] = "praktikum c";
    printf("%s", strstr(str, "tik")); // output: "tikum c"

    char str[] = "satu,dua,tiga";
    char *token = strtok(str, ",");
    while(token != NULL) {
        printf("%s\n", token);
        token = strtok(NULL, ",");
    }

    return 0;
    
}
```
</details>

[&gt;&gt; Silabus &gt;&gt;](/silabus.md)
