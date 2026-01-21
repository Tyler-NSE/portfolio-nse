---
layout: default
---

# HTTP

- [Capture Commands](#capture-commands)

## What is HTTP

The Hypertext Transfer Protocol (HTTP) is used to load webpages using hypertext links. HTTP is an application layer protocol designed to transfer information between networked devices and runs on top of other layers of the network protocol stack. HTTP usually involves a client machine making a request to a server, which then sends a response message.

## What is HTTPS

HTTPS, or HyperText Transfer Protocol Secure, is HTTP with an added layer of security. Data is encrypted using Transport Layer Security (TLS) or its predecessor, Secure Sockets Layer (SSL), which ensures that the information exchanged between the client and server is private and tamper-proof. It also verifies the authenticity of the server, protecting users from man-in-the-middle attacks.

## Understanding URLs

A Uniform Resource Locator (URL) is the address used to locate a resource on the internet.

![Branching](https://tyler-nse.github.io/assets/img/net_sec_101/url.PNG)

*   Scheme: Specifies the protocol.

*   User: Optional credentials for authentication.

*   Host: The domain name or IP address of the server.

*   Port: The network port for the connection.

*   Path: The specific resource or file location on the server.

*   Query String: Additional parameters sent to the server.

*   Fragment: A reference to a specific section of the page.

## HTTP Requests

An HTTP request is the way Internet communications platforms such as web browsers ask for the information they need to load a website. A HTTP Request usually contains:

*   HTTP version type

*   a URL

*   a HTTP method

*   HTTP request headers

*   Optional HTTP body.

For example:

'GET / HTTP/1.1
Host: tryhackme.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:87.0) Firefox/87.0
Referer: https://tryhackme.com/'

## HTTP Responses

An HTTP response is the message that a server sends back to a client in response to an HTTP request. It usually consists of a status line, headers, and a message body:

'HTTP/1.1 200 OK
Server: nginx/1.15.8
Date: Fri, 09 Apr 2021 13:34:03 GMT
Content-Type: text/html
Content-Length: 98

<html>
<head>
    <title>TryHackMe</title>
</head>
<body>
    Welcome To TryHackMe.com
</body>
</html>'

## HTTP Methods

The request method tells the server what kind of action the client wants the server to take. The most common methods are:

*  HEAD:	Asks the server for status (size, availability) of a resource.
*  GET:	Asks the server to retrieve a resource.
*  POST:	Asks the server to create a new resource.
*  PUT:	Asks the server to edit/update an existing resource.
*  DELETE:	Asks the server to delete a resource.

## HTTP Status Codes

## HTTP Headers

## Common Request Headers

## Common Response Headers

## Cookies



[back](/fundamentals/networks_and_security.html)