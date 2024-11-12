# Ex-3 Hill Cipher

### DATE:

Hill Cipher using with different key values

## AIM:
To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

Step 1: Design of Hill Cipher algorithnm

Step 2: Implementation using C or pyhton code

Step 3: Testing algorithm with different key values. 

## ALGORITHM DESCRIPTION: 

The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible n × n matrix, again modulus 26. To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption. The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of invertible n × n matrices (modulo 26). The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be done modulo the number of letters instead of modulo 26.

## PROGRAM:
```
#include <iostream>
#include <cstring>
using namespace std;

int keymat[3][3] = { { 1, 2, 1 }, { 2, 3, 2 }, { 2, 2, 1 } };
int invkeymat[3][3] = { { -1, 0, 1 }, { 2, -1, 0 }, { -2, 2, -1 } };
char key[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

// Function to encode a block of three characters
void encode(char a, char b, char c, char* result) {
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;
    
    int x = posa * keymat[0][0] + posb * keymat[1][0] + posc * keymat[2][0];
    int y = posa * keymat[0][1] + posb * keymat[1][1] + posc * keymat[2][1];
    int z = posa * keymat[0][2] + posb * keymat[1][2] + posc * keymat[2][2];
    
    result[0] = key[x % 26];
    result[1] = key[y % 26];
    result[2] = key[z % 26];
    result[3] = '\0';
}

// Function to decode a block of three characters
void decode(char a, char b, char c, char* result) {
    int posa = (int) a - 65;
    int posb = (int) b - 65;
    int posc = (int) c - 65;

    int x = posa * invkeymat[0][0] + posb * invkeymat[1][0] + posc * invkeymat[2][0];
    int y = posa * invkeymat[0][1] + posb * invkeymat[1][1] + posc * invkeymat[2][1];
    int z = posa * invkeymat[0][2] + posb * invkeymat[1][2] + posc * invkeymat[2][2];
    
    result[0] = key[(x % 26 < 0) ? (26 + x % 26) : (x % 26)];
    result[1] = key[(y % 26 < 0) ? (26 + y % 26) : (y % 26)];
    result[2] = key[(z % 26 < 0) ? (26 + z % 26) : (z % 26)];
    result[3] = '\0';
}

int main() {
    char msg[1000]; // Input message
    char enc[1000] = ""; // Encrypted message
    char dec[1000] = ""; // Decrypted message
    int n;

    strcpy(msg, "SecurityLaboratory");
    cout << "Simulation of Hill Cipher\n";
    cout << "Input Message: " << msg << endl;

    // Convert to uppercase and remove spaces
    for (int i = 0; i < strlen(msg); i++) {
        msg[i] = toupper(msg[i]);
    }

    // Padding the message with X if necessary
    n = strlen(msg) % 3;
    if (n != 0) {
        for (int i = 1; i <= (3 - n); i++) {
            strcat(msg, "X");
        }
    }
    
    cout << "Padded Message: " << msg << endl;

    // Encrypt the message
    for (int i = 0; i < strlen(msg); i += 3) {
        char block[4];
        encode(msg[i], msg[i + 1], msg[i + 2], block);
        strcat(enc, block);
    }

    cout << "Encrypted Message: " << enc << endl;

    // Decrypt the message
    for (int i = 0; i < strlen(enc); i += 3) {
        char block[4];
        decode(enc[i], enc[i + 1], enc[i + 2], block);
        strcat(dec, block);
    }

    cout << "Decrypted Message: " << dec << endl;

    return 0;
}
```
## OUTPUT:

![image](https://github.com/user-attachments/assets/b04886e1-7eea-4a11-be26-34b484c9d74f)

## RESULT:

The program is executed successfully
