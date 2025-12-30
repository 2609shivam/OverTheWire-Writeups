# 🧪 Natas 17

## 🎯 Objective
Obtain the password for **Natas 18**.

---

## 👀 Observation
- Website provides a **username input field**, similar to Natas 15.
- No visible password or direct output is shown.
- The page **does not display different messages** for true/false conditions.
- However, **reponse time changes** based on certain inputs.

---

## 🚨 Vulnerability
**Type:**  
- Blind SQL Injection (time-based)

**Root Cause:**  
User input is directly embedded into an SQL query without sanitization.
Although no input is reflected in the response, the application leaks information via **time delays**,
which can be used as a side channel to infer database values.

---

## 🛠️ Exploitation Steps
1. Entered a normal username to observe baseline response time.
2. Injected SQL conditions that introduce a **delay** (**SLEEP**) when a condition is true.
3. Measured the server's response time for each request.
4. Used conditional queries to check characters of the password one by one.
5. Observed:
   - **Delayed response** -> condition is **true**
   - **Normal response** -> condition is **false**
6. Automated the attack usind **Burp Intruder** to brute-force the password character by character.
7. Reconstructed the full password for **Natas 18**.

---

## 💻 Key Payload / Command
```bash
natas18" AND IF(SUBSTRING(password,<position>,1)="<char>", SLEEP(5), 0) #
```

---

## 📖 Key Takeaways
- Lack of output does not mean lack of vulnerability.
- Time-based side channels can fully leak sensitive data.
- Blind SQL injection is powerful but requires automation.
- Proper use of prepared statements prevents all forms of SQL injection.
  
---

## 🖼️ Screenshots 
<img width="873" height="546" alt="image" src="https://github.com/user-attachments/assets/ae241bd7-8c08-4c7e-83bf-e90d5afd70b5" />
<img width="1916" height="920" alt="image" src="https://github.com/user-attachments/assets/e10ab8d9-4f35-4c6f-a878-3d03f1a0ee0a" />
<img width="1817" height="782" alt="image" src="https://github.com/user-attachments/assets/9eaac781-11b3-4c3b-a115-8a85b4ddda88" /> <br>

*Password redacted for ethical reasons*
