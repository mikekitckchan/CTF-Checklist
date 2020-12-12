## Introduction

### What is Keep-Alive?

- In HTTP, all connections would be closed after each request. In the other words, for each time we refresh a webpage, a new request is sent and a new connection is established. And once it is finished, the connection would be closed; 

- Thus, it is considered as inefficient if the page's resources are "heavy";

- Another approach is to enable keep-alive in HTTP header ```Connection: Keep-Alive```. By enabling the function, client side and server side will establish a persistent connections. It reduces the number of TCP and SSL/TLS connection requests;

- The Keep-alive function was enabled by default in http 1.1. You can disable it by adding ```Connection: close```

### Pipeline

- In http 1.1, there is also a new technology introduced called Pipeline. In Pipeline, multiple requests can be sent via one connction instead of sending each request in one connection;

- Thus, under Pipeline, server can handles multiple request from client simultaneously;

### Chunk-Encoding

- 


## CVE-2017-20372
The subjec CVE is about a HTTP smuggling vuln of Niginx 
