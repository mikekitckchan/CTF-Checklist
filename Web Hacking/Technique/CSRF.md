## Checkpoint of CSRF token bypass

1. Check if a random number with same length would be valid for csrf token
2. Check if empty csrf token can be treated as valid
3. Check if changing POST request to GET request or PUT request can disregard the csrf token and successfully changing info.
4. Check if csrf token are tight to session
5. Check if csrf token can be reused in other sessions.
6. Check if csrf token can be decoded using base64, md5, sha256 etc.
7. Try if deleting first char or last char would make it still valid.
8. changing origin and referer
9. Use another method such as PUT then add ?_method=POST at the end of URL

## Bypass for origin check 

1. Check if an request can be made if origin header is removed.

2. If so, try crafting below payload in attacker's site:

```html
 <iframe src='data:text/html,<body onload="document.forms[0].submit()"><form action="https://www.victim.com" method="get"></body>'></iframe>
```

3. If it allows frame ancester, it should works.
