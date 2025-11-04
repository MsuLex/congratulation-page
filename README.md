<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Congratulations</title>
  <style>
    :root{
      --bg:#0f1724; --accent:#ffd166; --muted:#94a3b8;
      --ff: "Segoe UI", Roboto, system-ui, -apple-system, "Helvetica Neue", Arial;
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:var(--ff);
      background: radial-gradient(800px 400px at 10% 10%, rgba(255,209,102,0.06), transparent 8%),
                  radial-gradient(600px 300px at 90% 90%, rgba(99,102,241,0.04), transparent 6%),
                  var(--bg);
      color:#fff;
      display:flex;
      align-items:center;
      justify-content:center;
      height:100vh;
    }

    .overlay{
      position:fixed;
      inset:0;
      display:flex;
      align-items:center;
      justify-content:center;
      z-index:9999;
      opacity:0;
      transition:opacity 0.4s ease;
      pointer-events:none;
    }
    .overlay.show{opacity:1; pointer-events:auto;}

    .congratsBox{
      background: linear-gradient(180deg, rgba(9,16,28,0.95), rgba(6,10,16,0.95));
      border-radius:20px;
      padding:36px 28px;
      text-align:center;
      box-shadow:0 30px 90px rgba(3,6,20,0.8), 0 6px 30px rgba(0,0,0,0.6);
      transform:translateY(20px) scale(0.98);
      transition: transform 0.4s cubic-bezier(.2,.9,.3,1);
      width:min(90%,600px);
    }
    .overlay.show .congratsBox{transform:translateY(0) scale(1);}
    .congratsTitle{
      font-size:40px;
      margin:0 0 10px;
      color:var(--accent);
    }
    .congratsMessage{
      font-size:18px;
      line-height:1.6;
      color:#dbeafe;
    }
    .glow{
      position:absolute;
      inset:-20% -10% auto auto;
      width:600px;
      height:600px;
      background: radial-gradient(circle at 20% 20%, rgba(255,221,150,0.10), transparent 15%),
                  radial-gradient(circle at 80% 80%, rgba(120,98,255,0.06), transparent 12%);
      transform:rotate(-12deg);
      filter: blur(36px);
      pointer-events:none;
      z-index:-1;
    }
  .msgBtn{
      margin-top:24px;
      display:inline-flex;
      align-items:center;
      gap:10px;
      padding:14px 26px;
      background:var(--accent);
      color:#000;
      font-weight:600;
      border-radius:9999px;
      text-decoration:none;
      box-shadow:0 0 0 rgba(255,209,102,0.5);
      transition:transform .25s, box-shadow .25s;
    }
    .msgBtn:hover{
      transform:translateY(-3px) scale(1.05);
      box-shadow:0 0 25px rgba(255,209,102,0.45);
    }
    .msgBtn:hover{
      transform:translateY(-2px);
      opacity:0.9;
    }
  </style>
</head>
<body>
  <div id="overlay" class="overlay" aria-hidden="true" aria-modal="true" role="dialog">
    <div class="congratsBox">
      <div class="glow"></div>
      <h2 class="congratsTitle">🎉 Congratulations!</h2>
      <div id="congratsText" class="congratsMessage">
        <!-- Replace this message with your own -->
        You did it — this is your custom congratulation message. Replace me with the message you want shown immediately on page load.
      </div>
      <a href="https://m.me/921757524343785" class="msgBtn"><svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M22 2L2 12l7.5 2.5L12 22l3.5-7.5L22 2z"/></svg> Message Me on Messenger</a>
    </div>
  </div>

  <script>
    // === YOUR CUSTOM MESSAGE ===
    const CONGRATS_MESSAGE = `
      <strong>My lovely fan!</strong><br>
      You've been successfully been adeed to the Wener Music Nashville Membership!
      Your official membership card will be delivered to you soon. Make sure to stay active by following up with our shows and event to enjoy all the exclusive benefit that come with your membership
    `;
    // ===========================

    const overlay = document.getElementById('overlay');
    const congratsText = document.getElementById('congratsText');
    congratsText.innerHTML = CONGRATS_MESSAGE;

    function showOverlay() {
      overlay.classList.add('show');
      overlay.setAttribute('aria-hidden','false');
    }

    // Show overlay immediately after page load
    window.addEventListener('DOMContentLoaded', () => setTimeout(showOverlay, 10));
  </script>
<canvas id="fireworksCanvas" style="position:fixed; inset:0; pointer-events:none; z-index:9998;"></canvas>

<script>
  const canvas = document.getElementById('fireworksCanvas');
  const ctx = canvas.getContext('2d');
  let W, H;
  function resize(){ W = canvas.width = innerWidth; H = canvas.height = innerHeight; }
  resize(); addEventListener('resize', resize);

  const particles = [];
  function fire(x,y){
    for(let i=0;i<60;i++){
      particles.push({
        x, y,
        angle: Math.random()*Math.PI*2,
        speed: Math.random()*4+2,
        life: 60
      });
    }
  }

  function animate(){
    ctx.clearRect(0,0,W,H);
    for(let i=particles.length-1;i>=0;i--){
      const p = particles[i];
      p.x += Math.cos(p.angle)*p.speed;
      p.y += Math.sin(p.angle)*p.speed;
      p.speed *= 0.96;
      p.life--;
      ctx.fillStyle = 'rgba(255,209,102,'+(p.life/60)+')';
      ctx.fillRect(p.x,p.y,3,3);
      if(p.life<=0) particles.splice(i,1);
    }
    requestAnimationFrame(animate);
  }
  animate();

  window.addEventListener('DOMContentLoaded',()=>{
    setTimeout(()=>{
      const {innerWidth:w, innerHeight:h} = window;
      fire(w*0.3,h*0.4);
      fire(w*0.7,h*0.4);
      fire(w*0.5,h*0.6);
    },600);
  });
</script>
</body>
</html>
