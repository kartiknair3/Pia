<html lang="de">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Will You Be My Valentine? 💙</title>

  <style>
    :root{
      --card:rgba(255,255,255,.10);
      --stroke:rgba(255,255,255,.18);
      --text:rgba(255,255,255,.94);
      --muted:rgba(255,255,255,.74);
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family: system-ui, -apple-system, Segoe UI, Roboto, Helvetica, Arial, sans-serif;
      color:var(--text);
      overflow:hidden;
      background:#020617;
    }

    /* ===== Northern Lights VIDEO background ===== */
    .bg-video{
      position:fixed;
      inset:0;
      z-index:0;
      overflow:hidden;
      background:#020617;
    }
    .bg-video video{
      width:100%;
      height:100%;
      object-fit:cover;
      object-position:center;
      filter:saturate(1.1) contrast(1.05) brightness(.95);
      transform: scale(1.02);
    }
    /* dark overlay so text is readable */
    .bg-video::after{
      content:"";
      position:absolute;
      inset:0;
      background: radial-gradient(900px 600px at 20% 20%, rgba(0,0,0,.25), rgba(0,0,0,.55));
      pointer-events:none;
    }

    /* ===== Foreground ===== */
    .wrap{
      min-height:100%;
      display:grid;
      place-items:center;
      padding:24px;
      position:relative;
      z-index:2;
    }
    .card{
      width:min(760px, 92vw);
      background:var(--card);
      border:1px solid var(--stroke);
      border-radius:28px;
      padding:26px 22px;
      box-shadow: 0 18px 60px rgba(0,0,0,.45);
      backdrop-filter: blur(14px);
      text-align:center;
      position:relative;
      overflow:hidden;
    }

    /* Intro text */
    .intro-text{
      display:flex;
      flex-direction:column;
      gap:14px;
      font-size: clamp(16px, 2.2vw, 20px);
      line-height: 1.7;
      color: rgba(255,255,255,.95);
      text-shadow:
        0 0 22px rgba(120,200,255,.28),
        0 0 44px rgba(80,160,255,.12);
      margin-bottom: 14px;
    }
    .intro-text span{
      opacity:0;
      transform: translateY(10px);
      animation: fadeLine 1.2s ease forwards;
    }
    @keyframes fadeLine{
      to{ opacity:1; transform: translateY(0); }
    }

    /* Buttons */
    .buttons{
      margin-top: 18px;
      display:flex;
      justify-content:center;
      gap:12px;
      flex-wrap:wrap;
      position:relative;
      min-height:64px;
    }
    button{
      border:0;
      border-radius: 16px;
      padding: 14px 22px;
      font-size: 16px;
      font-weight: 800;
      cursor:pointer;
      transition: transform .12s ease, opacity .12s ease;
      user-select:none;
    }
    button:active{ transform: translateY(1px); }

    .yes{
      background: linear-gradient(135deg, #34d399, #22c55e);
      color: #062016;
      box-shadow: 0 12px 30px rgba(34,197,94,.25);
    }
    .no{
      background: rgba(255,255,255,.14);
      color: rgba(255,255,255,.92);
      border: 1px solid rgba(255,255,255,.18);
      box-shadow: 0 12px 30px rgba(0,0,0,.22);
      position:absolute; /* so left/top works */
      left: 52%;
      top: 0;
    }

    h1{
      margin: 0 0 14px;
      font-size: clamp(26px, 3.2vw, 40px);
      letter-spacing:-0.02em;
    }
    .sub{
      margin: 0 0 6px;
      color: var(--muted);
      font-size: clamp(14px, 1.8vw, 17px);
    }

    /* Modal */
    .overlay{
      position:fixed;
      inset:0;
      z-index:50;
      display:none;
      place-items:center;
      background: rgba(0,0,0,.45);
      padding:18px;
    }
    .overlay.show{ display:grid; }
    .modal{
      width:min(640px, 92vw);
      background: rgba(255,255,255,.12);
      border: 1px solid rgba(255,255,255,.18);
      border-radius: 28px;
      padding: 24px 20px;
      text-align:center;
      backdrop-filter: blur(14px);
      box-shadow: 0 22px 70px rgba(0,0,0,.5);
    }

    /* Confetti */
    canvas#confetti{
      position:fixed;
      inset:0;
      z-index:60;
      pointer-events:none;
      display:none;
    }
    canvas#confetti.show{ display:block; }

    /* small hint */
    .hint{
      margin-top: 10px;
      font-size: 12px;
      color: rgba(255,255,255,.55);
    }
  </style>
</head>

<body>
  <!-- VIDEO BACKGROUND -->
  <div class="bg-video" aria-hidden="true">
    <video id="auroraVideo" autoplay muted loop playsinline preload="auto">
      <source src="northern-lights.mp4" type="video/mp4">
    </video>
  </div>

  <div class="wrap">
    <div class="card" id="card">

      <!-- INTRO -->
      <div id="intro">
        <div id="introMessage" class="intro-text">
          <span>Ich will, dass du eines weißt: 💫</span>
          <span>Ich werde immer hart dafür arbeiten, dir jeden Wunsch zu erfüllen. 🤍</span>
          <span>Für dein Lächeln würde ich alles tun, wirklich alles. ✨</span>
          <span>Ich gehe in jede Bäckerei, bis ich deinen Lieblingskuchen gefunden habe. 🍰</span>
          <span>Ich lerne jedes Rezept, nur um für dich zu kochen und dich dabei glücklich zu sehen. 🍽️</span>
          <span>Ich bringe dir das Leuchten der Nordlichter, nur für dich. 🌌</span>
          <span>Und bei jeder Sternschnuppe wünsche ich mir zuerst dich, noch bevor ich an mich denke. 🌠</span>
          <span>Denn dein Glück bedeutet mir mehr als alles andere. 💙</span>
        </div>

        <div class="buttons" style="position:relative;">
          <button class="yes" id="startBtn">Weiter 💌</button>
        </div>
        <div class="hint">Musik startet nach Klick (Browser-Regel).</div>
      </div>

      <!-- QUESTION (unchanged vibe: Yes/No) -->
      <div id="questionArea" style="display:none;">
        <p class="sub">One tiny question…</p>
        <h1>Will you be my Valentine? 💘</h1>

        <div class="buttons" id="questionButtons">
          <button class="yes" id="yesBtn">Yes 💖</button>
          <button class="no" id="noBtn">No 🙃</button>
        </div>
      </div>

    </div>
  </div>

  <!-- FINAL MODAL -->
  <div class="overlay" id="overlay" aria-hidden="true">
    <div class="modal">
      <h2 style="margin:0 0 10px; font-size:clamp(26px, 3.2vw, 40px);">💖 YAYYYYY 💖</h2>
      <p style="margin:0; font-size:clamp(15px, 2vw, 18px); line-height:1.6; color:rgba(255,255,255,.92);">
        Du hast mir gerade die ganze Woche versüßt. ✨<br><br>
        Mach dich am <b>14. Februar um 19:00 Uhr</b> bereit —<br>
        wir gehen ins <b>beste Steakhouse der Stadt</b>. 🥩🍷<br><br>
        Ich lade dich ein.<br>
        Und ich verspreche dir:<br>
        <b>Ich werde dich wie eine Prinzessin behandeln. 👑💙</b>
      </p>
    </div>
  </div>

  <canvas id="confetti"></canvas>

  <!-- MUSIC (plays once from beginning to end; starts on click) -->
  <audio id="bgMusic" preload="auto">
    <source src="i-wanna-touch-the-northern-lights.mp3" type="audio/mpeg">
  </audio>

  <script>
    // Intro line-by-line fade timing
    document.querySelectorAll("#introMessage span").forEach((line, i) => {
      line.style.animationDelay = `${i * 1.2}s`;
    });

    const auroraVideo = document.getElementById("auroraVideo");
    // Ensure video always starts from the beginning on load
    try { auroraVideo.currentTime = 0; } catch(e) {}

    const music = document.getElementById("bgMusic");
    music.volume = 0.35;

    const intro = document.getElementById("intro");
    const questionArea = document.getElementById("questionArea");
    const startBtn = document.getElementById("startBtn");

    startBtn.addEventListener("click", async () => {
      // Start music from beginning (plays to end, no loop)
      music.pause();
      music.currentTime = 0;
      try { await music.play(); } catch(e) {}

      // Show question
      intro.style.display = "none";
      questionArea.style.display = "block";

      // Make sure No button starts somewhere reasonable
      moveNoButton(true);
    });

    // No button dodge inside button area
    const noBtn = document.getElementById("noBtn");
    const yesBtn = document.getElementById("yesBtn");
    const questionButtons = document.getElementById("questionButtons");

    function moveNoButton(initial=false){
      const areaRect = questionButtons.getBoundingClientRect();
      const btnRect  = noBtn.getBoundingClientRect();

      const padding = 10;
      const maxX = Math.max(padding, areaRect.width - btnRect.width - padding);
      const maxY = Math.max(padding, areaRect.height - btnRect.height - padding);

      const x = padding + Math.random() * (maxX - padding);
      const y = padding + Math.random() * (maxY - padding);

      noBtn.style.left = `${x}px`;
      noBtn.style.top  = `${y}px`;
      if(initial) noBtn.style.opacity = "1";
    }

    noBtn.addEventListener("mouseenter", () => moveNoButton(false));
    noBtn.addEventListener("touchstart", (e) => { e.preventDefault(); moveNoButton(false); }, {passive:false});

    window.addEventListener("resize", () => {
      if(questionArea.style.display === "block") moveNoButton(true);
    });

    // Confetti + final modal
    const overlay = document.getElementById("overlay");
    const canvas = document.getElementById("confetti");
    const ctx = canvas.getContext("2d");

    function resizeCanvas(){
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener("resize", resizeCanvas);
    resizeCanvas();

    let confetti = [];
    let animId = null;

    function startConfetti(){
      overlay.classList.add("show");
      canvas.classList.add("show");

      confetti = Array.from({length: 220}, () => ({
        x: Math.random() * canvas.width,
        y: Math.random() * canvas.height,
        s: 3 + Math.random() * 5,
        vx: -2 + Math.random() * 4,
        vy: 2 + Math.random() * 5,
        h: 300 + Math.random() * 60
      }));

      if(animId) cancelAnimationFrame(animId);
      draw();
    }

    function draw(){
      ctx.clearRect(0,0,canvas.width,canvas.height);
      for(const p of confetti){
        p.x += p.vx;
        p.y += p.vy;
        if(p.y > canvas.height + 20) p.y = -20;
        if(p.x < -20) p.x = canvas.width + 20;
        if(p.x > canvas.width + 20) p.x = -20;

        ctx.fillStyle = `hsl(${p.h} 90% 70%)`;
        ctx.fillRect(p.x, p.y, p.s, p.s);
      }
      animId = requestAnimationFrame(draw);
    }

    yesBtn.addEventListener("click", startConfetti);
  </script>
</body>
</html>
