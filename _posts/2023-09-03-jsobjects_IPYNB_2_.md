---
toc: True
comments: True
layout: post
title: JS Tutorial
description: General tutorial for JavaScript basic functionality.
type: hacks
courses: {'csp': {'week': 3, 'categories': ['4.A']}}
categories: ['C1.4']
---

# Summary (Hack 1)
<p>
Hack: Adapt this tutorial to your own work and interests, how many steps do you understand?
</p>
<p>
Let's take a look at the tutorial code provided:
</p>

## Block 1
<p>
This opens up an HTML window which makes a header with <mark>%%html</mark>.
</p>
<p>
Using the <mark>style</mark> tag, the header's background colour is set as a blue-black (hex code #353b45), 10 pixels of padding are added between the header and the edges of the window, and a 3-pixel grey border (hex code #ccc).
</p>
<p>
The header contains the text specified in the <mark>div</mark> data container "output", specifically "Hello!".
</p>


```python
%%html
<html>
    <head>
        <style>
            #output {
                background-color: #353b45;
                padding: 10px;
                border: 3px solid #ccc;
            }
        </style>
    </head>
    <body>
        <p id="data" hidden>
        </p>
        <div id="output">
            Hello!
        </div>
    </body>
</html>
```

## Block 2
<p>
console.log() prints out the string passed to it within the browser console. Here, we are passing the strings <mark>"JavaScript/Jupyter Output Intro"</mark> and <mark>"Hellow World!"</mark>. <mark>alert()</mark> prints a string to a pop-up alert within the Jupyter browser window.
</p>
<p>
getElementById is setting "output" to "Hello World!" but I'm unsure of the functionality of the element.textContext definitinon.
</p>


```python
%%js // required to allow cell to be JavaScript enabled

console.log("JavaScript/Jupyter Output Intro");

// Browser Console output; debugging or tracing
console.log("Hello, World!");

// Set element in HTML above using DOM (Document Object Model)
document.getElementById("output").textContent = "Hello, World!";

// Jupyter built in magic element for testing and convenience of development
element.textContent = "Hello, World!";  // element is an output option as part of %%js magic

alert("Hello, World!");
```

## Block 3
<p>
The variable msg is set using <mark>var</mark> to the string "Hello, World Again!". This string is appended to "output" and the contents of msg are printed to the console and Jupyter with <mark>console.log()</mark> and <mark>alert()</mark>.
</p>


```python
%%js
console.log("Variable Definition");

var msg = "Hello, World Again!";

// Use msg to output code to Console and Jupyter Notebook
console.log(msg);  //right click browser select Inspect, then select Console to view
document.getElementById("output").textContent = msg;
element.append(msg);
alert(msg);

```

## Block 4
<p>
This defines a function called <mark>logIt</mark> which takes a parameter <mark>msg</mark>. It appends this parameter to <mark>element</mark> and appends to <mark>"output"</mark>.
</p>
<p>
Two variables, <mark>msg</mark> and <mark>classOf</mark> are defined as the strings "Hello, Students!" and "Welcome CS class of 2023-2024.". A concatentation of these strings (which would be "Hello, Students! Welcome CS class of 2023-2024.") is passed to the funciton logIt.
</p>


```python
%%js
console.log("Function Definition");

/* Function: logIt
 * Parameter: output
 * Description: The parameter is "output" to console and jupyter page
*/
function logIt(msg) {
    console.log(msg); 
    element.append(msg);
    document.getElementById("output").textContent = msg;
    //alert(output);
}

// sequence of code build logIt parameter using concatenation
var msg = "Hello, Students!" // replaces content of variable
var classOf = "Welcome CS class of 2023-2024."
logIt(msg + "  " + classOf); // concatenation of strings
```

## Block 5
<p>
A number of functions are defined.  
</p>

- <mark>getType</mark> returns the variable type of its parameter <mark>output</mark> using <mark>typeof</mark>.
- <mark>logIt</mark> is unchanged, except also logging <mark>console.info(msg)</mark>, the object information of the parameter.
- logIt is used to append the string <mark>"Mr M"</mark>, the integer <mark>1997</mark>, and the boolean <mark>true</mark>, the array <mark>scores = [90, 80, 100]</mark>, and the dictionary <mark>person = {"name":"Mr M", "role":"teacher"}</mark>.


```python
%%js
console.log("Examine Data Types");

// Function to add typeof to output
function getType(output) {
    return typeof output + ": " + output;
}

// Function defintion
function logIt(msg) {
    console.log(getType(msg));  // logs string
    console.info(msg);          // logs object
    document.getElementById("output").textContent = msg;
    element.append(getType(msg) + " ");  // adds to Jupyter output
    //alert(getType(msg));
}

// Common Types
element.append("Common Types ");
logIt("Mr M"); // String
logIt(1997);    // Number
logIt(true);    // Boolean

// Object Type, this definition is often called a array or list
element.append("Object Type, array ");
var scores = [
    90,
    80, 
    100
];  
logIt(scores);

// Complex Object, this definition is often called hash, map, hashmap, or dictionary
element.append("Object Type, hash or dictionary ");
var person = { // key:value pairs seperated by comma
    "name": "Mr M", 
    "role": "Teacher"
}; 
logIt(person);
logIt(JSON.stringify(person));  //method used to convert this object into readable format
```


```python

```

## Block 6
<p>
A class <mark>Person</mark> is defined, which allows all the associated data to be stored as a variable.
</p>

- <mark>constructor</mark> is used to pass parameters given when Person() is called: <mark>name, ghID, classOf, role</mark>
- The function <mark>setRole</mark> overwrites the parameter <mark>role</mark> of the class <mark>Person</mark>.
- The fucnction <mark>getJSON</mark> creates a dictionary indentifying each parameter with its value in the Person instance.
- The function <mark>logIt</mark> appends the JSON object made by <mark>getJSON</mark> to <mark>"outputs"</mark>.

<p>
Two Person instances are made: one callled <mark>teacher</mark> and another called <mark>student</mark>. <mark>teacher</mark>'s role is also set to "teacher".
</p>


```python
%%js
console.log("Person objects");

/* class: Person
 * Description: A collection of Person data
*/
class Person {
  /* method: constructor
   * parameters: name, ghID - GitHub ID, classOf - Graduation Class 
   * description: returns object when "new Person()" is called with matching parameters
   * assignment: this.name, this.ghID, ... are properties retained in the returned object
   * default: role uses a default property, it is set to "Student"
  */
  constructor(name, ghID, classOf, role="Student") {
    this.name = name;
    this.ghID = ghID;
    this.classOf = classOf;
    this.role = role;
  }

  /* method: setter
   * parameters: role - role in classroom
   * description: this.role is updated from default value to value contained in role parameter
  */
  setRole(role) {
    this.role = role;
  }
  
  /* method: getter
   * description: turns properties of object into JSON object
   * return value: JSON object
  */
  getJSON() {
    const obj = {type: typeof this, name: this.name, ghID: this.ghID, classOf: this.classOf, role: this.role};
    const json = JSON.stringify(obj);
    return json;
  }

  /* method: logIT
   * description: this Person object is logged to console
  */
  
  logIt() {
    //Person Object
    console.info(this);
       
    // HTML output
    document.getElementById("output").textContent = this.getJSON();

    //Log to Jupter
    element.append(this.role + " object in JSON: ");
    element.append(this.getJSON());  
    element.append(" ");


    //alert(this.getJSON());
  }
    
}

// make a new Person Object
const teacher = new Person("Mr M", "jm1021", 1977); // object type is easy to work with in JavaScript
// update role to Teacher
var role = "Teacher";
teacher.setRole(role); // set the role
teacher.logIt();  // log to console

// make a new Person Object
const student = new Person("Jane Doe", "jane", 2007); // object type is easy to work with in JavaScript
student.logIt(); // log to console
```

## Block 7
<p>
Class <mark>Person</mark> is unchanged. Another class, <mark>Classroom</mark>, is created and takes two parameters, <mark>teacher</mark> and <mark>students</mark>. An array <mark>classroom</mark> is created and recorded in the function <mark>logIt</mark>. A function <mark>constructCompsciClassroom()</mark> makes an instance of <mark>Classroom</mark> with preset teacher and student <mark>Person</mark> instances.
</p>


```python
%%js
console.log("Classroom object");

/* class: Person
 * Description: A collection of Person data
*/
class Person {
  /* method: constructor
   * parameters: name, ghID - GitHub ID, classOf - Graduation Class 
   * description: returns object when "new Person()" is called with matching parameters
   * assignment: this.name, this.ghID, ... are properties retained in the returned object
   * default: this.role is a default property retained in object, it is set to "Student"
  */
  constructor(name, ghID, classOf, role="Student") {
    this.name = name;
    this.ghID = ghID;
    this.classOf = classOf;
    this.role = role;
  }

  /* method: setter
   * parameters: role - role in classroom
   * description: this.role is updated from default value to value contained in role parameter
  */
  setRole(role) {
    this.role = role;
  }
  
  /* method: getter
   * description: turns properties of object into JSON object
   * return value: JSON object
  */
  getJSON() {
    const obj = {type: typeof this, name: this.name, ghID: this.ghID, classOf: this.classOf, role: this.role};
    const json = JSON.stringify(obj);
    return json;
  }

  /* method: logIT
   * description: this Person object is logged to console
  */
  logIt() {
    //Person Object
    console.info(this);
    // HTML output tag
    document.getElementById("output").textContent = this.getJSON();

    //Log to Jupter
    element.append("Person json <br>");
    element.append(this.getJSON() + "<br>"); 

    //alert(this.getJSON());
  }
    
}

/* class: Classroom
 * Description: A collection of Person objects
*/
class Classroom {
  /* method: constructor
   * parameters: teacher - a Person object, students - an array of Person objects
   * description: returns object when "new Classroom()" is called containing properties and methods of a Classroom
   * assignment: this.classroom, this.teacher, ... are properties retained in the returned object
  */
  constructor(teacher, students) {
    /* spread: this.classroom contains Teacher object and all Student objects
     * map: this.json contains of map of all persons to JSON
    */
    this.teacher = teacher;
    this.students = students;
    this.classroom = [teacher, ...students]; // ... spread option
    this.json = '{"classroom":[' + this.classroom.map(person => person.getJSON()) + ']}';
  }

  /* method: logIT
   * description: this Classroom object is logged to console
  */
  logIt() {
    //Classroom object
    console.log(this);

    // HTML output
    document.getElementById("data").textContent = this.json;
    document.getElementById("output").textContent = this.json;

    //Classroom json
    element.append("Classroom object in JSON: ");
    element.append(this.json);

    //alert(this.json);
  }
}

/* function: constructCompSciClassroom
 * Description: Create data for Classroom and Person objects
 * Returns: A Classroom Object
*/
function constructCompSciClassroom() {
    // define a Teacher object
    const teacher = new Person("Mr M", "jm1021", 1977, "Teacher");  // optional 4th parameter

    // define a student Array of Person objects
    const students = [ 
        new Person("Anthony", "tonyhieu", 2022),
        new Person("Bria", "B-G101", 2023),
        new Person("Allie", "xiaoa0", 2023),
        new Person("Tigran", "Tigran7", 2023),
        new Person("Rebecca", "Rebecca-123", 2023),
        new Person("Vidhi", "VidhiKulkarni", 2024)
    ];

    // make a CompSci classroom from formerly defined teacher and student objects
    return new Classroom(teacher, students);  // returns object
}

// assigns compsci to the object returned by "constructCompSciClassroom()" function
const compsci = constructCompSciClassroom();
// output of Objects and JSON in CompSci classroom
compsci.logIt();

```

## Block 8
<p>
The variable <mark>jsonText</mark> is assigned to the contents of "data". The variable <mark>classroom</mark> is assigned to the <mark>.classroom</mark> property of jsonText.
</p>
<p>
A HTML table is generated under the variable htmlOut, with columns corresponding to the categories in Person and the contents of <mark>classroom</mark>. This is the same format as the HTML table shown in the JQuery hack.
</p>


```python
%%js
console.log("Classroom Web Page");

// extract JSON text from output element in HTML page
const jsonText = document.getElementById("data").innerHTML;

// convert JSON text to a JavaScript Object to process
const classroom = JSON.parse(jsonText).classroom;
console.log(classroom);

// make an HTML Out format for pretty display
/* Template literals (`), can make HTML generation more concise;
 * the map functions generates row strings and the join method combines them;
 * this replaces longer and ugly for loop and string concatenation.
*/
const htmlOut = `
    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>GitHub ID</th>
                <th>Class Of</th>
                <th>Role</th>
            </tr>
        </thead>
        <tbody>
            ${classroom.map(row => `
                <tr>
                    <td>${row.name}</td>
                    <td>${row.ghID}</td>
                    <td>${row.classOf}</td>
                    <td>${row.role}</td>
                </tr>
            `).join('')}
        </tbody>
    </table>
`;

// assign/set htmlOut to output element in HTML page
document.getElementById("output").innerHTML = htmlOut;

// show raw HTML
console.log(htmlOut);
element.append(htmlOut);
```

# Hacks
<p>
console.log() can bring errors to attention by identifying incorrect outputs at various steps within the code process. In this JavaScript file we report elements of <mark>Person</mark> and <mark>Classroom</mark> during processing. If a datatype is incorrect, it will be shown.
</p>
