---
layout: assignment
due: 2023-02-14 23:59:59 -0800
permalink: assignments/project01.html
title: Project01 - Password Cracker
github_url: https://classroom.github.com/a/crZG8L3a
---

## Background

Passwords are a fundamental part of computer security. In this assignment, we will explore some common ways to attack passwords.

## Requirements

1. You will develop a C program which takes a hashed password (64 characters in length) on the command line.
1. Your program will compare the given hash with:
    1. The hash of each of a list of 10,000 common passwords
    1. The hash of each of the 10,000 passwords after substituting common "l33t speak" transformations like 'e' to '3'
    1. The hash of each of the 10,000 passwords with a '1' added to the end
1. If the given hash matches any of those hashes, your program should print the clear-text password of the match.
1. Your program must be called `project01` and must be built by a `Makefile` you provide.
1. No credit will be given for projects which hard-code the hashes from the test cases and print the expected result without computing the result as described above.

## Given

1. When you accept the assignment using the link above, your repo will contain the following given code:
    1. `passwords.h` and `passwords.c` which respectively declare and define the list of 10,000 common passwords
    1. `sha256.h` and `sha256.c` which respectively declare and define the code to compute a SHA-256 hash digest
    1. `project01.c` which shows how to use the SHA-256 functions.
1. Although there are a large number of l33t substitutions, we will use these common ones:
    1. Change '0' to 'o'
    1. Change '3' to 'e'
    1. Change '!' to 'i'  
    1. Change '@' to 'a'  
    1. Change '#' to 'h'
    1. Change '$' to 's'
    1. Change '+' to 't'
1. The test case for plus1 is separate from the test case for l33t, so yankees1 should match yankees, but y@nk33s1 should not match yankees. 
1. If you want to test some password hashes, there are many SHA-256 calculators online, including [this one](https://xorbin.com/tools/sha256-hash-calculator)

## Example Output

```sh
$ ./project01 5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8
password
```

## Rubric

1. Your project will be graded using autograder for correctness. You will need to `git pull` in the tests repo.
    1. 50 pts: passes 10k tests
    1. 20 pts: passes 10k-l33t tests
    1. 20 pts: passes 10k-plus1 tests
2. And manually for style
    1. 10 pts: readable coding style, no build products in repo
