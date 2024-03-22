---
toc: true
comments: true
layout: post
title: NBA Player Performance Prediction
description: Predict the scoring performance of NBA players
type: hacks
courses: { compsci: {week: 26} }
---

<title>NBA Player Performance Prediction</title>
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

<h2>NBA Player Performance Prediction</h2>

<div class="container">
  <form id="predictionForm">
    <label for="age">Age:</label>
    <input type="number" id="age" name="age" min="18" max="40" required>
    <label for="FG">Field Goals:</label>
    <input type="number" id="FG" name="FG" min="0" required>
    <label for="FG%">Field Goal Percentage:</label>
    <input type="number" id="FG%" name="FG%" step="0.1" min="0" max="100" required>
    <label for="3P">Three-Point Field Goals:</label>
    <input type="number" id="3P" name="3P" min="0" required>
    <label for="3P%">Three-Point Percentage:</label>
    <input type="number" id="3P%" name="3P%" step="0.1" min="0" max="100" required>
    <label for="FT">Free Throws:</label>
    <input type="number" id="FT" name="FT" min="0" required>
    <label for="FT%">Free Throw Percentage:</label>
    <input type="number" id="FT%" name="FT%" step="0.1" min="0" max="100" required>
    <button type="submit">Predict Performance</button>
  </form>
  <div id="above10"></div>
  <div id="below10"></div>
</div>

<script>
document.getElementById("predictionForm").addEventListener("submit", function(event) { //event lister tells it to do predict survival
  event.preventDefault(); // Prevent form submission
  predictSurvival(); // Call function to predict survival
});

function predictSurvival() {
  // Get input values from the form
  var formData = {
    age: parseFloat(document.getElementById("age").value),
    FG: parseInt(document.getElementById("FG").value),
    FGpercent: parseInt(document.getElementById("FG%").value),
    threeP: parseFloat(document.getElementById("3P").value),
    threePpercent: document.getElementById("3P%").value
    FrT: parseFloat(document.getElementById("FT").value),
    FrTpercent: parseFloat(document.getElementById("FT%").value),
  };
  const apiUrl = "http://127.0.0.1:8086/api/nba/predict"
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
    document.getElementById("above10").innerHTML = "Chance of scoring 10+ PPG: " + (100*data.above10).toFixed(2) + "%";
    document.getElementById("below10").innerHTML = "Chance of scoring less than 10 PPG: " + (100*data.below10).toFixed(2) + "%";
  })
  .catch(error => {
    console.error("Error:", error);
    document.getElementById("above10").innerHTML = "An error occurred. Please try again.";
  });
}
</script>

</body>
</html>
