# INS- Cipher Implementation and Comparative Analysis

## Overview
This repository contains implementations of classical encryption techniques, including the **Playfair Cipher, Hill Cipher, Vigenère Cipher**, and a **Hybrid Cipher** combining AES substitution and transposition techniques. Additionally, a comparative analysis of these ciphers is provided, including cryptanalysis and performance evaluation.

## Ciphers Implemented

### 1. Playfair Cipher
- **Type**: Digraph Substitution Cipher
- **Key**: 5x5 Matrix constructed from a keyword
- **Encryption Process**:
  - Organizes letters into digraphs
  - Applies substitution based on position in matrix
  - Handles duplicate letters and odd-length messages
- **Implementation**: `playfair_cipher.py`
- **Complexity**: **O(n)** for encryption and decryption

### 2. Hill Cipher
- **Type**: Matrix-Based Block Cipher
- **Key**: n x n Matrix (must have an inverse mod 26)
- **Encryption Process**:
  - Converts text into numerical vectors
  - Applies matrix multiplication mod 26
  - Uses modular inverse for decryption
- **Implementation**: `hill_cipher.py`
- **Complexity**: **O(n³)** for decryption (due to matrix inversion)

### 3. Vigenère Cipher
- **Type**: Polyalphabetic Substitution Cipher
- **Key**: Repeated keyword of arbitrary length
- **Encryption Process**:
  - Shifts letters based on the repeating key
  - Implements character-wise modulo arithmetic
- **Implementation**: `vigenere_cipher.py`
- **Complexity**: **O(n)** for encryption and decryption

### 4. Hybrid Cipher (Vigenère + Columnar Transposition)
- **Type**: Polyalphabetic Substitution + Transposition
- **Key**: Variable Length (Vigenère Key + Columnar Key)
- **Encryption Process**:
  - Encrypts with Vigenère cipher
  - Applies transposition based on a fixed seed
- **Implementation**: `hybrid_cipher.py`
- **Complexity**:
  - **AES Encryption**: **O(n)**
  - **Transposition**: **O(n log n)** (sorting-based shuffling)


## How to Run the Code

### Prerequisites
Before running the scripts, ensure you have the following installed:
- **Python 3.x**
- **NumPy** (for matrix operations in Hill Cipher)
- **PyCryptodome** (for AES encryption in Hybrid Cipher)

Install dependencies using:
```sh
pip install numpy pycryptodome
```

### Using GitHub Codespaces
If using **GitHub Codespaces**, follow these steps:

**Cipher_Codes Codespace**

Use this codespace to run the files

OR 

1. **Open the Repository in Codespaces**
   - Navigate to your repository on GitHub
   - Click on `<> Code` → `Codespaces` → `New Codespace`

2. **Run the Scripts**
   - Open the terminal in Codespaces
   - Run any of the Python scripts using:
     ```sh
     python3 <script_name>.py
     ```
   Example:
     ```sh
     python3 vigenere_cipher.py
     ```

3. **Provide Input When Prompted**
   - Each script may ask for input (key, plaintext, etc.)

## Example Usage

### Playfair Cipher
```sh
python3 playfair_cipher.py
```
**Input:**
```
Enter the key: SECRET
Enter the message: HELLO WORLD
```
**Output:**
```
Encrypted Message: KFMTHZBQKD
```

### Hill Cipher
```sh
python3 hill_cipher.py
```
**Input:**
```
Plaintext: SHORT
Key Matrix: [[7, 8], [11, 11]]
```
**Output:**
```
Encrypted: WFJTG
```

### Vigenère Cipher
```sh
python3 vigenere_cipher.py
```
**Input:**
```
Plaintext: HELLO
Key: KEY
```
**Output:**
```
Ciphertext: RIJVS
Decrypted: HELLO
```

### Hybrid Cipher (Vigenère + Columnar Transposition)
```sh
python3 hybrid_cipher.py
```
**Input:**
```
Plaintext: HELLO WORLD
Vigenère Key: SECRET
Columnar Transposition Key: KEY
```
**Output:**
```
Encrypted: LXFOP VEFGR HF
Decrypted: HELLO WORLD
```

## Comparative Analysis
| Cipher       | Type                         | Key Size        | Complexity (Enc/Dec) | Strengths                        | Weaknesses |
|-------------|------------------------------|-----------------|----------------------|---------------------------------|------------|
| Playfair    | Digraph Substitution         | 5x5 Key Matrix  | O(n)                 | More secure than simple monoalphabetic | Still vulnerable to digraph analysis |
| Hill        | Matrix-Based Block Cipher    | n x n Matrix    | O(n³)                 | Stronger encryption, uses algebra | Requires invertible key matrix |
| Vigenère    | Polyalphabetic Substitution  | Variable Length | O(n)                  | Resists simple frequency analysis | Still breakable with Kasiski method |
| Hybrid (AES+Transposition) | Polyalphabetic Substitution + Transposition | Variable Length (Vigenère Key + Columnar Key)  | O(n) Vigenère, O(n log n) Transposition | Combines substitution and transposition for enhanced security | Vulnerable to known-plaintext attacks, computationally heavier than standalone Vigenère
 |

## Future Improvements
- Implement **automated cryptanalysis tools** to break weak ciphers.
- Enhance **key management** for Hill and Playfair ciphers.
- A potential improvement for the Hybrid cipher could be dynamic key generation to enhance security against modern cryptanalysis.
  # Feistel-Cipher

# Introduction

This program implements the **Feistel Cipher**, a symmetric encryption algorithm used in many cryptographic systems.

## Working

- Encrypts and decrypts messages using a **Feistel network**.
- Converts text to **binary format** for processing.
- Uses a **user-provided key** for encryption.
- Supports **two rounds** of Feistel structure.

## `feistel_encrypt(plaintext, key)`

Encrypts the plaintext using the Feistel cipher algorithm.

## `feistel_decrypt(ciphertext, key)`

Decrypts the encrypted message back to its original form.

## Output
![Image](https://github.com/user-attachments/assets/0059dd58-4a81-4dac-ad68-04b0f780c04a)
# DES Key Generation

## Introduction

This program implements the **Key Generation** process of the **Data Encryption Standard (DES)** algorithm. It takes a **64-bit binary key** as input, applies **permutations and shifts**, and generates **16 subkeys** used in the encryption process.

## Working

- **Initial Permutation (PC1)**: Reduces the 64-bit key to 56 bits.
- **Left and Right Key Splitting**: The key is split into two 28-bit halves.
- **Left Circular Shifts**: Each half is rotated based on predefined shift values.
- **Permutation Choice 2 (PC2)**: Produces the final **48-bit subkeys**.
- **Generates 16 Subkeys**, one for each DES encryption round.

## `permute(input, table)`

Performs permutation on the input string based on the given table.

## `leftShift(input, shifts)`

Shifts the input string left by the given number of positions.

## Output Example
![Image](https://github.com/user-attachments/assets/896545ee-015b-435a-b2e3-a4b499816574)

# RSA Algorithm Implementation

## Introduction

This program implements the **RSA encryption and decryption algorithm** using two prime numbers. RSA is an **asymmetric cryptographic algorithm** that uses **public and private keys** for secure communication.

## Working

- **Choose two prime numbers (p, q)**.
- Compute **n = p × q**.
- Compute **Euler's Totient Function (φ(n)) = (p - 1) × (q - 1)**.
- Find **public key exponent (e)** such that `1 < e < φ(n)` and `gcd(e, φ(n)) = 1`.
- Compute **private key exponent (d)** such that `(d × e) % φ(n) = 1`.
- Encrypt the message using `c = (msg^e) % n`.
- Decrypt the message using `d = (c^d) % n`.

## `gcd(a, b)`

Finds the **greatest common divisor (GCD)** of two numbers.

## `RSA(p, q, msg)`

- Generates **public and private keys**.
- Encrypts the input message.
- Decrypts the encrypted message.

## Example Output
![Image](https://github.com/user-attachments/assets/a604e913-39dc-4d94-bf54-166d701ed274)


For any issues or contributions, feel free to submit a pull request or open an issue in the repository. 
