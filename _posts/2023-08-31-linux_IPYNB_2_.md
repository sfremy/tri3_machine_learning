---
toc: True
comments: True
layout: post
title: Linux Shell & Bash Usage
description: Bash Tutorial .ipynb test.
type: hacks
courses: {'csp': {'week': 2, 'categories': ['4.A']}}
categories: ['C1.4']
---

# How to Use Bash
## Overview
<p>
Bash is a shell and command language used by most Linux operating systems. It is a command-line interface but can also read and execute commands from a file, as is being done here.
</p>

## Setup
<p>
To make a Bash script in VSCode's Jupyter notebook implementation, use 'Shell Script' as the cell type and open with "%%script bash".
</p>


```python
%%script bash
```

<p>
You can treat the cell as a terminal and input your command list. When run, it will treat the commands the same as a normal Linux shell.
</p>

## Hack
### Part 1
<p>
"Come up with your own student view of this procedure to show your tools are installed. It is best that you keep the few things you understand, add things later as you start to understand them." (I understand this to mean an installation/version check on the tools.)
</p>
<p>
Let's check the installation and version status of Python, Ruby, and Jupyter, and also check to see whether the student directory exists.
</p>


```python
%%script bash

echo "Python version check"
which python
python --version
echo ""

echo "Ruby version check"
which ruby
ruby -v
echo ""

echo "Jupyter version check"
which jupyter
jupyter --version
echo ""

echo "Try to navigate to VSCode directory and display its contents."
cd ~
cd vscode
ls
echo ""
```

### Part 2
<p>
"Name and create blog notes on some Linux commands you will use frequently."
</p>
<p>
Some of the most commonly used Bash commands are:
</p>

- ls (Lists the contents of the present directory.)
- pwd (Reports the current working directory.)
- cd (Changes the present working directory.)
- echo "" (Prints the contents of the "".)
- man (command) (Gives a user manual on said command.)
- which (Searches for the filename provided.)

### Part 3
<p>
"Is there anything we use to verify tools we installed? Review versions?"
</p>
<p>
The command <mark>--version</mark> can be used to retrieve the version numbers of tools. The command <mark>which</mark> can be used to find the filepath of whatever it is given, or returns /dev/null if it does not exist.
</p>

### Part 4
<p>
"How would you update a repository? Use the git command line?"
</p>
<p>
To update a Github repository, do this:
</p>


```python
%%script bash

# Navigate to your desired directory
$ git clone https://github.com/sfremy/csablog.git
```

<p>
This should replace the file specified in the <mark>clone</mark> command with the latest version linked.
</p>
