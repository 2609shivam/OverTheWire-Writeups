# 🧪 Natas 20

## 🎯 Objective
Obtain the password for **Natas 21**.

---

## 👀 Observation
- Website provides a form to **set a name**.
- A session cookie (`PHPSESSID`) is used.
- The page behaves differently depending on stored session values.
- No direct option to login as admin is provided.

---

## 🚨 Vulnerability
**Type:**  
- Session handling flaw / Session data injection

**Root Cause:**  
The application stores session data in a **custom key=value format** and blindly appends user input into the session file.
Because user input is **not sanitized**, an attacker can inject **additional session variables**, including `admin=1`. 

---

## 🛠️ Exploitation Steps
1. Submitted a normal username to observe baseline behaviour.
2. Reviewed the source code and noticed session data is stored as `key value` pairs line by line.
3. Crafted a username containing a **newline character**.
4. Injected an additional session variable: `admin 1`
5. Submitted the malicious username using **Burp Repeater**.
6. Reloaded the page using same session.
7. Server interpreted the injected value as a valid session variable.
8. Admin privileges were granted.
9. Retrieved the password for **Natas 21**.

---

## 💻 Key Payload / Command
Injected username value using Burp Repeater:
```bash
test%0a%20admin%201 
```
(Values are URL encoded)

---

## 📖 Key Takeaways
- Custom session implementations are **extremely dangerous**.
- User input must never be written directly into sessions storage.
- Newline injection can be used to manipulate structured data.
- Authorization must be enforced independently of sessiond data.
  
---

## 🖼️ Screenshots 
<img width="721" height="446" alt="image" src="https://github.com/user-attachments/assets/4b369bbc-2c11-4a71-bbdf-30f8f1170482" />
<img width="710" height="409" alt="image" src="https://github.com/user-attachments/assets/fb295715-9552-4e90-9ebb-75855168559d" /> <br>

*Password redacted for ethical reasons*
