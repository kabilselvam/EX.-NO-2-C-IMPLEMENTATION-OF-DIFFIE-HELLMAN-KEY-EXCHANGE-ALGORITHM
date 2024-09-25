# EX.-NO-2-C-IMPLEMENTATION-OF-DIFFIE-HELLMAN-KEY-EXCHANGE-ALGORITHM

## AIM:
To implement the Diffie-Hellman Key Exchange algorithm using C language.

## ALGORITHM:
  
  STEP-1: Both Alice and Bob shares the same public keys g and p.
  
  STEP-2: Alice selects a random public key a.
  
  STEP-3: Alice computes his secret key A as g a mod p.
  
  STEP-4: Then Alice sends A to Bob.
  
  STEP-5: Similarly Bob also selects a public key b and computes his secret key as B and sends the same back to Alice.
  
  STEP-6: Now both of them compute their common secret key as the other one’s secret key power of a mod p.
  
## PROGRAM:
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

int prime_checker(int p) {
    if (p < 1) {
        return -1;
    } else if (p > 1) {
        if (p == 2) {
            return 1;
        }
        for (int i = 2; i < p; i++) {
            if (p % i == 0) {
                return -1;
            }
        }
        return 1;
    }
    return -1;
}

int primitive_check(int g, int p, int *L, int size) {
    for (int i = 1; i < p; i++) {
        L[i - 1] = (int)pow(g, i) % p;
    }
    for (int i = 1; i < p; i++) {
        int count = 0;
        for (int j = 0; j < size; j++) {
            if (L[j] == i) {
                count++;
            }
        }
        if (count > 1) {
            return -1;
        }
    }
    return 1;
}

int main() {
    int P, G, x1, x2;
    int l[100]; // Assuming a maximum size for L

    while (1) {
        printf("Enter P : ");
        scanf("%d", &P);
        if (prime_checker(P) == -1) {
            printf("Number Is Not Prime, Please Enter Again!\n");
            continue;
        }
        break;
    }

    while (1) {
        printf("Enter The Primitive Root Of %d : ", P);
        scanf("%d", &G);
        if (primitive_check(G, P, l, P - 1) == -1) {
            printf("Number Is Not A Primitive Root Of %d, Please Try Again!\n", P);
            continue;
        }
        break;
    }

    // Private Keys
    printf("Enter The Private Key Of User 1 : ");
    scanf("%d", &x1);
    printf("Enter The Private Key Of User 2 : ");
    scanf("%d", &x2);

    while (1) {
        if (x1 >= P || x2 >= P) {
            printf("Private Key Of Both The Users Should Be Less Than %d!\n", P);
            continue;
        }
        break;
    }

    // Calculate Public Keys
    int y1 = (int)pow(G, x1) % P;
    int y2 = (int)pow(G, x2) % P;

    // Generate Secret Keys
    int k1 = (int)pow(y2, x1) % P;
    int k2 = (int)pow(y1, x2) % P;

    printf("\nSecret Key For User 1 Is %d\nSecret Key For User 2 Is %d\n", k1, k2);

    if (k1 == k2) {
        printf("Keys Have Been Exchanged Successfully\n");
    } else {
        printf("Keys Have Not Been Exchanged Successfully\n");
    }

    return 0;
}

```

## OUTPUT:
![Screenshot 2024-09-25 153541](https://github.com/user-attachments/assets/20f820b4-60a7-4d95-bd21-bde86b617a7b)


## RESULT:
  Thus the Diffie-Hellman key exchange algorithm had been successfully implemented using C.
