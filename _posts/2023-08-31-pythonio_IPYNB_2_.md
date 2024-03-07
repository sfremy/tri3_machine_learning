---
toc: True
comments: True
layout: post
title: Python IO Hack
description: Python language structure tutorial.
type: hacks
courses: {'csp': {'week': 2, 'categories': ['4.A']}}
categories: ['C1.4']
---

# How to use Python
<p>
You've been working with Python for 10 years. You know what to do.
</p>

# Hacks
<p>
Build your own Jupyter Notebook meeting these College Board and CTE competencies
</p>

- Build your own quiz, including my questions and show outputs
- Create both Markdown for description and Code for execution
- Structure your Python code with comments “#” to complement Markdown descriptions

<p>
Additional requirements
</p>

- Build your quiz so that it captures the key Vocabulary from this Jupyter document
- Calculate the percentage of your quiz
- Review College Board Big Idea outline, see if you can reference locations in Markdown that support vocabulary

<p>
Extra credit, Advanced
</p>

- Do you see repeating pattern of code? Try to implement solution to avoid the repeating pattern (hint: list and iteration)

## Starting point
<p>
For starters, we have the original code:
</p>


```python
def question_and_answer(prompt):
    print("Question: " + prompt)
    msg = input()
    print("Answer: " + msg)

question_and_answer("Name the Python output command mentioned in this lesson?")
question_and_answer("If you see many lines of code in order, what would College Board call it?")
question_and_answer("Describe a keyword used in Python to define a function?")
```


```python
import getpass, sys

def question_with_response(prompt):
    print("Question: " + prompt)
    msg = input()
    return msg

questions = 3
correct = 0

print('Hello, ' + getpass.getuser() + " running " + sys.executable)
print("You will be asked " + str(questions) + " questions.")
question_and_answer("Are you ready to take a test?")

rsp = question_with_response("What command is used to include other functions that were previously developed?")
if rsp == "import":
    print(rsp + " is correct!")
    correct += 1
else:
    print(rsp + " is incorrect!")

rsp = question_with_response("What command is used to evaluate correct or incorrect response in this example?")
if rsp == "if":
    print(rsp + " is correct!")
    correct += 1
else:
    print(rsp + " is incorrect!")

rsp = question_with_response("Each 'if' command contains an '_________' to determine a true or false condition?")
if rsp == "expression":
    print(rsp + " is correct!")
    correct += 1
else:
    print(rsp + " is incorrect!")

print(getpass.getuser() + " you scored " + str(correct) +"/" + str(questions))
```

## My Solution
<p>
"Try to implement solution to avoid the repeating pattern."
</p>
<p>
In each iteration in the code provided, we see this identical pattern:
</p>


```python
rsp = question_with_response("Each 'if' command contains an '_________' to determine a true or false condition?")
if rsp == "expression":
    print(rsp + " is correct!")
    correct += 1
else:
    print(rsp + " is incorrect!")
```

<p>
Since this is the same every time and the only difference is the question and answer strings, we can just run through lists of questions and answers and substitute the instances into this function with a for loop. Defining this as a function allows us to call it for arbitrary <mark>qlist</mark> and <mark>answers</mark> arrays.
</p>
<p>
"Calculate the percentage of your quiz."
</p>
<p>
This can be done by simply multiplying the quantity <mark>correct/total</mark> by 100. Python has an inbuilt round() function which we can use to arbitrarily clip the resulting percentage.
</p>


```python
def quiz(qlist, answers):
    correct = 0
    if len(qlist) != len(answers):
        #Make sure that the two arrays are the same length.
        raise Exception("Each question needs an answer!")
    
    for i in range(len(qlist)):
        #Run through all the indices and ask the question for each one.
        rsp = question_with_response(qlist[i])
        if rsp == answers[i]:
            print(rsp + " is correct!")
            correct += 1
        else:
            print(rsp + " is incorrect!")
            
    #Calculate the percentage correctness and report it.
    print(getpass.getuser() + " you scored " + round(correct/len(qlist)*100,2) + "%")
```


<p>
"Build your quiz so that it captures the key Vocabulary from this Jupyter document"
</p>
<p>
Including the original questions, we can define a <mark>qlist</mark> and <mark>answers</mark> array for our quiz.
</p>


```python
qs = ["What command is used to include other functions that were previously developed?",
      "What command is used to evaluate correct or incorrect response in this example?", 
      "Each 'if' command contains an '_________' to determine a true or false condition?",
      "In what does Python store data that it is ordered to store?",
      "What is n_sigma in the Python expression: anticlip_data(view, n_sigma)?"]
ans = ["import", "if", "expression", "variables", "parameter"]
```
