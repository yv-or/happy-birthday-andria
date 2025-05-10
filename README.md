<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Happy Birthday Andria!</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: linear-gradient(to bottom right, #ffb6c1, #ffe4e1);
      font-family: 'Comic Sans MS', cursive, sans-serif;
      color: #fff;
      text-align: center;
      overflow: hidden;
    }
    h1 {
      margin-top: 3rem;
      font-size: 3rem;
      text-shadow: 2px 2px 5px #000;
    }
    button {
      margin-top: 2rem;
      padding: 1rem 2rem;
      font-size: 1.2rem;
      background-color: #fff;
      color: #ff69b4;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      z-index: 10;
      position: relative;
      transition: background-color 0.3s ease;
    }
    button:hover {
      background-color: #ffe4e1;
    }
    #candle {
      width: 50px;
      height: 100px;
      background: pink;
      margin: 2rem auto 1rem;
      position: relative;
      border-radius: 10px;
      z-index: 10;
      transition: transform 0.5s ease;
    }
    #flame {
      width: 20px;
      height: 20px;
      background: yellow;
      border-radius: 50%;
      position: absolute;
      top: -20px;
      left: 50%;
      transform: translateX(-50%);
      box-shadow: 0 0 15px yellow;
      animation: flicker 0.3s infinite alternate;
    }
    @keyframes flicker {
      from { transform: translateX(-50%) scale(1); opacity: 1; }
      to { transform: translateX(-50%) scale(1.2); opacity: 0.8; }
    }
    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 0;
    }
  </style>
</head>
<body>
  <canvas id="sparkleCanvas"></canvas>
  <h1>Happy Birthday Andria! 🎉</h1>
  <div id="candle">
    <div id="flame"></div>
  </div>
  <button onclick="makeAWish()">Blow the Candle & Make a Wish</button>
  <button onclick="toggleMusic()">Toggle Music</button>

  <!-- Updated Google Drive URL for the music -->
  <audio id="backgroundMusic" autoplay loop>
    <source src="https://drive.google.com/uc?id=1ffV_pSQ-u2fjkfq2RZmKAbOGSsoKJha8&export=download" type="audio/mpeg">
    Your browser does not support the audio element.
  </audio>

  <script>
    function makeAWish() {
      document.getElementById('flame').style.display = 'none';
      document.getElementById('candle').style.transform = 'scale(0)';
      alert("🎂 Make a wish, Andria!");
      createSparkles(); // Generate sparkles when the candle is blown
    }

    // Toggle background music play/pause
    function toggleMusic() {
      const music = document.getElementById('backgroundMusic');
      if (music.paused) {
        music.play();
      } else {
        music.pause();
      }
    }

    // Sparkle animation
    const canvas = document.getElementById("sparkleCanvas");
    const ctx = canvas.getContext("2d");
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    let sparkles = [];
    for (let i = 0; i < 100; i++) {
      sparkles.push({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        r: Math.random() * 2 + 1,
        dx: (Math.random() - 0.5) * 1,
        dy: (Math.random() - 0.5) * 1,
        alpha: Math.random()
      });
    }

    function drawSparkles() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      for (let s of sparkles) {
        ctx.beginPath();
        ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(255, 255, 255, ${s.alpha})`;
        ctx.fill();
        s.x += s.dx;
        s.y += s.dy;

        // Respawn if out of bounds
        if (s.x < 0 || s.x > canvas.width || s.y < 0 || s.y > canvas.height) {
          s.x = Math.random() * canvas.width;
          s.y = Math.random() * canvas.height;
        }
      }
      requestAnimationFrame(drawSparkles);
    }

    function createSparkles() {
      for (let i = 0; i < 300; i++) {
        sparkles.push({
          x: Math.random() * canvas.width,
          y: Math.random() * canvas.height,
          r: Math.random() * 2 + 1,
          dx: (Math.random() - 0.5) * 2,
          dy: (Math.random() - 0.5) * 2,
          alpha: Math.random()
        });
      }
    }

    drawSparkles();
  </script>
</body>
</html>
