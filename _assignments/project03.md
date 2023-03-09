---
layout: assignment
due: 2023-03-28 23:59:59 -0800
permalink: assignments/project03.html
title: Project03 - Tic-Tac-Toe using Minimax
github_url: https://classroom.github.com/a/saKNBXxB
---

## Requirements

1. Usage: `./project03 [-s board_size] [initial board state]
1. Your program must be called `project03` and the `Makefile` in the repo should create `project03`.
1. Your program must work with any board size. The default board size is 3. If `argv[1]` is equal to `-s`, then `argv[2]` gives a new board size.  For example, `./project03 -s 4` will play a full game on a 4x4 board. 
1. You will evolve your lab04 solution to support the following two modes of Tic-Tac-Toe game play:
    1. If `argc > 9` your program will accept board values in `argv[]`, just like lab04, and use Minimax to output the optimal next move for that board.
        - You may assume that it's 'O's turn, and 'X' is the maximizer
    1. If `argc < 4` your program will use a loop to play a full game, with a human playing 'X' and the computer using Minimax to play 'O'. 
        - 'X' always goes first


## Given

We will discuss recursion and the Minimax algorithm in lecture

## Example Output

Your program's output must exactly match the format below
```sh
$ ./project03 O _ O X _ X _ _ _
 O | _ | O
---+---+--
 X | _ | X
---+---+--
 _ | _ | _
O: 0 1

$ ./project03 -s 4 O _ X X X O _ X _ _ O _ _ _ _ _ 
 O | _ | X | X
---+---+---+--
 X | O | _ | X
---+---+---+--
 _ | _ | O | _
---+---+---+--
 _ | _ | _ | _
O: 3 3
```

## Rubric

**NB**: Since Minimax is a well-known algorithm, many explanations and implementations are available. You must develop your own original code, working individually.

** Project03 requires interactive grading. Multiple-move game play and style will be graded during the interactive grading session. Not attending an interactive grading session will result in 0 for project03.**

1. 70 pts: Correctness for a single move, tested by the `grade` script
1. 20 pts: Multiple-move game play including validation of input and legal moves, tested manually
    1. For full credit games should end in a draw
1. 10 pts: Style, including (but not limited to):
    1. Consistent naming and indentation
    1. Helpful comments
    1. No dead (commented-out) code or unnecessarily complex code
    1. No build products in the repo
