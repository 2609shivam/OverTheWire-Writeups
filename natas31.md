# 🧪 Natas 31

## 🎯 Objective
Obtain the password for **Natas 32**.

---

## 👀 Observation
- Website provides a **CSV file upload** feature.
- Uploaded files are processed server-side.
- The backend uses a **Perl script (`index.pl`)** to handle the uploaded CSV.
- The application passes **request parameters directly to the script**.
- The script relies on `@ARGV` for processing input.

---

## 🚨 Vulnerability
**Type:**  
- Command Injection / Argument Injection (ARGV injection)

**Root Cause:**  
The backend Perl script uses **command-line arguments (`@ARGV`)** derived directly from **user-controlled multipart form fields**.
Because the script does not validate or restrict these arguments, an attacker can inject arbitary arguments, causing the script to 
**read unintended files**, including sensitive system files.

---

## 🛠️ Exploitation Steps
1. Intercepted the file upload request using a proxy.
2. Observed that multiple `file` fields are accepted in the multipart request.
3. Added a **fake form field named** `file` with the value:
   ```nginx
   ARGV
   ```
4. Modified the request path to:
   ```bash
   /index.pl?/ect/natas_webpass/natas32
   ```
5. Uploaded a valid CSV file to keep the request structure intact.
6. The Perl script interpreted the injected parameter as a command-line argument.
7. The script treated `/etc/natas_webpass/natas32` as an input file.
8. The contents of the password file were processed and returned in the response.
9. Retrieved the password for **Natas 32**.

---

## 💻 Key Payload / Command
**Request path manipulation**:
```bash
POST /index.pl?/etc/natas_webpass/natas32 HTTP/1.1
```
**Multipart argument injection**:
```text
Content-Disposition: form-data; name="file";

ARGV
```
**Legitimate CSV upload (to avoid errors)**:
```csv
1,2,
3,4,
```

---

## 📖 Key Takeaways
- Command injection does not always require shell metacharacters.
- Argument injection via `@ARGV` is extermely powerful and often overlooked.
- Multipart form fields can be abused to inject unexpected arguments.
- Scripts must strictly validate **both parameters and execution context**.
- Never trust user-input to populate command-line arguments.
  
---

## 🖼️ Screenshots 
<img width="1302" height="756" alt="image" src="https://github.com/user-attachments/assets/31cd8e7a-456e-49a1-853a-706b699ca033" /> <br>

*Password redacted for ethical reasons*
