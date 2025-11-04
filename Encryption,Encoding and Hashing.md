# Encryption, Encoding, and Hashing: An Overview

This document provides a clear explanation of three fundamental data transformation techniques: **encryption**, **encoding**, and **hashing**. While they all involve changing data from one form to another, they have distinct purposes, use cases, and properties.

***

## Table of Contents
1.  [Encryption ](#-encryption)
2.  [Encoding ](#-encoding)
3.  [Hashing ](#-hashing)
4.  [Summary of Differences](#-summary-of-differences)

***

##  Encryption

Encryption is the process of converting data (plaintext) into a scrambled, unreadable format (ciphertext) to ensure **confidentiality and secrecy**. The primary goal is to prevent unauthorized parties from understanding the information.

* **Purpose:** To secure data and keep it secret.
* **How it works:** Uses a cryptographic algorithm and a secret **key** to transform the data. The reverse process, called decryption, requires the same (or a related) key to convert the data back to its original form.
* **Reversibility:** **Yes**, it is a two-way function.
* **Real-World Use Cases:**
    * **Secure Communications (HTTPS):** Protecting your data when browsing the web.
    * **End-to-End Encrypted Messaging:** Securing conversations in apps like Signal and WhatsApp.
    * **Full-Disk Encryption:** Protecting files on your computer's hard drive (e.g., BitLocker, FileVault).
    * **Virtual Private Networks (VPNs):** Encrypting your internet traffic on public networks.

***

##  Encoding

Encoding is the process of transforming data from one format to another to ensure **usability and proper consumption** by different systems. It is not used for security. The goal is to make sure data can be correctly transmitted or processed.

* **Purpose:** To change the format of data for compatibility or transmission.
* **How it works:** Uses a publicly available scheme to convert data. No secret key is involved.
* **Reversibility:** **Yes**, it is a two-way function.
* **Real-World Use Cases:**
    * **Character Encoding (ASCII, UTF-8):** Allowing computers to consistently store and display text.
    * **Base64 Encoding:** Converting binary data (like images) into a text format so it can be embedded in emails or web pages.
    * **URL Encoding:** Converting special characters into a valid format to be used in a URL (e.g., a space becomes `%20`).

***

##  Hashing

Hashing is the process of converting an input of any length into a **fixed-size** string of text using a mathematical function. This process is designed to be a **one-way function**, meaning it is practically impossible to reverse. Its main goal is to ensure **data integrity**.

* **Purpose:** To validate the integrity of data and securely store passwords.
* **How it works:** An input is passed through a hash algorithm (like SHA-256) to produce a unique, fixed-length output called a "hash" or "digest." Any small change to the input results in a completely different hash.
* **Reversibility:** **No**, it is a one-way function.
* **Real-World Use Cases:**
    * **Password Storage:** Websites store a hash of your password, not the password itself, for secure authentication.
    * **File Integrity Checks (Checksums):** Verifying that a downloaded file has not been corrupted or tampered with.
    * **Blockchain Technology:** Hashing is used to create secure and immutable links between blocks in a blockchain.

***

##  Summary of Differences

| Feature            | Encryption                                 | Encoding                                | Hashing                                      |
| :----------------- | :----------------------------------------- | :-------------------------------------- | :------------------------------------------- |
| **Primary Goal** | **Confidentiality** (Secrecy)              | **Usability** (Data Format)             | **Integrity** (Validation)                   |
| **Reversibility** | **Two-way** (Reversible)                   | **Two-way** (Reversible)                | **One-way** (Irreversible)                   |
| **Key** | Requires a **secret key** | No key required                         | No key required                              |
| **Output Size** | Varies with input length                   | Varies with input length                | **Fixed** length, regardless of input        |
| **Analogy** | Locking a message in a safe.               | Translating a book to another language. | Creating a unique fingerprint for a document. |