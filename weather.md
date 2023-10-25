---
layout: base
title: Home
---
<html>
<head>
    <title>Weather Data</title>
</head>
<body>
    <button id="getWeatherButton">Get Weather Data</button>
    <div id="weatherData"></div>
    <script>
        document.getElementById("getWeatherButton").addEventListener("click", function() {
            const latitude = 39.7456;
            const longitude = -97.0892;
            const apiUrl = `https://api.weather.gov/points/${latitude},${longitude}`;
            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    // Process and display the weather data
                    const weatherDataElement = document.getElementById("weatherData");
                    weatherDataElement.innerHTML = JSON.stringify(data, null, 2);
                })
                .catch(error => {
                    console.error("An error occurred:", error);
                });
        });
    </script>
</body>
</html>
