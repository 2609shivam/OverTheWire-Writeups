# Natas 1

## Objective
Obtain the password for **Natas 2**.

---

## Observation
- The webpage displays a message indicating that **right-click has been disabled**
- Attempting to view source via right-click does not work
- The page otherwise looks similar to Natas 0

---

## Vulnerability
**Type:**  
- Client-side restriction / Source code disclosure

**Root Cause:**  
The application relies on **client-side controls** (disabling right-click) to prevent users from viewing the page source.  
Client-side restrictions can be easily bypassed and do not provide real security.

---

## Exploitation Steps
1. Used the browser menu (`View Page Source`) or keyboard shortcut (`Ctrl+U`)
2. Inspected the HTML source directly
3. Located the password embedded in an HTML comment
4. Copied the password for the next level

---

## Key Payload / Command
```bash
# No payload required
# Used browser source view (Ctrl+U)
```

---

## Key Takeaways
- Client side restrictions are not security controls.
- Disabling right-click does not prevent source code inspection.
- Sensitive information should never be exposed in client-side code.
