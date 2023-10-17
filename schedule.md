---
layout: base
title: Schedule
---
## Schedule
- This is the schedule
<!DOCTYPE html>
<html>
<head>
    <title>The Current Schedule So far</title>
</head>
<body>
    <div id="message"></div>
    <script>
        // Function to display a message
        function showMessage() {
            const messageDiv = document.getElementById('message');
            messageDiv.innerHTML = 'Hello, World!';
        }
        // Schedule to display the message every second
        function startSchedule() {
            showMessage(); // Display the message immediately
            setInterval(showMessage, 1000); // Repeat every 1000 milliseconds (1 second)
        }
        // Start the schedule when the page loads
        window.onload = startSchedule;
    </script>
</body>
</html>
