# 🧪 Natas 4

## 🎯 Objective
Obtain the password for **Natas 5**.

---

## 👀 Observation
- Website displays a message saying access is not allowed.
- Page indicates that users are visiting from an **unauthorized location**.
- No useful information is visible on the webpage.
- Access seems to depend on where the request is coming from.

---

## 🚨 Vulnerability
**Type:**  
- Logic flaw / Trusting client-side headers

**Root Cause:**  
The application **trusts the HTTP** Referer header to validate access.
Since HTTP headers are fully controlled by the client, an attacker can **forge the** `Referer` **value** and bypass the restriction.

---

## 🛠️ Exploitation Steps
1. Opened the Natas 4 webpage.
2. Observed the message indicating an invalid referrer.
3. Intercepted the request using a proxy tool (Burp Suite).
4. Modified the `Referer` header to:
   ```sh
   http://natas5.natas.labs.overthewire.org/
   ```
5. Sent the modified request.
6. Retrieved the password for **Natas 5** from the response.

---

## 💻 Key Payload / Command
```bash
# Modified the Referer header
Referer: http://natas5.natas.labs.overthewire.org/
```

---

## 📖 Key Takeaways
- HTTP headers cannot be trusted for authentication or authorization.
- The `Referer` header is **optional and easily spoofed**.
- Access control must always be enforced on the server side.
- Client-controlled data should never decide security logic.
  
---

## 🖼️ Screenshot 
<img width="960" height="540" alt="image" src="https://github.com/user-attachments/assets/39e1f2d4-8107-441d-a0cf-37f01bca0d56" /> <br> 
*Password redacted for ethical reasons*
