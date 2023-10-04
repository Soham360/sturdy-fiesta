---
layout: base
title: Cube Animation
---



<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Rotating Cube Loading Animation</title>
<style>
  .cube-container {
    perspective: 800px;
    width: 200px;
    height: 200px;
    margin: 100px auto;
  }
  .cube {
    position: relative;
    transform-style: preserve-3d;
    transform: rotateX(0deg) rotateY(0deg);
    width: 100%;
    height: 100%;
    animation: spin 3s infinite linear;
  }
  .face {
    position: absolute;
    width: 200px;
    height: 200px;
    background: rgba(255, 0, 0, 0.7);
    border: 2px solid #333;
    opacity: 0.8;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.6);
  }
  .face:nth-child(1) { transform: rotateY(0deg) translateZ(100px); }
  .face:nth-child(2) { transform: rotateX(90deg) translateZ(100px); }
  .face:nth-child(3) { transform: rotateY(180deg) translateZ(100px); }
  .face:nth-child(4) { transform: rotateX(-90deg) translateZ(100px); }
  .face:nth-child(5) { transform: rotateY(90deg) translateZ(100px); }
  .face:nth-child(6) { transform: rotateY(180deg) rotateX(90deg) translateZ(100px); }
  @keyframes spin {
    0% { transform: rotateX(0deg) rotateY(0deg); }
    100% { transform: rotateX(360deg) rotateY(360deg); }
  }
</style>
</head>
<body>
  <div class="cube-container">
    <div class="cube">
      <div class="face"></div>
      <div class="face"></div>
      <div class="face"></div>
      <div class="face"></div>
      <div class="face"></div>
      <div class="face"></div>
    </div>
  </div>
</body>
</html>
