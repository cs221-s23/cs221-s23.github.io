---
layout: assignment
due: 2023-05-02 23:59:59 -0800
permalink: assignments/lab08.html
title: Lab08 - HTTP server part 2
github_url: https://classroom.github.com/a/48WI6NRj
---

## Requirements

In this assignment you will extend the PING/PONG server to implement
1. asynchronous network I/O using [`poll()`](https://linux.die.net/man/2/poll)
2. Basic [HTTP](https://datatracker.ietf.org/doc/html/rfc2616) requests

## Implementation Notes

### How to use poll()
1. The `poll()` takes an array of `struct pollfd` elements
1. Each `struct pollfd` wraps an `int` file descriptor, and includes some flags
1. We want to know when there is data to read on the file descriptor, so we set the pollfd's `events` field to `POLLIN`
1. When `poll()` returns, it tells us how many of the `struct pollfd` elements have input we can read
1. We loop over all of the pollfds, looking for `(revents & POLLIN) != 0`
1. The file descriptor in that pollfd can be read with `recv()`


### How to parse HTTP GET requests
1. Since HTTP requests are terminated by a `'\n'` you should `recv()` from a readable file descriptor into a buffer until you encounter a `'\n'`
1. The HTTP `Request-Line` contains a "method", a Uniform Resource Identifier (URI) and the protocol version, e.g. `GET / HTTP/1.1`. You should parse the request line into those pieces. 
1. If the request line contains a `GET` for `/` you should write a successful response into the file descriptor. For example: 
    ```
    HTTP/1.1 200 OK
    Content-Type: text/html
    Content-Length: <length in bytes>

    <!DOCTYPE html>
    <html>
        <body>
          Hello CS 221
      </body>
    </html>
    ```
1. If the request contains a method other than `GET` or a URI other then `/` you should write a error response into the file descriptor. For example:
    ```
    HTTP/1.1 404 Not Found
    Content-Type: text/html
    Content-Length: <length in bytes>

    <!DOCTYPE html>
    <html>
        <body>
          Not found
      </body>
    </html>
    ```



## Rubric

1. 50 pts for using `poll()` correctly (graded manually)
1. 50 pts for correctly interpreting an HTTP GET method (graded by autograder)