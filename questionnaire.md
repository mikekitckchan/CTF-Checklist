## Basic Information

### List out interesting subdomain and what it is for?

### Fuzz the directory of the subdomain above

### What ip:port is founded and what is the service of these ip:port?

### Point out some URL structure used by the web app:

### What parameter is commonly used in the web app?

### From manual and fuzzing, what directories name are commonly used by 

### Found any github of its employees?

### Any firewall?

## Account Takeover

### What happened if duplicated username or email is registered?

### List out which steps need email confirmations. For each POST request need email confirmation, put evil.com in host header, X-Forwarded-for header, X-forwarded-Host header

### List out which steps would put in username or email, try changing e-mail or username in the middle.

### Does it use SSO?

### Does it use JWT Token?

#### Using none hashing method

#### 

## Functionality

### Can the app disable visibility of its info? can other view it after disabled.

### Does the app contain diff user lvl? if yes, what function only allowed higher user priv to use. Can it be pypassed? 



## AWS Misconfig

### Does it use AWS?

### If yes, what is it S3 bucketname?

## Dependency

### What dependency the app is using?

### Any CVE related to it?

### Any endpoint related to these dependencies?

## Endpoints

### Endpoint return 403

### endpoint return 401
 
### endpoint return 400

### List some endpoints that can accessed by cross-site? What information contained in it?

### List endpoints that would change significant data

### What endpoint has reflected user input into body? Can it be exploited by xss?

### What endpointed reflected input to header? Try cache poison to xss?

### What endpoints are CDN files and can be cached? Try injecting Host / X-forwarded-for / X-forwarded-host to see if it can be redirected to evil host and cached?

### List out endpoints that contain sensitive information. How it is controlled the access? Can it be cached? Can it be access cross-site?

### List out endpoints that takes URL as input (Can it lead to open-redirect? SSRF?)

### List endpoints that with JS file (interesting)

## Websocket

### Does this web app using websocket?

### Can websocket access cross-site?
