#  Day 33 – Web Application Basics

## Overview

This room introduces the **fundamentals of web applications**, which are essential for understanding web vulnerabilities and web-based attacks.

Web applications are one of the most common attack surfaces in modern environments, making a solid foundation in web concepts critical for any penetration tester or Red Team operator.

---

## Learning Objectives

* Understand how web applications work
* Learn the structure of URLs
* Understand HTTP requests and responses
* Identify common HTTP methods
* Learn about response status codes and headers

---

## What Is a Web Application?

A web application is software that runs on a web server and is accessed through a web browser using the HTTP or HTTPS protocol.

Web applications typically consist of:

* A client (browser)
* A web server
* A backend application
* A database

---

## URLs (Uniform Resource Locators)

A URL specifies the location of a resource on the internet and how to access it.

Basic structure:

```
protocol://hostname:port/path?query
```

Components:

* Protocol (HTTP / HTTPS)
* Hostname or IP address
* Port (optional)
* Path
* Query parameters

---

## HTTP Protocol Basics

HTTP (Hypertext Transfer Protocol) is the protocol used for communication between clients and servers.

It is a **stateless protocol**, meaning each request is independent.

---

## HTTP Request Methods

Common HTTP methods include:

* `GET` – Retrieve data from the server
* `POST` – Send data to the server
* `PUT` – Update existing data
* `DELETE` – Remove data
* `HEAD` – Retrieve headers only
* `OPTIONS` – Discover supported methods

Understanding request methods is critical when testing web applications.

---

## HTTP Response Status Codes

Status codes indicate the result of an HTTP request.

Common categories:

* `1xx` – Informational responses
* `2xx` – Successful responses
* `3xx` – Redirection messages
* `4xx` – Client errors
* `5xx` – Server errors

Examples:

* `200 OK`
* `301 Moved Permanently`
* `403 Forbidden`
* `404 Not Found`
* `500 Internal Server Error`

---

## HTTP Headers

Headers provide additional information about requests and responses.

Common request headers:

* `Host`
* `User-Agent`
* `Cookie`
* `Authorization`

Common response headers:

* `Server`
* `Set-Cookie`
* `Content-Type`
* `Content-Length`

Headers often expose valuable information during reconnaissance.

---

## Why This Matters for Web Hacking

Understanding web basics allows attackers to:

* Manipulate requests
* Identify insecure configurations
* Bypass client-side controls
* Exploit authentication and authorization flaws

Every web vulnerability builds on these core concepts.

---

## Red Team Perspective

* Web applications are a primary attack vector
* Manual request inspection is more powerful than automated scanning
* Strong fundamentals improve tool effectiveness (Burp, SQLMap, etc.)

---

## Summary

* Learned core web application concepts
* Understood HTTP communication
* Identified key components used in web attacks
* Built the foundation for web exploitation

---
