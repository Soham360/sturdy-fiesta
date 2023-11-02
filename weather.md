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

<!-- <html>
<head>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            text-align: center;
            color: #000;
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
<html>
<body>
    <button id="getWeatherButton">Get Current Weather</button>
    <div id="weatherData"></div>
    <div id="clothingAdvice"></div>
    <script>
        function fetchWeatherData() {
            fetch('https://no-papels.stu.nighthawkcodingsociety.com//api/WeatherRequest')
                .then(response => response.json())
                .then(data => {
                    // Extract and display relevant data
                    const temperature = data.temperature;
                    const weatherConditions = data.weatherConditions;
                    const precipitation = data.precipitation;
                    const weatherDataElement = document.getElementById("weatherData");
                    weatherDataElement.innerHTML = `
                        <p>Temperature: ${temperature}°F</p>
                        <p>Weather Conditions: ${weatherConditions}</p>
                        <p>Chance of Precipitation: ${precipitation ? 'Yes' : 'No'}</p>
                    `;
                    const clothingAdviceElement = document.getElementById("clothingAdvice");
                    clothingAdviceElement.textContent = getClothingAdvice(temperature, weatherConditions, precipitation);
                })
                .catch(error => {
                    console.error('Error:', error);
                });
        }
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
        document.getElementById("getWeatherButton").addEventListener("click", function() {
            fetchWeatherData();
        });
        fetchWeatherData();
    </script>
</body>
</html> -->
