---
layout: base
title: Schedule
---
## Schedule
- This is the schedule for our project
<!DOCTYPE html>
<html>
<head>
    <title>Customizable Event Schedule</title>
</head>
<body>
    <table border="1">
        <tr>
            <td colspan="2" align="center">Customizable Event Schedule</td>
        </tr>
        <tr>
            <td colspan="2">Enter Event Details:</td>
        </tr>
        <tr>
            <td>
                Event Name:
                <input type="text" id="eventName">
            </td>
            <td>
                Event Date:
                <input type="date" id="eventDate">
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <button onclick="planEvent()">Plan Event</button>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div id="message"></div>
            </td>
        </tr>
    </table>
    <table border="1">
        <tr>
            <td colspan="2" align="center">Scheduled Events</td>
        </tr>
        <tr>
            <td>Event Name</td>
            <td>Event Date</td>
        </tr>
        <tbody id="eventList">
        </tbody>
    </table>
    <script>
        const events = [];
        function showMessage(message) {
            const messageDiv = document.getElementById('message');
            messageDiv.innerHTML = message;
        }
        function planEvent() {
            const eventName = document.getElementById('eventName').value;
            const eventDate = document.getElementById('eventDate').value;
            if (!eventName || !eventDate) {
                alert('Please enter event details.');
                return;
            }
            events.push({ name: eventName, date: eventDate });
            displayEvents();
            document.getElementById('eventName').value = '';
            document.getElementById('eventDate').value = '';
            showMessage('Event planned successfully.');
        }
        function displayEvents() {
            const eventList = document.getElementById('eventList');
            eventList.innerHTML = '';
            for (const event of events) {
                const row = document.createElement('tr');
                const nameCell = document.createElement('td');
                nameCell.textContent = event.name;
                const dateCell = document.createElement('td');
                dateCell.textContent = event.date;
                row.appendChild(nameCell);
                row.appendChild(dateCell);
                eventList.appendChild(row);
            }
        }
    </script>
</body>
</html>

