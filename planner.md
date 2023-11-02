<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Tasks</title>
    <style>
        /* CSS styles for the interface */
        .eventList {
            color: white;
            background-color: red; /* Optional background color for emphasis */
        }
        .eventName {
            color: blue;
        }
        .td {
            color: blue;
        }
        .title {
            color: white;
        }
    </style>
</head>
<body>
    <table border="1">
        <tr>
            <td colspan="2" align="center" id="title" class="title">Customizable Event Schedule</td>
        </tr>
        <tr>
            <td colspan="2">Enter Event Details:</td>
        </tr>
        <tr>
            <td>
                Event Name:
                <input type="text" id="task-input" class="eventName" placeholder="Enter a task">
            </td>
            <td>
                Event Date:
                <input type="date" id="eventDate">
            </td>
        </tr>
        <tr>
            <td>
                Event Time:
                <input type="time" id="eventTime">
            </td>
            <td>
                <button onclick="addTask()" class="td">Add Task</button>
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
            <td colspan="3" align="center" class="title">Scheduled Events</td>
        </tr>
        <tr>
            <td>Event Name</td>
            <td>Event Date</td>
            <td>Event Time</td>
        </tr>
        <tbody id="task-list" class="eventList">
        </tbody>
    </table>
    <script>
        // Initialize an array to store the tasks
        let tasks = [];
        // Function to update the tasks display
        function updateTaskList() {
            const taskList = document.getElementById("task-list");
            taskList.innerHTML = ""; // Clear the previous list
            tasks.forEach((task, index) => {
                const listItem = document.createElement("tr");
                listItem.innerHTML = `
                    <td>${index + 1}. ${task.name}</td>
                    <td>${task.date}</td>
                    <td>${task.time}</td>
                `;
                taskList.appendChild(listItem);
            });
        }
        // Function to add a task
        function addTask() {
            const taskNameInput = document.getElementById("task-input");
            const taskDateInput = document.getElementById("eventDate");
            const taskTimeInput = document.getElementById("eventTime");
            const taskName = taskNameInput.value.trim();
            const taskDate = taskDateInput.value;
            const taskTime = taskTimeInput.value;
            if (taskName) {
                tasks.push({ name: taskName, date: taskDate, time: taskTime });
                updateTaskList();
                taskNameInput.value = ""; // Clear the input field
                taskDateInput.value = ""; // Clear the date input
                taskTimeInput.value = ""; // Clear the time input
                // Store tasks in a cookie
                setCookie("tasks", JSON.stringify(tasks), 365);
            }
        }
        // Load tasks from a cookie when the page loads
        window.onload = function () {
            const storedTasks = getCookie("tasks");
            if (storedTasks) {
                tasks = JSON.parse(storedTasks);
                updateTaskList();
            }
        };
        // Helper function to set a cookie
        function setCookie(cname, cvalue, exdays) {
            const d = new Date();
            d.setTime(d.getTime() + (exdays * 24 * 60 * 60 * 1000));
            const expires = "expires=" + d.toUTCString();
            document.cookie = cname + "=" + cvalue + ";" + expires + ";path=/";
        }
        // Helper function to get a cookie
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
    </script>
</body>
</html>