---
layout: base
title: Weather
---
<html>
<head>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            text-align: center;
            color: #000; /* Set the text color to black */
        }
        h1 {
            color: #333;
        }
        button {
            background-color: #007BFF;
            color: #fff;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        p {
            margin: 0;
            padding: 10px 0;
        }
    </style>
</head>
<body>
    <div id="content">
        <button id="getWeatherButton">Get Current Weather</button>
        <div id="weatherData"></div>
        <div id="clothingAdvice"></div>
        <div id="clothingImage" style="text-align: center;">
    <img id="hotImage" src="https://github.com/DasMoge124/students/assets/75040379/37eedd64-48c1-45e7-ba55-75108b851efd" alt="Hot Weather" style="display: none; margin: 0 auto;">
    <img id="warmImage" src="https://github.com/AniCricKet/musical-guacamole/assets/91163802/97edf9f8-0114-440f-b383-a5f327648cee" alt="Warm Weather" style="display: none; margin: 0 auto;">
    <img id="mildImage" src="https://github.com/AniCricKet/musical-guacamole/assets/91163802/6104c0fe-2ac7-435b-bf75-1e1612592b5b" alt="Mild Weather" style="display: none; margin: 0 auto;">
    <img id="coolImage" src="https://github.com/AniCricKet/musical-guacamole/assets/91163802/7159ad70-8fb9-40b6-9bae-e1fa1b6ff07d" alt="Cool Weather" style="display: none; margin: 0 auto;">
    <img id="coldImage" src="https://github.com/AniCricKet/musical-guacamole/assets/91163802/1afab2be-b2fe-42bf-85d1-c9c83cab7952" alt="Cold Weather" style="display: none; margin: 0 auto;">
</div>
    </div>
    <script>
        document.getElementById("getWeatherButton").addEventListener("click", function() {
            const lat = 32.715736;
            const lon = -117.161087;
            const apiUrl = `https://api.weather.gov/points/${latitude},${longitude}`;
            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    // Get additional weather data
                    const forecast = data.properties.forecast;
                    fetch(forecast)
                        .then(response => response.json())
                        .then(forecastData => {
                            const currentWeather = forecastData.properties.periods[0];
                            const temperature = currentWeather.temperature;
                            const weatherConditions = currentWeather.shortForecast;
                            const precipitation = currentWeather.detailedForecast.includes('precipitation');
                            // Display temperature, weather conditions, and precipitation
                            const weatherDataElement = document.getElementById("weatherData");
                            weatherDataElement.innerHTML = `
                                <p>Temperature: ${temperature}°F</p>
                                <p>Weather Conditions: ${weatherConditions}</p>
                                <p>Chance of Precipitation: ${precipitation ? 'Yes' : 'No'}</p>
                                <p>${getClothingAdvice(temperature, weatherConditions, precipitation)}</p>
                            `;
                            // Show the corresponding image based on temperature range
                            const hotImage = document.getElementById("hotImage");
                            const warmImage = document.getElementById("warmImage");
                            const mildImage = document.getElementById("mildImage");
                            const coolImage = document.getElementById("coolImage");
                            const coldImage = document.getElementById("coldImage");
                            // Hide all images initially
                            hotImage.style.display = "none";
                            warmImage.style.display = "none";
                            mildImage.style.display = "none";
                            coolImage.style.display = "none";
                            coldImage.style.display = "none";
                            if (temperature >= 80) {
                                hotImage.style.display = "block";
                            } else if (temperature >= 70) {
                                warmImage.style.display = "block";
                            } else if (temperature >= 60) {
                                mildImage.style.display = "block";
                            } else if (temperature >= 40) {
                                coolImage.style.display = "block";
                            } else {
                                coldImage.style.display = "block";
                            }
                        })
                        .catch(error => {
                            console.error("An error occurred:", error);
                        });
                })
                .catch(error => {
                    console.error("An error occurred:", error);
                });
        });
        function getClothingAdvice(temperature, weatherConditions, precipitation) {
            if (temperature >= 80) {
                return "It's hot! Wear light and breathable clothing like short sleeves and shorts. Don't forget sunscreen!";
            } else if (temperature >= 70) {
                return "It's warm. Consider wearing short sleeves and pants or a skirt.";
            } else if (temperature >= 60) {
                if (precipitation) {
                    return "It's mild and may rain. A light jacket or sweater with an umbrella might be a good idea.";
                } else {
                    return "It's mild. A light jacket or sweater might be a good idea.";
                }
            } else if (temperature >= 40) {
                return "It's cool. Wear long sleeves and pants. You may want to add a jacket.";
            } else {
                return "It's cold. Bundle up with a warm coat, gloves, and a scarf.";
            }
        }
    </script>
</body>
</html>