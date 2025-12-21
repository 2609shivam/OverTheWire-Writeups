# 🧪 Natas 8

## 🎯 Objective
Obtain the password for **Natas 9**.

---

## 👀 Observation
- Website presents a form asking for a secret.
- Submitting random input returns **“Wrong secret”**.
- Page source reveals PHP code responsible for validating the secret.
- The secret is compared after applying a **custom encoding function**.

---

## 🚨 Vulnerability
**Type:**  
- Encoding flaw / Logic flaw 

**Root Cause:**  
The application stores the secret in an **encoded form** and exposes the **exact encoding logic** in the client-visible source code.
Since the encoding process is **reversible**, an attacker can decode the stored value to recover the original secret.

---

## 🛠️ Exploitation Steps
1. Viewed the page source and identified the encoding function:
   - Base64 encoding
   - String reversal
   - Hex encoding
2. Noted the stored encoded value.
3. Reversed the operations in the correct order:
   - Hex decode
   - Reverse the string
   - Base64 decode
4. Recovered the original secret.
5. Submitted the decoded secret in the form.
6. Retrieved the password for **Natas 9**.

---

## 💻 Key Payload / Command
```bash
# Step 1: Hex decode
echo "3d3d516343746d4d6d6c315669563362" | xxd -r -p

# Step 2: Reverse the string
echo "==QcCtmMml1ViV3b" | rev

# Step 3: Base64 decode
echo "b3ViV1lmMmtCcQ==" | base64 -d
```

---

## 📖 Key Takeaways
- Encoding is not encryption and provides no real security.
- Exposing transformation logic allows attackers to reverse secrets.
- Secrets should never be stored or verified using reversible schemes.
- Server-side secrets must remain inaccessible to users at all times.
  
---

## 🖼️ Screenshots 
<img width="725" height="319" alt="image" src="https://github.com/user-attachments/assets/99dab6eb-f02f-494a-bddd-10f85b24ff79" />
<img width="729" height="224" alt="image" src="https://github.com/user-attachments/assets/ee68584f-6ed2-46da-a657-64ad612ca2ec" /> <br>

*Password redacted for ethical reasons*
