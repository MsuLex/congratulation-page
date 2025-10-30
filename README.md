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
    </div>
  </div>

  <script>
    // === YOUR CUSTOM MESSAGE ===
    const CONGRATS_MESSAGE = `
      <strong>Deborah Cone(Debi)!</strong><br>
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
</body>
</html>

