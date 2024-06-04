
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define DIZI_BOYUTU 500

// Fonksiyon prototipleri
void rastgeleDiziOlustur(int dizi[], int boyut);
void birEnBuyukBirEnKucukSiralama(int dizi[], int boyut);
void kucuktenBuyugeSiralama(int dizi[], int boyut);
void diziYazdir(int dizi[], int boyut);

int main() {
    int dizi[DIZI_BOYUTU];

    // Rastgele sayı üreteciyi başlat
    srand(time(NULL));

    // Rastgele bir dizi oluştur
    rastgeleDiziOlustur(dizi, DIZI_BOYUTU);

    // Orijinal diziyi yazdır
    printf("Orijinal Dizi:\n");
    diziYazdir(dizi, DIZI_BOYUTU);

    // Diziyi bir en büyük bir en küçük şekilde sırala
    birEnBuyukBirEnKucukSiralama(dizi, DIZI_BOYUTU);

    // Sıralanmış diziyi yazdır
    printf("Bir En Buyuk Bir En Kucuk Siralanmis Dizi:\n");
    diziYazdir(dizi, DIZI_BOYUTU);

    return 0;
}

// Rastgele bir dizi oluşturur
void rastgeleDiziOlustur(int dizi[], int boyut) {
    for (int i = 0; i < boyut; i++) {
        dizi[i] = rand() % 1001; // 0-1000 arasında rastgele bir sayı
    }
}

// Diziyi bir en büyük bir en küçük olacak şekilde sırala
void birEnBuyukBirEnKucukSiralama(int dizi[], int boyut) {
    // Diziyi küçükten büyüğe sırala
    kucuktenBuyugeSiralama(dizi, boyut);

    int* tempDizi = (int*)malloc(boyut * sizeof(int));
    if (tempDizi == NULL) {
        printf("Hafiza tahsisi basarisiz!\n");
        exit(1);
    }

    int kucukIndis = 0;
    int buyukIndis = boyut - 1;

    for (int i = 0; i < boyut; i++) {
        if (i % 2 == 0) {
            tempDizi[i] = dizi[buyukIndis--];
        }
        else {
            tempDizi[i] = dizi[kucukIndis++];
        }
    }

    for (int i = 0; i < boyut; i++) {
        dizi[i] = tempDizi[i];
    }

    free(tempDizi);
}

// Küçükten büyüğe sıralama (Seçmeli Sıralama algoritması kullanarak)
void kucuktenBuyugeSiralama(int dizi[], int boyut) {
    for (int i = 0; i < boyut - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < boyut; j++) {
            if (dizi[j] < dizi[minIndex]) {
                minIndex = j;
            }
        }
        int temp = dizi[minIndex];
        dizi[minIndex] = dizi[i];
        dizi[i] = temp;
    }
}

// Diziyi ekrana yazdırır
void diziYazdir(int dizi[], int boyut) {
    for (int i = 0; i < boyut; i++) {
        printf("%d ", dizi[i]);
    }
    printf("\n");
}
