---
toc: True
comments: True
layout: post
title: SASS Javascript Login and Signup Page
description: Team teach about SASS Javascript login and signup page
courses: {'compsci': {'week': 20}}
type: hacks
---

## What exactly is SASS?
- SASS stands for Syntactically Awesome Stylesheet
- SASS adds extra toools to make styling websites easier and faster. Is is essentially a way to make writing and organzing styles more convinient.

### 1. Why use SASS for your Javascript Login and Signup Page?
- SASS allows you to write flexible and organized stylesheets by using features like variables, mixins, and nesting. This can make your code more maintainable and easier to understand, especially as your project grows
- SASS allows you to use variables to store values, such as colors or font sizes
- SASS code can be compiled into regular CSS, ensuring compatibility with all browsers

### Variables in SASS:
- Variables in SASS allow you to store values that you can reuse throughout your stylesheet. For instance, you can use them for colors, font sizes, or any other value you want to reuse. This makes it easy to maintain a consistent look and feel across your application.


```python
$primary-color: #3498db;
body {
  background-color: $primary-color;
}
```


      Cell In[1], line 1
        $primary-color: #3498db;
        ^
    SyntaxError: invalid syntax



### Mixins for Reusable Styles:
- Mixins are a powerful feature in SASS that lets you define a set of styles and reuse them throughout your stylesheet. This allows for a cleaner and more modular code by encapsulating styles into reusable patterns.



```python
@mixin button-styles {
    background-color: $primary-color;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
  }
  button {
    @include button-styles;
  }  
```

### Nesting in SASS:
- SASS allows you to nest your styles which makes your stylesheet more readable and mirroring the HTML structure. This feature enhances maintainability and helps you visualize the hierarchy of your styles.


```python
nav {
    background-color: $primary-color;
    ul {
      list-style: none;
      li {
        display: inline-block;
        margin-right: 10px;
        a {
          color: #fff;
          text-decoration: none;
        }
      }
    }
  }  
```

## JavaScript Integration
### Handling Asynchronous Requests:
- Asynchronous programming in JavaScript is crucial for tasks like fetching data from a server without blocking other operations. In the context of a login/signup page, it ensures a smooth user experience while the authentication process is underway.


```python
async function loginUser(username, password) {
    // Asynchronous logic using Fetch API
  }  
```

### Fetch API:
- The Fetch API is a modern JavaScript API for making network requests. It simplifies the process of sending HTTP requests and handling responses. It is widely used for AJAX-style requests in web applications.


```python
fetch('https://api.example.com/login', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({ username: 'user', password: 'pass' }),
});

```

### Sending POST Requests:
- In the context of a login/signup page, sending a POST request is fundamental for securely transmitting user credentials to the server. The Fetch API is employed to initiate this request, and the 'POST' method indicates the intention to submit data.


```python
async function loginUser(username, password) {
    const response = await fetch('https://api.example.com/login', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({ username, password }),
    });
  
    const data = await response.json();
    // Handle response data
  }  
```

### Error Handling for HTTP Status Codes:
- Proper error handling is essential for providing a meaningful user experience. This section covers how to handle various HTTP status codes returned by the server, such as success (200), unauthorized (401), forbidden (403), and not found (404). Each status code triggers a specific response, ensuring the user is informed of the outcome of their request.


```python
if (response.ok) {
    // Successful login logic
  } else if (response.status === 401) {
    // Handle unauthorized access
  } else if (response.status === 403) {
    // Handle forbidden access
  } else if (response.status === 404) {
    // Handle not found
  }  
```


```python
'https://drishyamody.github.io/DJAKTri2//2023/01/22/SASS_Javascript_Login.html'
```
