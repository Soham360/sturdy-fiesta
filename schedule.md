---
layout: base
title: Schedule
---
## Schedule
- This is the schedule for our project
<!DOCTYPE html>
<html>
<head>
    <title>Customizable Schedule</title>
</head>
<body>
    <div id="message"></div>
    <input type="date" id="startDate">
    <button onclick="startSchedule()">Start Schedule</button>
    <script>
        // Function to display a message
        function showMessage() {
            const messageDiv = document.getElementById('message');
            messageDiv.innerHTML = 'Your custom message here.';
        }
        // Schedule to display the message
        function startSchedule() {
            const startDate = new Date(document.getElementById('startDate').value);
            if (isNaN(startDate)) {
                alert('Please select a valid start date.');
                return;
            }  
            const endDate = new Date(startDate);
            endDate.setMonth(startDate.getMonth() + 3);
            // Clear any existing schedule (if any)
            if (window.scheduleInterval) {
                clearInterval(window.scheduleInterval);
            }
            showMessage(); // Display the message immediately
            // Schedule to display the message every 1 second
            window.scheduleInterval = setInterval(function () {
                const now = new Date();
                if (now >= endDate) {
                    clearInterval(window.scheduleInterval); // Stop the schedule
                    return;
                }
                showMessage();
            }, 1000);
        }
    </script>
</body>
</html>

