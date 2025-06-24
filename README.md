s box
#include <stdio.h>
#define SBOX_SIZE 16
int sbox[SBOX_SIZE]={0,14,4,13,1,2,15,11,8,3,10,6,12,5,9,7};
int inv_sbox[SBOX_SIZE];
void buildInverseSbox(){
    for(int i=1;i<SBOX_SIZE;i++){
        inv_sbox[sbox[i]]=i;
    }
}
void displaySbox(int box[],const char* name){
    printf("\n%s:\n",name);
    for(int i=1;i<SBOX_SIZE;i++){
        printf("%2d→%2d\n",i,box[i]);
    }
}
int main(){
    displaySbox(sbox,"S-Box");
    buildInverseSbox();
    displaySbox(inv_sbox,"Inverse S-Box");
    int input=9;
    int encrypted=sbox[input];
    int decrypted=inv_sbox[encrypted];
    printf("\nTest:\nInput:%d→Substituted:%d→Inverse:%d\n",input,encrypted,decrypted);
    return 0;
}

P box:
#include <stdio.h>
void applyPBox(int input[],int output[],int pbox[],int size){
    for(int i=0;i<size;i++)output[i]=input[pbox[i]-1];
}
void displayBits(const char *label,int bits[],int size){
    printf("%s: ",label);
    for(int i=0;i<size;i++)printf("%d",bits[i]);
    printf("\n");
}
int main(){
    int choice,inSize,outSize,input[16],output[16],pbox[16];
    printf("Choose:\n1.Straight\n2.Compression\n3.Expansion\nEnter choice: ");
    scanf("%d",&choice);

    if(choice==1||choice==2){
        inSize=8;
        printf("Enter %d-bit input: ",inSize);
        for(int i=0;i<inSize;i++)scanf("%d",&input[i]);
        outSize=(choice==1)?8:6;
    }else if(choice==3){
        inSize=4;outSize=6;
        printf("Enter %d-bit input: ",inSize);
        for(int i=0;i<inSize;i++)scanf("%d",&input[i]);
    }else{
        printf("Invalid choice");return 0;
    }

    printf("Enter %d P-box positions (1 to %d): ",outSize,inSize);
    for(int i=0;i<outSize;i++)scanf("%d",&pbox[i]);

    applyPBox(input,output,pbox,outSize);
    displayBits("Encrypted Output",output,outSize);
    return 0;
}
CRC-12:
#include <stdio.h>
#define POLY 0x180F
#define CRC_BITS 12
#define DATA_BITS 12

unsigned int computeCRC(unsigned int data, int totalBits) {
    for (int i = totalBits - 1; i >= CRC_BITS; i--) {
        if ((data >> i) & 1)
            data ^= (POLY << (i - CRC_BITS));
    }
    return data;
}

int main() {
    int choice;
    unsigned int data, codeword;
    while(1){
        printf("0. Exit\n1. Calculate CRC\n2. Verify Received Data\nChoice: ");
        scanf("%d", &choice);

        if (choice == 0) break;
        else if (choice == 1) {
            printf("Enter hex data (up to 0xFFF): ");
            scanf("%x", &data);
            unsigned int full = computeCRC(data << CRC_BITS, DATA_BITS + CRC_BITS);
            unsigned int crc = full & 0xFFF;
            codeword = (data << CRC_BITS) | crc;
            printf("CRC-12: %03X\n", crc);
            printf("Codeword: %06X\n", codeword);
        } else if (choice == 2) {
            printf("Enter received codeword: ");
            scanf("%x", &codeword);
            unsigned int result = computeCRC(codeword, DATA_BITS + CRC_BITS);
            if ((result & 0xFFF) == 0)
                printf("CRC Valid\n");
            else
                printf("CRC Error\n");
        } else {
            printf("Invalid choice\n");
        }
    }
    return 0;
}


CRC-16:
#include <stdio.h>
#define POLY 0x8005
#define CRC_BITS 16
#define DATA_BITS 16
unsigned int computeCRC(unsigned int data, int totalBits) {
    for (int i = totalBits - 1; i >= CRC_BITS; i--) {
        if ((data >> i) & 1)
            data ^= (POLY << (i - CRC_BITS));
    }
    return data;
}
int main() {
    int choice;
    unsigned int data, codeword;
    printf("1. Calculate CRC\n2. Verify Received Data\n");
    while(1){
        printf("Choice: ");
        scanf("%d", &choice);

        if (choice == 1) {
            printf("Enter hex data: ");
            scanf("%x", &data);
            unsigned int full = computeCRC(data << CRC_BITS, DATA_BITS + CRC_BITS);
            unsigned int crc = full & 0xFFFF;
            codeword = (data << CRC_BITS) | crc;
            printf("CRC-16: %04X\n", crc);
            printf("Codeword: %08X\n", codeword);
        } else if (choice == 2) {
            printf("Enter received codeword: ");
            scanf("%x", &codeword);
            unsigned int result = computeCRC(codeword, DATA_BITS + CRC_BITS);
            if ((result & 0xFFFF) == 0)
                printf("CRC Valid\n");
            else
                printf(" CRC Error\n");
        } else {
            printf("Invalid choice\n");
        }
    }
    return 0;
}
CRC-CCITT:
#include <stdio.h>
#define POLY 0x1021
#define CRC_BITS 16
#define DATA_BITS 16

unsigned int computeCRC(unsigned int data, int totalBits) {
    for (int i = totalBits - 1; i >= CRC_BITS; i--) {
        if ((data >> i) & 1)
            data ^= (POLY << (i - CRC_BITS));
    }
    return data;
}

int main() {
    int choice;
    unsigned int data, codeword;
    while(1){
        printf("0. Exit\n1. Calculate CRC\n2. Verify Received Data\nChoice: ");
        scanf("%d", &choice);

        if (choice == 0) break;
        else if (choice == 1) {
            printf("Enter hex data: ");
            scanf("%x", &data);
            unsigned int full = computeCRC(data << CRC_BITS, DATA_BITS + CRC_BITS);
            unsigned int crc = full & 0xFFFF;
            codeword = (data << CRC_BITS) | crc;
            printf("CRC-CCITT: %04X\n", crc);
            printf("Codeword: %08X\n", codeword);
        } else if (choice == 2) {
            printf("Enter received codeword: ");
            scanf("%x", &codeword);
            unsigned int result = computeCRC(codeword, DATA_BITS + CRC_BITS);
            if ((result & 0xFFFF) == 0)
                printf("CRC Valid\n");
            else
                printf("CRC Error\n");
        } else {
            printf("Invalid choice\n");
        }
    }
    return 0;
}

Recommended Primality Test#include <stdio.h>
#include <stdlib.h>
long long power(long long a, long long b, long long mod) {
    long long res = 1;
    a %= mod;
    while (b) {
        if (b & 1) res = (res * a) % mod;
        a = (a * a) % mod;
        b >>= 1;
    }
    return res;
}
int millerTest(long long d, long long n) {
    long long a = 2 + rand() % (n - 4);
    long long x = power(a, d, n);
    if (x == 1 || x == n - 1) return 1;
    while (d != n - 1) {
        x = (x * x) % n;
        d *= 2;
        if (x == 1) return 0;
        if (x == n - 1) return 1;
    }
    return 0;
}
int isPrime(long long n) {
    if (n < 2) return 0;
    int small[] = {2,3,5,7,11,13,17,19,23};
    for (int i = 0; i < 9; i++) {
        if (n == small[i]) return 1;
        if (n % small[i] == 0) return 0;
    }
    long long d = n - 1;
    while (d % 2 == 0) d /= 2;
    for (int i = 0; i < 5; i++)
        if (!millerTest(d, n)) return 0;
    return 1;
}
int main() {
    long long n;
    printf("Enter number: ");
    scanf("%lld", &n);
    if (isPrime(n))
        printf("probably Prime\n");
    else
        printf("composite\n");
    return 0;
}

rabin cryptosystem                                                                                                                    #include <stdio.h>
#include <stdlib.h>
#include <math.h>
int modInverse(int a, int m) {
    for (int x = 1; x < m; x++) {
        if ((a * x) % m == 1)
            return x;
    }
    return -1;
}
int modPow(int base, int exp, int mod) {
    int result = 1;
    base %= mod;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        base = (base * base) % mod;
        exp /= 2;
    }
    return result;
}
int main() {
    int p,q,n;
    printf("enter p,q values : ", p,q);
    scanf("%d%d", &p,&q);
    n = p * q;
    int message, ciphertext;
    printf("Public key (n = p * q): %d\n", n);
    printf("Enter message (M < %d): ", n);
    scanf("%d", &message);
    ciphertext = (message * message) % n;
    printf("Encrypted ciphertext (C = M^2 mod n): %d\n", ciphertext);
    int m1 = modPow(ciphertext, (p + 1) / 4, p);
    int m2 = modPow(ciphertext, (q + 1) / 4, q);
    int yp = modInverse(p, q);
    int yq = modInverse(q, p);
    int r = (yp * p * m2 + yq * q * m1) % n;
    int s = (yp * p * m2 - yq * q * m1) % n;
    if (r < 0) r += n;
    if (s < 0) s += n;
    printf("\nPossible decrypted messages:\n");
    printf("1. %d\n", r);
    printf("2. %d\n", n - r);
    printf("3. %d\n", s);
    printf("4. %d\n", n - s);
    return 0;
}


