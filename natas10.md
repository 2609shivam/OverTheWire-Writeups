# 🧪 Natas 10

## 🎯 Objective
Obtain the password for **Natas 11**.

---

## 👀 Observation
- Website provides a search input similar to Natas 9.
- Backend behavior still resembles a `grep` command.
- Some characters such as `;`, `|`, and `&` are filtered.
- Direct command injection attempts are blocked.

---

## 🚨 Vulnerability
**Type:**  
- Command Injection (filter bypass)

**Root Cause:**  
Although the application attempts to filter dangerous characters, it **still passes user input directly to a shell command**.
The filtering is **incomplete and blacklist-based**, allowing attackers to bypass it using alternative techniques supported by `grep`.

---

## 🛠️ Exploitation Steps
1. Tested normal input to confirm `grep`-like behaviour.
2. Tried common command seperators and observed they were blocked.
3. Noted that `grep` itself can read files when patterns are crafted carefully.
4. Used a newline-based injection technique to force `grep` to read the password file.
5. Submitted a payload that includes the target password file path.
6. Retrieved the password for **Natas 11** from the output.

---

## 💻 Key Payload / Command
```bash
.* /etc/natas_webpass/natas11
```

---

## 📖 Key Takeaways
- Blacklist-based filtering is **never sufficient** for security.
- Even when command separators are blocked, **command behavior can be abused**.
- Understanding how underlying tools work (like `grep`) enables powerful bypasses.
- Proper defense requires **avoiding shell execution entirely** or using strict allow-lists.
---

## 🖼️ Screenshots 
<img width="596" height="431" alt="image" src="https://github.com/user-attachments/assets/53310942-f3c4-4c50-9747-0620c8f7bcea" />
<img width="900" height="363" alt="image" src="https://github.com/user-attachments/assets/9068cfb6-994b-4de8-b460-62ad963b9021" />
<img width="452" height="206" alt="image" src="https://github.com/user-attachments/assets/96887362-93b6-40a1-9863-9f2d74145c1a" /> <br>

*Password redacted for ethical reasons*
