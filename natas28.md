# 🧪 Natas 28

## 🎯 Objective
Obtain the password for **Natas 29**.

---

## 👀 Observation
- Website provides a **search funtionality**.
- Search queries return results from a backend database.
- The query parameter appears to be **URL-encoded and encrypted**.
- Direct SQL injection attempts do not work as expected.

---

## 🚨 Vulnerability
**Type:**  
- Cryptographic flaw / SQL Injection (encrypted parameter misuse)

**Root Cause:**  
The applications encrypts the SQL query parameter using a **custom encryption scheme** but
**reuses the same encryption key** for all users.
Because encryption is deterministic and predictable, attackers can **manipulate the ciphertext**
to alter the decrypted SQL query on the server.

---

## 🛠️ Exploitation Steps
1. Submitted a normal search query and captured the request.
2. Observed that the query parameter is **URL-encoded encrypted data**.
3. Sent multiple requests with controlled plaintext input.
4. Compared encrypted outputs to identify block boundaries.
5. Manipulated the encrypted payload to inject **additional SQL logic**.
6. Created a modified encrypted query that appends a **UNION SELECT** statement.
7. Sent the manipulated request to the server.
8. Server decrypted the payload and executed the injected SQL.
9. Retrieved the password for **Natas 29** from the response.

---

## 💻 Key Payload / Command
Conceptual injected SQL logic after decryption:
```sql
UNION SELECT password FROM users -- 
```
(The payload was injected by **modifying the encrypted query parameter**, not by plaintext input.)

---

## 📖 Key Takeaways
- Encryption does **not** automatically make input safe.
- Reusing encryption keys enables **ciphertext manipulation**.
- Deterministic encryption leaks structures and patterns.
- Cryptography must be combined with **proper input validation**.
- Never trust encrypted user input to be safe for SQL queries.

---

## 🖼️ Screenshots 
<img width="959" height="242" alt="image" src="https://github.com/user-attachments/assets/1f4065c1-d7a8-4315-848a-e4f856ad07ad" /> <br>

*Password redacted for ethical reasons*
