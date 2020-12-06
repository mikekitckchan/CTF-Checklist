## Referrer Header Injection

- Some web app heavily relies on referrer header and are vulnerable. Belows are some basic example:-

### Redirect

- In some pages (e.g. login page), if certain condition happens (e.g. your login credential is incorret), it would refer back to where you were;

- Try intercept the request and change the referrer header to see if it would refer to your controlled pages;

### Token sending

- In some web app, its reset password token or e-mail verification link might relies on third party module and that module might relies on the referrer header to see which web app they refer to:

- Try intercept the request and change referrer header to see if the token would be sent to your contolled site.

