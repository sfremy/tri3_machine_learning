---
toc: True
comments: True
layout: notebook
title: Undecidable Problems
courses: {'csp': {'week': 12, 'categories': ['4.A']}}
categories: ['C1.4']
---

## What will we be doing today?
- Investigate the existance of undecidable problems in computer science


#### A decidable problem is a decision problem for wich an algorithm can be writen to produce a correct output for all inputs(eg."Is the number even?")



#### An undecidable problem is a problem that has no algorithim that can provide a yes or no answer, An undecidable problem may have an algorithim that works, but it can never fully work, and there are always instances in wich that is the case to make a problem undecidable.

### Example

- Decidable problem
        if n % 3 == 0:
            print("n is a multiple of three")
        else:
            print("n is not a multiple of three")
    There is a clear clear algorithim determining if  a number is a multilple of three that works for every case. 
- Undecidable problem
        Halting problem

        With any given arbituary computer program, will it run forever or will it stop

        No yes or no answer to this problem every time, how does a test happen if there is no ending?

        If ending takes too much time to find ending, does it even exist? what if it does, but computer is not fast enough to find it so it answers the ending as none?

        There is no algorithim for this that reliably gives a yes or no answer






## Where do we see this

When a program crashes, the computer cannot run the program causing backlog leading to the computer stopping the program after a few moments. We refer to this as a crash *pro tip, this is not the only reson for a crash, just a possible one*


###   Post Correspondence Problem
The Post Correspondence Problem (PCP) involves a set of tiles, each containing two strings. The problem asks whether it is possible to arrange these tiles in a sequence (repetitions allowed) so that concatenating the top strings of the selected tiles matches the concatenation of the bottom strings.

###   Tiling Problem
The Tiling Problem deals with determining whether a given shape (arbitrary shape) can be tiled using a finite set of smaller shapes (tiles). It remains undecidable due to the infinite possibilities and arrangements of shapes that would need to be considered to conclusively solve the problem.

###   Word Problem for Groups
The Word Problem for Groups asks whether, given a group presentation and two words formed from the group's generators, these words represent the same group element. This problem cannot be solved algorithmically due to the undecidable nature of the word problem for groups in general.

###   Busy Beaver Problem
The Busy Beaver Problem involves finding the Turing machine with the most significant number of steps executed before halting among all machines with a certain number of states. Due to the vast number of possible configurations and the infinite potential for different Turing machines, determining the Busy Beaver function for a given number of states remains undecidable.

###   Collatz Conjecture
The Collatz Conjecture follows an iterative sequence for positive integers: if the number is even, divide it by 2; if it's odd, triple it and add 1. The conjecture posits that regardless of the starting number, this sequence always reaches 1. Despite extensive computational verifications, a proof for all integers remains undetermined.

###   Post's Correspondence Problem
Post's Correspondence Problem (PCP) involves choosing sequences of pairs of strings from a finite set so that the concatenation of the first string in each pair matches the concatenation of the second string. The problem asks whether a sequence can be formed that produces a matching sequence of strings and is undecidable due to its relation to the Halting Problem.

###   Rice's Theorem
Rice's Theorem states that any non-trivial property about the behavior of programs that can be determined by examining their source code is undecidable. It asserts that it's impossible to create a general algorithm to decide non-trivial semantic properties of programs.

###   Emptiness Problem for Turing Machines
The Emptiness Problem for Turing Machines aims to determine whether a given Turing machine recognizes any strings in its language. This problem is undecidable since determining whether a Turing machine halts on all inputs (recognizes no strings) is equivalent to solving the Halting Problem.

###   The Entscheidungsproblem
The Entscheidungsproblem refers to David Hilbert's problem of finding an algorithm to decide the truth of any mathematical statement by creating a mechanical procedure for solving mathematical problems. This problem was proven undecidable by Turing, Church, and others in their work on computability theory and the limitations of computation.

## POPCORN HACK, Create your own undecidable problem
    Create a problem that is unsolvable by any single algorithim, for example, this problem could have infinite possibilities

### Example 
#### The "Infinite Sum Sequence Problem (ISSP)"
    Problem Statement: Given an infinite sequence of positive integers, can it be determined whether there exists a subsequence that sums up to a specific target value?

#### Undecidability:
    The ISSP is undecidable due to the infinite nature of sequences and the countless possible subsequence combinations, making it impossible to algorithmically determine the existence of a subsequence summing to a target value within a reasonable timeframe.


#### Response
    Problem Statement: Given an initial set of positions and masses of finite accuracy and an infinite integration time, can it be determined whether a set of three bodies in orbit around a star remains stable?

    Most n-body problems are dynamically chaotic over a long enough span of time and their parameters at a given epoch eventually become completely unpredictable without arbitrary precision in the starting parameters. Thus, this problem is not solvable for a majority of input parameters.

## Homework Due by Friday 11:59, message Daniel Choi, give an explaination for each problem that is one scentence long. Graded on completion and explaination. send popcorn hack as a screenshot

### Post Correspondence Problem:
What is the primary concern related to the Post Correspondence Problem (PCP)?

A) It involves matching strings using regular expressions.

B) It deals with finding the shortest path in a graph.

C) PCP revolves around identifying whether a set of strings can be matched in a specific sequence.

D) It's related to optimizing sorting algorithms.

A - PCP asks whether or not a set of matched pair strings can be arranged so that the two sequences of pair elements are identical, which is impossible for many inputs. The answer is C (A seems to refer to the Regular Post Embedding Problem, which is decidable.).

### Tiling Problem
Which statement accurately describes the undecidable nature of the Tiling Problem?

A) The Tiling Problem refers to arranging tiles in a specific pattern which can always be solved using a finite number of steps.

B) There exists an algorithm that can determine if a given shape can be tiled with a specific set of smaller shapes.

C) It's impossible to ascertain if an arbitrary shape can be tiled using a finite set of smaller shapes.

D) Tiling Problems can only be solved for regular polygons.

A - The Tiling Problem is undecidable, as it is not possible to search the infintely large set of possible shapes to determine whether a solution exists. The answer is C.

### Word Problem for Groups
What is the core issue represented by the Word Problem for Groups?

A) It focuses on finding the most efficient algorithm for text processing in groups.

B) This problem pertains to determining if two words representing group elements are equivalent.

C) The Word Problem for Groups refers to solving crossword puzzles collaboratively.

D) It involves identifying the most commonly occurring words in a group.

A - The Word Problem for Groups refers to the impossibility of determining whether two words have the same assigned meaning. The answer is B.

### Busy Beaver Problem
Which statement accurately describes the concept behind the Busy Beaver Problem?

A) It deals with optimizing the performance of multitasking systems.

B) Busy Beaver Problem revolves around finding the most efficient algorithm to sort a list of numbers.

C) It's about determining the longest-running and most productive Turing machine.

D) Busy Beaver Problem is concerned with scheduling tasks in a time-efficient manner.

A - This refers to identifying a TUring machine which runs the longest for a certin number of states. Thus the answer is C.

### Collatz Conjecture
What is the primary characteristic of the Collatz Conjecture?

A) It's a conjecture related to the distribution of prime numbers.

B) The conjecture revolves around finding the optimal path in a graph.

C) Collatz Conjecture deals with iterating over integers using a specific sequence until reaching the value 1.

D) It's a hypothesis about the behavior of sorting algorithms.

A - The Collatz Conjecture states that a certain iterative mathematical operation sequence always converges to 1, despite it never being proven. The answer is C.

### Post's Correspondence Problem
Which problem involves matching pairs of strings in a way that no two sequences produce identical combined strings?

A) Traveling Salesman Problem.

B) Knapsack Problem.

C) Post's Correspondence Problem.

D) Dijkstra's Shortest Path Problem.

A - Traveling Salesman and Dijkstra refer to optimizing path lengths, while Knapsack refers to optimizing volume space-filling, so PCP is the only remaining option though it asks for matching combined strings and not different ones. The answer is C.

### Rice's Theorem
What does Rice's Theorem state?

A) It claims that all programming languages are Turing-complete.

B) Rice's Theorem affirms that any non-trivial property about the behavior of programs is undecidable.

C) It asserts that all recursive functions can be computed using a Turing machine.

D) Rice's Theorem describes the limitations of parallel computing.

A - It states that any non-trivial informtion about the behavior of a program cannot be determined by looking at its source code. The answer is B.

### Emptiness Problem for Turing Machines
What does the Emptiness Problem for Turing Machines aim to determine?

A) It checks whether a Turing machine can recognize an empty language.

B) This problem is concerned with finding the smallest Turing machine.

C) Emptiness Problem verifies if a Turing machine has an infinite tape.

D) It examines whether a Turing machine can accept an infinite sequence of input.

A - This problem refers to whether a Turing machine can recognize strings. The answer is A.

### The Entscheidungsproblem
Which problem was famously formulated by David Hilbert and aimed to find a procedure that could decide the truth of any mathematical statement?

A) P vs NP Problem.

B) Riemann Hypothesis.

C) The Entscheidungsproblem.

D) Goldbach's Conjecture.

A - Based on how you titled this question, the answer is of course C. Of course, this is supported by the lecture.

