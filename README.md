<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no" />
  <title>Cricket Hotseat Sprint</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://fonts.googleapis.com/css2?family=Righteous&family=Nunito:wght@400;700;800&display=swap" rel="stylesheet">
  <style>
    body { font-family: 'Nunito', sans-serif; touch-action: manipulation; }
    h1, .font-title { font-family: 'Righteous', cursive; }
    canvas { display:block; width:100%; height:100%; image-rendering: pixelated; }
    .glass { background: rgba(255,255,255,.12); border: 1px solid rgba(255,255,255,.2); backdrop-filter: blur(12px); }
    .btn { transition: all .2s cubic-bezier(0.175, 0.885, 0.32, 1.275); cursor: pointer; }
    .btn:active { transform: scale(0.92); }
    .score-glow { text-shadow: 0 0 10px rgba(255,255,255,0.5); }
  </style>
</head>

<body class="bg-gradient-to-b from-sky-400 via-sky-300 to-green-500 min-h-screen text-white overflow-hidden">
  <div class="absolute top-0 left-0 right-0 z-20 p-4 flex justify-between items-start pointer-events-none">
    <div class="glass rounded-2xl p-3 px-6 pointer-events-auto">
      <div class="text-xs uppercase tracking-widest opacity-80 font-bold">Innings</div>
      <div class="text-2xl font-black" id="hudPlayer">PLAYER 1</div>
    </div>
    <div class="glass rounded-2xl p-3 px-6 text-right pointer-events-auto">
      <div class="text-xs uppercase tracking-widest opacity-80 font-bold">Runs (Meters)</div>
      <div class="text-2xl font-black score-glow"><span id="hudScore">0</span>m</div>
    </div>
  </div>

  <canvas id="game"></canvas>

  <div id="overlay" class="absolute inset-0 z-30 flex items-center justify-center p-4 bg-black/40 backdrop-blur-sm">
    <div class="glass w-full max-w-md rounded-[2rem] p-8 shadow-2xl border-t border-white/40">
      <div class="text-center space-y-2 mb-8">
        <h1 class="text-5xl font-black tracking-tighter italic" id="overlayTitle">READY?</h1>
        <p class="text-blue-50 opacity-90 font-medium" id="overlayText">Tap to jump over the wickets. One chance per player!</p>
      </div>

      <div id="setupControls" class="space-y-6">
        <div class="bg-black/20 rounded-2xl p-5">
          <div class="flex justify-between items-center mb-2">
            <label class="text-sm font-bold uppercase opacity-70">Number of Players</label>
            <span class="text-2xl font-black text-yellow-300" id="playerCountLabel">4</span>
          </div>
          <input id="playerCount" type="range" min="2" max="6" value="4" class="w-full h-2 bg-white/20 rounded-lg appearance-none cursor-pointer accent-yellow-400">
        </div>
      </div>

      <div class="mt-8 space-y-3">
        <button id="primaryBtn" class="btn w-full rounded-2xl py-4 bg-yellow-400 text-blue-900 text-xl font-black shadow-[0_5px_0_0_#ca8a04] hover:shadow-none hover:translate-y-1">
          START MATCH
        </button>
        <button id="secondaryBtn" class="btn w-full rounded-2xl py-4 bg-white/10 hover:bg-white/20 border border-white/30 font-bold hidden">
          VIEW SCOREBOARD
        </button>
      </div>
    </div>
  </div>

  <script>
    const canvas = document.getElementById('game');
    const ctx = canvas.getContext('2d');
    const hudPlayer = document.getElementById('hudPlayer');
    const hudScore = document.getElementById('hudScore');
    const overlay = document.getElementById('overlay');
    const primaryBtn = document.getElementById('primaryBtn');
    const secondaryBtn = document.getElementById('secondaryBtn');

    let W, H, DPR;
    let running = false;
    let currentPlayer = 0;
    let totalPlayers = 4;
    let scores = [];
    let speed = 6;
    let distance = 0;
    let obstacles = [];
    let spawnTimer = 0;

    // Player Object
    const player = {
      x: 0, y: 0, r: 25, vy: 0, rotation: 0,
      jumpPower: -16, gravity: 0.8, onGround: false
    };

    function resize() {
      DPR = window.devicePixelRatio || 1;
      W = window.innerWidth;
      H = window.innerHeight;
      canvas.width = W * DPR;
      canvas.height = H * DPR;
      ctx.scale(DPR, DPR);
      player.x = W * 0.2;
      player.r = Math.min(W, H) * 0.04;
    }
    window.onresize = resize;
    resize();

    // Game Logic
    function spawnObstacle() {
      const types = ['stumps', 'bat', 'bottle'];
      const type = types[Math.floor(Math.random() * types.length)];
      obstacles.push({
        x: W + 100,
        y: H * 0.8,
        w: type === 'stumps' ? 40 : 60,
        h: type === 'stumps' ? 70 : 30,
        type: type
      });
    }

    function update(dt) {
      if (!running) return;

      distance += speed * 0.1;
      speed += 0.002;
      hudScore.innerText = Math.floor(distance);

      // Physics
      player.vy += player.gravity;
      player.y += player.vy;
      player.rotation += speed * 0.05;

      const ground = H * 0.8 - player.r;
      if (player.y > ground) {
        player.y = ground;
        player.vy = 0;
        player.onGround = true;
      }

      // Obstacles
      spawnTimer -= dt;
      if (spawnTimer < 0) {
        spawnObstacle();
        spawnTimer = 1000 + Math.random() * 1500;
      }

      obstacles.forEach((o, i) => {
        o.x -= speed;
        // Collision (Circle vs Rect)
        const cx = Math.max(o.x, Math.min(player.x, o.x + o.w));
        const cy = Math.max(o.y - o.h, Math.min(player.y, o.y));
        const dist = Math.sqrt((player.x - cx)**2 + (player.y - cy)**2);
        
        if (dist < player.r * 0.8) gameOver();
      });

      obstacles = obstacles.filter(o => o.x > -100);
    }

    function draw() {
      ctx.clearRect(0, 0, W, H);

      // Draw Ground
      ctx.fillStyle = '#16a34a'; // Grass
      ctx.fillRect(0, H * 0.8, W, H * 0.2);
      ctx.strokeStyle = 'rgba(255,255,255,0.3)';
      ctx.lineWidth = 4;
      ctx.strokeRect(-10, H * 0.8, W + 20, 2);

      // Draw Obstacles
      obstacles.forEach(o => {
        ctx.fillStyle = o.type === 'stumps' ? '#fde047' : '#94a3b8';
        ctx.fillRect(o.x, o.y - o.h, o.w, o.h);
        // Detail
        ctx.strokeStyle = 'black';
        ctx.lineWidth = 1;
        ctx.strokeRect(o.x, o.y - o.h, o.w, o.h);
      });

      // Draw Player (Cricket Ball)
      ctx.save();
      ctx.translate(player.x, player.y);
      ctx.rotate(player.rotation);
      
      // Shadow
      ctx.beginPath();
      ctx.fillStyle = 'rgba(0,0,0,0.2)';
      ctx.ellipse(0, player.r + (groundY() - player.y - player.r), player.r, player.r*0.3, 0, 0, Math.PI*2);
      ctx.fill();

      // Ball
      ctx.beginPath();
      ctx.arc(0, 0, player.r, 0, Math.PI * 2);
      ctx.fillStyle = '#ef4444'; // Red ball
      ctx.fill();
      
      // Seam
      ctx.strokeStyle = 'white';
      ctx.lineWidth = 3;
      ctx.beginPath();
      ctx.arc(0, 0, player.r, -0.2, 0.2);
      ctx.stroke();
      ctx.restore();

      requestAnimationFrame(() => draw());
    }

    function groundY() { return H * 0.8; }

    function gameOver() {
      running = false;
      scores[currentPlayer] = Math.floor(distance);
      
      const isLastPlayer = currentPlayer === totalPlayers - 1;
      
      document.getElementById('overlayTitle').innerText = "WICKET!";
      document.getElementById('overlayText').innerText = `Player ${currentPlayer + 1} scored ${Math.floor(distance)} runs.`;
      
      if (isLastPlayer) {
        primaryBtn.innerText = "NEW TOURNAMENT";
        secondaryBtn.classList.remove('hidden');
      } else {
        primaryBtn.innerText = `READY PLAYER ${currentPlayer + 2}`;
      }
      overlay.classList.remove('hidden');
    }

    function resetGame() {
      distance = 0;
      speed = 7;
      obstacles = [];
      player.y = H * 0.8 - player.r;
      player.vy = 0;
      running = true;
      overlay.classList.add('hidden');
      hudPlayer.innerText = `PLAYER ${currentPlayer + 1}`;
    }

    // Controls
    window.onpointerdown = () => {
      if (running && player.onGround) {
        player.vy = player.jumpPower;
        player.onGround = false;
      }
    };

    primaryBtn.onclick = () => {
      if (!running && (currentPlayer === totalPlayers - 1 || scores.length === 0)) {
        // Start fresh
        totalPlayers = parseInt(document.getElementById('playerCount').value);
        scores = new Array(totalPlayers).fill(0);
        currentPlayer = 0;
        document.getElementById('setupControls').classList.add('hidden');
      } else {
        currentPlayer++;
      }
      resetGame();
    };

    secondaryBtn.onclick = () => {
      let results = scores.map((s, i) => `P${i+1}: ${s}m`).join(' | ');
      alert("FINAL STANDINGS: " + results);
    };

    document.getElementById('playerCount').oninput = (e) => {
      document.getElementById('playerCountLabel').innerText = e.target.value;
    };

    let lastTime = 0;
    function loop(t) {
      update(t - lastTime);
      lastTime = t;
      requestAnimationFrame(loop);
    }
    
    draw();
    loop(0);
  </script>
</body>
</html>
# Culor-Blue-Z-
