---
layout: base
title: Home
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>School Bell Schedule Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
        }
        h2 {
            text-align: center;
            color: #333;
        }
        label {
            display: block;
            margin: 10px 0;
            font-weight: bold;
        }
        input[type="text"] {
            width: 100%;
            padding: 5px;
            margin: 5px 0;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            background-color: #007BFF;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        #datetime {
            text-align: center;
            font-size: 20px;
            margin-top: 20px;
            display: block;
        }
        #scheduleResults {
            background-color: #fff;
            border: 0.5px solid #ccc;
            border-radius: 5px;
            padding: 10px;
            max-width: 50%;
            margin-top: 50px;
        }
        #scheduleResults p {
        margin: 0;
        padding: 5px 0;
        border-bottom: 1px solid #ccc;
        font-size: 16px; /* Adjust the font size as needed */
    }
        #inputSchedule, #scheduleResults {
            display: inline-block;
            width: 49%;
            vertical-align: top;
        }
        #inputSchedule {
            margin: 20px auto;
        }
    </style>
</head>
<body>
    <div style="display: flex; flex-direction: column; width: 100%; justify-content: center; align-items: center;">
        <h1 id="typewriter"></h1>
    </div>
    <div id="datetime">
        <div id="date"></div>
        <div id="time"></div>
    </div>
     <h2 style="color:white;">Enter Your School Schedule</h2>
    <div id="inputSchedule">
        <label for="classPeriod1">Period 1:</label>
        <input type="text" id="classPeriod1" style="color: blue;"><br>
        <label for="classPeriod2">Period 2:</label>
        <input type="text" id="classPeriod2" style="color: blue;"><br>
        <label for="classPeriod3">Period 3:</label>
        <input type="text" id="classPeriod3" style="color: blue;"><br>
        <label for="classPeriod4">Period 4:</label>
        <input type="text" id="classPeriod4" style="color: blue;"><br>
        <label for="classPeriod5">Period 5:</label>
        <input type="text" id="classPeriod5" style="color: blue;"><br>
        <button onclick="updateSchedule()">Update Schedule</button>
    </div>
    <div id="scheduleResults" style="color: blue;"></div>
    <!-- <div id="time" style="text-align: center; font-size: 20px;"></div> -->
  <script>
         var i = 0;
    var text = "Welcome to Project Pluto! 😱🤯🤩";
    var speed = 150; // Adjust typing speed (lower value = faster)
    function typeWriter() {
        if (i < text.length) {
            document.getElementById("typewriter").innerHTML += text.charAt(i);
            i++;
            setTimeout(typeWriter, speed);
        }
    }
    typeWriter();
        const commonSchedule = [
            { period: 'Period 1', startTime: '08:35', endTime: '09:44', duration: 69, class: '' },
            { period: 'Period 2', startTime: '09:49', endTime: '10:58', duration: 69, class: '' },
            { period: 'BREAK', startTime: '10:58', endTime: '11:08', duration: 10, class: 'Break' },
            { period: 'Period 3', startTime: '11:13', endTime: '12:22', duration: 69, class: '' },
            { period: 'LUNCH', startTime: '12:22', endTime: '12:52', duration: 30, class: 'Lunch' },
            { period: 'Period 4', startTime: '12:57', endTime: '14:06', duration: 69, class: '' },
            { period: 'OFFICE HOURS', startTime: '14:06', endTime: '14:31', duration: 25, class: 'Office Hours' },
            { period: 'Period 5', startTime: '14:36', endTime: '15:45', duration: 69, class: '' }
        ];
        const wednesdaySchedule = [
            { period: 'Period 1', startTime: '09:55', endTime: '10:53', duration: 58, class: '' },
            { period: 'Period 2', startTime: '10:58', endTime: '11:56', duration: 58, class: '' },
            { period: 'BREAK', startTime: '11:56', endTime: '12:06', duration: 10, class: 'Break' },
            { period: 'Period 3', startTime: '12:11', endTime: '13:09', duration: 58, class: '' },
            { period: 'LUNCH', startTime: '13:09', endTime: '13:39', duration: 30, class: 'Lunch' },
            { period: 'Period 4', startTime: '13:44', endTime: '14:42', duration: 58, class: '' },
            { period: 'Period 5', startTime: '14:47', endTime: '15:45', duration: 58, class: '' }
        ];
        const fridaySchedule = [
            { period: 'Period 1', startTime: '08:35', endTime: '09:49', duration: 74, class: '' },
            { period: 'Period 2', startTime: '09:54', endTime: '11:08', duration: 74, class: '' },
            { period: 'BREAK', startTime: '11:08', endTime: '11:18', duration: 10, class: 'Break' },
            { period: 'Period 3', startTime: '11:23', endTime: '12:37', duration: 74, class: '' },
            { period: 'LUNCH', startTime: '12:37', endTime: '13:07', duration: 30, class: 'Lunch' },
            { period: 'Period 4', startTime: '13:12', endTime: '14:26', duration: 74, class: '' },
            { period: 'Period 5', startTime: '14:31', endTime: '15:45', duration: 74, class: '' }
        ];
        function calculateTimeLeft(currentTime, startTime, endTime) {
            const current = new Date(currentTime);
            const start = new Date(currentTime);
            const end = new Date(currentTime);
            start.setHours(startTime.split(':')[0]);
            start.setMinutes(startTime.split(':')[1]);
            end.setHours(endTime.split(':')[0]);
            end.setMinutes(endTime.split(':')[1]);
            const timeLeft = Math.max(0, (end - current) / 60000);
            return timeLeft;
        }
        function updateSchedule() {
            const currentDay = new Date().getDay();
            let currentSchedule;
            switch (currentDay) {
                case 3: // WednesdayfridaySchedule
                    wednesdaySchedule[0].class = document.getElementById(`classPeriod${0 + 1}`).value;
                    wednesdaySchedule[1].class = document.getElementById(`classPeriod${1 + 1}`).value;
                    wednesdaySchedule[3].class = document.getElementById(`classPeriod${2 + 1}`).value;
                    wednesdaySchedule[5].class = document.getElementById(`classPeriod${3 + 1}`).value;
                    wednesdaySchedule[6].class = document.getElementById(`classPeriod${4 + 1}`).value;
                    currentSchedule = wednesdaySchedule;
                    break;
                case 5: // Friday
                    fridaySchedule[0].class = document.getElementById(`classPeriod${0 + 1}`).value;
                    fridaySchedule[1].class = document.getElementById(`classPeriod${1 + 1}`).value;
                    fridaySchedule[3].class = document.getElementById(`classPeriod${2 + 1}`).value;
                    fridaySchedule[5].class = document.getElementById(`classPeriod${3 + 1}`).value;
                    fridaySchedule[6].class = document.getElementById(`classPeriod${4 + 1}`).value;
                    currentSchedule = fridaySchedule;
                    break;
                default:
                    commonSchedule[0].class = document.getElementById(`classPeriod${0 + 1}`).value;
                    commonSchedule[1].class = document.getElementById(`classPeriod${1 + 1}`).value;
                    commonSchedule[3].class = document.getElementById(`classPeriod${2 + 1}`).value;
                    commonSchedule[5].class = document.getElementById(`classPeriod${3 + 1}`).value;
                    commonSchedule[7].class = document.getElementById(`classPeriod${4 + 1}`).value;
                    currentSchedule = commonSchedule;
                    break;
                saveScheduleToCookies();
                updateClock();
            }
        setCookie("currentSchedule", JSON.stringify(currentSchedule), 365);
        updateClock();
        displaySchedule(currentSchedule);
        }
            function displaySchedule(schedule) {
        const scheduleResults = document.getElementById('scheduleResults');
        scheduleResults.innerHTML = '';
        for (const item of schedule) {
            scheduleResults.innerHTML += `<p>${item.period} (${item.class}): Period finished</p>`;
        }
    }
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
    const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
    const dateString = now.toLocaleDateString('en-US', options);
    const dateElement = document.getElementById('date');
    dateElement.textContent = dateString;
    const scheduleResults = document.getElementById('scheduleResults');
    scheduleResults.innerHTML = '';
    const currentSchedule = getCurrentSchedule(now);
    for (const item of currentSchedule) {
        const timeLeft = calculateTimeLeft(now, item.startTime, item.endTime);
        if (timeLeft > 0) {
            if (timeLeft > 60) {
                const hoursLeft = Math.floor(timeLeft / 60);
                scheduleResults.innerHTML += `<p>${item.period} (${item.class}): ${hoursLeft} hours left</p>`;
            } else {
                scheduleResults.innerHTML += `<p>${item.period} (${item.class}): ${timeLeft.toFixed(0)} minutes left</p>`;
            }
        } else {
            scheduleResults.innerHTML += `<p>${item.period} (${item.class}): Period finished</p>`;
        }
    }
}
        function getCurrentSchedule(currentTime) {
            const currentDay = currentTime.getDay();
            switch (currentDay) {
                case 3: // Wednesday
                    return wednesdaySchedule;
                case 5: // Friday
                    return fridaySchedule;
                default:
                    return commonSchedule;
            }
        }
        updateClock();
        setInterval(updateClock, 1000);
        function setCookie(cname, cvalue, exdays) {
            const d = new Date();
            d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
            const expires = "expires=" + d.toUTCString();
            document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
        }
        // Function to get a cookie
        function getCookie(cname) {
            const name = cname + "=";
            const ca = document.cookie.split(';');
            for (let i = 0; i < ca.length; i++) {
                let c = ca[i];
                while (c.charAt(0) === ' ') {
                    c = c.substring(1);
                }
                if (c.indexOf(name) === 0) {
                    return c.substring(name.length, c.length);
                }
            }
            return "";
        }
        // Function to save the user's schedule inputs to cookies
        function saveScheduleToCookies() {
            // Get the values of the input fields
            const classPeriod1 = document.getElementById('classPeriod1').value;
            const classPeriod2 = document.getElementById('classPeriod2').value;
            const classPeriod3 = document.getElementById('classPeriod3').value;
            const classPeriod4 = document.getElementById('classPeriod4').value;
            const classPeriod5 = document.getElementById('classPeriod5').value;
            // Create an object to store the schedule data
            const scheduleData = {
                classPeriod1,
                classPeriod2,
                classPeriod3,
                classPeriod4,
                classPeriod5
            };
            // Convert the object to a JSON string and store it in a cookie
            setCookie("userSchedule", JSON.stringify(scheduleData), 365);
        }
        // Function to load the user's schedule from cookies
        function loadScheduleFromCookies() {
            const storedSchedule = getCookie("userSchedule");
            if (storedSchedule) {
                const scheduleData = JSON.parse(storedSchedule);
                // Set the input field values from the loaded data
                document.getElementById('classPeriod1').value = scheduleData.classPeriod1;
                document.getElementById('classPeriod2').value = scheduleData.classPeriod2;
                document.getElementById('classPeriod3').value = scheduleData.classPeriod3;
                document.getElementById('classPeriod4').value = scheduleData.classPeriod4;
                document.getElementById('classPeriod5').value = scheduleData.classPeriod5;
            }
        }
        // Call the function to load the user's schedule from cookies when the page loads
        window.onload = function () {
            loadScheduleFromCookies();
            updateClock(); // Update the schedule based on the loaded data
        }
        // Call the function to save the user's schedule to cookies when the "Update Schedule" button is clicked
        function updateschedule() {
            saveScheduleToCookies();
            updateClock(); // Update the schedule based on the updated data
        }
    </script>
</body>
</html>