# Data Lab: Learning Bit Magic

## Introduction

The purpose of this assignment is to become more familiar with bit-level representations of integers and floating point numbers. You’ll do this by solving a series of programming “puzzles.” Many of these puzzles are quite artificial, but you’ll find yourself thinking much more about bits in working your way through them.

## Logistics

This is an individual project. All handins are electronic. Clarifications and corrections will be posted on the course Web page.
3 Handout Instructions


Start by copying datalab-handout.tar to a (protected) directory on a Linux machine in which you plan to do your work. Then give the command

```bash
  $ tar xvf datalab-handout.tar.
```
This will cause a number of files to be unpacked in the directory. The only file you will be modifying and turning in is bits.c.

The bits.c file contains a skeleton for each of the 15 programming puzzles. Your assignment is to complete each function skeleton using only straightline code for the integer puzzles (i.e., no loops or con- ditionals) and a limited number of C arithmetic and logical operators. Specifically, you are only allowed to use the following eight operators:

```
!  ̃ & ˆ | + << >>
```

A few of the functions further restrict this list. Also, you are not allowed to use any constants longer than 8 bits. See the comments in bits.c for detailed rules and a discussion of the desired coding style.

## The Puzzles
This section describes the puzzles that you will be solving in bits.c.

### Bit Manipulations
Table 1 describes a set of functions that manipulate and test sets of bits. The “Rating” field gives the difficulty rating (the number of points) for the puzzle, and the “Max ops” field gives the maximum number of operators you are allowed to use to implement each function. See the comments in bits.c for more details on the desired behavior of the functions. You may also refer to the test functions in tests.c. These are used as reference functions to express the correct behavior of your functions, although they don’t satisfy the coding rules for your functions.


| Name        | Description           | Rating  | Max Ops |
| ------------- |:-------------:| -----:|-----:|
| bitAnd(x,y) | x & y using only &#124; and ̃|1 | 8|
| getByte(x,n) |Get byte n from x. | 2 | 6|
| logicalShift(x,n) | Shift right logical. | 3 |20|
| bitCount(x)| Count the number of 1’s in x. | 4|40|
| bang(x)| Compute !n without using ! operator. |4| 12|

Table 1: Bit-Level Manipulation Functions.

## Two’s Complement Arithmetic

Table 2 describes a set of functions that make use of the two’s complement representation of integers. Again, refer to the comments in bits.c and the reference versions in tests.c for more information.

| Name        | Description           | Rating  | Max Ops |
| ------------- |:-------------:| -----:|-----:|
| tmin()| Most negative two’s complement integer| 1 | 4|
| fitsBits(x,n) | Does x fit in n bits? | 2 | 15 |
| divpwr2(x,n)| Compute x/2n| 2| 15|
| negate(x) | -x without negation |2 | 5|
| isPositive(x)|x > 0? |3 | 8 |
| isLessOrEqual(x,y) | x <= y? | 3 | 24 |
| ilog2(x) | Compute ⌊log2(x)⌋ | 4 | 90 |

Table 2: Arithmetic Functions

## Floating-Point Operations
For this part of the assignment, you will implement some common single-precision floating-point operations. In this section, you are allowed to use standard control structures (conditionals, loops), and you may use both int and unsigned data types, including arbitrary unsigned and integer constants. You may not use any unions, structs, or arrays. Most significantly, you may not use any floating point data types, operations, or constants. Instead, any floating-point operand will be passed to the function as having type unsigned, and any returned floating-point value will be of type unsigned. Your code should perform the bit manipulations that implement the specified floating point operations.

Table 3 describes a set of functions that operate on the bit-level representations of floating-point numbers. Refer to the comments in bits.c and the reference versions in tests.c for more information.


| Name        | Description           | Rating  | Max Ops |
| ------------- |:-------------:| -----:|-----:|
| float_neg(uf) | Compute -f | 2 | 10 |
| float_i2f(x) | Compute(float) x | 4 | 30 |
| float_twice(uf) | Computer 2*f | 4 | 30 |

Table 3: Floating-Point Functions. Value f is the floating-point number having the same bit representation as the unsigned integer uf.

Functions float_neg and float_twice must handle the full range of possible argument values, including not-a-number (NaN) and infinity. The IEEE standard does not specify precisely how to handle NaN’s, and the IA32 behavior is a bit obscure. We will follow a convention that for any function returning a NaN value, it will return the one with bit representation 0x7FC00000.
The included program fshow helps you understand the structure of floating point numbers. To compile fshow, switch to the handout directory and type:

```bash
$ make
```
You can use fshow to see what an arbitrary pattern represents as a floating-point number:

```bash
$ ./fshow 2080374784
Floating point value 2.658455992e+36
Bit Representation 0x7c000000, sign = 0, exponent = f8, fraction = 000000
Normalized.  1.0000000000 X 2ˆ(121)
```

You can also give fshow hexadecimal and floating point values, and it will decipher their bit structure.

## Evaluation
Your score will be computed out of a maximum of 96 points based on the following distribution:
26 Correctness points.
22 Performance points.
48 Class Quiz points.

* **Correctness points.** The 11 puzzles you must solve have been given a difficulty rating between 1 and 4, such that their weighted sum totals to 26. We will evaluate your functions using the btest program, which is described in the next section. You will get full credit for a puzzle if it passes all of the tests performed by btest, and no credit otherwise.

* **Performance points.** Our main concern at this point in the course is that you can get the right answer. However, we want to instill in you a sense of keeping things as short and simple as you can. Furthermore, some of the puzzles can be solved by brute force, but we want you to be more clever. Thus, for each function we’ve established a maximum number of operators that you are allowed to use for each function. This limit is very generous and is designed only to catch egregiously inefficient solutions. You will receive two points for each correct function that satisfies the operator limit.

* **Class Quiz Points.** 48 points or 50% of the assignment's grade will come from your ability to adequately explain the logic from some of your solutions in an in class quiz. This is done to prevent you from just copying solutions found online or from a friend, the explaination will need to be tied to the underlying nature of your solution and not the operations it takes. 

### Extra Credit

There are two floating point puzzles included which add 6 points of correctness and 4 points for performance points. If you are missing points from other puzzles they'll play into your overall 48 points from the puzzle's score; however, if you are beyond the 48 points they'll count as extra credit up to 10 total extra points on the assignment. 

### Autograding your work
We have included some autograding tools in the handout directory — btest, dlc, and driver.pl — to help you check the correctness of your work.
* **btest**: This program checks the functional correctness of the functions in bits.c. To build and use it, type the following two commands:
```bash
$ make
$ ./btest
```
Notice that you must rebuild btest each time you modify your bits.c file.
You’ll find it helpful to work through the functions one at a time, testing each one as you go. You can
use the -f flag to instruct btest to test only a single function:

```bash
$ ./btest -f bitAnd
```

You can feed it specific function arguments using the option flags -1, -2, and -3:

```bash
$ ./btest -f bitAnd -1 7 -2 0xf
```
Check the file README for documentation on running the btest program.

* **dlc**: This is a modified version of an ANSI C compiler from the MIT CILK group that you can use to check for compliance with the coding rules for each puzzle. The typical usage is:

```bash
$ ./dlc bits.c
```

The program runs silently unless it detects a problem, such as an illegal operator, too many operators, or non-straightline code in the integer puzzles. Running with the -e switch:

```bash
$ ./dlc -e bits.c
```
causes dlc to print counts of the number of operators used by each function. Type ```./dlc -help``` for a list of command line options.

* **driver.pl**: This is a driver program that uses btest and dlc to compute the correctness and performance points for your solution. It takes no arguments:
```bash
$ ./driver.pl
```
I will use **driver.pl** to grade your solution. If it fails to run you can almost guarantee that you will be losing significant credit on the assignment, if not getting a 0.

## Handin Instructions
Submit your bits.c file to Tyson's Turnin system.

## Advice
* Don’t include the <stdio.h> header file in your bits.c file, as it confuses dlc and results in some non-intuitive error messages. You will still be able to use printf in your bits.c file for debugging without including the <stdio.h> header, although gcc will print a warning that you can ignore.
* The dlc program enforces a stricter form of C declarations than is the case for C++ or that is enforced by gcc. In particular, any declaration must appear in a block (what you enclose in curly braces) before any statement that is not a declaration. For example, it will complain about the following code:

```C
int foo(int x){
  int a = x;
  a *= 3;     /* Statement that is not a declaration */
  int b = a;  /* ERROR: Declaration not allowed here */
}
```

### The “Beat the Prof” Contest
For fun, we’re offering an optional “Beat the Prof” contest that allows you to compete with other students and the instructor to develop the most efficient puzzles. The goal is to solve each Data Lab puzzle using the fewest number of operators. Students who match or beat the instructor’s operator count for each puzzle are winners!
To submit your entry to the contest, type:

```bash
$ ./driver.pl -u ‘‘Your Nickname’’
```
Nicknames are limited to 35 characters and can contain alphanumerics, apostrophes, commas, periods, dashes, underscores, and ampersands. You can submit as often as you like. Your most recent submission will appear on a real-time scoreboard, identified only by your nickname. You can view the scoreboard by pointing your browser at:

[https://datalab1.bryancdixon.com/](https://datalab1.bryancdixon.com/)
