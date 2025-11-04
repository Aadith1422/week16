


---

### 1.0 Introduction

This report details three fundamental primitives in modern cryptography: **block ciphers**, **stream ciphers**, and **hashing functions**. Ciphers are used to ensure **confidentiality** by making data unreadable to unauthorized parties (encryption). Hashing, in contrast, is not encryption; it is a one-way function used to ensure **integrity** by verifying that data has not been altered. Understanding the distinct logic of each is critical to building secure systems.

---

### 2.0 Block Ciphers

A block cipher is an encryption algorithm that operates on a fixed-size group of bits, known as a **block**. The most common and secure modern block cipher, **AES (Advanced Encryption Standard)**, uses a block size of 128 bits.

#### 2.1 Core Logic

1.  **Fixed-Size Blocks:** The algorithm takes a 128-bit block of plaintext and a secret key (e.g., 128, 192, or 256 bits for AES). It then outputs a 128-bit block of ciphertext.
2.  **Iteration and Complexity:** The encryption is not a single step. It is an iterative process of multiple **rounds**. Each round applies a series of mathematical operations (substitution, permutation, and mixing) to the data, with each round's operation being influenced by the secret key. This layered complexity is what makes the encryption strong.
3.  **Reversibility:** The process is fully reversible. The decryption algorithm simply applies the inverse of these rounds, in reverse order, to turn the ciphertext back into plaintext. This only works if you have the correct secret key.

**Analogy:** Think of a block cipher as a highly complex, secure **lockbox**.  
* The **block** is the maximum amount of "stuff" you can put in the box at one time.  
* The **key** is the physical key that locks the box.  
* The **encryption algorithm** is the complex scrambling mechanism inside the box that is activated by the key.  
* Without the exact same key, the scrambling mechanism cannot be reversed.

#### 2.2 Modes of Operation

Because a block cipher only works on one fixed-size block, a **mode of operation** is required to encrypt a message larger than 128 bits (like a file or an email).

* **The Naive Mode (ECB):** The most basic mode, Electronic Codebook (ECB), encrypts each block independently. This is **highly insecure** because identical plaintext blocks will produce identical ciphertext blocks, leaving obvious patterns.  
* **Secure Modes (e.g., CBC, GCM):** Secure modes introduce "chaining" and "randomness." In **Cipher Block Chaining (CBC)**, the result of encrypting one block is XORed with the *next* plaintext block before it is encrypted. This ensures that every ciphertext block depends on all previous blocks, and identical plaintext blocks will result in completely different ciphertext. This process is started using a random value called an **Initialization Vector (IV)**.

**Common Use Cases:** Encrypting files (file system encryption), databases, and as a component in secure protocols like TLS (which secures HTTPS).

---

### 3.0 Stream Ciphers

A stream cipher is an encryption algorithm that encrypts data one bit or one byte at a time. It is designed to be fast and is useful when the length of the data is unknown or when it is arriving in a continuous stream.

#### 3.1 Core Logic

The logic of a stream cipher is fundamentally different from a block cipher. It does not operate on the plaintext directly.

1.  **Keystream Generation:** The stream cipher uses a secret key and a unique **nonce** (a "number used once") to generate a pseudo-random stream of bits called a **keystream**. This keystream must be the same length as the plaintext message.
2.  **XOR Operation:** The keystream is then combined with the plaintext using the **XOR ($\oplus$)** logical operation.  
    * Plaintext $\oplus$ Keystream = Ciphertext
3.  **Reversibility:** The beauty of XOR is its symmetrical property. To decrypt, the recipient (who has the same key and nonce) generates the *exact same keystream* and XORs it with the ciphertext.  
    * Ciphertext $\oplus$ Keystream = Plaintext

**Analogy:** A stream cipher is like a **digital one-time pad**.  
* The **key** and **nonce** are used to generate a secret, seemingly-random "codebook" (the keystream).  
* You "add" this codebook to your message to scramble it.  
* Your friend, who can generate the *exact same codebook*, "subtracts" (XORs) it from your scrambled message to read the original.

**Critical Security Rule:** The same key/nonce pair must *never* be reused. If it is, an attacker who has two ciphertexts (C1 and C2) can XOR them together ($C_1 \oplus C_2$). Since the keystream (K) is the same, it cancels out, leaving the attacker with the XOR of the two plaintexts ($P_1 \oplus P_2$). This can be used to break the encryption.

**Common Use Cases:** Real-time communications (voice and video calls), secure Wi-Fi (WPA2/3), and in modern TLS (e.g., ChaCha20-Poly1305).

---

### 4.0 The Logic Behind Hashing

Hashing is a completely different cryptographic primitive. It is **not encryption** and does not provide confidentiality. Its purpose is to provide **integrity** and **authentication**.

A hash function is a one-way "trapdoor" function that takes an input of *any size* (from a single character to a 10TB file) and produces a fixed-size string of characters, which is called a **hash** or **digest**. For example, SHA-256 always produces a 256-bit (64-character) hash.

#### 4.1 Core Logic and Properties

The logic of hashing is built on five key principles:

1.  **One-Way:** It is easy to compute a hash from a message, but it is computationally infeasible to reverse the process (i.e., to find the message from its hash). This is the "trapdoor" property.
2.  **Deterministic:** The same input message will *always* produce the exact same hash.
3.  **Fixed-Size Output:** Any input, regardless of its size, will produce an output of a single, consistent size (e.g., 256 bits).
4.  **Avalanche Effect:** A tiny change in the input (e.g., changing one bit) will produce a completely different and unrecognizable hash.
5.  **Collision Resistant:** It should be computationally infeasible to find two *different* inputs that produce the same hash.

**Analogy:** A hash is a **digital fingerprint** for data.  
* You can't look at a fingerprint and reconstruct the person (one-way).  
* A person always has the same fingerprint (deterministic).  
* No two people have the same fingerprint (collision resistant).  
* It's a small, fixed-size summary of a large, complex person (fixed-size output).

#### 4.2 How Hashing Works (Internal Logic)

Most hash functions (like SHA-256) use a structure that processes the data in blocks.

1.  The data is broken into fixed-size blocks (e.g., 512 bits).
2.  The function starts with a fixed initial value called an **internal state**.
3.  The first block of data is fed into the function, which scrambles and mixes it with the internal state, producing a *new* internal state.
4.  The *second* block of data is then fed in, and it is scrambled with the state *from the previous step*.
5.  This process "chains" all the blocks together. The final internal state, after all blocks are processed, is the hash. This "chaining" is what enables the avalanche effect.

#### 4.3 Key Use Cases

* **Password Storage:** Never store passwords. Store `hash(password + salt)`. When a user tries to log in, you hash their attempt and compare the hashes. If a database is stolen, the attackers only get the hashes, not the passwords.
* **Data Integrity:** When you download a file, a website often provides a hash for it. You can hash the file you downloaded on your computer. If your hash matches the one on the website, you know the file was not corrupted or tampered with.
* **Digital Signatures:** Hashing is the first step in creating a digital signature, which verifies the authenticity and integrity of a message.

---

### 5.0 Summary of Comparison

| Feature | Block Cipher (e.g., AES) | Stream Cipher (e.g., ChaCha20) | Hashing (e.g., SHA-256) |
| :--- | :--- | :--- | :--- |
| **Primary Goal** | Confidentiality | Confidentiality | Integrity & Authenticity |
| **Input** | Fixed-size block (e.g., 128 bits) | Continuous stream (bit/byte) | Any size (file, message, etc.) |
| **Output** | Fixed-size block (same as input) | Continuous stream (same as input) | Fixed-size hash (e.g., 256 bits) |
| **Key** | Yes (secret key) | Yes (secret key + nonce) | No key |
| **Reversible?** | **Yes**, with the key (Decryption) | **Yes**, with key/nonce (XOR) | **No**, it is a one-way function |
| **Analogy** | Secure lockbox | One-time pad | Digital fingerprint |