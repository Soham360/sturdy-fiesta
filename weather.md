---
layout: base
title: Weather
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
            const latitude = 33.01479454987898;
            const longitude = -117.12140255005595;
            const apiUrl = `https://api.weather.gov/points/${latitude},${longitude}`;
            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    // Extract and display relevant data
                    const properties = data.properties;
                    const forecast = properties.forecast;
                    const forecastZone = properties.forecastZone;
                    const weatherDataElement = document.getElementById("weatherData");
                    weatherDataElement.innerHTML = `
                        <p>Forecast URL: ${forecast}</p>
                        <p>Forecast Zone: ${forecastZone}</p>
                    `;
                })
                .catch(error => {
                    console.error("An error occurred:", error);
                });
        });
    </script>
</body>
</html>
