# EX. NO: 3 HILL CIPHER


## AIM:
To write a C program to implement the hill cipher substitution techniques.

## DESCRIPTION:

Each letter is represented by a number modulo 26. Often the simple scheme A = 0, B
= 1... Z = 25, is used, but this is not an essential feature of the cipher. To encrypt a message, each block of n letters is  multiplied by an invertible n × n matrix, against modulus 26. To
decrypt the message, each block is multiplied by the inverse of the m trix used for
 
encryption. The matrix used
 
for encryption is the cipher key, and it sho
 
ld be chosen
 
randomly from the set of invertible n × n matrices (modulo 26).


## ALGORITHM:

STEP-1: Read the plain text and key from the user. STEP-2: Split the plain text into groups of length three. STEP-3: Arrange the keyword in a 3*3 matrix.
STEP-4: Multiply the two matrices to obtain the cipher text of length three.
STEP-5: Combine all these groups to get the complete cipher text.

## PROGRAM 
```
#include <stdio.h>
#include <string.h>
#include <ctype.h>

int main() {
    char text[1000];
    int key[3][3];
    char processed[1010];
    char cipher[1010];
    int len, padded_len;

    // Input plaintext
    printf("Enter plaintext: ");
    fgets(text, sizeof(text), stdin);
    // Remove newline and convert to uppercase
    len = strlen(text);
    if (text[len-1] == '\n') text[--len] = '\0';
    for (int i = 0; i < len; i++) text[i] = toupper(text[i]);

    // Input 3x3 key matrix
    printf("Enter 3x3 key matrix:\n");
    for (int i = 0; i < 3; i++) {
        scanf("%d %d %d", &key[i][0], &key[i][1], &key[i][2]);
    }

    // Print key matrix
    printf("\nKey Matrix:\n");
    for (int i = 0; i < 3; i++) {
        printf("[%d, %d, %d]\n", key[i][0], key[i][1], key[i][2]);
    }

    // Copy text to processed and pad with 'X'
    strcpy(processed, text);
    padded_len = len;
    while (padded_len % 3 != 0) {
        processed[padded_len++] = 'X';
    }
    processed[padded_len] = '\0';
    printf("Processed Text: %s\n", processed);

    // Encrypt
    int cipher_idx = 0;
    for (int i = 0; i < padded_len; i += 3) {
        int pt[3], ct[3] = {0, 0, 0};

        // Print block
        printf("\nBlock: %c%c%c\n", processed[i], processed[i+1], processed[i+2]);

        // Convert letters to numbers
        for (int j = 0; j < 3; j++) pt[j] = processed[i+j] - 'A';

        // Matrix multiply mod 26
        for (int r = 0; r < 3; r++) {
            for (int c = 0; c < 3; c++) {
                ct[r] += key[r][c] * pt[c];
            }
            ct[r] %= 26;
        }

        printf("Numeric: [%d, %d, %d]\n", ct[0], ct[1], ct[2]);

        for (int j = 0; j < 3; j++) {
            cipher[cipher_idx++] = ct[j] + 'A';
        }
    }
    cipher[cipher_idx] = '\0';

    printf("\nFinal Cipher Text: %s\n", cipher);
    return 0;
}
```

## OUTPUT
<img width="543" height="695" alt="image" src="https://github.com/user-attachments/assets/4b626f97-33fa-4937-9c0b-a4f020288fdd" />

The program is executed successfully

