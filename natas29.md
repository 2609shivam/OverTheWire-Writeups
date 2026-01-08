# 🧪 Natas 29

## 🎯 Objective
Obtain the password for **Natas 30**.

---

## 👀 Observation
- Website provides a **file viewing functionality**.
- A parameter is used to specify which file should be opened.
- Input appears to be **filtered or modified**.
- Direct attempts to access sensitive files are blocked.

---

## 🚨 Vulnerability
**Type:**  
- Local File Inclusion (LFI) / Path traversal with filtering bypass

**Root Cause:**  
The application attempts to block directory traversal using **blacklist-based filtering**, but the filtering is incomplete. <br>
By carefully crafting the file path, an attacker can still traverse directories and read **arbitary files** on the server.

---

## 🛠️ Exploitation Steps
1. Tested the file parameter with normal values to observe expected behaviour.
2. Attempted basic path traversal payloads and observed they were filtered.
3. Analyzed how the application modifies or santizes the input.
4. Crafted a traversal payload that bypasses the filter.
5. Used the paylaod to read the password file for the next level.
6. Server successfully included the sensitive file.
7. Retrieved the password for **Natas 30**>

---

## 💻 Key Payload / Command
```bash
cat /etc/n?tas_webpass/n?tas30
```

---

## 📖 Key Takeaways
- Blacklist based filtering is **easy to bypass**.
- Path traversal vulnerabilities remain common and dangerous.
- Input should be validated using **strict allow-lists**, not pattern removal.
- File inclusion logic must never trust user input.
---

## 🖼️ Screenshots 
<img width="1534" height="908" alt="image" src="https://github.com/user-attachments/assets/41583c1c-4398-4076-bd5a-8a9b77a385ab" />
<img width="960" height="283" alt="image" src="https://github.com/user-attachments/assets/a1945c93-29dc-47be-94ad-3965cadd8457" /> <br>

*Password redacted for ethical reasons*
