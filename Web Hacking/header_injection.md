## Referrer Header Injection

- Some web app heavily relies on referrer header and are vulnerable. Belows are some basic example:-

#### Redirect

- In some pages (e.g. login page), if certain condition happens (e.g. your login credential is incorret), it would refer back to where you were;

- Try intercept the request and change the referrer header to see if it would refer to your controlled pages;

#### Token sending

- In some web app, its reset password token or e-mail verification link might relies on third party module and that module might relies on the referrer header to see which web app they refer to:

- Try intercept the request and change referrer header to see if the token would be sent to your contolled site.

## Header injection via CRLF in 302

- When your request results in 302. the redirected url most likely reflect in location in its response:

```
GET /something?url=www.redirected.com HTTP/1.1
Host: www.victim.com
Accept: */*
Connection: Close
```
```
302 Found
.
.
.
Location:www.redirected.com
```
- In this case, try amending url parameter to www.redirected.com%0AInjected-header:%20Value. You might able to inject a header value;

## Bypass Host Header injection check

- Normally, there would be a check on whether the host header is valid. But if the site has available all subdomain of its site to access. Try:

Host: evil.com?.example.com

- If it leads to a link sending back to that subdomain and sensitive info is inside URL, it might lead to leakage of sensitive info. 


