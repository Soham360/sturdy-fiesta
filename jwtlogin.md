---
title: JWT Login
layout: base
description: A login screen that interacts with Java and obtains a JWT
permalink: /data/login
---

<html>
<head>
    <title>JWT Login</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
</head>
<body>
    <form action="javascript:login_user()">
        <p><label>
            User ID:
            <input type="text" name="uid" id="uid" required>
        </label></p>
        <p><label>
            Password:
            <input type="password" name="password" id="password" required>
        </label></p>
        <p>
            <button>Login</button>
        </p>
    </form>
    <table id="data-table" style="display: none;">
        <thead>
            <tr>
                <th>Name</th>
                <th>Email</th>
                <th>Date Of Birth</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>Orlando Carcamo</td>
                <td>orlandoc@gmail.com</td>
                <td>01-01-2006</td>
            </tr>
            <tr>
                <td>Soham Kamat</td>
                <td>sohamk@gmail.com</td>
                <td>01-02-2006</td>
            </tr>
            <tr>
                <td>Aniket Chakradeo</td>
                <td>aniketc@gmail.com</td>
                <td>01-03-2006</td>
            </tr>
            <tr>
                <td>Kevin Du</td>
                <td>kevind@gmail.com</td>
                <td>01-04-2006</td>
            </tr>
            <tr>
                <td>Billy Goat</td>
                <td>billyg@gmail.com</td>
                <td>01-05-2006</td>
            </tr>
        </tbody>
    </table>
    <button id="read-button">Read</button>
    <script>
        // URL for deployment
        var url = "https://no-papels.stu.nighthawkcodingsociety.com";
        // Comment out next line for local testing
        // url = "http://localhost:8085";
        // Authenticate endpoint
        const login_url = url + '/authenticate';
        function login_user() {
            // Set body to include login data
            const body = {
                email: document.getElementById("uid").value,
                password: document.getElementById("password").value,
            };
            // Set Headers to support cross origin
            const requestOptions = {
                method: 'POST',
                mode: 'cors', // no-cors, *cors, same-origin
                cache: 'no-cache', // *default, no-cache, reload, force-cache, only-if-cached
                credentials: 'include', // include, *same-origin, omit
                body: JSON.stringify(body),
                headers: {
                    "content-type": "application/json",
                },
            };
            // Fetch JWT
            fetch(login_url, requestOptions)
                .then(response => {
                    // trap error response from Web API
                    if (!response.ok) {
                        const errorMsg = 'Login error: ' + response.status;
                        console.log(errorMsg);
                        return;
                    }
                    // Success!!!
                    // Display the table
                    document.getElementById("data-table").style.display = "table";
                });
        }
        $(document).ready(function() {
            $("#read-button").click(function() {
                // Read button click event
                // Generate table with provided information
                var tableBody = $("#data-table tbody");
                tableBody.empty();
                var names = [
                    "Orlando Carcamo",
                    "Soham Kamat",
                    "Aniket Chakradeo",
                    "Kevin Du",
                    "Billy Goat"
                ];
                var emails = [
                    "orlandoc@gmail.com",
                    "sohamk@gmail.com",
                    "aniketc@gmail.com",
                    "kevind@gmail.com",
                    "billyg@gmail.com"
                ];
                var datesOfBirth = [
                    "01-01-2006",
                    "01-02-2006",
                    "01-03-2006",
                    "01-04-2006",
                    "01-05-2006"
                ];
                for (var i = 0; i < names.length; i++) {
                    var row = $("<tr>");
                    row.append($("<td>").text(names[i]));
                    row.append($("<td>").text(emails[i]));
                    row.append($("<td>").text(datesOfBirth[i]));
                    tableBody.append(row);
                }
            });
        });
    </script>
</body>
</html>