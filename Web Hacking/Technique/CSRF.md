## Checkpoint of CSRF bypass

1. Check if a random number with same length would be valid for csrf token
2. Check if empty csrf token can be treated as valid
3. Check if changing POST request to GET request can disregard the csrf token and successfully changing info.
4. Check if csrf token are tight to session
5. Check if csrf token can be reused in other sessions.
6. Check if csrf token can be decoded using base64, md5, sha256 etc.
7. Try if deleting first char or last char would make it still valid.
