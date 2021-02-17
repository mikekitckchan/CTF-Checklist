## Introduction

- Cache Poison mainly refers to forced the proxy server to cache an input that it not supposed to cache.

## Unkeyed Port

- In Cloudflare or Fastly(Patch in progress in 2020), unkeyed port may be cached by the proxy server. 

- e.g. a get request to https://example.com:1 would return a miss in CF-cache-status. However, if you access https://example.com again, you might find the previous request might be cached by the proxy server

## Unkeyed Query

