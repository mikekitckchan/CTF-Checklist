# Table of Content
- [session] (#session)
- [CSRF] (#csrf)
- [Account](#Account)

<a name="session"></a>
# session
```
1. Check if session would be reused after logout
2. Check if session can be decoded using base64, md5
3. Check if session can be decoded using Flask Forge
```

<a name="csrf"></a>
# Csrf
```
1. Check if a random number with same length would be valid for csrf token
2. Check if csrf token are tight to session
2. Check if csrf token can be reused 
3. Check if csrf token can be decoded using base64, md5 etc.
```

<a name="useraccount></a>
# User Account
```
1. To submit registration, try intercept and add "X-Forwarded-For", "X-Forwarded-Host" and add evil.com. Check if the confirmation link would be showing evil.com
2. Check if OTP can be bruteforced, reused in other accounts  or shown in initial request.
3. Check if adding %00 space, %0d , %2e , %09 , %20 after username can bypass rate limit. 
4. Check "timestamp", "base64" on reuse password token
5. If user e-mail appeared in request of reset password/registration, try change the e-mail. 
6. Check if changing account details (including password) include csrf token in its POST request. 
```
