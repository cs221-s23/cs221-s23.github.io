---
layout: assignment
due: 2023-03-07 23:59:59 -0800
permalink: assignments/lab04.html
title: Lab04 - Tic-Tac-Toe
github_url: https://classroom.github.com/a/jP7xMMqU
---

## Requirements

1. You will write a C program called `lab04` and provide a `Makefile` to implement a rudimentary Tic-Tac-Toe game
1. Your program will include three functions declared in `lab04.h`. 
    1. `init_board`: accept input from `char* argv[]`specifying Row and Column inputs to the Tic-Tac-Toe board. 0 0 is the upper left and 2 2 is the lower right.
    1. `print_board`: print the content of the 3x3 board.
    1. `check_board`: win and draw patterns on the board. return 1 if X wins, -1 if O wins, 0 if draw.

## Given

1. `lab04.h` includes the `board_t` type definition and function declarations, and `test.c` includes the `main` function that runs test cases. Do NOT create another `main` function in your code. 
1. In lecture we will discuss the basics of the game, including alternating turns, making legal moves, and detecting a win.
1. We will learn several new C language features, including two-dimensional arrays.

## Example Output

```sh
$ ./lab04 empty
 _ | _ | _
---+---+---
 _ | _ | _
---+---+---
 _ | _ | _

$ ./lab04 xhoriz
 X | X | X
---+---+---
 _ | O | _
---+---+---
 _ | _ | O
X wins

$ ./lab04 draw
 X | O | X
---+---+---
 O | X | O
---+---+---
 O | X | O
draw
```

## Rubric
1. Your score will be as indicated by the autograder
