# 🧪 Natas 19

## 🎯 Objective
Obtain the password for **Natas 20**.

---

## 👀 Observation
- Website behaviour is similar to **Natas 18**.
- A session cookie named `PHPSESSID` is used.
- Session ID looks **non-numeric** at first glance.
- Logging in multiple times produced different session IDs.

---

## 🚨 Vulnerability
**Type:**  
- Insecure session management / Encoded predictable session IDs

**Root Cause:**  
The application uses **encoded session IDs** that are actually derived from predictable values
(session number + username).
Although the session IDs appear complex, they are **not random** and can be decoded and brute-forced.

---

## 🛠️ Exploitation Steps
1. Logged in with a normal username.
2. Captured the `PHPSESSID` cookie.
3. Observed that the session ID resembles a **hex-encoded value**.
4. Decoded the session ID to reveal a pattern:
   `<session_number>-<username>`
5. Assumed the admin username is `admin`.
6. Generated encoded session IDs for `admin` with different session numbers.
7. Replaced the `PHPSESSID` cookie with crafted values.
8. Found the session corresponding to **admin access**.
9. Retrieved the password for **Natas 20**.

---

## 💻 Key Payload / Command
```bash
# Used Burp Intruder to brute-force the Admin session ID
```

---

## 📖 Key Takeaways
- Encoding does **not** provide security.
- Session IDs must be **random, not derived from user data.**
- Obscurity fails, when pattern exists.
- Weak session design leads to privilege escalation.
---

## 🖼️ Screenshots 
<img width="1916" height="429" alt="image" src="https://github.com/user-attachments/assets/cd0e24c3-f83f-4580-a73a-169794975173" />
<img width="937" height="539" alt="image" src="https://github.com/user-attachments/assets/fc8245d3-4e68-42aa-8738-7791e21b36fd" />
<img width="454" height="187" alt="image" src="https://github.com/user-attachments/assets/c2734c68-4b7e-462a-9d1b-c9465cefb9aa" /> <br>

*Password redacted for ethical reasons*
