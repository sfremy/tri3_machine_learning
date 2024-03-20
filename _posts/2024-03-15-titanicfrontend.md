---
toc: true
comments: true
layout: post
title: Can You Survive the Titanic?
description: 
type: hacks
courses: { compsci: {week: 26} }
---
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Titanic Passenger Survival Prediction</title>
<style>
body {
  font-family: Arial, sans-serif;
  background-color: #212121;
  color: #fff;
}

.container {
  width: 50%;
  margin: 20px auto;
  background-color: #333;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

h2 {
  text-align: center;
}

form {
  margin-bottom: 20px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input[type="text"],
input[type="number"],
select {
  width: calc(100% - 18px);
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #555;
  border-radius: 4px;
  background-color: #444;
  color: #fff;
}

select {
  appearance: none;
}

button {
  background-color: #4CAF50;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  width: 100%;
}

button:hover {
  background-color: #45a049;
}

#result {
  font-size: 18px;
  text-align: center;
  margin-top: 20px;
}
</style>
</head>
<body>

<h2>Titanic Passenger Survival Prediction</h2>

<div class="container">
  <form id="predictionForm">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" pattern="[A-Za-z]+" title="Name must contain only alphabet letters" required>
    <label for="class">Class (1, 2, 3):</label>
    <input type="number" id="class" name="class" min="1" max="3" required>
    <label for="sex">Sex:</label>
    <select id="sex" name="sex" required>
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select>
    <label for="age">Age:</label>
    <input type="number" id="age" name="age" min="1" max="199" required>
    <label for="sibsp">Sibsp (number of siblings/spouses aboard):</label>
    <input type="number" id="sibsp" name="sibsp" min="0" max="99" required>
    <label for="parch">Parch (number of parents/children aboard):</label>
    <input type="number" id="parch" name="parch" min="0" max="99" required>
    <label for="fare">Fare:</label>
    <input type="number" id="fare" name="fare" min="0" step="0.01" required>
    <label for="embarked">Embarked (C, Q, S):</label>
    <input type="text" id="embarked" name="embarked" pattern="[CQS]" title="Enter C, Q, or S" required>
    <label for="alone">Alone:</label>
    <select id="alone" name="alone" required>
      <option value="true">True</option>
      <option value="false">False</option>
    </select>
    <button type="submit">Predict Survival</button>
  </form>

  <div id="surv"></div>
  <div id="death"></div>
</div>

<script>
document.getElementById("predictionForm").addEventListener("submit", function(event) {
  event.preventDefault(); // Prevent form submission
  predictSurvival(); // Call function to predict survival
});

function predictSurvival() {
  // Get input values from the form
  var formData = {
    name: document.getElementById("name").value,
    pclass: parseInt(document.getElementById("class").value),
    sex: document.getElementById("sex").value,
    age: parseFloat(document.getElementById("age").value),
    sibsp: parseInt(document.getElementById("sibsp").value),
    parch: parseInt(document.getElementById("parch").value),
    fare: parseFloat(document.getElementById("fare").value),
    embarked: document.getElementById("embarked").value,
    alone: document.getElementById("alone").value
  };
  const apiUrl = "http://127.0.0.1:8086/api/titanic/predict"
  // Send input data to server for prediction
  fetch(apiUrl, {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
      'Access-Control-Allow-Origin': 'http://127.0.0.1:4100',
      'Access-Control-Allow-Credentials': 'true'
    },
    body: JSON.stringify(formData)
  })
  .then(response => response.json())
  .then(data => {
    // Display prediction result
    document.getElementById("surv").innerHTML = data.survival;
    document.getElementById("death").innerHTML = data.death
  })
  .catch(error => {
    console.error("Error:", error);
    document.getElementById("surv").innerHTML = "An error occurred. Please try again.";
  });
}
</script>

</body>
</html>
