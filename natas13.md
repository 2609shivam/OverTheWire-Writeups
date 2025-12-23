# 🧪 Natas 13

## 🎯 Objective
Obtain the password for **Natas 14**.

---

## 👀 Observation
- Webiste provides a **file upload** functionality similar to Natas 12.
- The page claims that **only image files** are allowed.
- Uploading a PHP file directly is rejected.
- Server now performs additional checks compared to the previous levels.

---

## 🚨 Vulnerability
**Type:**  
- File upload vulnerability / MIME type validation bypass

**Root Cause:**  
The application validates uploaded files based on the **MIME type provided by the client**.
Since MIME types can be easily **forged**, an attacker can disguise a malicious file as an image while still executing server-side code.

---

## 🛠️ Exploitation Steps
1. Created a PHP file containing code to read the password file.
2. Renamed the file extension to `.jpg`.
3. Intercepted the upload request using a proxy tool.
4. Modified the file header: `GIF89a`
5. Uploaded the modified file successfully.
6. Accessed the uploaded file via the generated link.
7. Executed the embedded PHP code.
8. Retrieved the password for **Natas 14**.

---

## 💻 Key Payload / Command
**Malicious File Content**:
```bash
GIF89a
<?php
echo file_get_contents("/etc/natas_webpass/natas14");
?>
```

---

## 📖 Key Takeaways
- MIME types provided by clients are **not trustworthy**.
- File content and extension must be validated server-side.
- Upload directories should never allow **script execution**.
- Defense-in-depth is required for secure file uploads.
  
---

## 🖼️ Screenshots 
<img width="915" height="379" alt="image" src="https://github.com/user-attachments/assets/12403a3c-5707-4d7d-b2ed-7e41fa50e330" />
<img width="907" height="266" alt="image" src="https://github.com/user-attachments/assets/4cc8d506-a375-4c2a-a9b1-07c3a72f84b1" /> <br>

*Password redacted for ethical reasons*
