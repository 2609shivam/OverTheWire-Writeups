# 🧪 Natas 24

## 🎯 Objective
Obtain the password for **Natas 25**.

---

## 👀 Observation
- Website displays a **password input field**.
- Submitting incorrect input returns **"Wrong password""**.
- Page source reveals a PHP comparison using `strcmp()`.
- User input is taken directly from request parameters.

---

## 🚨 Vulnerability
**Type:**  
- PHP Type Juggling / Logic flaw

**Root Cause:**  
The application uses `strcmp()` for password comparison **without validating the input type**.
In PHP, if an **array** is passed instead of a string, `strcmp()` returns `NULL`, which 
can be interpreted in a way that **bypasses the check**.

---

## 🛠️ Exploitation Steps
1. Viewed the page source to understand the password comparison logic.
2. Noted that `strcmp($input, $password)` is used.
3. Crafted a request that sends the password as an **array**.
4. Submitted the request with: `passwd[]=anything`
5. PHP treated the input as an array, causing `strcmp()` to behave unexpectedly.
6. The condition was bypassed.
7. Retrieved the password for **Natas 25**.

---

## 💻 Key Payload / Command
```bash
?passwd[]=anything
(Submitted via request parameter)
```

---

## 📖 Key Takeaways
- PHP performs **automatic type juggling**, which can be dangerous.
- Functions expecting strings may behave incorrectly when given arrays.
- Input types must be strictly validated before comparisons.
- Security logic should never rely on loose or unchecked comparisons.

---

## 🖼️ Screenshots 
<img width="450" height="230" alt="image" src="https://github.com/user-attachments/assets/ffbe17c3-0528-4fef-bb89-a2c6595a4d9a" /> <br>

*Password redacted for ethical reasons*
