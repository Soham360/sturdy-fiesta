---
layout: base
title: Announcements
---

<html lang="en">
<style>
    body {
        background-color: #333;
        color: #fff;
        font-family: Arial, sans-serif;
    }
    .container {
        max-width: 600px;
        margin: 10px auto;
        padding: 20px;
        background-color: #153e8f;
        border-radius: 8px;
    }
    h1 {
        text-align: center;
    }
    .announcement-form {
        display: flex;
        margin-top: 20px;
    }
    input[type="text"] {
        flex: 1;
        padding: 10px;
        border: none;
        border-radius: 4px;
        margin-right: 10px;
        background-color: #ADD8E6;
        color: #fff;
    }
    button {
        padding: 10px 20px;
        border: none;
        border-radius: 4px;
        background-color: #007bff;
        color: #fff;
        cursor: pointer;
    }
    button:hover {
        background-color: #0056b3;
    }
</style>
<body>
    <div class="container">
        <h1>Announcements</h1>
        <div id="announcements"></div>
        <div class="announcement-form">
            <input type="text" id="announcementText" placeholder="Write your announcement...">
            <button onclick="postAnnouncement()">Post</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>
<script>
    function postAnnouncement() {
    var announcementText = document.getElementById('announcementText').value;
    if (announcementText.trim() !== '') {
        var announcementsDiv = document.getElementById('announcements');
        var announcementElement = document.createElement('div');
        announcementElement.className = 'announcement';
        announcementElement.innerText = announcementText;
        announcementsDiv.appendChild(announcementElement);
        document.getElementById('announcementText').value = '';
    }
}
</script>
</html>
