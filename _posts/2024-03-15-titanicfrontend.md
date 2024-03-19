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
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f2f2f2;
        }
        h1 {
            text-align: center;
            margin-top: 20px;
        }
        form {
            width: 300px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        label {
            display: block;
            margin-bottom: 10px;
            color: black;
        }
        input[type="text"],
        input[type="number"] {
            width: calc(100% - 12px);
            padding: 6px;
            margin-bottom: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            width: 100%;
            padding: 10px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        #result {
            width: 300px;
            margin: 20px auto;
            padding: 10px;
            background-color: #dff0d8;
            border: 1px solid #c3e6cb;
            border-radius: 4px;
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>Titanic Database Frontend</h1>
    <div id="result"></div>
    <form id="passengerForm">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <label for="pclass">Passenger Class (1st, 2nd, 3rd):</label>
        <input type="number" id="pclass" name="pclass" min="1" max="3" required>
        <label for="sex">Sex (male/female):</label>
        <input type="text" id="sex" name="sex" required>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" required>
        <label for="sibsp">Number of Siblings/Spouses Aboard:</label>
        <input type="number" id="sibsp" name="sibsp" required>
        <label for="parch">Number of Parents/Children Aboard:</label>
        <input type="number" id="parch" name="parch" required>
        <label for="fare">Passenger Fare:</label>
        <input type="number" id="fare" name="fare" min="0" required>
        <label for="alone">Alone (true/false):</label>
        <input type="text" id="alone" name="alone" required>
        <button type="submit">Predict Survival</button>
    </form>
    <script>
        document.getElementById('passengerForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const formData = new FormData(this);
            const passenger = {
                name: formData.get('name'),
                pclass: parseInt(formData.get('pclass')),
                sex: formData.get('sex'),
                age: parseInt(formData.get('age')),
                sibsp: parseInt(formData.get('sibsp')),
                parch: parseInt(formData.get('parch')),
                fare: parseFloat(formData.get('fare')),
                alone: formData.get('alone') === 'true'
            };
            fetch('http://127.0.0.1:8086/api/titanic/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(passenger)
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('result').innerText = data.alive_proba;
            })
            .catch(error => {
                console.error('Error:', error);
            });
        });
    </script>
</body>
</html>
