[<< Linked List](1-LinkedList.md)

# 8.2 - Double Linked List

## Pengertian

Double Linked List adalah salah satu jenis linked list yang setiap node-nya memiliki dua referensi: satu menunjuk ke node sebelumnya **(prev)** dan satu lagi menunjuk ke node berikutnya **(next)**. Ini berbeda dengan Single Linked List yang hanya memiliki satu referensi yang menunjuk ke node berikutnya. Struktur node ganda ini memungkinkan traversal dua arah, yaitu dari awal ke akhir (forward) dan dari akhir ke awal (backward).

Struktur node pada double linked list terdiri dari tiga komponen utama:
1. Data: Komponen yang menyimpan nilai atau informasi yang disimpan dalam node.
2. Pointer ke Node Sebelumnya (prev): Referensi yang menunjuk ke node sebelumnya dalam linked list.
3. Pointer ke Node Berikutnya (next): Referensi yang menunjuk ke node berikutnya dalam linked list.

### Definisi

Definisi berisi data informasi tentang elemennya:

```c
struct node {
    int data;
    struct node *next;
    struct node *prev;
};

struct node *createNode (int data) {

    struct node *temp = malloc (sizeof (struct node));
    temp->prev = NULL;
    temp->data = data;
    temp->next = NULL;

    return temp;
}
```

### Iterasi Seluruh Node Linked List

Mencetak list secara urut
```c
void printList(struct node *head) {

    struct node *temp = head;

    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");

}
```

Mencetak list secara terbalik (dari belakang)
```c
void printListReversed(struct node *head) {

    struct node *tail = head;
    struct node *temp = tail;

    if (head == NULL) {
        return;
    }
    
    while (tail->next != NULL) {
        tail = tail->next;
    }
    
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->prev;
    }
    printf("\n");
}
```

<details>
<summary> Weapon Code 1 </summary>

```c
struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
};

/* Merepresentasikan tiap elemen dalam linked list dalam bentuk node */
struct WeaponNode {
    /* data elemen yang tersimpan dalam node */
    struct Weapon data;

    /* pointer menuju elemen/node sebelumnya dalam koleksi */
    /* beri nilai NULL apabila sudah tidak ada elemen lagi (dlm kata lain, elemen pertama) */
    struct WeaponNode *prev;

    /* pointer menuju elemen/node berikutnya dalam koleksi */
    /* beri nilai NULL apabila sudah tidak ada elemen lagi (dlm kata lain, elemen terakhir) */
    struct WeaponNode *next;
};

/* Representasi linked list yang menyatakan koleksi dari `struct Weapon` */
struct WeaponList {
    /* pointer menuju elemen pertama dalam linked list */
    /* beri nilai NULL apabila linked list masih kosongan */
    struct WeaponNode *first;

    /* pointer menuju elemen terakhir dalam linked list */
    /* beri nilai NULL apabila linked list masih kosongan */
    struct WeaponNode *last;
};
```

</details>

<details>
<summary> Clean Weapon Code 1 </summary>

```c
struct Weapon {
    char name[50];
    int price;
    int damage;
    int rounds;
};

struct WeaponNode {
    struct Weapon data;
    struct WeaponNode *prev;
    struct WeaponNode *next;
};

struct WeaponList {
    struct WeaponNode *first;
    struct WeaponNode *last;
};
```

</details>


<details>
<summary> Weapon Code 2 </summary>

```c
struct WeaponList weapons;

/* keadaan awal : linked list masih kosongan */
weapons.first = NULL;
weapons.last = NULL;
```

</details>

### Menambahkan Elemen

Menambahkan di Awal:
```c
struct node *addAtBeginning (struct node *head, int data) {
    struct node *temp = createNode (data);

    if (head != NULL) {
        temp->next = head;
        head->prev = temp;
    }
    
    return temp;
}
```

Menambahkan di Akhir:
```c
struct node *addAtEnd (struct node *head, int data) {

    struct node *temp = createNode (head, data);
    struct node *ptr = head;

    if (head != NULL) {
        
        while (ptr->next != NULL) {
            ptr = ptr->next;
        }

        temp->prev = ptr;
        ptr->next = temp;

    } else {
        return temp;
    }

    return head;
}
```

Menambahkan di Suatu Posisi:
```c
struct node *addAtPosition (struct node *head, int data, int position) {
    
    struct node *temp = createNode (data);
    struct node *ptr = head;
    
    if (position == 1) {
        return addAtBeginning (head, data);
    }
    
    if (ptr->next == NULL) {
        return addAtEnd (head, data); 
    }
    
    int pos = 1;
    while (pos != position - 1) {
        ptr = ptr->next;
        pos++;
    }
    temp->next = ptr->next;
    ptr->next = temp;

    if (temp->next != NULL) 
        temp->next->prev = temp;
    temp->prev = ptr;

    return head;
}
```

<details>
<summary> Weapon Code 3 </summary>

```c
/* akan menambah elemen setelah `after` */
/* `after` dapat diperoleh dari penjelajahan/iterasi seluruh node dalam linked list */
/* jika after bernilai `NULL`, maka tambahkan ke awal list */
void insertWeapon(struct WeaponList *list, struct WeaponNode *after, const struct Weapon *data) {
    if (after != NULL) {
        /* tambahkan node baru setelah `after` */

        struct WeaponNode *newNode, *oldNext;

        /* ciptakan elemen baru */
        newNode = (struct WeaponNode *)malloc(sizeof(struct WeaponNode));
        newNode->data = *data;
        newNode->prev = after; /* selaraskan rantai linked list */
        newNode->next = after->next; /* selaraskan rantai linked list */

        /* selaraskan rantai linked list */
        after->next = newNode;

        /* cek untuk kasus penambahan di akhir linked list */
        /* sesuai definisi, `next` bernilai NULL apabila merupakan elemen terakhir linked list */
        if (newNode->next == NULL) {
            /* selaraskan juga pointer elemen terakhir */
            list->last = newNode;
        } else {
            /* jika penambahan terjadi di tengah, selaraskan rantai linked listnya */
            newNode->next->prev = newNode;
        }
    } else {
        /* tambahkan node baru pada awal linked list */

        struct WeaponNode *newNode;

        /* ciptakan elemen baru */
        newNode = (struct WeaponNode *)malloc(sizeof(struct WeaponNode));
        newNode->data = *data;
        newNode->prev = NULL; /* sesuai definisi, beri NULL apabila merupakan elemen pertama */
        newNode->next = list->first; /* selaraskan rantai linked list */

        /* atur pointer elemen pertama ke node yang baru saja ditambahkan */
        list->first = newNode;

        /* cek untuk kasus transisi dari linked list yang tadinya kosong menjadi terisi 1 elemen */
        if (list->last == NULL) {
            /* atur pointer elemen terakhir ke node yang baru saja ditambahkan */
            list->last = newNode;
        } else {
            /* jika sebelumnya linked list masih terisi, selaraskan rantai linked list */
            newNode->next->prev = newNode;
        }
    }
}
```

</details>

<details>
<summary> Clean Weapon Code 3 </summary>

```c
void insertWeapon(struct WeaponList *list, struct WeaponNode *after, const struct Weapon *data) {
    if (after != NULL) {

        struct WeaponNode *newNode, *oldNext;

        newNode = (struct WeaponNode *)malloc(sizeof(struct WeaponNode));
        newNode->data = *data;
        newNode->prev = after; 
        newNode->next = after->next;

        after->next = newNode;

        if (newNode->next == NULL) {
            list->last = newNode;
        } else {
            newNode->next->prev = newNode;
        }
    } else {

        struct WeaponNode *newNode;

        newNode = (struct WeaponNode *)malloc(sizeof(struct WeaponNode));
        newNode->data = *data;
        newNode->prev = NULL;
        newNode->next = list->first; 

        list->first = newNode;

        if (list->last == NULL) {
            list->last = newNode;
        } else {
            newNode->next->prev = newNode;
        }
    }
}
```

</details>

### Menghapus Elemen

Menghapus di Awal:
```c
struct node *delAtBeginning (struct node *head) {
    
    struct node *ptr = head;
    
    if (head == NULL) {
        return NULL;
    }
    
    head = head->next;
    free(ptr);

    if (head != NULL)
        head->prev = NULL;

    return head;
}
```

Menghapus di Akhir:
```c
struct node *delAtEnd (struct node *head) {

    struct node *ptr = head;

    while (ptr->next->next != NULL) {
        ptr = ptr->next;
    }

    free (ptr->next);
    ptr->next = NULL;

    return head;
}
```

Menghapus di Suatu Posisi:
```c
struct node *delAtPosition (struct node *head, int position) {

    struct node *ptr = head;
    struct node *temp;

    if (position == 1) {
        head = delAtBeginning (head);
        return head;
    } else if (ptr->next == NULL) {
        head = delAtEnd (head);
    }

    int pos = 1;
    while (pos != position) {
        ptr = ptr->next;
        pos++;
    }
    
    temp = ptr->prev;
    temp->next = ptr->next;
    ptr->next->prev = temp;

    free(ptr);

    return head;
}
```

<details>
<summary> Weapon Code 4 </summary>

```c
/* akan menghapus elemen `node` pada linked list */
/* `node` dapat diperoleh dari penjelajahan/iterasi seluruh node dalam linked list */
void deleteWeapon(struct WeaponList *list, struct WeaponNode *node) {
    /* pastikan linked list tidak dalam keadaan kosong */
    if (list->first != NULL) {
        /* cek lokasi penghapusan terlebih dahulu */
        /* apakah berada di awal linked list, di akhir linked list, atau di tengah linked list */
        if (node == list->first) {
            /* kasus menghapus elemen di awal linked list */

            struct WeaponNode *oldNext;

            /* catat elemen setelah elemen pertama terlebih dahulu */
            oldNext = list->first->next;

            /* hapus elemen pertama dari memori */
            free(list->first);

            /* selaraskan pointer elemen pertama */
            list->first = oldNext;

            if (list->first == NULL) {
                /* jika keadaan akhir linked list menjadi kosong */
                /* selaraskan juga pointer elemen terakhir linked list */
                list->last = NULL;
            } else {
                /* jika keadaan akhir linked list masih terisi */
                /* selaraskan pointer elemen pertama */
                list->first->prev = NULL;
            }
        } else if (node == list->last) {
            /* kasus menghapus elemen di akhir linked list */

            struct WeaponNode *oldPrev;

            /* catat elemen sebelum elemen terakhir terlebih dahulu */
            oldPrev = list->last->prev;

            /* hapus elemen terakhir dari memori */
            free(list->last);

            /* selaraskan pointer elemen terakhir */
            list->last = oldPrev;

            if (list->last == NULL) {
                /* jika keadaan akhir linked list menjadi kosong */
                /* selaraskan juga pointer elemen pertama linked list */
                list->first = NULL;
            } else {
                /* jika keadaan akhir linked list masih terisi */
                /* selaraskan pointer elemen terakhir */
                list->last->next = NULL;
            }
        } else {
            /* kasus menghapus elemen di tengah linked list */

            struct WeaponNode *oldPrev, *oldNext;

            /* catat elemen sebelum dan sesudah `node` terlebih dahulu */
            oldPrev = node->prev;
            oldNext = node->next;

            /* hapus elemen `node` dari memori */
            free(node);

            /* selaraskan rantai linked list */
            oldPrev->next = oldNext;
            oldNext->prev = oldPrev;
        }
    }
}
```

</details>

<details>
<summary> Clean Weapon Code 4 </summary>

```c
void deleteWeapon(struct WeaponList *list, struct WeaponNode *node) {
    if (list->first != NULL) {
        if (node == list->first) {

            struct WeaponNode *oldNext;

            oldNext = list->first->next;

            free(list->first);

            list->first = oldNext;

            if (list->first == NULL) {
                list->last = NULL;
            } else {
                list->first->prev = NULL;
            }
        } else if (node == list->last) {

            struct WeaponNode *oldPrev;

            oldPrev = list->last->prev;

            free(list->last);

            list->last = oldPrev;

            if (list->last == NULL) {
                list->first = NULL;
            } else {
                list->last->next = NULL;
            }
        } else {

            struct WeaponNode *oldPrev, *oldNext;

            oldPrev = node->prev;
            oldNext = node->next;

            free(node);

            oldPrev->next = oldNext;
            oldNext->prev = oldPrev;
        }
    }
}
```

</details>

<details>
<summary> Weapon Code 5 </summary>

```c
struct WeaponList list;
struct WeaponNode *iterator;

/* ... */

for (iterator = list.first; iterator != NULL; iterator = iterator->next) {
    /* lakukan sesuatu dengan `iterator` */
    print_weapon(&iterator->data);
}
```

Atau menggunakan while loop (kasus penghapusan elemen tertentu):

```c
struct WeaponList list;
struct WeaponNode *iterator;

/* hapus semua senjata yang memiliki harga di atas 3000 */
iterator = list.first;
while (iterator != NULL) {
    struct WeaponList *next;

    next = iterator->next;
    if (iterator->data.price > 3000) {
        deleteWeapon(iterator);
    }
    iterator = next;
    /* `iterator = iterator->next` akan error apabila `iterator` sudah terhapus dengan `deleteWeapon` */
}
```

</details>

<details>
<summary> Full Weapon Code </summary>

### Contoh Penggunaan

```c
void printWeapons(struct WeaponList *list) {
    if (list->first != NULL) {
        struct WeaponNode *iterator;

        for (iterator = list->first; iterator != NULL; iterator = iterator->next) {
            printf("Weapon: %s ($: %d, %%: %d, n: %d)\n", iterator->data.name, iterator->data.price, iterator->data.damage, iterator->data.rounds);
        }
    } else {
        printf("(list is empty)\n");
    }
    printf("\n");
}

int main() {
    struct WeaponNode *iterator;
    struct WeaponList list;
    struct Weapon wpn;

    list.first = NULL;
    list.last = NULL;

    strcpy(wpn.name, "Desert Eagle");
    wpn.price = 750;
    wpn.damage = 35;
    wpn.rounds = 7;
    insertWeapon(&list, list.last, &wpn);

    strcpy(wpn.name, "M4A1");
    wpn.price = 3100;
    wpn.damage = 20;
    wpn.rounds = 30;
    insertWeapon(&list, list.last, &wpn);

    strcpy(wpn.name, "H&K MP5");
    wpn.price = 1500;
    wpn.damage = 15;
    wpn.rounds = 30;
    insertWeapon(&list, list.last, &wpn);

    strcpy(wpn.name, "AK-47");
    wpn.price = 2500;
    wpn.damage = 25;
    wpn.rounds = 30;
    insertWeapon(&list, list.last, &wpn);

    printWeapons(&list);

    printf("Menghapus elemen pertama...\n");
    deleteWeapon(&list, list.first);
    printWeapons(&list);

    printf("Menghapus elemen terakhir...\n");
    deleteWeapon(&list, list.last);
    printWeapons(&list);

    printf("Menambahkan AWP...\n");
    strcpy(wpn.name, "AWP Magnum");
    wpn.price = 4750;
    wpn.damage = 100;
    wpn.rounds = 10;
    insertWeapon(&list, list.last, &wpn);
    printWeapons(&list);

    printf("Menghapus senjata yang harganya lebih dari $3000...\n");
    iterator = list.first;
    while (iterator != NULL) {
        struct WeaponNode *next;

        next = iterator->next;
        if (iterator->data.price > 3000) {
            deleteWeapon(&list, iterator);
        }
        iterator = next;
    }
    printWeapons(&list);

    printf("Menghapus elemen pertama...\n");
    deleteWeapon(&list, list.first);
    printWeapons(&list);

    return 0;
}

/*
Output:

Weapon: Desert Eagle ($: 750, %: 35, n: 7)
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)
Weapon: AK-47 ($: 2500, %: 25, n: 30)

Menghapus elemen pertama...
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)
Weapon: AK-47 ($: 2500, %: 25, n: 30)

Menghapus elemen terakhir...
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)

Menambahkan AWP...
Weapon: M4A1 ($: 3100, %: 20, n: 30)
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)
Weapon: AWP Magnum ($: 4750, %: 100, n: 10)

Menghapus senjata yang harganya lebih dari $3000...
Weapon: H&K MP5 ($: 1500, %: 15, n: 30)

Menghapus elemen pertama...
(list is empty)

*/
```

</details>

## Kelebihan dan Kekurangan Masing-Masing

Array memiliki kelebihan yaitu dapat mengakses suatu elemen posisi tertentu dengan cepat dan mudah hanya berdasarkan indeks angka. Namun kekurangannya adalah proses penambahan/penghapusan elemen sulit dilakukan secara efektif. Cocok digunakan apabila ukuran koleksi tidak berubah-ubah dan dapat diidentifikasi dengan suatu indeks angka (dalam kata lain, pengaksesan suatu elemen berdasarkan indeks juga dipertimbangkan)

Kemudian linked list memiliki kelebihan yaitu proses penambahan/penghapusan elemen mudah dilakukan secara efektif. Namun kekurangannya adalah untuk mengakses suatu elemen/node tidak bisa langsung berdasarkan indeks namun harus melalui proses iterasi terlebih dahulu untuk menemukan elemen/node yang cocok. Cocok digunakan apabila ukuran koleksi berubah-ubah dan tidak perlu mengidentifikasi elemen berdasarkan indeks (dalam kata lain, hanya operasi iterasi seluruh elemen saja yang dipertimbangkan).

[Stack dan Queue >>](3-StackQueue.md)