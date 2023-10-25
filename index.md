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
    <h2>Enter Your School Schedule</h2>
    <div>
        <label for="classPeriod1">Period 1:</label>
        <input type="text" id="classPeriod1"><br>
        <label for="classPeriod2">Period 2:</label>
        <input type="text" id="classPeriod2"><br>
        <label for="classPeriod3">Period 3:</label>
        <input type="text" id="classPeriod3"><br>
        <label for="classPeriod4">Period 4:</label>
        <input type="text" id="classPeriod4"><br>
        <label for="classPeriod5">Period 5:</label>
        <input type="text" id="classPeriod5"><br>
        <button onclick="updateSchedule()">Update Schedule</button>
    </div>
    <div id="time"></div>
    <div id="date"></div>
    <div id="scheduleResults"></div>
    <script>
        const commonSchedule = [
            { period: 'Period 1', startTime: '08:35', endTime: '09:44', duration: 69, class: '' },
            { period: 'Period 2', startTime: '09:49', endTime: '10:58', duration: 69, class: '' },
            { period: 'BREAK', startTime: '10:58', endTime: '11:08', duration: 10, class: 'AP Snacktime' },
            { period: 'Period 3', startTime: '11:13', endTime: '12:22', duration: 69, class: '' },
            { period: 'LUNCH', startTime: '12:22', endTime: '12:52', duration: 30, class: 'AP Lunch' },
            { period: 'Period 4', startTime: '12:57', endTime: '14:06', duration: 69, class: '' },
            { period: 'OFFICE HOURS', startTime: '14:06', endTime: '14:31', duration: 25, class: 'AP Tomfoolery' },
            { period: 'Period 5', startTime: '14:36', endTime: '15:45', duration: 69, class: '' }
        ];
        const wednesdaySchedule = [
            { period: 'Period 1', startTime: '09:55', endTime: '10:53', duration: 58, class: '' },
            { period: 'Period 2', startTime: '10:58', endTime: '11:56', duration: 58, class: '' },
            { period: 'BREAK', startTime: '11:56', endTime: '12:06', duration: 10, class: 'AP Snacktime' },
            { period: 'Period 3', startTime: '12:11', endTime: '13:09', duration: 58, class: '' },
            { period: 'LUNCH', startTime: '13:09', endTime: '13:39', duration: 30, class: 'AP Lunch' },
            { period: 'Period 4', startTime: '13:44', endTime: '14:42', duration: 58, class: '' },
            { period: 'Period 5', startTime: '14:47', endTime: '15:45', duration: 58, class: '' }
        ];
        const fridaySchedule = [
            { period: 'Period 1', startTime: '08:35', endTime: '09:49', duration: 74, class: '' },
            { period: 'Period 2', startTime: '09:54', endTime: '11:08', duration: 74, class: '' },
            { period: 'BREAK', startTime: '11:08', endTime: '11:18', duration: 10, class: 'AP Snacktime' },
            { period: 'Period 3', startTime: '11:23', endTime: '12:37', duration: 74, class: '' },
            { period: 'LUNCH', startTime: '12:37', endTime: '13:07', duration: 30, class: 'AP Lunch' },
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
            switch (currentDay) {
                case 3: // WednesdayfridaySchedule
                    wednesdaySchedule[0].class = document.getElementById(`classPeriod${0 + 1}`).value;
                    wednesdaySchedule[1].class = document.getElementById(`classPeriod${1 + 1}`).value;
                    wednesdaySchedule[3].class = document.getElementById(`classPeriod${2 + 1}`).value;
                    wednesdaySchedule[5].class = document.getElementById(`classPeriod${3 + 1}`).value;
                    wednesdaySchedule[6].class = document.getElementById(`classPeriod${4 + 1}`).value;
                case 5: // Friday
                    fridaySchedule[0].class = document.getElementById(`classPeriod${0 + 1}`).value;
                    fridaySchedule[1].class = document.getElementById(`classPeriod${1 + 1}`).value;
                    fridaySchedule[3].class = document.getElementById(`classPeriod${2 + 1}`).value;
                    fridaySchedule[5].class = document.getElementById(`classPeriod${3 + 1}`).value;
                    fridaySchedule[6].class = document.getElementById(`classPeriod${4 + 1}`).value;
                    break;
                default:
                    commonSchedule[0].class = document.getElementById(`classPeriod${0 + 1}`).value;
                    commonSchedule[1].class = document.getElementById(`classPeriod${1 + 1}`).value;
                    commonSchedule[3].class = document.getElementById(`classPeriod${2 + 1}`).value;
                    commonSchedule[5].class = document.getElementById(`classPeriod${3 + 1}`).value;
                    commonSchedule[7].class = document.getElementById(`classPeriod${4 + 1}`).value;
                    break;
            }
            updateClock();
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
    </script>
</body>
</html>