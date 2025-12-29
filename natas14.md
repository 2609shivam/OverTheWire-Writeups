# 🧪 Natas 14

## 🎯 Objective
Obtain the password for **Natas 15**.

---

## 👀 Observation
- Website displays a **login form** asking for a username and password.
- Submitting random credentials results in **"Access Denied"**.
- No client-side validation is present.
- Page behaviour suggests a backend **database query** is being used for authentication.

---

## 🚨 Vulnerability
**Type:**  
- SQL Injection (authentication bypass)

**Root Cause:**  
User input is **directly embedded into an SQL query** without sanitization or prepared statements.
This allows an attacker to manipulate the query logic and bypass authentication checks.

---

## 🛠️ Exploitation Steps
1. Entered random credentials to observe normal behaviour.
2. The backend query resembles:
   ```sql
   SELECT * FROM users WHERE username="input" AND password="input";
   ```
3. Injected a crafted SQL payload into the username field.
4. Used a condition that always evaluates to **true**.
5. Submitted the form with the injected payload.
6. Successfully bypassed authentication.
7. Retrieved the password for **Natas 15**.
   
---

## 💻 Key Payload / Command
```bash
Username: " OR 1=1 --
Password: anything
```

---

## 📖 Key Takeaways
- SQL queries must never be constructed using raw user input.
- Authentication logic is a high-value target for attackers.
- Prepared statements and parameterized queries prevent SQL injection.
  
---

## 🖼️ Screenshots 
<img width="1336" height="418" alt="image" src="https://github.com/user-attachments/assets/bdc1a172-948a-49e3-9c71-a518c3aa67e1" />
<img width="909" height="305" alt="image" src="https://github.com/user-attachments/assets/df12b92b-d5e3-4280-bfaf-e17a63473aa5" />
<img width="454" height="124" alt="image" src="https://github.com/user-attachments/assets/499f327c-59b0-44ec-a69f-44e151ea4d1a" /> <br>

*Password redacted for ethical reasons*
