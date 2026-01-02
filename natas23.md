# 🧪 Natas 23

## 🎯 Objective
Obtain the password for **Natas 24**.

---

## 👀 Observation
- Website displays a **password input field**.
- Submitting random input returns **"Wrong!**.
- Page source shows a PHP condition that checks whether the input **contains a specific substring**.
- The check is not a strict equality comparison.

---

## 🚨 Vulnerability
**Type:**  
- Logic flaw / Insecure String comparison

**Root Cause:**  
The application validates the password using a **substring check** instead of an exact match.
If the required keyword appears **anywhere inside the input**, the condition evaluates to true,
allowing authentication bypass.

---

## 🛠️ Exploitation Steps
1. Viewed the page source to understand the password validation logic.
2. Noted that the condition checks whether the input **contains** a specific string.
3. Crafted an input that **includes the required keyword** along with extra characters.
4. Submitted the crafted input as password.
5. The condition evaluated to true.
6. Retrieved the password for **Natas 24**.

---

## 💻 Key Payload / Command
```bash
11iloveyou
```

---

## 📖 Key Takeaways
- Authentication checks must use **strict equality**, not substring matching.
- Partial matches can easily be abused.
- Logic flaws are often more dangerous than technical vulnerabilities.
- Always validate credentials exactly as intended.

---

## 🖼️ Screenshots 
<img width="452" height="191" alt="image" src="https://github.com/user-attachments/assets/96d746e1-ef12-4751-aab1-9eaff73332e9" /> <br>

*Password redacted for ethical reasons*
