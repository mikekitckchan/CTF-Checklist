## Scenario

#### Search Function

#### Login form

#### 302 redirect -> XSS

- For example, if a request with ```GET /sth?redirect=https://www.sth.com/``` and response is 302 found with ```location: https://www.sth.com/```, can try the below for further exploitation:

- First, change request to ```GET /sth?redirect=https//www.sth.com/%0Aheader: %20value%0A%0A<script>alert("XSS")</script>```. It might inject header into response

- However, as it is 302, the payload would not be interpreted by most of the browser. 

- To get around, use payload like this: ```http://victim.site/sth?redirect=[URI_SCHEME]://www.sth.com%0A%0A[XSS_PAYLOAD]```

- Can find RPC for all URI_SCHEME to try

#### 
