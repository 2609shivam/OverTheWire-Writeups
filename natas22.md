# 🧪 Natas 22

## 🎯 Objective
Obtain the password for **Natas 23**.

---

## 👀 Observation
- Website shows a message indicating that **access is forbidden**.
- The page suggests that users are being **redirected away** automatically.
- No password is visible on the page.
- Viewing the source code reveals logic related to **HTTP redirection**.

---

## 🚨 Vulnerability
**Type:**  
- Access control bypass / Forced browsing

**Root Cause:**  
The application uses an **HTTP redirect** (`Location` header) to prevent unauthorized access
but still **processes and generates the protected content** on the server.
The server relies on the browser to follow the redirect instead of enforcing access control server-side.

---

## 🛠️ Exploitation Steps
1. Opened the Natas 22 webpage.
2. Observed that the browser automatically redirects to another page.
3. Intercepted the request using a proxy tool or command-line utility.
4. Prevented the client from following the redirect.
5. Inspected the **raw HTTP response**.
6. Found the password for **Natas 23** in the response body.

---

## 💻 Key Payload / Command
```bash
# Used Burp Repeater to send the request
```

---

## 📖 Key Takeaways
- Redirects are **not access control mechanisms**.
- Sensitive data should never be included in responses for unauthorized users.
- Authorization must be enforced **before generating content**, not after.
- Attackers often inspect **raw HTTP responses**, not just rendered pages.
---

## 🖼️ Screenshots 
<img width="994" height="179" alt="image" src="https://github.com/user-attachments/assets/8a40c18e-abdd-4164-bd37-b5c3a43557dd" />
<img width="1433" height="756" alt="image" src="https://github.com/user-attachments/assets/f5c3b808-562c-43cd-ae9a-c073f55ed38f" /> <br>

*Password redacted for ethical reasons*
