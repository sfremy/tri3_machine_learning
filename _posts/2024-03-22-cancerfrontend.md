---
toc: true
comments: true
layout: post
title: Cancer Prediction Form
description: Predict the scoring performance of NBA players
type: hacks
courses: { compsci: {week: 26} }
---

</head>
<body>
    <h1>Breast Cancer Prediction Form</h1>
    <form id="predictionForm">
        <label for="clumpThickness">Clump Thickness:</label>
        <input type="number" id="clumpThickness" name="clumpThickness"><br>
        <label for="cellSizeUniformity">Uniformity of Cell Size:</label>
        <input type="number" id="cellSizeUniformity" name="cellSizeUniformity"><br>
        <label for="cellShapeUniformity">Uniformity of Cell Shape:</label>
        <input type="number" id="cellShapeUniformity" name="cellShapeUniformity"><br>
        <label for="marginalAdhesion">Marginal Adhesion:</label>
        <input type="number" id="marginalAdhesion" name="marginalAdhesion"><br>
        <label for="epithelialCellSize">Single Epithelial Cell Size:</label>
        <input type="number" id="epithelialCellSize" name="epithelialCellSize"><br>
        <label for="bareNuclei">Bare Nuclei:</label>
        <input type="number" id="bareNuclei" name="bareNuclei"><br>
        <label for="blandChromatin">Bland Chromatin:</label>
        <input type="number" id="blandChromatin" name="blandChromatin"><br>
        <label for="normalNucleoli">Normal Nucleoli:</label>
        <input type="number" id="normalNucleoli" name="normalNucleoli"><br>
        <label for="mitoses">Mitoses:</label>
        <input type="number" id="mitoses" name="mitoses"><br>
        <button type="submit">Predict</button>
    </form>
    <div id="predictionResult"></div>
    <script>
        document.getElementById('predictionForm').onsubmit = function(event) {
            event.preventDefault();
            const formData = new FormData(event.target);
            const data = {};
            formData.forEach((value, key) => {
                data[key] = value;
            });
            fetch('/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(data),
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('predictionResult').textContent = 'Prediction result: ' + (data.prediction === 1 ? 'Malignant' : 'Benign');
            })
            .catch(error => {
                console.error('Error:', error);
                document.getElementById('predictionResult').textContent = 'Error predicting the result';
            });
        };
    </script>
</body>
</html>
