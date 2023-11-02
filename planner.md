---
layout: base
title: Planner
---
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Tasks</title>
    <style>
        /* CSS styles for the interface */
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
        }
        .eventList {
            color: black;
            background-color: white;
            border-radius: 10px;
            padding: 10px;
            margin: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }
        .eventName {
            color: blue;
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 5px;
        }
        .td {
            color: blue;
            background-color: #1E90FF;
            border: none;
            border-radius: 5px;
            padding: 10px 20px;
            cursor: pointer;
            color: white;
        }
        .td:hover {
            background-color: #0077B6;
        }
        .title {
            color: white;
            background-color: #0077B6;
            border-radius: 10px;
            padding: 10px;
            text-align: center;
        }
        .delete-button {
            color: white;
            background-color: red;
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            cursor: pointer;
        }
        .delete-button:hover {
            background-color: #B22222;
        }
        table {
            width: 100%;
            border-collapse: collapse;
        }
        th, td {
            border: 1px solid #ccc;
            padding: 10px;
            text-align: left;
        }
        th {
            background-color: #0077B6;
            color: white;
        }
        td {
            background-color: white;
        }
    </style>
</head>
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
            <td colspan="5" align="center" class="title">Scheduled Events</td>
        </tr>
        <tr>
            <th>Task</th>
            <th>Event Date</th>
            <th>Event Time</th>
            <th>Done</th>
            <th>Delete</th>
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
</html>