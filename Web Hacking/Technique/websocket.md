## What is Websocket

- Websocket is a technology in html5 that allows 2-ways communication under TCP.

- It enables a web to deliver info to browser in realtime. (e.g. a chat app)

- RFC documents for the subject connection can refer to RFC6455 and RFC7936


## Example of a simple websocket

- A simple websocket request from client side is as per below:

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: dGhlIHNhbXBsZSBub25jZQ==
Origin: http://example.com
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
```
- And response from server is something like:

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: s3pPLMBiTxaQ9kYGzzhZRbK+xOo=
Sec-WebSocket-Protocol: chat
```

- Below are explanation of the lines above:

## Vulnerability

#### Cross-site web socket hijacking

- Online tester

https://cow.cat/cswsh.html

