---
toc: True
comments: True
layout: post
title: Boolean If Student Teaching Lesson
description: Student lesson on AND/OR/NOT/ETC operators and Python scripts involving booleans.
author: Kyle Liang, Ian Wu, Trevor Huang, Jason Guan
type: hacks
courses: {'csp': {'week': 7, 'categories': ['4.A']}}
categories: ['C1.4']
---

## Review
Quick review on if statements, boolean expressions, and college-board pseudo code

### Boolean
Data-type that can either be true or false


```python
boolean = True
print(boolean)
boolean = False
print(boolean)
boolean = 1
## boolean is not longer a boolean, now an integer
print(type(boolean))
```

    True
    False
    <class 'int'>


### If-Statements/Conditionals

Self, explanatory, runs a portion of code if expression/condition is satisfied.

<code>
if (EXPRESSION):
    print('code to run here')
</code>


```python
number = int(input('Enter a number: '))

# Collegeboard talks about the modulo operation even in this section so here it is
# % is the modulo operation
# Easier way to think about it is the remainder when two numbers are divided
# Ex. 14 % 6 = remainder of 14/6 = 2
if (number % 2 == 0):
    print('Number is even')
else: 
    print('Number is odd')
```

    Number is even


## Relational Operators
Used to compare two variables, returns a boolean

- ==
    - Checks if two variables are equal
- != 
    - Checks if two variables are not equal
- a > b
    - Checks if variable a is greater than b
- a < b
    - Checks if variable a is less than b
- a >= b and a <= b
    - Same as above, but greater than or equal to and less than or equal to


```python
a = 7
b = 5

if a == b:
    print('a equals b')
else: 
    print('a does not equal b')

if a > b:
    print('a is greater than b')
elif a < b: 
    print('a is less than b')
```

    a does not equal b
    a is greater than b


#### Hack #1: Relational Operators
Create a program that takes two numbers from the user (use input()) and displays the larger one. If the numbers are equal, state that they are equal.
Challenge: Use relational operators to compare two words and display whichever one comes first alphabetically (Can you apply it to a list?)


```python
## Program Here

a = int(input("1st Number:"))
b = int(input("2nd Number:"))

if a == b:
    print('a equals b')
else:
    print('a does not equal b')
    
    
alphabet = ['a','b','c','d','e','f','g','h','i','j','k','l','m','n','o','p','q','r','s','t','u','v','w','x','y','z']
w1 = str(input("Enter a word")).lower()
w2 = str(input("Enter another word")).lower()

for i in range(len(w1)):
    if alphabet.index(w1[i]) > alphabet.index(w2[i]):
        print(w2)
        break
    if alphabet.index(w1[i]) < alphabet.index(w2[i]):
        print(w1)
        break
    else:
        continue


```

    a does not equal b
    amplectobelua


## Logic Gates
Logic gates combine different boolean (true/false or 1/0) values into a single boolean value. As computers are composed of a bunch of binary/boolean values, logic gates are the "logic" of the computer (the ability to code).

### Boolean Operators + Algebra
> The basic operators in Boolean algebra are AND, OR, and NOT. The secondary operators are eXclusive OR (often called XOR) and eXclusive NOR (XNOR, sometimes called equivalence). They are secondary in the sense that they can be composed from the basic operators.

### AND
>The AND of two values is true only whenever both values are true. It is written as *AB* or *A⋅B*.

| A | B | A AND B |
|---|---|---------|
| 0 | 0 |   0     |
| 0 | 1 |   0     |
| 1 | 0 |   0     |
| 1 | 1 |   1     |

![image.png](http://www.categories.acsl.org/wiki/images/thumb/d/d8/And-gate.png/192px-And-gate.png)

Real-life example of AND: If it's sunny (A) AND it's a weekend (B), then I will go to the beach :)

#### Hack #2: AND in Python
>1. Add an "else" statement to the current if-statement, and display an appropriate response for each block
>2. Rename the two variables to a realistic scenario (i.e. sunny and weekend example above)
>3. Change the two variables between True and False to see what output you'll get!
>4. (CHALLENGE): Make the code more user-friendly with "input()"
# CB Pseudo Code

A ← true
B ← true

IF (A AND B) {
   DISPLAY("It's true!")
}

```python
# Python

A = bool(input("T/F?"))
B = bool(input("T/F?"))
# A = True
# B = True
#B = False

if A and B: # Bitwise syntax: A & B
    print("All true!")
    
else:
    print("Not fully true.")

```

    It's true!


### OR
>The OR of two values is true whenever either or both values are true. It is written as *A+B*. The values of or for all possible inputs is shown in the following truth table 

| A | B | A OR B |
|---|---|--------|
| 0 | 0 |   0    |
| 0 | 1 |   1    |
| 1 | 0 |   1    |
| 1 | 1 |   1    |

![image-2.png](http://www.categories.acsl.org/wiki/images/thumb/4/4c/Or-gate-en.svg/192px-Or-gate-en.svg.png)

Real-life example of OR: If it's my birthday (A) OR it's Christmas (B), then I will get a present :D

#### Optional Hack: OR in Python
>1. Add an else statement to create output appropriately
>2. Try different combinations of A and B 
# CB Pseudo Code

A ← true
B ← false

IF (A OR B) {
   DISPLAY("It's true!")
}

```python
# Python

A = True
B = False

if A or B: # Bit-mask syntax: A | B
    print("One's true!")
else:
    print("Neither's True!")

```

    It's true!
    True


### NOT
>The NOT of a value is its opposite; that is, the not of a true value is false whereas the not of a false value is true. It is written as [x with a dash above] or ¬x. 

| A | NOT A |
|---|-------|
| 0 |   1   |
| 1 |   0   |

![image-2.png](http://www.categories.acsl.org/wiki/images/thumb/9/9f/Not-gate-en.svg/192px-Not-gate-en.svg.png)

Real-life example of NOT: If I do NOT eat dessert (A), then I will be sad ;-;

#### Hack #3: NOT in Python
>1. Follow the "AND in Python" hack to add an else statement to output when gate returns false, and change the program to apply in real life
>2. Try different combinations of A
>3. (CHALLENGE): Combine the NOT logic gate with the AND logic gate and the OR logic gate from above
# CB Pseudo Code

A ← false

IF (NOT A) {
   DISPLAY("It's true!")
}

```python
# Python

A = True
B = True

if not A: # No equivalent bitwise syntax in python
    print("A false")
if A or B:
    print("partial?")
if A and B:
    print("completely true")

```

    partial?
    completely true


### XOR
>The XOR of two values is true whenever the values are different. It uses the ⊕ operator, and can be built from the basic operators: x⊕y = x*(not y) + (not x)*y 

| A | B | A XOR B |
|---|---|--------|
| 0 | 0 |   0    |
| 0 | 1 |   1    |
| 1 | 0 |   1    |
| 1 | 1 |   0    |

![image-3.png](http://www.categories.acsl.org/wiki/images/thumb/6/6d/Xor-gate-en.svg/192px-Xor-gate-en.svg.png)

Real-life example of XOR: If I play video games (A) XOR I watch a movie (B), I will be entertained :O

Another example: There is a light connected to two switches. If the first switch is on (A) XOR the second switch is on (B), then the light will turn on. Note here that flipping either switch (changing either input) changes the output.

The XOR gate is often use in binary calculators as well, because if two ones results in a zero, and an AND gate can be used to calculate the next bit.

#### Hack #4: XOR in Python
>1. Follow the "AND in Python" hack to add else output
>2. Try different combinations of A and B
>3. (CHALLENGE): Assuming True is 1 and False is 0, write an expression that takes two inputs and outputs the result of a XOR gate
# CB Pseudo Code

A ← false
B ← true

IF (A XOR B) {
   DISPLAY("It's true!")
}

```python
# Python

A = False
B = False

if A ^ B: # Only bitwise syntax, no "xor" keyword
    print("One true")
else:
    print("Types alike")
    
a = 1
b = 1
if (a+b)%2 == 1:
    print("XOR True")
else:
    print("XOR False")
```

    Types alike
    XOR False


### NAND
>NAND is the NOT of the result of AND. In other words, the result of NAND is true if at least one value is false.

| A | B | A NAND B |
|---|---|--------|
| 0 | 0 |   1    |
| 0 | 1 |   1    |
| 1 | 0 |   1    |
| 1 | 1 |   0    |

![image-3.png](http://www.categories.acsl.org/wiki/images/thumb/5/58/Nand-gate-en.svg/192px-Nand-gate-en.svg.png)

Real-life example of NAND: If I forget my computer (A) NAND I forget my phone (B), I can access the internet :P

#### Optional Hack: NAND in Python
>1. Follow the "AND in Python" hack to make the code applicable to a real-life example (e.g. forgetting your phone NAND forgetting your computer).
>2. Try different combinations of A and B
>3. Follow the "AND in Python" hack to add else output
# CB Pseudo Code

A ← false
B ← true

IF (NOT (A AND B)) {
   DISPLAY("It's true!")
}

```python
# Python

A = True
B = True

if not (A and B): 
    print("At least one false!")
else:
    print("Both true!")

```

    Both true!


### NOR
>NOR is the NOT of the result of OR. In other words, the result of NOR is true if and only if both values are false.

| A | B | A NOR B |
|---|---|--------|
| 0 | 0 |   1    |
| 0 | 1 |   0    |
| 1 | 0 |   0    |
| 1 | 1 |   0    |

![image-4.png](http://www.categories.acsl.org/wiki/images/thumb/9/94/Nor-gate-en.svg/192px-Nor-gate-en.svg.png)

Real-life example of NOR: If there's a fire (A) NOR there's an earthquake (B) then I'll be ok :S

#### Optional Hack: NOR in python
>1. Follow the "AND in Python" hack to make the code applicable to a real-life example (e.g. there's a fire NOR there's an earthquake).
>2. Try different combinations of A and B
>3. Follow the "AND in Python" hack to add else output
# CB Pseudo Code

A ← false
B ← true

IF (NOT (A OR B)) {
   DISPLAY("It's true!")
}

```python
# Python

A = False
B = False

if not (A or B):
    print("Both false")
else:
    print("At least one true")

```

    Both false


### De-Morgan's Law
>An OR (AND) expression that is negated is equal to the AND (OR) of the negation of each term. 

NOT (A AND B) = (NOT A) OR (NOT B)

- Using same beach example as above:
    - If it is sunny OR it is a weekend, I will go the beach (A AND B). If I go to the beach, I will NOT stay home.
    - The above can be simplified to if it is NOT sunny (A), OR NOT a weekend (B), I will stay home.

NOT (A OR B) = (NOT A) AND (NOT B)

- If it is NOT (my birthday (A) OR Christmas (B)), then I don't get a present
- The above is the same as if it is NOT my birthday (A) AND NOT Christmas (B), then I don't get a present

## Homework Hacks

1. There is one more logic gate, known as an XNOR, or exclusive-NOR gate. It is a combination of an XOR and a NOT gate. Create a table like the ones above to demonstrate input and output values of this gate.



<p>XNOR Response Table:</p>

| A | B | A XNOR B |
|---|---|--------|
| 0 | 0 |   1    |
| 0 | 1 |   0    |
| 1 | 0 |   0    |
| 1 | 1 |   1    |

2. Create python functions for three of the above logic gates. Implement two of them in an interactive program (with input) with a purpose.


```python
def and_gate(A,B):
    if A and B:
        return True
    else:
        return False
def xnor_gate(A,B):
    if A == B:
        return True
    else:
        return False
def nand_gate(A,B):
    if not A or not B:
        return True
    else:
        return False
    
s1 = float(input("Measured luminosity in solar units: "))
s2 = int(input("Derived temperature (K): "))

F_B = False
T_B = False

if 0.8 < s1 < 1.2:
    F_B = True
if 5000 < s2 < 6000:
    T_B = True

if and_gate(F_B,T_B) == True:
    print("Stellar characteristics are consistent with solar analogs.")
if nand_gate(F_B,T_B) == True:
    print("This star is not Sun-like.")
```

    Stellar characteristics are consistent with solar analogs.


3. Bob is grading homework from a peer teaching project. He needs to mark a student's homework as incomplete if they did NOT complete all the problems, OR did NOT submit it on time. Unfortunately, his teammate Cob did not give him any other information, and is now on vacation. Bob needs to do this using only TWO logic gates (don't ask why). Help Bob write a program to grade his class's homework!


```python
isComplete = {'Student 1': 1, 'Student 2': 1, 'Student 3': 0, 'Student 4': 1, 'Student 5': 0, 'Student 6': 1}
isOnTime = {'Student 1': 1, 'Student 2': 0, 'Student 3': 0, 'Student 4': 1, 'Student 5': 1, 'Student 6': 1}

## Extra: Format the output nicely

comp_status = {}
for student in isComplete:
    #I assumed one should be fine.
    if isComplete[student] and isOnTime[student]:
        comp_status[student] = "Complete"
    else:
        comp_status[student] = "Incomplete"
        
import pandas as pd
pd.DataFrame.from_dict(comp_status,orient='index',columns=['Status'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Student 1</th>
      <td>Complete</td>
    </tr>
    <tr>
      <th>Student 2</th>
      <td>Incomplete</td>
    </tr>
    <tr>
      <th>Student 3</th>
      <td>Incomplete</td>
    </tr>
    <tr>
      <th>Student 4</th>
      <td>Complete</td>
    </tr>
    <tr>
      <th>Student 5</th>
      <td>Incomplete</td>
    </tr>
    <tr>
      <th>Student 6</th>
      <td>Complete</td>
    </tr>
  </tbody>
</table>
</div>



4. BONUS:
Construct a XOR gate from a NAND gate, an OR gate, and an AND gate.


```python
def nandgate(a, b):
    if not (a and b):
        return True
    elif a and b:
        return False
    
def andgate(a, b):
    if a and b:
        return True
    elif not (a and b):
        return False
    
def orgate(a, b):
    if a or b:
        return True
    else:
        return False

def xorgate(a, b):
    return andgate(nandgate(a,b),orgate(a,b))

print(xorgate(True, True))
print(xorgate(True, False))
print(xorgate(False, True))
print(xorgate(False, False))
```

    False
    True
    True
    False

