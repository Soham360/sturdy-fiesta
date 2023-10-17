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
<table border="1">
<tr>
    <td colspan="2" align="center">Customizable Schedule</td>
</tr>
<tr>
    <td colspan="2">Enter the Start Date:</td>
</tr>
<tr>
    <td>
        <input type="date" id="startDate">
    </td>
    <td>
        <button onclick="startSchedule()">Start Schedule</button>
    </td>
</tr>
<tr>
    <td colspan="2">
        <div id="message"></div>
    </td>
</tr>
</table>

<script>
function showMessage() {
    const messageDiv = document.getElementById('message');
    messageDiv.innerHTML = 'Your custom message here.';
}

function startSchedule() {
    const startDate = new Date(document.getElementById('startDate').value);
    if (isNaN(startDate)) {
        alert('Please select a valid start date.');
        return;
    }

    const endDate = new Date(startDate);
    endDate.setMonth(startDate.getMonth() + 3);

    if (window.scheduleInterval) {
        clearInterval(window.scheduleInterval);
    }

    showMessage();

    window.scheduleInterval = setInterval(function() {
        const now = new Date();
        if (now >= endDate) {
            clearInterval(window.scheduleInterval);
            return;
        }
        showMessage();
    }, 1000);
}
</script>
</body>
</html>


