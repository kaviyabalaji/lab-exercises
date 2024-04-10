coding # lab-exercises
# Name:B.Kaviya
# Register Number:212221040079
## Caesar Cipher
~~~
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char plain[10], cipher[10];
    int key, i, length;
    
    printf("Enter the plain text: ");
    scanf("%s", plain);
    printf("Enter the key value: ");
    scanf("%d", &key);

    printf("\nPLAIN TEXT: %s\n", plain);

    length = strlen(plain);

    printf("\nENCRYPTED TEXT: ");
    for (i = 0; i < length; i++) {
        cipher[i] = plain[i] + key;
        if (isupper(plain[i]) && (cipher[i] > 'Z'))
            cipher[i] -= 26;
        if (islower(plain[i]) && (cipher[i] > 'z'))
            cipher[i] -= 26;
        printf("%c", cipher[i]);
    }

    printf("\n\nAFTER DECRYPTION: ");
    for (i = 0; i < length; i++) {
        plain[i] = cipher[i] - key;
        if (isupper(cipher[i]) && (plain[i] < 'A'))
            plain[i] += 26;
        if (islower(cipher[i]) && (plain[i] < 'a'))
            plain[i] += 26;
        printf("%c", plain[i]);
    }

    printf("\n");

    return 0;
}
~~~
## Output

![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/d3a484ef-1f99-4b40-a308-c07d90e9c784)
## Hill Cipher
~~~
#include<stdio.h>
#include<string.h>

int main() {
    unsigned int a[3][3] = {{6, 24, 1}, {13, 16, 10}, {20, 17, 15}};
    unsigned int b[3][3] = {{8, 5, 10}, {21, 8, 21}, {21, 12, 8}};
    int i, j, t = 0;
    unsigned int c[20], d[20];
    char msg[20];

    printf("Enter plain text: ");
    scanf("%s", msg);

    for(i = 0; i < strlen(msg); i++) { 
        c[i] = msg[i] - 65;
        printf("%d ", c[i]);
    }

    for(i = 0; i < 3; i++) { 
        t = 0;
        for(j = 0; j < 3; j++) {
            t += (a[i][j] * c[j]);
        }
        d[i] = t % 26;
    }

    printf("\nEncrypted Cipher Text:");
    for(i = 0; i < 3; i++)
        printf(" %c", d[i] + 65);

    for(i = 0; i < 3; i++) {
        t = 0;
        for(j = 0; j < 3; j++) {
            t += (b[i][j] * d[j]);
        }
        c[i] = t % 26;
    }

    printf("\nDecrypted Cipher Text:");
    for(i = 0; i < 3; i++)
        printf(" %c", c[i] + 65);

    printf("\n");
    return 0;
}
~~~
## Output
![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/db3efa16-73e1-4cff-85e2-da411a202eb5)
## Vigenere Cipher
~~~
#include <stdio.h>
#include <ctype.h>
#include <string.h>

void encipher();
void decipher();

int main() {
    int choice;

    while (1) {
        printf("\n1. Encrypt Text");
        printf("\t2. Decrypt Text");
        printf("\t3. Exit");
        printf("\n\nEnter Your Choice: ");
        scanf("%d", &choice);

        if (choice == 3)
            break;
        else if (choice == 1)
            encipher();
        else if (choice == 2)
            decipher();
        else
            printf("Please Enter a Valid Option.");
    }

    return 0;
}

void encipher() {
    unsigned int i, j;
    char input[50], key[10];
    printf("\n\nEnter Plain Text: ");
    scanf("%s", input);
    printf("Enter Key Value: ");
    scanf("%s", key);
    printf("Resultant Cipher Text: ");

    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }
        printf("%c", 'A' + (((toupper(input[i]) - 'A') + (toupper(key[j]) - 'A')) % 26));
    }

    printf("\n");
}

void decipher() {
    unsigned int i, j;
    char input[50], key[10];
    int value;

    printf("\n\nEnter Cipher Text: ");
    scanf("%s", input);
    printf("Enter the Key Value: ");
    scanf("%s", key);

    for (i = 0, j = 0; i < strlen(input); i++, j++) {
        if (j >= strlen(key)) {
            j = 0;
        }
        value = (toupper(input[i]) - 'A') - (toupper(key[j]) - 'A');
        if (value < 0) {
            value += 26;
        }
        printf("%c", 'A' + (value % 26));
    }

    printf("\n");
}
~~~
## Output
![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/ebe9c58f-2d02-4f3b-8084-550c671a2866)
## Rail Fence
```
#include <stdio.h>
#include <string.h>

int main() {
    int i, j, k, l;
    char a[20], c[20], d[20];
    
    printf("\n\t\t RAIL FENCE TECHNIQUE");
    printf("\n\nEnter the input string : ");
    fgets(a, sizeof(a), stdin);
    a[strcspn(a, "\n")] = '\0'; // Remove newline character
    l = strlen(a);
    
    /* Ciphering */
    for (i = 0, j = 0; i < l; i += 2) {
        c[j++] = a[i];
    }
    for (i = 1; i < l; i += 2) {
        c[j++] = a[i];
    }
    c[j] = '\0';
    
    printf("\nCipher text after applying rail fence :");
    printf("\n%s", c);
    
    /* Deciphering */
    if (l % 2 == 0)
        k = l / 2;
    else
        k = (l / 2) + 1;
    
    for (i = 0, j = 0; i < k; i++) {
        d[j] = c[i];
        j += 2;
    }
    for (i = k, j = 1; i < l; i++) {
        d[j] = c[i];
        j += 2;
    }
    d[l] = '\0';
    
    printf("\nText after decryption : ");
    printf("%s", d);
    
    return 0;
}
```
## Output
![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/2feef613-9624-4169-8689-12764c2617c4)
## RSA
~~~
#include<stdio.h>
#include<stdlib.h>
#include<math.h>
#include<string.h>

long int p, q, n, t, flag, e[100], d[100], temp[100], j, m[100], en[100], i;
char msg[100];

int prime(long int);
void ce();
long int cd(long int);
void encrypt();
void decrypt();

void main() {
    printf("\nENTER FIRST PRIME NUMBER\n");
    scanf("%ld", &p);
    flag = prime(p);
    if(flag == 0) {
        printf("\nWRONG INPUT\n");
        exit(0);
    }
    printf("\nENTER ANOTHER PRIME NUMBER\n");
    scanf("%ld", &q);
    flag = prime(q);
    if(flag == 0 || p == q) {
        printf("\nWRONG INPUT\n");
        exit(0);
    }
    printf("\nENTER MESSAGE\n");
    fflush(stdin);
    scanf("%s", msg);
    for(i = 0; msg[i] != '\0'; i++)
        m[i] = msg[i];
    n = p * q;
    t = (p - 1) * (q - 1);
    ce();
    printf("\nPOSSIBLE VALUES OF e AND d ARE\n");
    for(i = 0; i < j - 1; i++)
        printf("\n%ld\t%ld", e[i], d[i]);
    encrypt();
    decrypt();
}

int prime(long int pr) {
    int i;
    j = sqrt(pr);
    for(i = 2; i <= j; i++) {
        if(pr % i == 0)
            return 0;
    }
    return 1;
}

void ce() {
    int k;
    k = 0;
    for(i = 2; i < t; i++) {
        if(t % i == 0)
            continue;
        flag = prime(i);
        if(flag == 1 && i != p && i != q) {
            e[k] = i;
            flag = cd(e[k]);
            if(flag > 0) {
                d[k] = flag;
                k++;
            }
            if(k == 99)
                break;
        }
    }
}

long int cd(long int x) {
    long int k = 1;
    while(1) {
        k = k + t;
        if(k % x == 0)
            return(k / x);
    }
}

void encrypt() {
    long int pt, ct, key = e[0], k, len;
    i = 0;
    len = strlen(msg);
    while(i != len) {
        pt = m[i];
        pt = pt - 96;
        k = 1;
        for(j = 0; j < key; j++) {
            k = k * pt;
            k = k % n;
        }
        temp[i] = k;
        ct = k + 96;
        en[i] = ct;
        i++;
    }
    en[i] = -1;
    printf("\nTHE ENCRYPTED MESSAGE IS\n");
    for(i = 0; en[i] != -1; i++)
        printf("%c", en[i]);
}

void decrypt() {
    long int pt, ct, key = d[0], k;
    i = 0;
    while(en[i] != -1) {
        ct = temp[i];
        k = 1;
        for(j = 0; j < key; j++) {
            k = k * ct;
            k = k % n;
        }
        pt = k + 96;
        m[i] = pt;
        i++;
    }
    m[i] = -1;
    printf("\nTHE DECRYPTED MESSAGE IS\n");
    for(i = 0; m[i] != -1; i++)
        printf("%c", m[i]);
}
~~~
## Output
![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/d2e009c1-0d2e-464a-9482-b90a85cfb881)
## MD5
~~~
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>

typedef union {
    unsigned w;
    unsigned char b[4];
} MD5union;

typedef unsigned DigestArray[4];

unsigned func0(unsigned abcd[]) {
    return (abcd[1] & abcd[2]) | (~abcd[1] & abcd[3]);
}

unsigned func1(unsigned abcd[]) {
    return (abcd[3] & abcd[1]) | (~abcd[3] & abcd[2]);
}

unsigned func2(unsigned abcd[]) {
    return abcd[1] ^ abcd[2] ^ abcd[3];
}

unsigned func3(unsigned abcd[]) {
    return abcd[2] ^ (abcd[1] | ~abcd[3]);
}

typedef unsigned (*DgstFctn)(unsigned a[]);

unsigned *calctable(unsigned *k) {
    double s, pwr;
    int i;
    pwr = pow(2, 32);
    for (i = 0; i < 64; i++) {
        s = fabs(sin(1 + i));
        k[i] = (unsigned)(s * pwr);
    }
    return k;
}

unsigned rol(unsigned r, short N) {
    unsigned mask1 = (1 << N) - 1;
    return ((r >> (32 - N)) & mask1) | ((r << N) & ~mask1);
}

unsigned *md5(const char *msg, int mlen) {
    static DigestArray h0 = {0x67452301, 0xEFCDAB89, 0x98BADCFE, 0x10325476};
    static DgstFctn ff[] = {&func0, &func1, &func2, &func3};
    static short M[] = {1, 5, 3, 7};
    static short O[] = {0, 1, 5, 0};
    static short rot0[] = {7, 12, 17, 22};
    static short rot1[] = {5, 9, 14, 20};
    static short rot2[] = {4, 11, 16, 23};
    static short rot3[] = {6, 10, 15, 21};
    static short *rots[] = {rot0, rot1, rot2, rot3};
    static unsigned kspace[64];
    static unsigned *k = NULL;
    static DigestArray h;
    DigestArray abcd;
    DgstFctn fctn;
    short m, o, g;
    unsigned f;
    short *rotn;
    union {
        unsigned w[16];
        char b[64];
    } mm;

    int os = 0;
    int grp, grps, q, p;
    unsigned char *msg2;
    if (k == NULL) k = calctable(kspace);

    for (q = 0; q < 4; q++) h[q] = h0[q]; // initialize
    grps = 1 + (mlen + 8) / 64;
    msg2 = malloc(64 * grps);
    memcpy(msg2, msg, mlen);
    msg2[mlen] = (unsigned char)0x80;
    q = mlen + 1;
    while (q < 64 * grps) {
        msg2[q] = 0;
        q++;
    }
    {
        MD5union u;
        u.w = 8 * mlen;
        q -= 8;
        memcpy(msg2 + q, &u.w, 4);
    }

    for (grp = 0; grp < grps; grp++) {
        memcpy(mm.b, msg2 + os, 64);

        for (q = 0; q < 4; q++) abcd[q] = h[q];
        for (p = 0; p < 4; p++) {
            fctn = ff[p];
            rotn = rots[p];
            m = M[p];
            o = O[p];
            for (q = 0; q < 16; q++) {
                g = (m * q + o) % 16;
                f = abcd[1] + rol(abcd[0] + fctn(abcd) + k[q + 16 * p] + mm.w[g], rotn[q % 4]);
                abcd[0] = abcd[3];
                abcd[3] = abcd[2];
                abcd[2] = abcd[1];
                abcd[1] = f;
            }
        }
        for (p = 0; p < 4; p++) h[p] += abcd[p];
        os += 64;
    }
    return h;
}

int main() {
    int j, k;
    const char *msg = "The quick brown fox jumps over the lazy dog";
    unsigned *d = md5(msg, strlen(msg));
    MD5union u;

    printf("\t MD5 ENCRYPTION ALGORITHM IN C \n\n");
    printf("Input String to be Encrypted using MD5 : \n\t%s\n", msg);
    printf("\n\nThe MD5 code for input string is: \n");
    printf("\t= 0x");
    for (j = 0; j < 4; j++) {
        u.w = d[j];
        for (k = 0; k < 4; k++) printf("%02x", u.b[k]);
    }
    printf("\n\n\t MD5 Encryption Successfully Completed!!!\n\n");

    return 0;
}
~~~

## Output
![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/8e73478e-c9dc-44dd-ba2c-54fe7ec04fd3)
## SHA 1
~~~
import java.security.*;

public class SHA1 {
    public static void main(String[] args) {
        try {
            MessageDigest md = MessageDigest.getInstance("SHA1");
            System.out.println("Message digest object info:");
            System.out.println(" Algorithm = " + md.getAlgorithm());
            System.out.println(" Provider = " + md.getProvider());
            System.out.println(" ToString = " + md.toString());

            String input = "";
            md.update(input.getBytes());
            byte[] output = md.digest();
            System.out.println("\nSHA1(\"" + input + "\") = " + bytesToHex(output));

            input = "abc";
            md.update(input.getBytes());
            output = md.digest();
            System.out.println("\nSHA1(\"" + input + "\") = " + bytesToHex(output));

            input = "abcdefghijklmnopqrstuvwxyz";
            md.update(input.getBytes());
            output = md.digest();
            System.out.println("\nSHA1(\"" + input + "\") = " + bytesToHex(output));
            System.out.println();
        } catch (NoSuchAlgorithmException e) {
            System.out.println("Exception: " + e);
        }
    }

    public static String bytesToHex(byte[] bytes) {
        char[] hexDigits = {'0', '1', '2', '3', '4', '5', '6', '7', '8', '9', 'A', 'B', 'C', 'D', 'E', 'F'};
        StringBuilder hexString = new StringBuilder();
        for (byte b : bytes) {
            hexString.append(hexDigits[(b >> 4) & 0x0f]);
            hexString.append(hexDigits[b & 0x0f]);
        }
        return hexString.toString();
    }
}
~~~
## Output
![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/637f4ab4-8ddd-4524-a70a-62c0cadb3f27)

