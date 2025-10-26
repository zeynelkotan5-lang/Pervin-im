<!doctype html>
<html lang="tr">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Pervin, benimle çıkar mısın?</title>
  <style>
    :root{
      --bg:#100b1d;
      --accent:#ff2d95;
      --muted:#f3e9f5;
    }
    html,body{height:100%;margin:0;font-family: "Helvetica Neue", Arial, sans-serif;background: radial-gradient(circle at 10% 10%, #261441 0%, var(--bg) 60%);color:var(--muted);}
    .wrap{min-height:100%;display:flex;align-items:center;justify-content:center;padding:24px;box-sizing:border-box;}
    .card{width:100%;max-width:720px;background:linear-gradient(180deg, rgba(255,255,255,0.03), rgba(0,0,0,0.06));border-radius:16px;padding:28px;box-shadow:0 8px 30px rgba(0,0,0,0.6);position:relative;overflow:hidden;text-align:center;}
    .title{font-size:28px;margin:0 0 8px;color:var(--muted);letter-spacing:0.4px;}
    .subtitle{font-size:16px;margin:0 0 18px;opacity:0.9;}
    .heart{font-size:92px;line-height:1;margin:6px 0 10px;color:var(--accent);text-shadow:0 6px 18px rgba(255,45,149,0.16);}
    .message{font-size:18px;margin-bottom:20px;}
    .controls{display:flex;gap:12px;justify-content:center;flex-wrap:wrap;margin-top:6px;}
    button{padding:12px 22px;font-size:18px;border-radius:999px;border:0;cursor:pointer;transition:transform .12s ease,box-shadow .12s;box-shadow:0 6px 18px rgba(0,0,0,0.45);outline:none;}
    .yes{background:linear-gradient(90deg,var(--accent),#ff6ab3);color:white;}
    .no{background:transparent;border:2px solid rgba(255,255,255,0.12);color:var(--muted);}
    .note{margin-top:14px;font-size:13px;opacity:0.85;}
    .confetti {position:absolute;left:0;top:0;right:0;bottom:0;pointer-events:none;overflow:hidden;}
    .confetti i{position:absolute;display:block;width:12px;height:12px;background:var(--accent);transform:rotate(25deg);border-radius:3px;opacity:0.95;animation:fall 1600ms linear forwards;}
    @keyframes fall {to{transform:translateY(110vh) rotate(360deg);opacity:0;}}
    @media (max-width:420px){.title{font-size:22px}.heart{font-size:68px}.message{font-size:16px}}
  </style>
</head>
<body>
  <div class="wrap">
    <div class="card" id="card">
      <div class="heart">💗</div>
      <h1 class="title">Pervin, benimle çıkar mısın?</h1>
      <p class="subtitle">Küçük bir soru... ama cevabını tahmin ediyorum 😊</p>

      <p class="message" id="message">Pervin, bu sayfa senin için hazırlandı. "Hayır"a bastıkça "Evet" tuşu büyür... belki kalbim kadar 💞</p>

      <div class="controls">
        <button class="yes" id="yesBtn">Evet ❤️</button>
        <button class="no" id="noBtn">Hayır 😅</button>
      </div>

      <p class="note">Not: "Evet"e bastığında küçük bir sürpriz seni bekliyor 🎉</p>

      <div class="confetti" id="confetti"></div>
    </div>
  </div>

  <script>
    const yesBtn = document.getElementById('yesBtn');
    const noBtn = document.getElementById('noBtn');
    let yesScale = 1;

    noBtn.addEventListener('click', ()=> {
      yesScale += 0.15;
      yesBtn.style.transform = `scale(${yesScale})`;
      yesBtn.style.boxShadow = '0 10px 30px rgba(0,0,0,0.55)';
      setTimeout(()=> yesBtn.style.boxShadow = '', 350);
      if (yesScale > 2.4) {
        document.getElementById('message').textContent = 'Artık evet demenin zamanı geldi sanırım 😄';
      }
    });

    yesBtn.addEventListener('click', ()=> {
      spawnConfetti(30);
      yesBtn.textContent = 'Evet, kesinlikle! 💖';
      yesBtn.disabled = true;
      noBtn.disabled = true;
      setTimeout(()=> {
        document.getElementById('message').textContent = 'Pervin, seni çok seviyorum 💞';
      }, 600);
    });

    function spawnConfetti(count=20){
      const box = document.getElementById('confetti');
      for(let i=0;i<count;i++){
        const el = document.createElement('i');
        el.style.left = Math.random()*100 + '%';
        el.style.top = (-10 - Math.random()*20) + 'px';
        el.style.width = (8 + Math.random()*12) + 'px';
        el.style.height = el.style.width;
        el.style.background = `linear-gradient(180deg, rgba(255,45,149,1), rgba(255,185,220,1))`;
        el.style.animationDuration = (1000 + Math.random()*1200) + 'ms';
        box.appendChild(el);
        setTimeout(()=> el.remove(), 2200);
      }
    }
  </script>
</body>
</html>
