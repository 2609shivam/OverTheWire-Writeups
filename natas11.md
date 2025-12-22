# 🧪 Natas 11

## 🎯 Objective
Obtain the password for **Natas 12**.

---

## 👀 Observation
- Website displays a page that allows changing **background color**.
- A cookie named `data` is set in the browser.
- Page source shows PHP code that **encrypts and decrypts the cookie**.
- The cookie value looks like **random encoded data**.

---

## 🚨 Vulnerability
**Type:**  
- Cryptographic flaw / Logic flaw (XOR encryption misuse)

**Root Cause:**  
The application uses **XOR encryption with a repeating key** to protect cookie data.
The encryption logic is exposed in the source code, and XOR is reversible if plaintext is known.
Since part of the plaintext (`bgcolor=...`) is predictable, the encryption key can be recovered.

---

## 🛠️ Exploitation Steps
1. Viewed the page source and analyzed the encryption function.
2. Identified the XOR encryption is used with a repeating secret key.
3. Observed that the cookie decrypts to a known format: <br>
   `bgcolor=#ffffff`
4. XORed the known plaintext with the encrypted cookie value to recover the key.
5. Used the recovered key to encrypt a modified payload:<br>
   `bgcolor=#ffffff; showpassword="yes"`
6. Replaced the `data` cookie with the newly encrypted value.
7. Refreshed the page.
8. Retrieved the password for **Natas 12**.

---

## 💻 Key Payload / Command
```bash
# XOR logic (conceptual)
encrypted ^ plaintext = key
plaintext ^ key = encrypted
```

---

## 📖 Key Takeaways
- XOR encryption is **not secure** when used with predictable plaintext.
- Repeating keys make XOR trivial to break.
- Client-side encrypted cookies should never be trusted for authorization.
- Custom cryptography almost always leads to vulnerabilities.
  
---

## 🖼️ Screenshots 
<img width="1308" height="948" alt="image" src="https://github.com/user-attachments/assets/6e8c393d-6f9c-42aa-af8f-3e681a338de7" />
<img width="1486" height="341" alt="image" src="https://github.com/user-attachments/assets/abfdaa60-f57c-4fa1-b95d-5be177668488" />
<img width="1258" height="593" alt="image" src="https://github.com/user-attachments/assets/52d86cdd-7b97-476b-8659-ee547570e68e" />
<img width="1252" height="569" alt="image" src="https://github.com/user-attachments/assets/2c5aeaac-08e0-4edb-8744-3822c6b86b4c" />
<img width="454" height="164" alt="image" src="https://github.com/user-attachments/assets/cc8b315d-5404-4c48-916e-330b94fe437d" /> <br>

*Password redacted for ethical reasons*
