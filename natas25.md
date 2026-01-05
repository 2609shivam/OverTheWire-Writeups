# 🧪 Natas 25

## 🎯 Objective
Obtain the password for **Natas 26**.

---

## 👀 Observation
- Website displays a **language selecetion feature**.
- The selected language is passed via a `lang` parameter.
- Page source reveals that the value of `lang` is **included as a file**.
- Error messages reveal paths related to **log files**.
- The application logs user-controlled data.

---

## 🚨 Vulnerability
**Type:**  
- Local File Inclusion (LFI)
- Log Poisioning

**Root Cause:**  
The application includes files based on a **user-controlled parameter** without proper sanitization.
Additionally, user input is written into server **log files**, which can later be included via LFI, resulting in
**remote code execution**.

---

## 🛠️ Exploitation Steps
1. Observed that the `lang` parameter is used to include language files.
2. Tested path traversal using: `....//`
3. Identified that log files are stored in a predictable location.
4. Injected PHP code into the logs via the **User-Agent** header.
5. Used the `lang` parameter to include poisioned log file.
6. Executed the injected PHP code.
7. Read the password file for **Natas 26**.

---

## 💻 Key Payload / Command
**Log poisioning (User-Agent injection):**
```bash
User-Agent: <?php echo shell_exec("cat /etc/natas_webpass/natas26"); ?>
```
**LFI payload**:
```bash
/?lang=....//....//natas25/logs/natas25_PHPSESSID.log
```

---

## 📖 Key Takeaways
-  Local File Inclusion becomes far more dangerous when combined with **log poisioning**.
-  Logs often contain **user-controlled data** and should be treated as untrusted.
-  Input validation and allow-listing are essential for file inclusion logic.
-  Storing logs in web-reachable paths can lead to full compromise.
  
---

## 🖼️ Screenshots 
<img width="914" height="186" alt="image" src="https://github.com/user-attachments/assets/e061713f-bb30-4c63-b2b4-118c6eeb9f0f" />
<img width="716" height="410" alt="image" src="https://github.com/user-attachments/assets/7f177e9c-ee03-4e81-9f34-458edcaaf8d0" /> <br>

*Password redacted for ethical reasons*
