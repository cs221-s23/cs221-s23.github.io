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
1. The `poll()` takes an array of `struct pollfd` elements (see `man poll`)
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

## Example Output

```sh
lab08@vlab30$ ./lab08 -p 9000 &
[1] 14205
lab08@vlab30$ telnet localhost 9000
Trying ::1...
telnet: connect to address ::1: Connection refused
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
GET / HTTP/1.1

HTTP/1.1 200 OK
Content-Length: 59
Content-Type: text/plain

<!DOCTYPE html>
<html>
<body>
Hello CS 221
</body>
</html>


Connection closed by foreign host.
lab08@vlab30$ telnet localhost 9000
Trying ::1...
telnet: connect to address ::1: Connection refused
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
GET /wrong.html HTTP/1.1

HTTP/1.1 404 Not Found
Content-Length: 55
Content-Type: text/html

<!DOCTYPE html>
<html>
<body>Not Found
</body>
</html>


Connection closed by foreign host.
```

## Rubric

1. We will use autograder to test lab08 as follows:
    1. 49 pts for returning the default index page given above
    1. 49 pts for returning the not-found page given above
    1. 1 pt each for successfully starting and stopping the server
1. Remember to include `port.txt` like we did for lab07
1. Please don't commit the `*.tmp` or `*.html` files that autograder creates. 
You may wish to create a `.gitignore` file
