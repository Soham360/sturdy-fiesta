---
layout: base
title: Planner
---
## Student Planner
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Tasks</title>
</head>
<body>
    <h1>Student Tasks</h1>
    <!-- Input field for entering tasks -->
    <input type="text" id="task-input" placeholder="Enter a task">
    <!-- Button to add tasks -->
    <button id="add-task">Add Task</button>
    <!-- Task list display -->
    <ul id="task-list"></ul>
    <script>
        // Initialize an array to store the tasks
        let tasks = [];
        // Function to update the tasks display
        function updateTaskList() {
            const taskList = document.getElementById("task-list");
            taskList.innerHTML = ""; // Clear the previous list
            tasks.forEach((task, index) => {
                const listItem = document.createElement("li");
                listItem.textContent = `${index + 1}. ${task}`;
                taskList.appendChild(listItem);
            });
        }
        // Function to add a task
        function addTask() {
            const taskInput = document.getElementById("task-input");
            const newTask = taskInput.value.trim();
            if (newTask) {
                tasks.push(newTask);
                updateTaskList();
                taskInput.value = ""; // Clear the input field
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
        // Add a task when the "Add Task" button is clicked
        const addTaskButton = document.getElementById("add-task");
        addTaskButton.addEventListener("click", addTask);
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