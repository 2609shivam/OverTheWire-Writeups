# 🧪 Natas 6

## 🎯 Objective
Obtain the password for **Natas 7**.

---

## 👀 Observation
- Website displays a form asking for a secret value.
- Submitting random input returns “Wrong secret”.
- Page source contains PHP code that references an **external file**.
- The secret itself is not hardcoded directly in the main file.

---

## 🚨 Vulnerability
**Type:**  
- Source code disclosure / Misconfiguration

**Root Cause:**  
The application includes a **server-side PHP file** (`includes/secret.inc`) that contains sensitive data.
This file is stored in a web-accessible location and can be directly accessed by users, leading to disclosure of the secret.

---

## 🛠️ Exploitation Steps
1. Viewed the page source of the Natas 6 webpage.
2. Noticed a PHP include statement referencing `includes/secret.inc`.
3. Manually navigated to the file:
   ```sh
   http://natas6.natas.labs.overthewire.org/includes/secret.inc
   ```
4. Found the secret value defined in the file.
5. Submitted the extracted secret through the form.
6. Retrieved the password for **Natas 7**.

---

## 💻 Key Payload / Command
```bash
# Direct access to included file
http://natas6.natas.labs.overthewire.org/includes/secret.inc
```

---

## 📖 Key Takeaways
- Included files can still be accessed directly if improperly protected.
- Sensitive configuration or secret files must be placed **outside the web root**.
- Source code disclosure often leads to full application compromise.
- Never assume users cannot guess or access internal paths.
  
---

## 🖼️ Screenshots
<img width="1919" height="1021" alt="image" src="https://github.com/user-attachments/assets/4494926a-c6ba-4027-84be-d25e6f736bec" />
<img width="524" height="82" alt="image" src="https://github.com/user-attachments/assets/3d25d445-5fc0-4c89-8827-b61ae7773d06" />
<img width="707" height="242" alt="image" src="https://github.com/user-attachments/assets/f688809c-c8e0-4135-aa26-951d3fc50edf" /> <br>

*Password redacted for ethical reasons*
