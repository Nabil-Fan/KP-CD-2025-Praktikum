# Nested Loop dalam Bahasa C - Penjelasan Lengkap dengan Implementasi

## **Konsep Dasar Nested Loop**

### 1. **Pengertian Nested Loop**
**Nested Loop** (Perulangan Bersarang) adalah struktur loop yang berada di dalam loop lainnya. Loop di dalam disebut inner loop, sedangkan loop di luar disebut outer loop. 

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
    printf("Contoh Nested Loop Sederhana:\n");
    
    for (int i = 1; i <= 3; i++) {          // Outer Loop
        printf("Outer Loop i = %d\n", i);
        
        for (int j = 1; j <= 2; j++) {      // Inner Loop
            printf("  Inner Loop j = %d\n", j);
        }
    }
    
    return 0;
}
```

**Output:**
```
Contoh Nested Loop Sederhana:
Outer Loop i = 1
  Inner Loop j = 1
  Inner Loop j = 2
Outer Loop i = 2
  Inner Loop j = 1
  Inner Loop j = 2
Outer Loop i = 3
  Inner Loop j = 1
  Inner Loop j = 2
```
