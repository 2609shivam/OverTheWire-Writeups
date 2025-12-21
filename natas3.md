# 🧪 Natas 3

## 🎯 Objective
Obtain the password for **Natas 4**.

---

## 👀 Observation
- Website displays a simple message with no visible password.
- No useful information is revealed in the page source.
- A hint on the page suggests that **"something related to search engines"**.
- This hint implies something intended for **automated crawlers** rather than users.

---

## 🚨 Vulnerability
**Type:**  
- Misconfiguration / Information disclosure

**Root Cause:**  
The website exposes sensitive information through the `robots.txt` file.
This file is intended to guide search engine crawlers, but it is **publicly accessible** and can reveal hidden or restricted paths.

---

## 🛠️ Exploitation Steps
1. Opened the Natas 3 webpage and noted the hint about “humans.”
2. Checked the `robots.txt` file by navigating to:
   ```sh
   http://natas3.natas.labs.overthewire.org/robots.txt
   ```
3. Found a disallowed directory listed in the file.
4. Navigated to the hidden directory.
5. Located a file containing the password for **Natas 4**.

---

## 💻 Key Payload / Command
```bash
# Accessing robots.txt
http://natas3.natas.labs.overthewire.org/robots.txt
```

---

## 📖 Key Takeaways
- `robots.txt` is not a security mechanism—it only provides instructions to crawlers.
- Attackers routinely check `robots.txt` for hidden or sensitive paths.
- Never rely on “security through obscurity” for protecting confidential resources.
- Any publicly accessible file can be inspected and abused.
  
---

## 🖼️ Screenshot 
<img width="1186" height="133" alt="image" src="https://github.com/user-attachments/assets/a3eedba3-fac0-484b-bd6a-98907812b47c" /> 
<img width="810" height="317" alt="image" src="https://github.com/user-attachments/assets/56c45ce9-4ecf-4901-864c-c28248cbfce8" />
<img width="505" height="53" alt="image" src="https://github.com/user-attachments/assets/1d3e6115-7184-4662-b1ef-c27f11448f96" />
<br> <br>

*Password redacted for ethical reasons*
