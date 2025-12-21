# 🧪 Natas X

## 🎯 Objective
Obtain the password for **Natas 1**.

---

## 👀 Observation
- Website shows a simple web webpage with a message indicating that the password is hidden.
- No visible input fields or interactive elements are present.
- Page hints that the password is not directly shown on the UI.

---

## 👨‍💻 Source Code Analysis
- Viewing the page source reveals an HTML comment.
- The password for the next level is present inside this comment.
- The browser does not render HTML comments, making the password invisible during normal browsing.

---
## 🚨 Vulnerability
**Type:**  
- Source code disclosure

**Root Cause:**  
The application embeds sensitive information (password) directly in the client-side HTML source.
Although the password is hidden inside an HTML comment, any user can view the page source, leading to unintended information disclosure.

---

## 🛠️ Exploitation Steps
1. Opened the website for Natas 0.
2. Right-clicked on the page and selected “View Page Source”.
3. Located the HTML comment containing the password.
4. Used the extracted password to log in to Natas 1.

---

## 💻 Key Payload / Command
```bash
# No payload required
# Vulnerability exploited via browser "View Page Source"
```

---

## 📖 Key Takeaways
- HTML comments are not secure and should never contain sensitive data.
- Anything sent to the client can be viewed and analyzed by the user.
- Even the most basic misconfigurations can lead to full credential disclosure.
- Always assume that attackers can see all client-side code.
  
---

## 🖼️ Screenshot 
