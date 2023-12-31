---
layout: base
title: Weather
---
<html>
<head>
    <style>
        @import url('https://fonts.googleapis.com/css?family=Jost');
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
        text{
            font-family: 'Jost';
        }
            ::-webkit-scrollbar {
        width: 8px;
    }
    ::-webkit-scrollbar-track {
        background: #333;
    }
    ::-webkit-scrollbar-thumb {
        background: #a0daf2;
        border-radius: 4px;
        width: 4px; 
    }
    ::-webkit-scrollbar-thumb:hover {
        background: #FFF;
        width: 4px;
    }
    </style>
</head>
<body>
    <div id="content">
        <h3>What's our weather like? 🌧️</h3>
        <button id="getWeatherButton">Get Current Weather</button>
        <div id="weatherData" class = "text"></div>
        <div id="clothingAdvice"></div>
         <div id="clothingImage" style="text-align: center;">
    <img id="hotImage" src="https://raw.githubusercontent.com/Soham360/sturdy-fiesta/main/images/279477144-37eedd64-48c1-45e7-ba55-75108b851efd.png" alt="Hot Weather" style="display: none; margin: 0 auto; width: 50%;">
    <img id="warmImage" src="https://github.com/Soham360/sturdy-fiesta/blob/main/images/279540917-7159ad70-8fb9-40b6-9bae-e1fa1b6ff07d.png?raw=true" alt="Warm Weather" style="display: none; margin: 0 auto; width: 50%;">
    <img id="mildImage" src="https://github.com/Soham360/sturdy-fiesta/blob/main/images/279541100-97edf9f8-0114-440f-b383-a5f327648cee.png?raw=true" alt="Mild Weather" style="display: none; margin: 0 auto; width: 50%;">
    <img id="coolImage" src="https://github.com/Soham360/sturdy-fiesta/blob/main/images/279540782-6104c0fe-2ac7-435b-bf75-1e1612592b5b.png?raw=true" alt="Cool Weather" style="display: none; margin: 0 auto; width: 50%;">
    <img id="coldImage" src="https://github.com/Soham360/sturdy-fiesta/blob/main/images/279541006-1afab2be-b2fe-42bf-85d1-c9c83cab7952.png?raw=true" alt="Cold Weather" style="display: none; margin: 0 auto; width: 50%;">

</div>
    </div>
    <script>
        document.getElementById("getWeatherButton").addEventListener("click", function() {
            const apiUrl = `https://no-papels.stu.nighthawkcodingsociety.com/api/weather/daily`;
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