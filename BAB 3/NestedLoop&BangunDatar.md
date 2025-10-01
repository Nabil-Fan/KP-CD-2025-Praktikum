# 🔄 Nested Loop dalam Bahasa C - Penjelasan Lengkap dengan Implementasi

## 📚 **TEORI NESTED LOOP**

### 1. **Pengertian Nested Loop**
**Nested Loop** (Perulangan Bersarang) adalah struktur perulangan yang berada di dalam perulangan lainnya. 

**Analoginya:** 
Seperti jam yang memiliki jarum jam (outer loop) dan jarum menit (inner loop). Untuk setiap 1 langkah jarum jam, jarum menit harus menyelesaikan 60 langkah terlebih dahulu.

### 2. **Struktur Dasar**
```c
for (inisialisasi_outer; kondisi_outer; increment_outer) {    // Outer Loop
    for (inisialisasi_inner; kondisi_inner; increment_inner) { // Inner Loop
        // Statement yang diulang
    }
}
```

### 3. **Alur Eksekusi**
```c
#include <stdio.h>

int main() {
    printf("Demo Alur Nested Loop:\n");
    
    for (int i = 1; i <= 2; i++) {          // Outer Loop
        printf("🔹 Outer Loop ke-%d dimulai\n", i);
        
        for (int j = 1; j <= 3; j++) {      // Inner Loop
            printf("   🔸 Inner Loop ke-%d (dalam outer %d)\n", j, i);
        }
        
        printf("🔹 Outer Loop ke-%d selesai\n\n", i);
    }
    
    return 0;
}
```

**Output:**
```
Demo Alur Nested Loop:
🔹 Outer Loop ke-1 dimulai
   🔸 Inner Loop ke-1 (dalam outer 1)
   🔸 Inner Loop ke-2 (dalam outer 1)
   🔸 Inner Loop ke-3 (dalam outer 1)
🔹 Outer Loop ke-1 selesai

🔹 Outer Loop ke-2 dimulai
   🔸 Inner Loop ke-1 (dalam outer 2)
   🔸 Inner Loop ke-2 (dalam outer 2)
   🔸 Inner Loop ke-3 (dalam outer 2)
🔹 Outer Loop ke-2 selesai
```

### 4. **Rumus Total Iterasi**
```
Total Iterasi = Iterasi Outer Loop × Iterasi Inner Loop
```

## 🎯 **IMPLEMENTASI BANGUN DATAR**

### 1. **PERSEGI / KOTAK**

#### **Kode Program:**
```c
#include <stdio.h>

void buatPersegi(int sisi) {
    printf("\n🟦 MEMBUAT PERSEGI %dx%d 🟦\n", sisi, sisi);
    
    // Outer loop: mengontrol BARIS
    for (int baris = 1; baris <= sisi; baris++) {
        
        // Inner loop: mengontrol KOLOM  
        for (int kolom = 1; kolom <= sisi; kolom++) {
            printf("■ "); // Karakter untuk membentuk persegi
        }
        
        printf("\n"); // Pindah ke baris berikutnya
    }
    
    printf("Total karakter: %d x %d = %d\n", sisi, sisi, sisi * sisi);
}

int main() {
    buatPersegi(5);
    return 0;
}
```

#### **Output:**
```
🟦 MEMBUAT PERSEGI 5x5 🟦
■ ■ ■ ■ ■ 
■ ■ ■ ■ ■ 
■ ■ ■ ■ ■ 
■ ■ ■ ■ ■ 
■ ■ ■ ■ ■ 
Total karakter: 5 x 5 = 25
```

#### **Penjelasan Detil:**
- **Outer Loop (`baris`)**: Bertanggung jawab untuk membuat 5 baris
- **Inner Loop (`kolom`)**: Untuk setiap baris, membuat 5 kolom
- **Total Eksekusi**: 5 baris × 5 kolom = 25 kali printf("■ ")

---

### 2. **SEGITIGA SIKU-SIKU**

#### **Kode Program:**
```c
#include <stdio.h>

void buatSegitigaSiku(int tinggi) {
    printf("\n📐 MEMBUAT SEGITIGA SIKU-SIKU 📐\n");
    
    // Outer loop: mengontrol jumlah baris (tinggi segitiga)
    for (int baris = 1; baris <= tinggi; baris++) {
        
        // Inner loop: jumlah bintang = nomor baris saat ini
        for (int bintang = 1; bintang <= baris; bintang++) {
            printf("★ ");
        }
        
        printf("\n");
    }
    
    // Hitung total bintang (rumus segitiga: n(n+1)/2)
    int totalBintang = tinggi * (tinggi + 1) / 2;
    printf("Total bintang: %d\n", totalBintang);
}

int main() {
    buatSegitigaSiku(5);
    return 0;
}
```

#### **Output:**
```
📐 MEMBUAT SEGITIGA SIKU-SIKU 📐
★ 
★ ★ 
★ ★ ★ 
★ ★ ★ ★ 
★ ★ ★ ★ ★ 
Total bintang: 15
```

#### **Penjelasan Detil:**
- **Baris 1**: Inner loop jalan 1 kali → 1 bintang
- **Baris 2**: Inner loop jalan 2 kali → 2 bintang  
- **Baris 3**: Inner loop jalan 3 kali → 3 bintang
- **Pola**: Jumlah bintang = nomor baris
- **Total**: 1+2+3+4+5 = 15 bintang

---

### 3. **SEGITIGA SAMA KAKI**

#### **Kode Program:**
```c
#include <stdio.h>

void buatSegitigaSamaKaki(int tinggi) {
    printf("\n🔺 MEMBUAT SEGITIGA SAMA KAKI 🔺\n");
    
    // Outer loop: mengontrol baris
    for (int baris = 1; baris <= tinggi; baris++) {
        
        // INNER LOOP 1: Mencetak SPASI untuk perataan tengah
        for (int spasi = 1; spasi <= tinggi - baris; spasi++) {
            printf("  "); // 2 spasi untuk alignment yang baik
        }
        
        // INNER LOOP 2: Mencetak BINTANG 
        for (int bintang = 1; bintang <= (2 * baris - 1); bintang++) {
            printf("★ ");
        }
        
        printf("\n");
    }
    
    printf("Tinggi: %d, Lebar dasar: %d\n", tinggi, 2*tinggi-1);
}

int main() {
    buatSegitigaSamaKaki(5);
    return 0;
}
```

#### **Output:**
```
🔺 MEMBUAT SEGITIGA SAMA KAKI 🔺
        ★ 
      ★ ★ ★ 
    ★ ★ ★ ★ ★ 
  ★ ★ ★ ★ ★ ★ ★ 
★ ★ ★ ★ ★ ★ ★ ★ ★ 
Tinggi: 5, Lebar dasar: 9
```

#### **Penjelasan Detil:**
- **Dua Inner Loop** dalam satu outer loop
- **Inner Loop 1**: Mencetak spasi untuk pusatkan segitiga
  - Spasi berkurang seiring naiknya baris: `tinggi - baris`
- **Inner Loop 2**: Mencetak bintang dengan pola ganjil
  - Pola: 1, 3, 5, 7, 9 → `2 * baris - 1`

---

### 4. **BELAH KETUPAT (DIAMOND)**

#### **Kode Program:**
```c
#include <stdio.h>

void buatBelahKetupat(int setengahTinggi) {
    printf("\n💎 MEMBUAT BELAH KETUPAT 💎\n");
    
    // ========== BAGIAN ATAS ==========
    printf("--- Bagian Atas ---\n");
    for (int baris = 1; baris <= setengahTinggi; baris++) {
        
        // Spasi sebelum bintang
        for (int spasi = 1; spasi <= setengahTinggi - baris; spasi++) {
            printf("  ");
        }
        
        // Bintang
        for (int bintang = 1; bintang <= (2 * baris - 1); bintang++) {
            printf("★ ");
        }
        printf("\n");
    }
    
    // ========== BAGIAN BAWAH ==========
    printf("--- Bagian Bawah ---\n");
    for (int baris = setengahTinggi - 1; baris >= 1; baris--) {
        
        // Spasi sebelum bintang  
        for (int spasi = 1; spasi <= setengahTinggi - baris; spasi++) {
            printf("  ");
        }
        
        // Bintang
        for (int bintang = 1; bintang <= (2 * baris - 1); bintang++) {
            printf("★ ");
        }
        printf("\n");
    }
}

int main() {
    buatBelahKetupat(5);
    return 0;
}
```

#### **Output:**
```
💎 MEMBUAT BELAH KETUPAT 💎
--- Bagian Atas ---
        ★ 
      ★ ★ ★ 
    ★ ★ ★ ★ ★ 
  ★ ★ ★ ★ ★ ★ ★ 
★ ★ ★ ★ ★ ★ ★ ★ ★ 
--- Bagian Bawah ---
  ★ ★ ★ ★ ★ ★ ★ 
    ★ ★ ★ ★ ★ 
      ★ ★ ★ 
        ★ 
```

#### **Penjelasan Detil:**
- **Dua Tahap**: Segitiga atas + Segitiga bawah terbalik
- **Bagian Atas**: Sama seperti segitiga sama kaki
- **Bagian Bawah**: Outer loop decrement (`baris--`)
- **Simetri**: Membentuk diamond sempurna

---

### 5. **PERSEGI BERONGGA (HOLLOW SQUARE)**

#### **Kode Program:**
```c
#include <stdio.h>

void buatPersegiBerongga(int panjang, int lebar) {
    printf("\n🟨 MEMBUAT PERSEGI BERONGGA %dx%d 🟨\n", panjang, lebar);
    
    for (int baris = 1; baris <= lebar; baris++) {
        for (int kolom = 1; kolom <= panjang; kolom++) {
            
            // Cek apakah di border (pinggiran)
            if (baris == 1 || baris == lebar || kolom == 1 || kolom == panjang) {
                printf("■ "); // Border
            } else {
                printf("  "); // Bagian dalam (kosong)
            }
        }
        printf("\n");
    }
    
    printf("Border luar dengan bagian dalam kosong\n");
}

int main() {
    buatPersegiBerongga(8, 5);
    return 0;
}
```

#### **Output:**
```
🟨 MEMBUAT PERSEGI BERONGGA 8x5 🟨
■ ■ ■ ■ ■ ■ ■ ■ 
■             ■ 
■             ■ 
■             ■ 
■ ■ ■ ■ ■ ■ ■ ■ 
Border luar dengan bagian dalam kosong
```

#### **Penjelasan Detil:**
- **Konsep IF dalam Nested Loop**: Mengecek posisi setiap karakter
- **Border Conditions**:
  - `baris == 1` → Baris paling atas
  - `baris == lebar` → Baris paling bawah  
  - `kolom == 1` → Kolom paling kiri
  - `kolom == panjang` → Kolom paling kanan
- **Efisiensi**: Hanya border yang dicetak, dalamnya kosong

---

## 🎮 **PROGRAM UTAMA LENGKAP DENGAN MENU**

```c
#include <stdio.h>

// Deklarasi semua fungsi
void buatPersegi(int sisi);
void buatSegitigaSiku(int tinggi);
void buatSegitigaSamaKaki(int tinggi);
void buatBelahKetupat(int setengahTinggi);
void buatPersegiBerongga(int panjang, int lebar);
void tampilkanMenu();

int main() {
    int pilihan, ukuran1, ukuran2;
    
    printf("===========================================\n");
    printf("       PROGRAM BANGUN DATAR C\n");
    printf("     dengan NESTED LOOP Implementation\n");
    printf("===========================================\n");
    
    do {
        tampilkanMenu();
        printf("Pilih bentuk (1-6): ");
        scanf("%d", &pilihan);
        
        switch(pilihan) {
            case 1:
                printf("Masukkan sisi persegi: ");
                scanf("%d", &ukuran1);
                buatPersegi(ukuran1);
                break;
                
            case 2:
                printf("Masukkan tinggi segitiga siku: ");
                scanf("%d", &ukuran1);
                buatSegitigaSiku(ukuran1);
                break;
                
            case 3:
                printf("Masukkan tinggi segitiga sama kaki: ");
                scanf("%d", &ukuran1);
                buatSegitigaSamaKaki(ukuran1);
                break;
                
            case 4:
                printf("Masukkan setengah tinggi belah ketupat: ");
                scanf("%d", &ukuran1);
                buatBelahKetupat(ukuran1);
                break;
                
            case 5:
                printf("Masukkan panjang: ");
                scanf("%d", &ukuran1);
                printf("Masukkan lebar: ");
                scanf("%d", &ukuran2);
                buatPersegiBerongga(ukuran1, ukuran2);
                break;
                
            case 6:
                printf("Terima kasih! Program selesai.\n");
                break;
                
            default:
                printf("Pilihan tidak valid! Coba lagi.\n");
        }
        
        if (pilihan != 6) {
            printf("\nTekan Enter untuk melanjutkan...");
            getchar(); getchar(); // Tunggu input user
        }
        
    } while (pilihan != 6);
    
    return 0;
}

void tampilkanMenu() {
    printf("\n");
    printf("===========================================\n");
    printf("                MENU UTAMA\n");
    printf("===========================================\n");
    printf("1. Persegi\n");
    printf("2. Segitiga Siku-Siku\n");
    printf("3. Segitiga Sama Kaki\n");
    printf("4. Belah Ketupat\n");
    printf("5. Persegi Berongga\n");
    printf("6. Keluar\n");
    printf("===========================================\n");
}

// Implementasi fungsi-fungsi (sama seperti di atas)
void buatPersegi(int sisi) {
    printf("\n🟦 MEMBUAT PERSEGI %dx%d 🟦\n", sisi, sisi);
    for (int baris = 1; baris <= sisi; baris++) {
        for (int kolom = 1; kolom <= sisi; kolom++) {
            printf("■ ");
        }
        printf("\n");
    }
}

void buatSegitigaSiku(int tinggi) {
    printf("\n📐 MEMBUAT SEGITIGA SIKU-SIKU 📐\n");
    for (int baris = 1; baris <= tinggi; baris++) {
        for (int bintang = 1; bintang <= baris; bintang++) {
            printf("★ ");
        }
        printf("\n");
    }
}

void buatSegitigaSamaKaki(int tinggi) {
    printf("\n🔺 MEMBUAT SEGITIGA SAMA KAKI 🔺\n");
    for (int baris = 1; baris <= tinggi; baris++) {
        for (int spasi = 1; spasi <= tinggi - baris; spasi++) {
            printf("  ");
        }
        for (int bintang = 1; bintang <= (2 * baris - 1); bintang++) {
            printf("★ ");
        }
        printf("\n");
    }
}

void buatBelahKetupat(int setengahTinggi) {
    printf("\n💎 MEMBUAT BELAH KETUPAT 💎\n");
    for (int baris = 1; baris <= setengahTinggi; baris++) {
        for (int spasi = 1; spasi <= setengahTinggi - baris; spasi++) {
            printf("  ");
        }
        for (int bintang = 1; bintang <= (2 * baris - 1); bintang++) {
            printf("★ ");
        }
        printf("\n");
    }
    for (int baris = setengahTinggi - 1; baris >= 1; baris--) {
        for (int spasi = 1; spasi <= setengahTinggi - baris; spasi++) {
            printf("  ");
        }
        for (int bintang = 1; bintang <= (2 * baris - 1); bintang++) {
            printf("★ ");
        }
        printf("\n");
    }
}

void buatPersegiBerongga(int panjang, int lebar) {
    printf("\n🟨 MEMBUAT PERSEGI BERONGGA %dx%d 🟨\n", panjang, lebar);
    for (int baris = 1; baris <= lebar; baris++) {
        for (int kolom = 1; kolom <= panjang; kolom++) {
            if (baris == 1 || baris == lebar || kolom == 1 || kolom == panjang) {
                printf("■ ");
            } else {
                printf("  ");
            }
        }
        printf("\n");
    }
}
```

## 📊 **KESIMPULAN DAN APLIKASI**

### **Keunggulan Nested Loop:**
1. ✅ **Powerful** untuk pola dan struktur berulang
2. ✅ **Efisien** untuk array multidimensi
3. ✅ **Fleksibel** bisa dikombinasi dengan conditional statement
4. ✅ **Dasar** untuk algoritma kompleks

### **Aplikasi Real World:**
- 🎮 Game development (peta, grid)
- 📊 Data processing (matriks, tabel)
- 🎨 Graphic design (pola, pattern)
- 🔢 Scientific computing (perhitungan multidimensi)

### **Tips Pengembangan:**
```c
// Selalu gunakan nama variabel yang deskriptif
for (int baris = 0; baris < tinggi; baris++) {
    for (int kolom = 0; kolom < lebar; kolom++) {
        // Kode yang jelas
    }
}

// Bukan:
for (int i = 0; i < x; i++) {
    for (int j = 0; j < y; j++) {
        // Kode yang membingungkan
    }
}
```

Dengan memahami nested loop, Anda membuka pintu untuk pemrograman yang lebih kompleks dan struktural! 🚀
