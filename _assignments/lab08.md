---
layout: assignment
due: 2022-11-29 23:59:59 -0800
permalink: assignments/lab08.html
title: Lab08 - Using UDP to Broadcast Presence
github_url: https://classroom.github.com/a/fLOAZUkS
---

## Requirements
1. In this lab, you will evolve the code you wrote to poll `stdin`
1. You will use material presented in lecture to
    1. Use UDP broadcast to tell all computers on the lab network that you are online and ready to chat
    1. Poll port 8221 for broadcast UDP broadcast messages from other computers on the network
    1. Maintain a data structure with the user name, port, and online/offline status
1. Every UDP presence message must include the following infomation, in this order: `username status port`
1. Behavior requirements
    1. You must use your USF username (e.g. phpeterson) for presence and chat messages -- no pseudonyms
    1. You must use the network in accordance with the USF's [Technology Resources Appropriate Use Policy](https://usf.service-now.com/usf?id=usf_kb_article&sys_id=49f4ed8b1bc7f890345a0dc8cc4bcb98)


## Given
1. In preparation for sending and receiving actual chat messages, I am providing a [spreadsheet](https://docs.google.com/spreadsheets/d/1t192niRJdXrSLps2SUOoP1_J5lSUjNb7Z_V2oYH8iIw/edit#gid=745709958) which assigns two TCP ports to each student
1. You will not need to do anything with the TCP port in this lab. For this lab, we are simply recording the TCP port which is provided in every UDP presence message

## Implementation Guide
1. To initialize a socket to read and write UDP messages, you'll need to
    1. Use `getaddrinfo()` to request an `addrinfo` which supports the required "hints"
    1. Use `socket()` to create a file descriptor for the `addrinfo` returned from `getaddrinfo()`
    1. Use `setsockopt()` to enable these options on the file descriptor: `SO_BROADCAST`, `SO_REUSEADDR`, `SO_REUSEPORT`
    1. Use `bind()` to associate the file descriptor with the address you got from `getaddrinfo()`
2. To write presence information to the presence file descriptor, you'll need to
    1. Format a buffer using the username, online/offline status, and TCP port number
    2. Construct a `sockaddr_in` using the broadcast address for the CS Labs network
    3. Use `sendto()` to send the buffer to the `sockaddr_in`
3. To read presence information from the presence file descriptor, you'll need to
    1. Use `recvfrom()` to read from the socket into a buffer
    1. Scan through the buffer to populate the name, online/offline status, and port number. You may use `sscanf()` if you wish.
4. You should maintain a data structure (such as an array or linked list) which stores the information about each user
    1. When a user changes online/offline status, you should record that information
1. Development tips
    1. I suggest adding a verbose mode (`-v` or similar) so you can `printf()` what your program is doing as it runs
    1. Remember to check for errors and use `perror()`

## Rubric
1. 50 pts: sends online/offline status so that my solution can see it
1. 50 pts: reads online/offline status from other users
1. Unfortunately autograder is not sophisticated enough to grade this work, so we'll do it by hand.