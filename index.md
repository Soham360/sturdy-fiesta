---
layout: base
title: Home
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Display Local Time</title>
</head>
<body>
    <div id="time"></div>
    <script>
        // Get the current date and time
            const now = new Date();
        // Get the hours, minutes, and seconds
        const hours = now.getHours();
        const minutes = now.getMinutes();
        const seconds = now.getSeconds();
        // Display the time in a 12-hour format with AM/PM
        const ampm = hours >= 12 ? 'PM' : 'AM';
        const formattedHours = hours % 12 || 12; // Convert 0 to 12 for 12 AM
        const timeString = `${formattedHours}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')} ${ampm}`;
        // Display the time on the webpage
        const timeElement = document.getElementById('time'); // Change 'time' to the ID of your HTML element
        timeElement.textContent = timeString;
        function updateClock() {
            // Get the current date and time
            const now = new Date();
            // Get the hours, minutes, and seconds
            const hours = now.getHours();
            const minutes = now.getMinutes();
            const seconds = now.getSeconds();
            // Display the time in a 12-hour format with AM/PM
            const ampm = hours >= 12 ? 'PM' : 'AM';
            const formattedHours = hours % 12 || 12; // Convert 0 to 12 for 12 AM
            const timeString = `${formattedHours}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')} ${ampm}`;
            // Display the time on the webpage
            const timeElement = document.getElementById('time'); // Change 'time' to the ID of your HTML element
            timeElement.textContent = timeString;
        }
        // Call updateClock initially to set the time
        updateClock();
        // Update the clock every second
        setInterval(updateClock, 1000);
    </script>
</body>
</html>