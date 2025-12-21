# 🧪 Natas 2

## 🎯 Objective
Obtain the password for **Natas 3**.

---

## 👀 Observation
- Website displays a simple page with an image and a short message.
- No password is visible on the page itself.
- Source code does not directly reveal the password.
- An image file is loaded from a directory named `files/`.

---

## 🚨 Vulnerability
**Type:**  
- Misconfiguration / Directory exposure

**Root Cause:**  
The web server allows public access to a directory (`/files/`) that should not be exposed.
This directory contains sensitive files, including a text file with credentials, and directory listing is enabled.

---

## 🛠️ Exploitation Steps
1. Opened the **page source** of the Natas2 webpage.
2. Noticed an image being loaded from the path /files/.
3. Manually navigated to:
   ```sh
   http://natas2.labs.overthewire.org/files/
   ```
4. Found a file named `users.txt` inside the directory.
5. Opened `users.txt` to retrieve the password for **Natas 3**.

---

## 💻 Key Payload / Command
```bash
# Direct browser access
http://natas2.natas.labs.overthewire.org/files/users.txt
```

---

## 📖 Key Takeaways
- **Directory listing should always be disabled** in production environments.
- Sensitive files must never be stored in publicly accessible web directories.
- Attackers often look for **hidden paths referenced by static resources** like images or scripts.
  
---

## 🖼️ Screenshot 
<img width="785" height="200" alt="image" src="https://github.com/user-attachments/assets/aadfc8ef-e7c4-4526-a644-fb102443b8ac" />
<img width="239" height="103" alt="image" src="https://github.com/user-attachments/assets/529e7b45-fbe0-48ed-96db-fe4fdb7a0443" />
*Password redacted due to ethical reasons*
