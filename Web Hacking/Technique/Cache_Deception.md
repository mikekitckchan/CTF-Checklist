## What is Cache

- In modern web app, in order to deliver web content quicker, a cache server would be used to deliver public content;

- Cache server normally served in proxy server. Thus, when user sends request to proxy server. Proxy would identify whether the content request can be served by cache server or need to make request to back-end web server for such content.

- Information served in cache serve includes company logo, js files, css files etc.

## What is Cache Deception

- In some wierd situation, if you send a request to a target with url ```www.example.com/account_info/notexist.css``` whilst notexist.css is not an existing css file of the web app, web app would return and cache the page of ```www.example.com/account_info```.

- If the page is cached, attacker can visit your account_info by simpley access ```www.example.com/account_info/notexist.css```.

