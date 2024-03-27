---
toc: true
comments: true
layout: post
title: Breast Cancer Prediction Form
description: Predict the likelihood of breast cancer
type: hacks
courses: { compsci: {week: 26} }
---

<body>
    <h1>Breast Cancer Prediction Form</h1>
    <form id="predictionForm">
        <label for="clumpThickness">Clump Thickness:</label>
        <input type="number" id="clumpThickness" name="clumpThickness" value="10"><br>
        <label for="cellSizeUniformity">Uniformity of Cell Size:</label>
        <input type="number" id="cellSizeUniformity" name="cellSizeUniformity" value="10"><br>
        <label for="cellShapeUniformity">Uniformity of Cell Shape:</label>
        <input type="number" id="cellShapeUniformity" name="cellShapeUniformity" value="10"><br>
        <label for="epithelialCellSize">Single Epithelial Cell Size:</label>
        <input type="number" id="epithelialCellSize" name="epithelialCellSize" value="8"><br>
        <label for="bareNuclei">Bare Nuclei:</label>
        <input type="number" id="bareNuclei" name="bareNuclei" value="10"><br>
        <label for="normalNucleoli">Normal Nucleoli:</label>
        <input type="number" id="normalNucleoli" name="normalNucleoli" value="10"><br>
        <label for="mitoses">Mitoses:</label>
        <input type="number" id="mitoses" name="mitoses" value="1"><br>
        <button type="submit">Predict</button>
    </form>
    <div id="result"></div>
    <script>
    document.getElementById("predictionForm").addEventListener("submit", function(event) {
        event.preventDefault();
        predictCancer();
    });
    function predictCancer() {
        var formData = {
            clumpThickness: parseInt(document.getElementById("clumpThickness").value),
            cellSizeUniformity: parseInt(document.getElementById("cellSizeUniformity").value),
            cellShapeUniformity: parseInt(document.getElementById("cellShapeUniformity").value),
            epithelialCellSize: parseInt(document.getElementById("epithelialCellSize").value),
            bareNuclei: parseInt(document.getElementById("bareNuclei").value),
            normalNucleoli: parseInt(document.getElementById("normalNucleoli").value),
            mitoses: parseInt(document.getElementById("mitoses").value)
        };
        const apiUrl = "http://127.0.0.1:8086/api/cancer/predict"
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
            document.getElementById("result").innerHTML = "Predicted Probability of Malignancy: " + (data.malignantProbability).toFixed(2);
        })
        .catch(error => {
            console.error("Error:", error);
            document.getElementById("result").innerHTML = "An error occurred. Please try again.";
        });
    }
    </script>
</body>