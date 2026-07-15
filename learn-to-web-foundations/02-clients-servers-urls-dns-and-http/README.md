# Module 02: Clients, Servers, URLs, DNS, and HTTP

## What you will learn

Follow one browser navigation from a typed URL through name lookup, request, response, and page rendering.

## A URL identifies how and where to request a resource

The scheme selects a protocol such as HTTPS. The host identifies a server name. The port is normally implied. The path and query identify a resource and parameters, while the fragment stays in the browser.

## DNS and HTTP solve different jobs

DNS resolves a host name to network information. HTTP defines request and response messages. HTTPS protects HTTP in transit using TLS when certificate validation succeeds.

## A status code is only part of the response

Headers describe metadata and policy. The body carries representation bytes. A 404 can still contain a useful HTML body, while a 204 intentionally has no body.

## Complete example

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

## Try it and inspect the result

Read the message from top to bottom and label scheme, host, port, path, query, fragment, method, status, headers, and body.

Expected result: The fragment is absent from the HTTP request because the browser uses it for navigation inside the returned document.

## Common mistake

HTTPS protects data in transit but does not prove that a site is honest, bug-free, or authorized to receive every piece of information.

## Practice and continue

Complete the [exercise](exercise/exercise.md) and [quiz](quiz/quiz.md) before opening the [exercise solution](answers/exercise/exercise-solutions.md) or [quiz answers](answers/quiz/quiz-answers.md).

Continue to [Module 03](../03-html-documents-metadata-and-language/README.md).

