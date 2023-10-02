---
layout: base
permalink: /wheel/
title: Wheel
---

<html>
<head>
  <title>Rigged Spinning Wheel</title>
  <style>
    #wheel {
      width: 200px;
      height: 200px;
      border: 1px solid black;
      border-radius: 100px;
      margin: 0 auto;
    }
    .slice {
      width: 12.5%;
      height: 100%;
      border-radius: 100px;
      float: left;
    }
    .slice-1 {
      background-color: red;
    }
    .slice-2 {
      background-color: green;
    }
    .slice-3 {
      background-color: blue;
    }
    .slice-4 {
      background-color: yellow;
    }
    .slice-5 {
      background-color: orange;
    }
    .slice-6 {
      background-color: purple;
    }
    .slice-7 {
      background-color: pink;
    }
    .slice-8 {
      background-color: black;
    }
    #pointer {
      position: relative;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 10px;
      height: 10px;
      background-color: black;
    }
  </style>
</head>
<body>
  <div id="wheel">
    <div class="slice slice-1"></div>
    <div class="slice slice-2"></div>
    <div class="slice slice-3"></div>
    <div class="slice slice-4"></div>
    <div class="slice slice-5"></div>
    <div class="slice slice-6"></div>
    <div class="slice slice-7"></div>
    <div class="slice slice-8"></div>
    <div id="pointer"></div>
  </div>

  <button type="button" onclick="spin()">Spin</button>

  <script>
    var wheel = document.getElementById('wheel');
    var pointer = document.getElementById('pointer');

    function spin() {
      // Rig the wheel to always land on the black slice.
      wheel.style.transform = 'rotate(360deg)';

      // Start the spinning animation.
      pointer.classList.add('spinning');

      // Create a variable to store the current rotation of the wheel.
      var currentRotation = 0;

      // Create a function to slow down the rotation of the wheel.
      function slowDown() {
        // Decrease the rotation speed of the wheel.
        currentRotation -= 1;

        // Set the rotation of the wheel.
        wheel.style.transform = 'rotate(' + currentRotation + 'deg)';

        // If the wheel has not yet landed on the rigged slice, continue slowing down the rotation.
        if (currentRotation > 270) {
          setTimeout(slowDown, 10);
        } else {
          // The wheel has landed on the rigged slice.
          // Stop the spinning animation.
          pointer.classList.remove('spinning');

          // Determine where the pointer landed.
          var landedSlice = pointer.classList[1];

          // Display the result.
          alert('You landed on the ' + landedSlice + ' slice!');
        }
      }

      // Start slowing down the rotation of the wheel after 1 second.
      setTimeout(slowDown, 1000);
    }
  </script>
</body>
</html>
