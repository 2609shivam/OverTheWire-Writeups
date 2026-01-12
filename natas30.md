# 🧪 Natas 30

## 🎯 Objective
Obtain the password for **Natas 31**.

---

## 👀 Observation
- Website provides a **login form** with username and password fields.
- Submitting incorrect credentials returns **"Login failed"**.
- Page source shows a SQL query using **prepared-looking logic**, but with unusual handling of input.
- The backend uses **PHP arrays** when processing request parameters.

---

## 🚨 Vulnerability
**Type:**  
- SQL Injection / PHP Type Juggling

**Root Cause:**  
The application passess user input directly into an SQL query **without enforcing scalar inputs**.
By sending parameters as **arrays**, PHP handles them differently, resulting in malformed SQL logic that can be exploited to bypass authentication.

---

## 🛠️ Exploitation Steps
1. Viewed the page source to understand how login parameters are processed.
2. Noticed that `username` and `password` are taken directly from request parameters.
3. Crafted a requested with multiple `password` parameter to be interpreted as an **array** instead of a string.
4. Submitted the request with: `password='whatever' or 1&password=4`
5. PHP converted the array into an unexpected value during SQL query construction.
6. The SQL condition evaluated in a way that bypassed authentication.
7. Successfully logged in as the target user.
8. Retrieved the password for **Natas 31**.
   
---

## 💻 Key Payload / Command
```bash
username=natas31&password='whatever' or 1&password=4
```

---

## 📖 Key Takeaways
- PHP's flexible typing can introduce **critical security flaws**.
- SQL queries must enforce **strict input validation**.
- Arrays should never be accepted where strings are expected.
- Even partial "protection" fails when input types are not controlled.
  
---

## 🖼️ Screenshots 
<img width="717" height="441" alt="image" src="https://github.com/user-attachments/assets/1b3fcc38-dd87-4f42-a31f-9e86c31bed5a" /> <br>

*Password redacted for ethical reasons*
