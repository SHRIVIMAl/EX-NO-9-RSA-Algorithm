# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: **Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:

```
#include <stdio.h>

/* Function to calculate GCD */
int gcd(int a, int b)
{
    while(b != 0)
    {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

/* Function for modular exponentiation */
long long modExp(long long base, long long exp, long long mod)
{
    long long result = 1;

    while(exp > 0)
    {
        if(exp % 2 == 1)
        {
            result = (result * base) % mod;
        }

        base = (base * base) % mod;
        exp = exp / 2;
    }

    return result;
}

/* Function to find modular inverse */
int modInverse(int e, int phi)
{
    int d;

    for(d = 1; d < phi; d++)
    {
        if((d * e) % phi == 1)
        {
            return d;
        }
    }

    return -1;
}

int main()
{
    int p, q;
    int n, phi;
    int e, d;
    int message;
    long long encrypted, decrypted;

    printf("Enter prime number p: ");
    scanf("%d", &p);

    printf("Enter prime number q: ");
    scanf("%d", &q);

    n = p * q;

    phi = (p - 1) * (q - 1);

    printf("Enter public exponent e: ");
    scanf("%d", &e);

    /* Check if e and phi are coprime */
    if(gcd(e, phi) != 1)
    {
        printf("e and phi(n) are not coprime.\n");
        return 0;
    }

    d = modInverse(e, phi);

    printf("\nPublic Key  : (%d, %d)\n", e, n);
    printf("Private Key : (%d, %d)\n", d, n);

    printf("\nEnter message (number): ");
    scanf("%d", &message);

    /* Encryption */
    encrypted = modExp(message, e, n);

    printf("Encrypted Message : %lld\n", encrypted);

    /* Decryption */
    decrypted = modExp(encrypted, d, n);

    printf("Decrypted Message : %lld\n", decrypted);

    return 0;
}
```


## Output:

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/e0ea7fd8-887f-4fe8-9036-d47166b30efe" />



## Result:
 The program is executed successfully.
