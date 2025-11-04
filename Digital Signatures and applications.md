# Digital Signatures 

A **digital signature** cleverly uses **asymmetric encryption** (public
and private keys) --- but in reverse. Instead of encrypting for secrecy,
you encrypt to **prove identity**.

The process involves creating a unique *fingerprint* of your message and
encrypting that fingerprint.

------------------------------------------------------------------------

##  How Digital Signatures Work

### 1. Hashing

The sender (let's say **Alice**) takes her message (e.g., a PDF
contract) and runs it through a **hash function**.\
This creates a unique, fixed-length string of text called a **hash** (or
*message digest*).\
This hash is a unique **digital fingerprint** for that exact file.

### 2. Signing (Encryption)

Alice then **encrypts this hash using her own private key**.\
This encrypted hash is the **digital signature**.

### 3. Sending

Alice attaches this **digital signature** to the **original, unencrypted
message** (the PDF contract) and sends both to the receiver (**Bob**).

### 4. Verification (Decryption)

Bob receives the message and the signature. He uses **Alice's public
key** (which is available to everyone) to **decrypt the digital
signature**.\
This reveals the original hash that Alice created.

### 5. Verification (Hashing)

Bob then takes the message (the PDF contract) he received and runs it
through the **same hash function** Alice used.\
This creates a new hash.

### 6. Comparison

Bob compares: - The **decrypted hash** (from Alice's signature), and -
The **newly generated hash** (from his own hashing).

**If they match** → The signature is **valid**.\
**If they don't match** → The signature is **invalid**.

------------------------------------------------------------------------

##  What a Valid Signature Proves

### 1. **Authenticity**

Only Alice's private key could have created a signature that her public
key can decrypt.\
It confirms **who** sent the message.

### 2. **Integrity**

The message hasn't been changed. If even one bit of the message were
altered, the hash would differ, and verification would fail.

### 3. **Non-Repudiation**

Alice cannot later deny sending the message.\
Since only she has access to her **private key**, she can't claim
someone else signed it.\
This is essential in **legal contracts and digital evidence**.

------------------------------------------------------------------------

##  The Three Guarantees of a Digital Signature

  -----------------------------------------------------------------------
  Guarantee                          Description
  ---------------------------------- ------------------------------------
  **Authenticity**                   Confirms the identity of the sender
                                     (proves who signed it).

  **Integrity**                      Ensures the message or document
                                     hasn't been tampered with.

  **Non-Repudiation**                Prevents the sender from denying the
                                     signature later.
  -----------------------------------------------------------------------

------------------------------------------------------------------------

##  Real-World Applications of Digital Signatures

### 1. **Secure Software Distribution**

When you download software (like drivers or browsers), your computer
checks its **digital signature**.\
This ensures it came from the **official developer** (e.g., Microsoft,
Google) and hasn't been modified with malware.

### 2. **Legal Documents and E-Signing**

Services like **DocuSign** and **Adobe Sign** use digital signatures for
**legally binding electronic contracts**.\
When you "e-sign" a lease, employment offer, or loan document, a digital
signature provides **authenticity and non-repudiation**.

### 3. **Financial Transactions**

Banks and fintech services use digital signatures to **authorize
transactions** and **secure communications**.\
Official PDFs like bank statements are often digitally signed to prove
authenticity.

### 4. **Government E-Filing**

Digital signatures are used in **online tax filing**, **citizen
services**, and **official document submissions** to verify identity and
ensure data integrity.

------------------------------------------------------------------------

##  Summary

A **digital signature** = Hash (integrity) + Private Key Encryption
(authenticity) + Verification (non-repudiation)

Together, these provide trust and legal assurance in the digital world.

------------------------------------------------------------------------

**Example (Conceptual):**

    # Alice signs
    message = "Contract.pdf"
    hash_value = Hash(message)
    signature = Encrypt(hash_value, Alice_private_key)

    # Bob verifies
    decrypted_hash = Decrypt(signature, Alice_public_key)
    new_hash = Hash(message)

    if decrypted_hash == new_hash:
        print(" Signature valid - Authentic & Untampered")
    else:
        print(" Signature invalid - Possible tampering")

------------------------------------------------------------------------