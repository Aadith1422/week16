# Symmetric Encryption (Secret Key Encryption)

Symmetric encryption is a method of encryption where a single, shared
key is used for both **encrypting** (locking) and **decrypting**
(unlocking) data.

Think of it like a physical safe that uses a traditional metal key.
Anyone who has a copy of that exact key can open the safe, and they also
use that same key to lock it back up. The sender and receiver must both
have an identical copy of this secret key before they can communicate
securely.

## How it Works

1.  **Sender:** Takes the plaintext message (e.g., "Hello") and the
    shared secret key.
2.  **Encryption:** Applies an encryption algorithm (like AES) to the
    message using the key. This scrambles the message into unreadable
    ciphertext (e.g., "aXj8\$k#@!f").
3.  **Transmission:** The ciphertext is sent over an insecure channel
    (like the internet).
4.  **Receiver:** Takes the received ciphertext ("aXj8\$k#@!f") and uses
    the exact same shared key.
5.  **Decryption:** Applies the decryption algorithm (the reverse of
    encryption) to the ciphertext, which reveals the original plaintext
    message ("Hello").

## Pros and Cons

-   **Pro: Speed.** Symmetric algorithms are very fast and
    computationally efficient. This makes them ideal for encrypting
    large amounts of data, such as entire hard drives (disk encryption)
    or large file transfers.
-   **Con: Key Distribution.** The biggest challenge is securely sharing
    the key. How do you get the secret key to the receiver in the first
    place without someone else intercepting it? If the key is
    intercepted, the entire security is broken.

------------------------------------------------------------------------

# Examples of Symmetric Encryption

## 1. AES (Advanced Encryption Standard)

**What it is:** AES is the modern, global standard for symmetric
encryption. It is used by governments (including the U.S. government to
protect classified information), businesses, and individuals worldwide.
It is widely considered to be extremely secure.

**How it Works:** AES is a block cipher, meaning it encrypts data in
fixed-size blocks of 128 bits. It uses key sizes of **128, 192, or 256
bits**. A longer key size means there are more possible key
combinations, making it exponentially harder to guess or "brute-force."
AES performs multiple rounds of substitution and permutation operations
on the data block to thoroughly scramble it.

## 2. DES (Data Encryption Standard)

**What it is:** DES is an older symmetric-key algorithm that was a U.S.
government standard from 1977. It is now considered insecure and
obsolete.

**How it Works:** DES is also a block cipher, but it uses a much smaller
**56-bit key** and encrypts data in **64-bit blocks**. Its small key
size is its critical weakness; modern computers can brute-force a 56-bit
key quickly, making DES unsuitable for protecting sensitive data today.
It is primarily studied for historical and academic purposes.

------------------------------------------------------------------------

# Asymmetric Encryption (Public-Key Cryptography)

Asymmetric encryption uses two mathematically related keys to form a key
pair: a **public key** and a **private key**.

This is like having a special mailbox with two keys.

-   The **public key** is like the mail slot on the mailbox. You can
    give copies of this "key" (the slot's location and dimensions) to
    anyone in the world. Anyone can use it to deposit a message (encrypt
    data) into the mailbox.
-   The **private key** is like the physical key that unlocks the
    mailbox. Only you, the owner, have this key. It is the only key that
    can open the mailbox and retrieve the messages (decrypt data).

## How it Works

1.  **Key Generation:** The receiver (Alice) generates her own unique
    key pair (a public key and a private key).
2.  **Key Distribution:** Alice keeps her private key absolutely secret.
    She shares her public key with anyone who wants to send her a secure
    message (e.g., by publishing it online).
3.  **Sender (Bob):** Bob wants to send Alice a secret message. He takes
    his plaintext message ("Hello Alice"), finds Alice's public key, and
    uses it to encrypt the message. This creates ciphertext
    ("qZtR#9!p&o").
4.  **Transmission:** Bob sends this ciphertext over the internet.
5.  **Receiver (Alice):** Alice receives the ciphertext. She uses her
    own private key to decrypt it, which reveals the original message
    ("Hello Alice").

**Crucially:** A message encrypted with a public key can only be
decrypted by its corresponding private key. Even if someone intercepts
the message and has Alice's public key, they cannot decrypt the message.

## Pros and Cons

-   **Pro: Secure Key Exchange.** It solves the key distribution problem
    of symmetric encryption. You never have to share your secret
    (private) key.
-   **Pro: Digital Signatures.** It can also be used in reverse to prove
    identity. If Alice encrypts (or signs) a message with her private
    key, anyone can verify/decrypt it with her public key. This doesn't
    provide secrecy, but it proves that the message must have come from
    Alice, because only she has the private key that matches her public
    key.
-   **Con: Speed.** Asymmetric encryption involves complex mathematics,
    making it much slower and more computationally intensive than
    symmetric encryption. It is not suitable for encrypting large
    amounts of data.

In practice, most systems (like HTTPS / SSL / TLS on websites) use a
**hybrid approach**:

1.  **Asymmetric encryption** is used first to securely exchange a
    symmetric key.
2.  Once both sides have the shared symmetric key, they switch to
    **symmetric encryption** for the rest of the conversation to take
    advantage of its high speed.

------------------------------------------------------------------------

# Examples of Asymmetric Encryption

## 1. RSA (Rivest--Shamir--Adleman)

**What it is:** RSA is one of the first and most widely known asymmetric
algorithms. It's used heavily in secure data transmission (like SSL/TLS)
and for digital signatures.

**How it Works:** The security of RSA is based on a simple mathematical
principle: it is easy to multiply two very large prime numbers together,
but it is extremely difficult to do the reverse (to find the original
two prime numbers if you only know the product).

**Key Generation:** You secretly select two massive prime numbers (p and
q) and multiply them to get a public number n. Your public key and
private key are then derived from these numbers through further
calculations.

**Security:** An attacker might know your public number n, but to figure
out your private key, they would have to factor n back into p and q. For
commonly used key sizes today (e.g., **2048 or 4096 bits**), factoring n
is considered computationally infeasible with current classical
computers.

## 2. ECC (Elliptic Curve Cryptography)

**What it is:** ECC is a newer, more advanced type of asymmetric
cryptography that is rapidly becoming the standard, especially for
mobile devices and IoT.

**How it Works:** Instead of relying on large prime numbers, ECC's
security is based on the mathematical properties of elliptic curves (a
specific type of algebraic equation). The security relies on the
**elliptic curve discrete logarithm problem (ECDLP)**.

**Analogy:** Imagine a point on a curve. You "add" that point to itself
k times (where k is your private key) to get a new point on the curve
(your public key). It's easy to calculate the public key if you know the
starting point and k. However, it is astronomically difficult for
someone to figure out k (the private key) even if they know both the
starting point and the final public key.

**Main Advantage:** ECC provides the same level of security as RSA but
with much smaller key sizes. For example, a **256-bit ECC key** is
considered as secure as a **3072-bit RSA key**. This makes it much
faster and more efficient, requiring less computing power and battery
life --- perfect for smartphones and other low-power devices.

------------------------------------------------------------------------

# Quick Comparison (at a glance)

  -----------------------------------------------------------------------
  Feature                  Symmetric (AES, DES)     Asymmetric (RSA, ECC)
  ------------------- ------------------------- -------------------------
  Keys required             1 shared secret key  2 keys: public + private

  Speed                               Very fast   Slower, computationally
                                                                    heavy

  Use cases               Bulk data encryption,      Secure key exchange,
                           disk encryption, VPN       digital signatures,
                                        tunnels            authentication

  Key distribution         Hard (must be shared Easier (public key can be
                                      securely)                published)

  Typical algorithms        AES, ChaCha20, 3DES    RSA, ECC (ECDSA, ECDH)
                                       (legacy) 
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# Practical Notes

-   **Hybrid systems** (as used in TLS) combine the strengths of both:
    asymmetric crypto for secure key exchange, symmetric crypto for fast
    bulk encryption.
-   **Choosing algorithms and key sizes** should follow current
    standards and recommendations (for example, using AES-256 for
    symmetric encryption and at least 2048-bit RSA or 256-bit ECC where
    appropriate).

------------------------------------------------------------------------

# Short examples (conceptual)

**Symmetric (AES):**

    key = shared_secret_key
    ciphertext = AES_Encrypt(key, "Hello")
    plaintext  = AES_Decrypt(key, ciphertext)

**Asymmetric (RSA):**

    (public_key, private_key) = RSA_GenerateKeys()
    ciphertext = RSA_Encrypt(public_key, "Hello Alice")
    plaintext  = RSA_Decrypt(private_key, ciphertext)