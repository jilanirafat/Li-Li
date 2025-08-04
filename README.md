<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Click the Box Game</title>
  <style>
    body {
      font-family: sans-serif;
      text-align: center;
      background-color: #f0f8ff;
    }
    h1 {
      color: #333;
    }
    #gameArea {
      position: relative;
      width: 600px;
      height: 400px;
      margin: 20px auto;
      border: 2px solid #000;
      background-color: #e0f7fa;
      overflow: hidden;
    }
    .box {
      width: 50px;
      height: 50px;
      background-color: red;
      position: absolute;
      cursor: pointer;
      border-radius: 10px;
    }
    #score, #time {
      font-size: 20px;
      margin: 10px;
    }
    #startBtn {
      padding: 10px 20px;
      font-size: 16px;
      margin: 10px;
      cursor: pointer;
    }
  </style>
</head>
<body>

<h1>🎯 Click the Box Game 🎯</h1>
<div id="score">Score: 0</div>
<div id="time">Time left: 30s</div>
<button id="startBtn">Start Game</button>
<div id="gameArea"></div>

<script>
  const gameArea = document.getElementById("gameArea");
  const scoreDisplay = document.getElementById("score");
  const timeDisplay = document.getElementById("time");
  const startBtn = document.getElementById("startBtn");

  let score = 0;
  let timeLeft = 30;
  let timer;
  let boxInterval;

  function getRandomPosition() {
    const x = Math.floor(Math.random() * (gameArea.clientWidth - 50));
    const y = Math.floor(Math.random() * (gameArea.clientHeight - 50));
    return { x, y };
  }

  function createBox() {
    const box = document.createElement("div");
    box.classList.add("box");
    const pos = getRandomPosition();
    box.style.left = pos.x + "px";
    box.style.top = pos.y + "px";
    box.onclick = function () {
      score++;
      scoreDisplay.textContent = "Score: " + score;
      box.remove();
    };
    gameArea.appendChild(box);

    setTimeout(() => {
      if (gameArea.contains(box)) {
        box.remove();
      }
    }, 1500);
  }

  function startGame() {
    score = 0;
    timeLeft = 30;
    scoreDisplay.textContent = "Score: 0";
    timeDisplay.textContent = "Time left: 30s";
    gameArea.innerHTML = "";
    startBtn.disabled = true;

    timer = setInterval(() => {
      timeLeft--;
      timeDisplay.textContent = "Time left: " + timeLeft + "s";
      if (timeLeft <= 0) {
        clearInterval(timer);
        clearInterval(boxInterval);
        alert("⏰ Time's up! Your final score is: " + score);
        startBtn.disabled = false;
      }
    }, 1000);

    boxInterval = setInterval(createBox, 800);
  }

  startBtn.addEventListener("click", startGame);
</script>

</body>
</html>
