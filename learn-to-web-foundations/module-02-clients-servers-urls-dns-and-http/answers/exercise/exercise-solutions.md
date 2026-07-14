# Exercise Solution: Clients, Servers, URLs, DNS, and HTTP

```text
URL:
https://example.test:443/articles?id=42#comments

Request:
GET /articles?id=42 HTTP/1.1
Host: example.test
Accept: text/html

Response:
HTTP/1.1 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 31

<h1>Requested article</h1>
```

## Why this works

The fragment is absent from the HTTP request because the browser uses it for navigation inside the returned document. Use the browser inspector to connect each exercise requirement to the exact element, attribute, rule, request, or computed value that satisfies it. File names and content may differ when the same semantic and accessibility contracts are preserved.

