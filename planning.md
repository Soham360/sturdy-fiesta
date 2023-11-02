---
layout: base
title: Planner
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        /* CSS styles for the interface */
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
        }
        h2 {
            text-align: center;
            color: #333;
        }
        /* Styling for the tables */
        table {
            width: 80%;
            margin: 0 auto;
            border-collapse: collapse;
            background-color: #fff;
        }
        table, th, td {
            border: 1px solid #333;
            background-color: #007BFF;
        }
        th {
            background-color: #007BFF;
            color: black;
            font-weight: bold;
            text-align: center;
            padding: 10px;
        }
        td {
            padding: 10px;
            text-align: center;
        }
        .eventName {
            color: blue;
        }
        .delete-button {
            color: red;
            background-color: white;
            border: 1px solid red;
            padding: 5px 10px;
            cursor: pointer;
        }
        .delete-button:hover {
            background-color: red;
            color: white;
        }
        .title {
            background-color: #333;
            color: white;
            font-size: 24px;
            text-align: center;
            padding: 10px;
        }
    </style>
</head>
<body>
    <h2 style="color:white">Student Planner</h2>
    <table>
        <tr>
            <td colspan="2" class="title">Customizable Event Schedule</td>
        </tr>
        <tr>
            <td colspan="2" style="color:white">Enter Event Details:</td>
        </tr>
        <tr>
            <td>
                <span style="color:white">Event Name:</span>
                <input type="text" id="task-input" class="eventName" placeholder="Enter a task">
            </td>
            <td>
                <span style="color:white">Event Date:</span>
                <input type="date" id="eventDate">
            </td>
        </tr>
        <tr>
            <td>
                <span style="color:white">Event Time:</span>
                <input type="time" id="eventTime">
            </td>
            <td>
                <button onclick="addTask()" class="eventName">Add Task</button>
            </td>
        </tr>
        <tr>
            <td colspan="2">
                <div id="message"></div>
            </td>
        </tr>
    </table>
    <table>
        <tr>
            <td colspan="5" class="title">Scheduled Events</td>
        </tr>
        <tr>
            <th>Task</th>
            <th>Event Date</th>
            <th>Event Time</th>
            <th>Mark as Done</th>
            <th>Delete</th>
        </tr>
        <tbody id="task-list" class="eventList" style="color:white">
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
                    <td>${task.name}</td>
                    <td>${task.date}</td>
                    <td>${task.time}</td>
                    <td><input type="checkbox" id="doneCheckbox${index}" onchange="markTaskAsDone(${index})"></td>
                    <td><button onclick="deleteTask(${index})" class="delete-button">Delete</button></td>
                `;
                if (task.isDone) {
                    listItem.querySelector(`#doneCheckbox${index}`).checked = true;
                }
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
                tasks.push({ name: taskName, date: taskDate, time: taskTime, isDone: false });
                updateTaskList();
                taskNameInput.value = ""; // Clear the input field
                taskDateInput.value = ""; // Clear the date input
                taskTimeInput.value = ""; // Clear the time input
                // Store tasks in a cookie
                setCookie("tasks", JSON.stringify(tasks), 365);
            }
        }
        // Function to delete a task by index
        function deleteTask(index) {
            if (index >= 0 && index < tasks.length) {
                tasks.splice(index, 1);
                updateTaskList();
                // Update the stored tasks in the cookie
                setCookie("tasks", JSON.stringify(tasks), 365);
            }
        }
        // Function to mark a task as done
        function markTaskAsDone(index) {
            if (index >= 0 && index < tasks.length) {
                tasks[index].isDone = !tasks[index].isDone;
                // Update the stored tasks in the cookie
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