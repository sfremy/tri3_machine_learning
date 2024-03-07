---
toc: True
comments: True
layout: post
title: JS DOM Demonstration
description: JS DOM implementation for the JS Basics Test.
type: hacks
courses: {'csp': {'week': 5, 'categories': ['4.A']}}
categories: ['C1.4']
---

```python
%%html

<p id="e">I am a very cool guy</p>
<button id="buttonID" onclick="linkswitch()">Click here!</button>
<div>
    <p>I love my life</p>
    <p>I am in eleventh grade</p>
</div>

<a id="tlink" href="https://nighthawkcoders.github.io/teacher//2023/09/12/unit-1-summary.html">Teacher Website</a>
<a id="mlink" href="https://th35py27.github.io/CSP/">My website</a>

<p>I love CSP</p>

<div>
    <p>I love HTML</p>
    <p>I love divs</p>
</div>

<script>
    function linkswitch() {
        var link1 = document.getElementById("tlink");
        link1.innerHTML = "<a href='https://th35py27.github.io/CSP/'>Teacher Website</a>";
        var link2 = document.getElementById("mlink");
        link2.innerHTML = "<a href='https://nighthawkcoders.github.io/teacher//2023/09/12/unit-1-summary.html'>My Website</a>";
        var text1 = document.getElementById("e");
        text1.innerHTML = "<p>Links Switched!</p>";
    }
</script>

```



<p id="e">I am a very cool guy</p>
<button id="buttonID" onclick="linkswitch()">Click here!</button>
<div>
    <p>I love my life</p>
    <p>I am in eleventh grade</p>
</div>

<a id="tlink" href="https://nighthawkcoders.github.io/teacher//2023/09/12/unit-1-summary.html">Teacher Website</a>
<a id="mlink" href="https://th35py27.github.io/CSP/">My website</a>

<p>I love CSP</p>

<div>
    <p>I love HTML</p>
    <p>I love divs</p>
</div>

<script>
    function linkswitch() {
        var link1 = document.getElementById("tlink");
        link1.innerHTML = "<a href='https://th35py27.github.io/CSP/'>Teacher Website</a>";
        var link2 = document.getElementById("mlink");
        link2.innerHTML = "<a href='https://nighthawkcoders.github.io/teacher//2023/09/12/unit-1-summary.html'>My Website</a>";
        var text1 = document.getElementById("e");
        text1.innerHTML = "<p>Links Switched!</p>";
    }
</script>




```python
%%html
<head>
    <title>Button Click Example</title>
</head>
<body>
    <button id="myButton" onclick="myFunction()">Click Me</button>

    <script>
        function myFunction() {
            alert("Button Clicked!");
        }
    </script>
</body>
```


<head>
    <title>Button Click Example</title>
</head>
<body>
    <button id="myButton" onclick="myFunction()">Click Me</button>

    <script>
        function myFunction() {
            alert("Button Clicked!");
        }
    </script>
</body>




```python

```
