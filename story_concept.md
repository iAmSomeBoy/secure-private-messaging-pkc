# 🔐 Public Key Cryptography – মূল ধারণা (Fundamentals)

প্রতিটি user-এর কাছে থাকে দুটি key:

1. **Public Key**  
   সবাই দেখতে পারে  
   Message encrypt করার জন্য ব্যবহার হয়

2. **Private Key**  
   শুধু owner জানে  
   Message decrypt করার জন্য ব্যবহার হয়

📌 **গুরুত্বপূর্ণ কথা:**  
Public key দিয়ে encrypt করা message শুধু সংশ্লিষ্ট private key দিয়েই decrypt করা যায়।

---

🧑‍🤝‍🧑 **ধরো:**  
- তুমি = Alice  
- তোমার বন্ধু (England) = Bob

## 🔄 পুরো Process (Step by Step)

### 🔹 Step 1: Bob key pair তৈরি করে
Bob তার device-এ একটি algorithm (RSA / ECC) দিয়ে তৈরি করে:

- Bob-এর **Public Key** (PK_Bob)  
- Bob-এর **Private Key** (SK_Bob)  

Private key সে গোপন রাখে।

### 🔹 Step 2: Bob তার Public Key তোমাকে দেয়
Bob তার public key তোমাকে পাঠায় (Email, WhatsApp, Website, QR code ইত্যাদি)।

> 📌 Public key leak হলে সমস্যা নেই।

### 🔹 Step 3: তুমি message encrypt করো
তুমি যে message পাঠাতে চাও:  

**M** = "Hi Bob, how are you?"

তুমি Bob-এর public key দিয়ে encrypt করো:  

**C** = Encrypt(PK_Bob, M)

এখন **C** হলো ciphertext (অপাঠ্য data)।

### 🔹 Step 4: Encrypted message পাঠানো
এই ciphertext **C** তুমি পাঠাও:  
WhatsApp, Messenger, Email, Any insecure channel

> ❌ মাঝখানে কেউ দেখলেও বুঝবে না

### 🔹 Step 5: Bob message decrypt করে
Bob তার private key ব্যবহার করে:  

**M** = Decrypt(SK_Bob, C)

এবং সে আসল message পড়ে।

---

## 🔐 কেন এটা Secure?

**Attack কেন কাজ করে না**

- Hacker message intercept করল → Ciphertext unreadable  
- Hacker public key পেল → Private key ছাড়া decrypt অসম্ভব  
- Server message দেখল → Encryption থাকার কারণে useless

## 🧠 Mathematical Foundation (সংক্ষেপে)

### 🔸 RSA
- দুটি বড় prime সংখ্যা: **p**, **q**  
- **n** = p × q  
- Security নির্ভর করে prime factorization-এর difficulty-র উপর

### 🔸 ECC (Elliptic Curve Cryptography)
- Elliptic curve discrete logarithm problem  
- কম key size-এ বেশি security

## 🔑 Authentication Problem (খুব গুরুত্বপূর্ণ)

**সমস্যা:**  
Public key আসলেই Bob-এর কিনা, আমি কীভাবে জানবো?

**সমাধান:**
- Digital Certificate  
- Certificate Authority (**CA**)  
(HTTPS, Signal, WhatsApp এসব এই পদ্ধতি ব্যবহার করে)

## 🧩 Real-Life Example

| Application   | কী ব্যবহার করে                              |
|---------------|---------------------------------------------|
| WhatsApp      | Public key + Symmetric key                  |
| Signal        | Double Ratchet + Public Key Cryptography    |
| Email (PGP)   | Public key cryptography                     |
| HTTPS         | RSA / ECC                                   |

## ✨ সংক্ষেপে পুরোটা এক লাইনে

তুমি বন্ধুর public key দিয়ে message encrypt করো → message পাঠাও → বন্ধু তার private key দিয়ে decrypt করে → কেউ মাঝখানে পড়তে পারে না