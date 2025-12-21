# 🧪 Natas 7

## 🎯 Objective
Obtain the password for **Natas 8**.

---

## 👀 Observation
- Website shows two clickable links: **Home** and **About**.
- Clicking either link loads different content on the same page.
- The URL changes and includes a `page` **parameter**.
- Source code comments hint at the location of the password file.

---

## 🚨 Vulnerability
**Type:**  
- Local File Inclusion (LFI) / Path Traversal

**Root Cause:**  
The application dynamically includes files based on the **user-controlled** `page` parameter without proper validation or sanitization.
This allows attackers to manipulate file paths and include **arbitrary local files** from the server.

---

## 🛠️ Exploitation Steps
1. Clicked the **Home** and **About** links to observe URL behavior.
2. Noticed the URL pattern:
   ```sh
   index.php?page=home
   index.php?page=about
   ```
3. Checked the page source and found a comment mentioning the password file location.
4. Replaced the `page` parameter with the password file path:
   ```bash
   index.php?page=/etc/natas_webpass/natas8
   ```
5. Loaded the modified URL.
6. Retrieved the password for **Natas 8**.
---

## 💻 Key Payload / Command
```bash
# Path traversal via page parameter
http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8
```

---

## 📖 Key Takeaways
- User-controlled parameters must never be directly used in file inclusion logic.
- Local File Inclusion vulnerabilities can expose **sensitive system files**.
- Comments in source code can unintentionally leak critical information.
- Input validation and allow-lists are essential for secure file handling.
---

## 🖼️ Screenshots 
<img width="785" height="271" alt="image" src="https://github.com/user-attachments/assets/dd0366e7-bb66-48f8-956e-10c77f9edc63" />
<img width="722" height="212" alt="image" src="https://github.com/user-attachments/assets/ec196a1a-70fb-4c3f-b747-454a7a812d41" /> <br>

*Password redacted for ethical reasons*
