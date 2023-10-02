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
      width: 33.33%;
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
    <div id="pointer"></div>
  </div>

  <button type="button" onclick="spin()">Spin</button>

  <script>
    var wheel = document.getElementById('wheel');
    var pointer = document.getElementById('pointer');

    function spin() {
      // Rig the wheel to always land on the green slice.
      wheel.style.transform = 'rotate(120deg)';

      // Start the spinning animation.
      pointer.classList.add('spinning');

      setTimeout(function() {
        // Stop the spinning animation.
        pointer.classList.remove('spinning');

        // Determine where the pointer landed.
        var landedSlice = pointer.classList[1];

        // Display the result.
        alert('You landed on the ' + landedSlice + ' slice!');
      }, 1000);
    }
  </script>
</body>
</html>
