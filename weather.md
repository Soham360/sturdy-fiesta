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
    <div id="clothingAdvice"></div>
    <script>
        document.getElementById("getWeatherButton").addEventListener("click", function() {
            const latitude = 33.01479454987898;
            const longitude = -117.12140255005595;
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