---
layout: base
title: Home
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>School Schedule Tracker</title>
</head>
<body>
    <div id="time"></div>
    <div id="scheduleResults"></div>
    <script>
        // Function to calculate the time left in a period
        function calculateTimeLeft(currentTime, startTime, endTime) {
            const current = new Date(currentTime);
            const start = new Date(currentTime);
            const end = new Date(currentTime);
            start.setHours(startTime.split(':')[0]);
            start.setMinutes(startTime.split(':')[1]);
            end.setHours(endTime.split(':')[0]);
            end.setMinutes(endTime.split(':')[1]);
            const timeLeft = Math.max(0, (end - current) / 60000); // in minutes
            return timeLeft;
        }
        // Define your school schedule
        const schedule = [
            { period: 'Period 1', startTime: '08:35', endTime: '09:44', duration: 69 },
            { period: 'Period 2', startTime: '09:49', endTime: '10:58', duration: 69 },
            { period: 'BREAK', startTime: '10:58', endTime: '11:08', duration: 10 },
            { period: 'Period 3', startTime: '11:13', endTime: '12:22', duration: 69 },
            { period: 'LUNCH', startTime: '12:22', endTime: '12:52', duration: 30 },
            { period: 'Period 4', startTime: '12:57', endTime: '02:06', duration: 69 },
            { period: 'OFFICE HOURS', startTime: '02:06', endTime: '02:31', duration: 25 },
            { period: 'Period 5', startTime: '02:36', endTime: '03:45', duration: 69 }
        ];
        function updateClock() {
            const now = new Date();
            const hours = now.getHours();
            const minutes = now.getMinutes();
            const seconds = now.getSeconds();
            const ampm = hours >= 12 ? 'PM' : 'AM';
            const formattedHours = hours % 12 || 12;
            const timeString = `${formattedHours}:${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')} ${ampm}`;
            const timeElement = document.getElementById('time');
            timeElement.textContent = timeString;
            // Calculate and display time left for each schedule period
            const scheduleResults = document.getElementById('scheduleResults');
            scheduleResults.innerHTML = '';
            for (const item of schedule) {
                const timeLeft = calculateTimeLeft(now, item.startTime, item.endTime);
                scheduleResults.innerHTML += `<p>${item.period}: ${timeLeft.toFixed(0)} minutes left</p>`;
            }
        }
        // Call updateClock initially to set the time and schedule
        updateClock();
        // Update the clock and schedule every second
        setInterval(updateClock, 1000);
    </script>
</body>
</html>