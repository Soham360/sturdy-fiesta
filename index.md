---
layout: base
title: Home
---

| Week | Topics | Review Ticket | Summary |
|-|-|-|-|
| 0 | General Setup | [Link](https://github.com/Soham360/APCSA/issues/1) | This week we set up/updated the tools needed for this trimester. We also created a new github page instead of a fastpage because fastpages is now deprecated. I also added a theme to my github page. I wanted to make a custom theme but that requires a lot of css and causes a lot of formatting issues. I also added a typing game that gives you 5 words to type and you have to type them as fast as you can. |

Oh no! A markdown table! Please don't torture me Mr. Mortensen 🥺🥺


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