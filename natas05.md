# 🧪 Natas 5

## 🎯 Objective
Obtain the password for **Natas 6**.

---

## 👀 Observation
- Website displays a message indicating that the user is **not logged in**.
- No username or password input fields are present.
- Page suggests that login status is required to view the password.
- Refreshing the page does not change the result.

---

## 🚨 Vulnerability
**Type:**  
- Logic flaw / Insecure cookie handling

**Root Cause:**  
The application relies on a **client-side cookie** (`loggedin`) to determine authentication status.
Since cookies are fully controllable by the client, an attacker can manually modify the cookie value and bypass authentication.

---

## 🛠️ Exploitation Steps
1. Opened the Natas 5 webpage.
2. Checked browser cookies for the site.
3. Found a cookie named `loggedin` set to `0`.
4. Modified the cookie value from `0` to `1`.
5. Refreshed the page.
6. Password for **Natas 6** was revealed.

---

## 💻 Key Payload / Command
```bash
# Using curl with modified cookie
curl -u natas5:<password> \
--cookie "loggedin=1" \
http://natas5.natas.labs.overthewire.org/
```

---

## 📖 Key Takeaways
- Authentication decisions should never be made using client-side data alone.
- Cookies can be edited, deleted, or forged by attackers.
- Server-side session validation is essential for secure authentication.
- Any trust in user-controlled values leads to access control bypasses.
  
---

## 🖼️ Screenshot 
<img width="1040" height="541" alt="image" src="https://github.com/user-attachments/assets/32861367-c946-46c8-89e1-87b99f38be88" />
<img width="959" height="185" alt="image" src="https://github.com/user-attachments/assets/d65cd5a3-2da7-4522-8d9d-e2217605fd31" /> <br>

*Password redacted for ethical reasons*
