## What is Sentry

According to some background search, sentry is a third party software which is used to handle CSP report.

## What is CSP report

- Modern website normally facing many attack such as XSS etc. In order to prevent such attack, a CSP policy is made to whitelisting what resources can be loaded.

## Footprinting

- If a website has made some request with sentry_key, it is most likely the website is using sentr.

## Possoible attack

#### Source-code Scrapping

- There is a function in Sentry that called source-code scrapping. If it is turned on, the server with source-code scrapping will make request to outside website with error reported. Thus, a potential ssrf vuln would be founded;

- 
