# 🧪 Natas 21

## 🎯 Objective
Obtain the password for **Natas 22**.

---

## 👀 Observation
- Natas 21 consists of **two related web applications** on different subdomains.
- One application allows users to **set preferences** such as `admin`.
- The main Natas 21 page checks for an **admin session variable**.
- Both applications **share the same session cookie** (`PHPSESSID`).
  
---

## 🚨 Vulnerability
**Type:**  
- Cross site session poisioning / Logic flaw

**Root Cause:**  
Two different applications **share the same session storage** without proper isolation.
The secondary application allows users to set arbitary session variables, which are then 
**trusted by the main application** for authorization decisions.

---

## 🛠️ Exploitation Steps
1. Visited the **secondary application** linked from the Natas 21 page.
2. Noted that it allows setting user preferences via request parameters.
3. Intercepted the request and added: `admin=1`
4. Sent the modified request, which stored `admin=1` in the shared session.
5. Returned to the **main Natas 21 page** using the same session cookie.
6. The application detected `admin=1` in the session.
7. Admin access was granted.
8. Retrieved the password for **Natas 22**.

---

## 💻 Key Payload / Command
```bash
admin=1
```

---

## 📖 Key Takeaways
- Sharing sessions across applications is **dangerous without strict isolation**.
- Authorization decisions must not rely solely on session variables.
- One insecure application can compromise another via shared sessions.
- Cross-application trust boundaries must be carefully designed.
  
---

## 🖼️ Screenshots 
<img width="932" height="655" alt="image" src="https://github.com/user-attachments/assets/f78bfe2b-ba1e-4a7b-8a19-5f0783acdbe2" />
<img width="1440" height="825" alt="image" src="https://github.com/user-attachments/assets/6b1a6acd-8969-4655-a1c0-f7fc1834f2d0" />a
<img width="452" height="197" alt="image" src="https://github.com/user-attachments/assets/e49c69e5-4166-4af4-88a6-8a290d52b774" /> <br>

*Password redacted for ethical reasons*
