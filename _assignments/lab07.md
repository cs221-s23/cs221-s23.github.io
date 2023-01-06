---
layout: assignment
due: 2022-11-22 23:59:59 -0800
permalink: assignments/lab07.html
title: Lab07 - Polling for input
github_url: https://classroom.github.com/a/nTBzGv5Y
---

## Requirements

1. In this lab, you will use the C `poll()` function in a loop to read keyboard input 
1. You will collect characters input from `stdin` into a string until a newline
1. When you encounter a newline (`\n`), you will null-terminate the string and print it out
1. When you encounter an `EOF`, you will stop the loop and your program will exit normally
1. There are other ways to echo user input besides using `poll()` (e.g. `scanf()`) but please use `poll()` so you can add network sockets to your implementation in the next lab.

## Example Output
```
$ ./lab07
Hello there!
Hello there!
More input
More input
^D
$
```

## Rubric
1. 100 pts
1. Test cases vs. manual grading TBD
