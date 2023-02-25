---
layout: assignment
due: 2023-02-28 23:59:59 -0800
permalink: assignments/project02.html
title: Project02 - Sorted Dictionary
github_url: https://classroom.github.com/a/X-i9Dw0f
---

## Goal
You will learn more about pointer manipulation and using struct by creating your own linked list and keeping it sorted. 

## Background
In reality, hackers learn more (password, hash) pairs as they continue to attack, so the dictionary has to be expandable. Also, the hackers do not wish to do a linear search, i.e. scan the whole dictionary to find the corresponding password for the given hash, so the dictionary needs to be sorted so that the hackers can use a binary search. 

## Requirements
1. You will write a C program called `project02` to help build a sorted dictionary file.
1. You must provide a `Makefile` 
1. Your program will build a sorted dictionary as follows:
    1. Use the following `struct entry` to store a (password, hash) pair. 

        ```c
        struct entry {
            char password[MAX_PASSWORD + 1];
            char hash[DIG_STR_LEN + 1];
            struct entry *next;
        } entry;
        ```
    1. Passwords are stored in a file given in `argv[1]`, and the number of passwords in this file is unknown. In the password file, one password is stored in one line. For every password in the file, create (password, its sha256 hash), (l33t version of the password, its sha256 hash), (plus1 version of the password, its sha256 hash) pairs and add these 3 pairs as 3 nodes to a linked list. 

    1. The linked list must be sorted in the **ascending order by the hash value**. If the given (password, hash) pair exists in the linked list already, do not insert. 

    1. You should sort the list as you insert items. You must implement sorting yourself, i.e. do not use any sort functions provided in a library, e.g. C `qsort()`

    1. Store the sorted linked list in the file given by `argv[2]`. The first line of this file should be the number of pairs in the file. The subsequent lines would contain one (hash, password) pair per line, with a comma in between. 
1. Given "-v" (verbose) option, display how the linked list changes as shown in the Example Output.

## Given
1. You will see a single-linked list demo and discuss Insertion Sort in class.
1. You may use any code from project01 and lab03. To copy files from one directory to another, see [shell basics](https://github.com/usfca-cs-tools/docs/blob/main/shell-basics.md).

## Example Output

```sh
$ cat passwords.txt
password
12345678
qwerty
$ ./project02 passwords.txt dictionary.txt
$ cat dictionary.txt
8
0b14d501a594442a01c6859541bcb3e8164d183d32937b851835442f69d5c94e,password1
154c4c511cbb166a317c247a839e46cac6d9208af5b015e1867a84cd9a56007b,123456781
18f3c96386407ba486f6f6178a14639194e498c4f8338fc61bf2945653fe058a,p@$$w0rd
5e884898da28047151d0e56f8dc6292773603d0d6aabbdd62a11ef721d1542d8,password
65e84be33532fb784c48129675f9eff3a682b27168c0ea744b2cf58ee02337c5,qwerty
8e87f3b4d7e4a5bf207860f45f2a09f091928c549341bab786adaec8396e48aa,qw3r+y
b6ad34b0b6b7e38f878a513b3f7927ebeb4cffb01aeb6d9fd9f9ad67fbc76517,qwerty1
ef797c8118f02dfb649607dd5d3f8c7623048c9c063d532cc95c5ed7a898a64f,12345678
$ ./project02 passwords.txt dictionary.txt -v
inserting: password
password 5e884...

inserting: p@$$w0rd
p@$$w0rd 18f3c...
password 5e884...

inserting: password1
password1 0b14d...
p@$$w0rd 18f3c...
password 5e884...

inserting: 12345678
password1 0b14d...
p@$$w0rd 18f3c...
password 5e884...
12345678 ef797...

inserting: 12345678
password1 0b14d...
p@$$w0rd 18f3c...
password 5e884...
12345678 ef797...

inserting: 123456781
password1 0b14d...
123456781 154c4...
p@$$w0rd 18f3c...
password 5e884...
12345678 ef797...

inserting: qwerty
password1 0b14d...
123456781 154c4...
p@$$w0rd 18f3c...
password 5e884...
qwerty 65e84...
12345678 ef797...

inserting: qw3r+y
password1 0b14d...
123456781 154c4...
p@$$w0rd 18f3c...
password 5e884...
qwerty 65e84...
qw3r+y 8e87f...
12345678 ef797...

inserting: qwerty1
password1 0b14d...
123456781 154c4...
p@$$w0rd 18f3c...
password 5e884...
qwerty 65e84...
qw3r+y 8e87f...
qwerty1 b6ad3...
12345678 ef797...


```

## Rubric

** Project02 requires interactive grading. Defensive coding and style will be graded during the interactive grading session. Not attending an interactive grading session will result in 0 for project02.**

1. 80 pts (autograding): correctness demonstrated by the `grade` script
1. 10 pts (defensive coding): Show the grader examples of defensive coding practice, such as:
    1. Checking for memory and I/O errors
    1. No unbounded memory copies
    1. No memory leaks
1. 10 pts (style): Neatness, including (but not limited to) the items described in the [C Style Guide](https://github.com/usfca-cs-tools/docs/blob/main/c-style.md)
    1. Consistent naming and indentation
    1. Well-designed functions
    1. Helpful comments
    1. No dead (commented-out) code or unnecessarily complex code
    1. No build products or output dictionary files in the repo

## Tips
1. You should start with designing functions, and build and test one function at a time. It's too much code to write it all at once.
1. You may want to copy the project02 test files in the autograder to your project02 directory and test one test case at a time. 
1. A well-designed function tends to do one dedicated job. and is highly reusable. For example, finding the n<sup>th</sup> node in a linked list is reusable in any other program with a linked list.
