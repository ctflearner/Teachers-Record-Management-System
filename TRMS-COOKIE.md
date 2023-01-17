```
Exploit Title: Teachers Record Management System 1.0 – Cookie without Secure attribute 
Date: 17-01-2023
Vendor Homepage: https://phpgurukul.com
Software Link: https://phpgurukul.com/teachers-record-management-system-using-php-and-mysql/
Version: 1.0
Tested on: Windows 11 + XAMPP 
```
<h1>TITLE</h1>
Teachers Record Management System 1.0 – Cookie without Secure attribute 

<h2>DESCRIPTION</h2>
The Secure attribute for sensitive cookies in HTTPS sessions is not set, which could cause the user agent to send those cookies in plaintext over an HTTP session


<h2>STEPS-TO-REPRODUCE</h2>

1. Login to admin account with the Credentials as `Username:admin` and `Password:Test@123` 
2. After Login into Admin Account Intercept the the Request with help of Burpsuite
3. In the Request Section , “ Secure ”, “ HttpOnly”   attribute is missing

<h2>PROOF-OF-CONCEPT</h2>
Below is the GET Request After Logged-In as Admin

```
GET /trms/admin/dashboard.php HTTP/1.1
Host: localhost
sec-ch-ua: "Chromium";v="109", "Not_A Brand";v="99"
sec-ch-ua-mobile: ?0
sec-ch-ua-platform: "Windows"
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.5414.75 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-Dest: document
Referer: http://localhost/trms/admin/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=8alf0rbfjmhm3ddra7si0cv7qc
Connection: close
```

![Teacher-management-poc-1](https://user-images.githubusercontent.com/98345027/212894700-1f1a2094-2bfd-4e71-8fa8-700bd20a02f2.png)



<h2>IMPACT</h2>
When a cookie is set with the Secure flag, it instructs the browser that the cookie can only be accessed over secure SSL/TLS channels. This is an important security protection for session cookies. The secure flag should be set on all cookies that are used for transmitting sensitive data when accessing content over HTTPS. If cookies are used to transmit session tokens, then areas of the application that are accessed over HTTPS should employ their own session handling mechanism, and the session tokens used should never be transmitted over unencrypted communications.

<h3>REFERENCE</h3>

[CWE-614: Sensitive Cookie in HTTPS Session Without 'Secure' Attribute](https://cwe.mitre.org/data/definitions/614.html )
