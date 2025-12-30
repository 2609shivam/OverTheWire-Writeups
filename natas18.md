# 🧪 Natas 18

## 🎯 Objective
Obtain the password for **Natas 19**.

---

## 👀 Observation
- Website displays a **login form** asking for a username.
- After logging in, the page shows a message indicating whether the user is **admin or not**.
- A session cookie named `PHPSESSID` is assigned.
- Logging in multiple times generate **different numeric session IDs**.

---

## 🚨 Vulnerability
**Type:**  
- Insecure session management / Predictable session IDs

**Root Cause:**  
The application uses **predictable, numeric session IDs** and assigns admin privileges based solely on the session ID value.
There is no proper authentication or access control verifying whether a session truly belongs to an admin user. 

---

## 🛠️ Exploitation Steps
1. Logged in with a normal username.
2. Observed the assigned `PHPSESSID` cookie.
3. Noted that session IDs are **small integers** (e.g., 1-1000)
4. Assumed that one of the session IDs belongs to the **admin user**.
5. Used **Burp Intruder** to brute-force session IDs by manually setting the `PHPSESSID` cookie.
6. Iterated through all possible session IDs.
7. Identified the session ID where the response indicated **admin access**.
8. Retrieved the password for **Natas 19**.

---

## 💻 Key Payload / Command
```bash
# No payload required
# Vulnerability exploited using Burp Suite
```

---

## 📖 Key Takeaways
- Session IDs must be **unpredictable** and **securely generated**.
- Authorization must never solely rely on session identifiers.
- Predictable sessions enable **privilege escalation**.
  
---

## 🖼️ Screenshots 
<img width="935" height="448" alt="image" src="https://github.com/user-attachments/assets/00a583a7-50a1-44e3-968c-e872932d8361" />
<img width="452" height="148" alt="image" src="https://github.com/user-attachments/assets/964fab1d-6473-480c-8d55-cfc20e1423f5" /> <br>

*Password redacted for ethical reasons*
