---
layout: assignment
due: 2023-04-25 23:59:59 -0800
permalink: assignments/lab07.html
title: Lab07 - HTTP server part 1 ping-pong
github_url: https://classroom.github.com/a/nUS5t88R
---

## Requirements

In project05, you will be implementing an [HTTP server software](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/Web_mechanics/What_is_a_web_server), i.e. a software that handles an HTTP request and sends back an HTTP response. HTTP requests and responses are sent over TCP. In preparation for project05, you will implement a simple server on TCP.

- The server should listen for incoming TCP connections on a specified port. [Here](./cs221-s23-port.txt) is the unique port number for each student.
- Your repo **must** include a file called `port.txt` which contains the port number for your server.
- When a client connects, the server should wait for incoming data from the client.
- If the incoming message is "PING", the server should respond with "PONG" and close the TCP connection.
- If the incoming message is any other message, the server should respond with "INVALID" and close the TCP connection.

## Implementation

You may use the following libraries:

- <sys/socket.h> for socket programming.
	- Create a TCP socket using `socket()` function. 
	- Bind the socket to a specified port using `bind()` function. (`man 2 bind`)
	- Start listening for incoming TCP connections using `listen()` function. 
	- When a client connects, accept the connection using `accept()` function.
	- Receive data from the client using `recv()` function.
	- If the incoming message is "PING", send "PONG" message back to the client using `send()` function.
	- If the incoming message is any other message, send "INVALID" message back to the client using `send()` function.
- < unistd.h> for closing connection.
	- Close the connection using `close()` function.	

## Example Output

If you run your server in the background using `&`, note the process ID (pid)
```sh
user@vlab31:lab07 $ ./lab07 -p 9000 &
[1] 14205
```
Use `telnet` to connect to your server 
```sh
user@vlab31:lab07 $ telnet localhost 9000
Trying ::1...
telnet: connect to address ::1: Connection refused
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
```
Type `PING` and your server should respond with `PONG` 
```sh
PING
PONG
Connection closed by foreign host.
```
You can stop your server using the `kill` command with its `pid`
```sh
user@vlab31:lab07 $ kill 14205
```

## Debugging Tips 

1. When debugging your server, you may run it in the background (using `&`) or in the foreground if you want to run it in `gdb` or watch `printf()` output
1. If you try to run your server and get an error like this:
	```sh
	user@vlab31:lab07 $ bind: Address already in use
	```
	that means your server is still bound to the port and you need to kill it.
	```sh
	user@vlab31:lab07 $ ps ax |grep lab07
	14280 pts/0    S      0:00 ./lab07 -p 9000
	14283 pts/0    S+     0:00 grep --color=auto lab07
	user@vlab31:lab07 $ kill 14280
	```

## Rubric

1. Autograder contains one test case, using a [shell script](https://github.com/cs221-s23/tests/blob/main/lab07/test.sh) which runs your server in the background and telnets to it on your port.
	```sh
	user@vlab31:lab07 $ grade test -p lab07
	. pong(100/100) 100/100
	```
