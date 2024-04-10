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
```
## Output

![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/d3a484ef-1f99-4b40-a308-c07d90e9c784)
## Hill Cipher
```
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
```
## Output
![image](https://github.com/kaviyabalaji/lab-exercises/assets/113762813/db3efa16-73e1-4cff-85e2-da411a202eb5)
## Vigenere Cipher
```
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
```
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
