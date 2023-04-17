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

TBD

## Rubric

1. Your score will be as indicated by the autograder
