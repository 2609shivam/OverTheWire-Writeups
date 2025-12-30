# 🧪 Natas 15

## 🎯 Objective
Obtain the password for **Natas 16**.

---

## 👀 Observation
- Website provides a **username input field**.
- The page responds with :
  - **"This user exists."** or
  - **"This user doesn't exist."**
- No password field is present.
- Response behaviour changes based on backend query results.

---

## 🚨 Vulnerability
**Type:**  
- Blind SQL Injection (Boolean-based)

**Root Cause:**  
The application embeds user input directly into an SQL query and reveals **boolean-based responses** depending on whether the query condition evaluates to true or false.
Although it doesn't reveal the password directly, the response can be used as an **oracle** to infer it character by character.

---

## 🛠️ Exploitation Steps
1. Entered a valid username (`natas16`) to observe a positive response.
2. Injected SQL conditions into the username field.
3. Used conditional queries to test whether specific characters of the password match.
4. Observed the response:
   - "This user exists." -> condition is **true**
   - "This user doesn't exist." -> condition is **false**
5. Repeated the process for each character position.
6. Reconstructed the full password for **Natas 16**.

---

## 💻 Key Payload / Command
```bash
natas16" AND BINARY SUBSTRING(password,<position>,1)="<char>" #
```

---

## 📖 Key Takeaways
- Blind SQL injection relies on **response behaviour**, not direct output.
- Even minimal feedback can fully leak sensitive data.
- Boolean-based SQLi is slow but extremely powerful.
- Proper input sanitization and prepared statements completely prevent this attack.
  
---

## 🖼️ Screenshots 
<img width="879" height="466" alt="image" src="https://github.com/user-attachments/assets/db8d665b-32f4-49e7-9b67-afb616769f34" />
<img width="1862" height="846" alt="image" src="https://github.com/user-attachments/assets/16ff4b5e-96d9-4e8d-b935-164e6c55c0c4" />
<img width="1822" height="667" alt="image" src="https://github.com/user-attachments/assets/fbfb2726-b52e-4220-8471-42c19344c3b8" /><br>
