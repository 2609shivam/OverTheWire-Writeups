# 🧪 Natas 27

## 🎯 Objective
Obtain the password for **Natas 28**.

---

## 👀 Observation
- Website provides a **login and user creation** functionality.
- Username appears to have a **maximum length restriction**.
- Attempting to login as `natas28` directly is not possible.
- Backend uses a database to store usernames and passwords.

---

## 🚨 Vulnerability
**Type:**  
- SQL Logic Flaw / Truncation issue

**Root Cause:**  
The application truncates usernames to a fixed length **before storing them in the database**,
but comparisons during login are done in a way that allows **multiple usernames to resolve to the same truncated value**.
This enables an attacker to create a new user whose truncated username collides with an existing privileged user.

---

## 🛠️ Exploitation Steps
1. Reviewed the page source to understand username handling.
2. Noted that the usernames are truncated to a fixed length (64 characters).
3. Created a new user with a username crafted as: `natas28<extra_characters>` <br>
such that truncataion results in `natas28`.
4. Set a known password for the crafted user.
5. Logged in using the truncated username.
6. Backend mathced the truncated value to the **real** `natas28` **user**.
7. Successfully authenticated as `natas28`.
8. Retrieved the password for **Natas 28**.

---

## 💻 Key Payload / Command
**Crafted Username** (spaces URL encoded as '+'):
```bash
natas28+++++++++++++++++++++++++++++++++++++++++++++++++++++++++X
```
**Login Username**:
```bash
natas28+++++++++++++++++++++++++++++++++++++++++++++++++++++++++
```
(X being the 65th character, gets truncated)

---

## 📖 Key Takeaways
- Truncation-based logic flaws can lead to **account takeover**.
- Usernames must be validated and compared **consistently**.
- Database field length limits must align with application logic.
- Logic flaws in authentication are as dangerous as injection bugs.
  
---

## 🖼️ Screenshots 
<img width="1443" height="825" alt="image" src="https://github.com/user-attachments/assets/6d8eee72-6661-4d28-a0f8-37354be9a65d" />
<img width="722" height="410" alt="image" src="https://github.com/user-attachments/assets/ca90709b-ec53-4e35-853b-1583a700d179" /> <br>

*Password redacted for ethical reasons*
