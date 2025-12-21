# 🧪 Natas 9

## 🎯 Objective
Obtain the password for **Natas 10**.

---

## 👀 Observation
- Website provides an input box to search for a string.
- The result shows output similar to a **Linux `grep` command**.
- Entering normal text returns expected search results.
- No authentication-related fields are present on the page.

---

## 🚨 Vulnerability
**Type:**  
- Command Injection

**Root Cause:**  
The application directly passes **user-supplied input** into a system command without proper sanitization.
Since shell metacharacters are not filtered, an attacker can **inject additional commands** and execute arbitrary system commands.

---

## 🛠️ Exploitation Steps
1. Entered a normal search term to understand application behavior.
2. Observed that the backend executes a shell command similar to `grep`.
3. Injected a command separator (`;`) to break out of the intended command.
4. Appended a command to read the password file.
5. Submitted the malicious input.
6. Password for **Natas 10** was displayed in the response.

---

## 💻 Key Payload / Command
```bash
; cat /etc/natas_webpass/natas10
```

---

## 📖 Key Takeaways
- Never pass user input directly to system commands.
- Command injection can lead to **full server compromise**.
- Input validation and proper escaping are critical.
- Using safe APIs instead of shell execution greatly reduces risk.
  
---

## 🖼️ Screenshots 
<img width="492" height="335" alt="image" src="https://github.com/user-attachments/assets/bf6d0fca-251a-4362-94e5-79329a2008fd" />
<img width="923" height="321" alt="image" src="https://github.com/user-attachments/assets/5d1475c3-650e-4ec0-a7f0-fe19cddc7dc9" />
<img width="454" height="119" alt="image" src="https://github.com/user-attachments/assets/f08e5884-1657-45ac-80e4-47c8bd1ae0d4" /> <br>

*Password redacted for ethical reasons*
