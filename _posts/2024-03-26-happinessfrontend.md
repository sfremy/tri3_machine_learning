---
toc: true
comments: true
layout: post
title: Happiness of a Fictional Country
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

<h2>How Happy is Your Country?</h2>

<div class="container">
  <form id="predictionForm">
    <!--Location select: Note that the options pass encoded values.-->
    <label for="loc">Where Are You?</label>
    <select id="loc" name="loc" required>
      <option value="0">Southeast Asia</option>
      <option value="1">South Asia</option>    
      <option value="2">Western Europe</option>  
      <option value="3">North America</option>
      <option value="4">East Asia & Pacific Islands</option>    
      <option value="5">Middle East & North Africa</option>    
      <option value="6">Central & Eastern Europe</option>
      <option value="7">Latin America & Caribbean</option>
      <option value="8">Former USSR</option>    
      <option value="9">Sub-Saharan Africa</option>    
    </select>
    <!--Per Capita GDP input-->
    <label for="wealth">Per Capita Yearly GDP ($):</label>
    <input type="number" id="wealth" name="wealth" value = "12647" required>
    <!--Social Support input-->
    <label for="soc">Social Support (Scale 0 - 1)</label>
    <input type="number" id="soc" name="soc" min="0" max="1"  value = "0.5" required>
    <!--Life Expectancy input-->
    <label for="life">Life Expectancy, in years</label>
    <input type="number" id="life" name="life" value = "50" required>
    <!--Freedom input-->
    <label for="freedom">Social Freedom (Scale 0 - 1)</label>
    <input type="number" id="freedom" name="freedom" min="0" max="1" value = "0.5" required>
    <!--Year input-->
    <label for="year">What year is it?</label>
    <input type="number" id="year" name="year" value = "2020" required>
    <button type="submit">Predict Happiness</button>
  </form>
  <div id="result"></div>
</div>

<script>
//Adds an event listner for when the submit button is pushed
document.getElementById("predictionForm").addEventListener("submit", function(event) {
    event.preventDefault();
    predictHappiness();
  });

//Get data from the HTML elements
function predictHappiness() {
    //Define formData as a JSON containing all of the elements
    var formData = {
        year: parseInt(document.getElementById("year").value),
        //Take base 10 log of "wealth"
        money: Math.log10(parseFloat(document.getElementById("wealth").value)),
        social: parseFloat(document.getElementById("soc").value),
        lifespan: parseFloat(document.getElementById("life").value),
        freedom: parseFloat(document.getElementById("freedom").value),
        location: parseInt(document.getElementById("loc").value)
    };

//Set API url
const apiUrl = "http://127.0.0.1:8086/api/happiness/predict"

//Send data to backend and report prediction
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
    document.getElementById("result").innerHTML = "Your Country's Happiness Score: " + (data.score).toFixed(2);
  })
  .catch(error => {
    console.error("Error:", error);
    document.getElementById("surv").innerHTML = "An error occurred. Please try again.";
  });
}
</script>

</body>
</html>
