# Table of Content
- [session](#session)
- [CSRF](#csrf)
- [Account](#Account)
- [IDOR](#IDOR)
- [XSS](#xss)
- [SSRF/Redirect](#ssrf) 
- [API](#API)

<a name="session"></a>
# session
```
1. Check if session would be reused after logout
2. Check if session can be decoded using base64, md5, sha256
3. Check if session can be decoded using Flask Forge
```

<a name="csrf"></a>
# Csrf
```
1. Check if a random number with same length would be valid for csrf token
2. Check if empty csrf token can be treated as valid
3. Check if changing POST request to GET request can disregard the csrf token and successfully changing info.
4. Check if csrf token are tight to session
5. Check if csrf token can be reused in other sessions.
6. Check if csrf token can be decoded using base64, md5, sha256 etc.
```

<a name="useraccount"></a>
# User Account
```
1. To submit registration, try intercept and add "X-Forwarded-For", "X-Forwarded-Host" and add evil.com. Check if the confirmation link would be showing evil.com
2. Check if OTP can be bruteforced, reused in other accounts  or shown in initial request.
3. Check if adding %00 space, %0d , %2e , %09 , %20 after username can bypass rate limit. 
4. Check "timestamp", "base64" on reuse password token
5. If user e-mail appeared in request of reset password/registration, try change the e-mail. 
6. Check if changing account details (including password) include csrf token in its POST request. 
```

<a name="IDOR"></a>
# IDOR
```
1. Changing request from your id to another id
2. Try adding both id to one request
3. 
GET /admin HTTP/1.1 
Host: example.com --> 403

GET /whatever HTTP/1.1
Host: example.com
X-Original-URL --> 200
4.
example.com/admin -->403
example.com/%2e/admin -->200
5.
/admin/panel --> 403
/admin/monitor --> 200
/admin/monitor/;admin --> 200
6. 
GET /delete?user=1 -->401
GET /delete?user=1 
X-custome-IP-Authorization:127.0.0.1 --> 200
7.
example.com/admin --> 403
example.com/admin/. -->200
example.com/admin// --> 200
example.com/./admin/./ --> 200
8.
example.com/admin/ --> 302
example.com/admin..;/ --> 200
9.
If '/endpoint' ->403
Try:
/endpoint/
/endpoint/%20
/endpoint.html
/endpoint/?someparameter
/endpoint#
/endpoint.json
/endpoint.cgi
/endpoint.php
/endpoint.aspx
10.
{"id":1} --> 403
try 
{"id":{"id":1}}
{"id":"1"}
{"id":[1]}

11.
in pdf generator, try generate pdf with different user id

12.
/api/v2/userid/1 -> 403
/api/v1/userid/1 -> 200
```
<a name="xss"></a>
# XSS
```
1. Try Login page (Reflect username with no such user)
2. Try search (Reflect cannot find such thing)
3. Any other that would reflect to the page
```
<a name="ssrf"></a>
# SSRF/Redirect
```
Check if any parameter, header took url as input as would lead to redirect
check if any url in meta tag of html would lead to redirect
check API endpoint in Javascript would lead to redirect.
Check for function in Javascript file e.g. document.location, document.URL, doucment.open, window.location.href, window.navigate, window.open
```
Trick to bypass filter
```
Using HtTps instead of https
Add space of %00 before or after the url
remove https (e.g. //evil.com)
Replace by uri encoding (e.g. http:// to %68%74%74%70%3a%2f%2f)
Using \\ instead of //
<<insecured url>>?<<secured url>>
<<insecured url>>%23<<secured url>>
```


<a name="API"></a>
# API
For each parameter, check
```
1. XSS payloads and check response
2. Type in very long value (e.g. 100 As or 100 1s)
3. Type very long value (e.g. 100 As or 100 1s) with %00, %0d , %2e , %09 , %20, space etc. in between
4. For numeric input, check negative number or string
5. Try something like {{2+2}}
6. Try put in URL to see if it would submit request to that URL
5. 
```
