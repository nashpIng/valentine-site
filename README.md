<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8"/>
  <meta name="viewport" content="width=device-width,initial-scale=1"/>
  <title>Cat Quest: Valentine Edition 🐾</title>
  <style>
    :root{
      --bg:#0b1020;
      --card:#121a33cc;
      --line:#ffffff14;
      --text:#eaf0ff;
      --muted:#b9c5ffcc;
      --accent:#ff4d8d;
      --accent2:#7c5cff;
      --good:#39d98a;
      --shadow: 0 18px 70px rgba(0,0,0,.45);
      --radius: 22px;
      --font: ui-sans-serif, system-ui, -apple-system, Segoe UI, Roboto, Arial, "Apple Color Emoji","Segoe UI Emoji";
    }
    *{box-sizing:border-box}
    body{
      margin:0;
      font-family:var(--font);
      background:
        radial-gradient(900px 540px at 15% 10%, #1a2a6b44, transparent 60%),
        radial-gradient(900px 540px at 85% 20%, #ff4d8d33, transparent 60%),
        radial-gradient(900px 540px at 50% 90%, #7c5cff33, transparent 60%),
        linear-gradient(180deg, #070a14, var(--bg));
      color:var(--text);
      min-height:100vh;
      display:grid;
      place-items:center;
      overflow:hidden;
    }
    .stars{ position:fixed; inset:0; pointer-events:none; opacity:.35; }
    .star{
      position:absolute;
      width:2px; height:2px;
      background:white;
      border-radius:999px;
      animation: twinkle 3.8s ease-in-out infinite;
    }
    @keyframes twinkle{ 0%,100%{opacity:.15; transform:scale(.9)} 50%{opacity:.9; transform:scale(1.3)} }

    .wrap{
      width:min(820px, 92vw);
      margin:24px 0;
    }
    .topbar{
      display:flex; justify-content:space-between; align-items:center;
      gap:12px; margin-bottom:14px;
    }
    .pill{
      display:inline-flex; align-items:center; gap:8px;
      padding:10px 12px;
      border:1px solid var(--line);
      border-radius:999px;
      background:#0f1730a8;
      backdrop-filter: blur(10px);
      font-size:13px;
      color:var(--muted);
    }
    .pill b{ color:var(--text); }
    .card{
      background:var(--card);
      border:1px solid var(--line);
      border-radius:var(--radius);
      box-shadow:var(--shadow);
      backdrop-filter: blur(12px);
      overflow:hidden;
    }
    .hero{
      padding:22px;
      border-bottom:1px solid var(--line);
      background:
        radial-gradient(900px 260px at 20% 0%, #ff4d8d22, transparent 70%),
        radial-gradient(900px 260px at 80% 0%, #7c5cff22, transparent 70%),
        linear-gradient(180deg, #111a38aa, transparent);
    }
    h1{
      margin:0 0 6px;
      font-size: clamp(26px, 4.8vw, 44px);
      letter-spacing:-.02em;
      line-height:1.05;
    }
    p{ margin:0; color:var(--muted); line-height:1.6; }

    .content{ padding:18px; }
    .screen{ display:none; }
    .screen.active{ display:block; }

    .grid{
      display:grid;
      grid-template-columns: 1.1fr .9fr;
      gap:14px;
    }
    @media (max-width: 760px){ .grid{ grid-template-columns: 1fr; } }

    .panel{
      border:1px solid var(--line);
      border-radius:18px;
      background:#0f1730a8;
      padding:16px;
    }

    .btnRow{ display:flex; gap:10px; flex-wrap:wrap; margin-top:14px; }
    button{
      font-family:var(--font);
      border:0; border-radius:16px;
      padding:12px 14px;
      font-weight:800;
      cursor:pointer;
      transition: transform .08s ease, box-shadow .18s ease, opacity .2s ease;
      user-select:none;
    }
    button:active{ transform: translateY(1px) scale(.99); }
    .primary{
      background: linear-gradient(135deg, var(--accent), var(--accent2));
      color:white;
      box-shadow: 0 18px 45px rgba(255,77,141,.22);
      flex: 1 1 220px;
    }
    .ghost{
      background: transparent;
      border:1px solid var(--line);
      color:var(--text);
      flex: 1 1 220px;
    }
    .good{
      background: linear-gradient(135deg, var(--good), #2bb8ff);
      color:#061018;
      box-shadow: 0 18px 45px rgba(57,217,138,.14);
      flex: 1 1 220px;
    }

    .catTerm{
      font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, "Liberation Mono","Courier New", monospace;
      font-size:13px;
      line-height:1.55;
      color:#dbe6ff;
      background:#070b18;
      border:1px solid #ffffff12;
      border-radius:16px;
      padding:14px;
      min-height:110px;
      white-space:pre-wrap;
    }

    /* Mini-game pawprints */
    .paws{
      display:grid;
      grid-template-columns: repeat(3, 1fr);
      gap:10px;
      margin-top:10px;
    }
    .paw{
      border:1px solid var(--line);
      border-radius:18px;
      background:#0b1228;
      padding:16px;
      text-align:center;
      font-size:30px;
      cursor:pointer;
      transition: transform .12s ease, box-shadow .18s ease;
      position:relative;
      overflow:hidden;
    }
    .paw:hover{ box-shadow: 0 14px 40px rgba(0,0,0,.28); }
    .paw.hit{
      outline:2px solid #39d98a66;
      background:#071a12;
    }
    .paw .spark{
      position:absolute; inset:0;
      background: radial-gradient(200px 120px at 50% 30%, #39d98a33, transparent 70%);
      opacity:0; transition:opacity .2s ease;
    }
    .paw.hit .spark{ opacity:1; }

    /* Question buttons area */
    .qWrap{ position:relative; height:130px; margin-top:10px; }
    .qBtns{
      display:flex; gap:10px; flex-wrap:wrap;
      align-items:center;
      position:absolute; left:0; top:0; right:0;
    }
    .noWrap{ position:relative; flex: 1 1 220px; min-width:220px; height:48px; }
    .noBtn{
      position:absolute; left:0; top:0;
      width:100%;
      border:1px solid var(--line);
      background: transparent;
      color:var(--text);
    }
    .fineprint{
      margin-top:10px;
      font-size:12px;
      color:#c9d4ffb3;
    }
    .fineprint a{ color:#c9d4ff; text-decoration:underline; }
    .result{
      margin-top:12px;
      padding:12px;
      border-radius:16px;
      border:1px solid var(--line);
      background:#0b1228;
      display:none;
    }
    .result.show{ display:block; }

    .tag{
      display:inline-flex; align-items:center; gap:8px;
      padding:8px 10px;
      border-radius:999px;
      border:1px solid var(--line);
      background:#0b1228;
      color:var(--muted);
      font-size:12px;
      margin-top:10px;
    }
  </style>
</head>
<body>
  <div class="stars" id="stars" aria-hidden="true"></div>

  <div class="wrap">
    <div class="topbar">
      <div class="pill">🐾 <b>Cat Quest</b> Valentine Edition</div>
      <div class="pill">💌 For: <b id="nameA">Aaliya</b> · From: <b id="nameN">Nash</b></div>
    </div>

    <div class="card">
      <div class="hero">
        <h1 id="title">Aaliya, you’ve been invited to a tiny quest ✨</h1>
        <p id="subtitle">Complete the cat’s mini-missions to unlock a question. No pressure, just cute.</p>
      </div>

      <div class="content">

        <!-- Screen 1 -->
        <section class="screen active" id="s1">
          <div class="grid">
            <div class="panel">
              <div class="catTerm" id="term"></div>
              <div class="tag">Tip: it’s short — like a cat’s attention span.</div>
            </div>
            <div class="panel">
              <p><b>Mission 1:</b> Start the quest.</p>
              <p style="margin-top:8px">
                A small cat courier insists you’re the chosen one.
                Tap “Begin” to proceed to Mission 2.
              </p>
              <div class="btnRow">
                <button class="primary" id="beginBtn">Begin Quest 🗝️</button>
                <button class="ghost" id="peekBtn">Peek the map 🗺️</button>
              </div>
              <div class="result" id="mapResult"></div>
            </div>
          </div>
        </section>

        <!-- Screen 2 -->
        <section class="screen" id="s2">
          <div class="grid">
            <div class="panel">
              <p><b>Mission 2:</b> Help the cat collect <b>3 pawprints</b>.</p>
              <p style="margin-top:8px">Tap any paw tiles until you’ve collected three. (The cat says thank you.)</p>
              <div class="paws" id="paws">
                <div class="paw" data-i="1">🐾<div class="spark"></div></div>
                <div class="paw" data-i="2">🐾<div class="spark"></div></div>
                <div class="paw" data-i="3">🐾<div class="spark"></div></div>
                <div class="paw" data-i="4">🐾<div class="spark"></div></div>
                <div class="paw" data-i="5">🐾<div class="spark"></div></div>
                <div class="paw" data-i="6">🐾<div class="spark"></div></div>
              </div>
              <div class="tag" id="pawCount">Collected: 0 / 3</div>
            </div>
            <div class="panel">
              <p><b>Cat status:</b> <span id="status">curious…</span></p>
              <p style="margin-top:8px">Once you collect 3, you’ll unlock Mission 3.</p>
              <div class="btnRow">
                <button class="ghost" id="back1">← Back</button>
                <button class="good" id="toQ" disabled>Unlock Mission 3 🔓</button>
              </div>
              <div class="result" id="unlockMsg"></div>
            </div>
          </div>
        </section>

        <!-- Screen 3 -->
        <section class="screen" id="s3">
          <div class="grid">
            <div class="panel">
              <p style="font-size:18px; margin:0 0 8px;"><b>Mission 3:</b> The question 💖</p>
              <p>
                I was thinking: a cozy date + your favorite snacks + maybe a dessert run or movie night.

              </p>
              <div class="tag">You can choose freely — the cat respects consent 🐱</div>

              <div class="qWrap">
                <div class="qBtns">
                  <button class="primary" id="yes">Yes, I’ll be your Valentine 🐾</button>

                  <!-- The playful “dodging” button lives inside this wrapper -->
                  <div class="noWrap" id="noWrap">
                    <button class="noBtn" id="no">Not right now</button>
                  </div>
                </div>
              </div>

              

              <div class="result" id="finalResult"></div>
            </div>

            <div class="panel">
              <p><b>Bonus:</b> Choose the “date vibe”</p>
              <p style="margin-top:8px">This just personalizes the message if she taps “Yes”.</p>
              <div class="btnRow">
                <button class="ghost vibe" data-v="Dessert run">🍰 Dessert run</button>
                <button class="ghost vibe" data-v="Movie night">🎬 Movie night</button>
              </div>
              <div class="tag" id="vibeTag">Selected vibe: Cat café</div>

              <div class="btnRow" style="margin-top:14px">
                <button class="ghost" id="back2">← Back</button>
                <button class="ghost" id="restart">Restart Quest ↻</button>
              </div>
            </div>
          </div>
        </section>

      </div>
    </div>
  </div>

  <script>
    // Personalization
    const HER_NAME = "Aaliya";
    const YOUR_NAME = "Nash";

    document.getElementById("nameA").textContent = HER_NAME;
    document.getElementById("nameN").textContent = YOUR_NAME;
    document.getElementById("title").textContent = `${HER_NAME}, you’ve been invited to a tiny quest ✨`;
    document.getElementById("subtitle").textContent = `From ${YOUR_NAME}: three small missions, then one sweet question.`;

    // Stars
    const stars = document.getElementById("stars");
    for(let i=0;i<90;i++){
      const s = document.createElement("div");
      s.className="star";
      s.style.left = Math.random()*100+"vw";
      s.style.top = Math.random()*100+"vh";
      s.style.animationDelay = (-Math.random()*5)+"s";
      s.style.opacity = (0.12 + Math.random()*0.9).toFixed(2);
      s.style.transform = `scale(${(0.8 + Math.random()*1.6).toFixed(2)})`;
      stars.appendChild(s);
    }

    // Screen navigation helpers
    const screens = ["s1","s2","s3"].map(id=>document.getElementById(id));
    function show(id){
      screens.forEach(s => s.classList.remove("active"));
      document.getElementById(id).classList.add("active");
      window.scrollTo({ top: 0, behavior: "smooth" });
    }

    // Typewriter terminal
    const term = document.getElementById("term");
    const intro =
`> booting cat-quest…
> courier: "hello ${HER_NAME}."
> mission: deliver valentine message
> requirement: 3 pawprints
> reward: a question 💌`;
    (function typewrite(text, speed=16){
      term.textContent = "";
      let i=0;
      const tick=()=>{
        term.textContent += text[i] ?? "";
        i++;
        if(i<text.length) setTimeout(tick, speed);
      };
      tick();
    })(intro);

    // Screen 1 actions
    const mapResult = document.getElementById("mapResult");
    document.getElementById("peekBtn").addEventListener("click", ()=>{
      mapResult.classList.add("show");
      mapResult.innerHTML = `🗺️ Map: Mission 1 → Mission 2 → Mission 3 (Question).`;
    });
    document.getElementById("beginBtn").addEventListener("click", ()=> show("s2"));

    // Screen 2 paw mini-game
    let collected = 0;
    const pawCount = document.getElementById("pawCount");
    const toQ = document.getElementById("toQ");
    const status = document.getElementById("status");
    const unlockMsg = document.getElementById("unlockMsg");

    document.getElementById("paws").addEventListener("click", (e)=>{
      const tile = e.target.closest(".paw");
      if(!tile) return;
      if(tile.classList.contains("hit")) return;

      tile.classList.add("hit");
      collected++;
      pawCount.textContent = `Collected: ${collected} / 3`;

      if(collected === 1) status.textContent = "purring softly…";
      if(collected === 2) status.textContent = "very pleased…";
      if(collected >= 3){
        status.textContent = "zoomies unlocked!!";
        toQ.disabled = false;
        unlockMsg.classList.add("show");
        unlockMsg.innerHTML = `✅ Pawprints collected. Mission 3 is ready.`;
      }
    });

    document.getElementById("back1").addEventListener("click", ()=> show("s1"));
    document.getElementById("toQ").addEventListener("click", ()=> show("s3"));

    // Screen 3 vibe picker
    let vibe = "Cat café";
    const vibeTag = document.getElementById("vibeTag");
    document.querySelectorAll(".vibe").forEach(btn=>{
      btn.addEventListener("click", ()=>{
        vibe = btn.dataset.v;
        vibeTag.textContent = `Selected vibe: ${vibe}`;
      });
    });

    // Yes / No logic (playful, but not coercive)
    const yes = document.getElementById("yes");
    const no = document.getElementById("no");
    const noWrap = document.getElementById("noWrap");
    const finalResult = document.getElementById("finalResult");
    const realNo = document.getElementById("realNo");

    let dodgesLeft = 4; // playful dodges, then it stops dodging
    function showYes(){
      finalResult.classList.add("show");
      finalResult.innerHTML =
        `🥹💖 <b>YAY!!</b><br>
         Text ${YOUR_NAME}: <b>"YES 🐾"</b><br>
         Plan idea: <b>${vibe}</b> + favorite snacks + cozy time.`;
      burst();
    }
    function showNo(){
      finalResult.classList.add("show");
      finalResult.innerHTML =
        `Not Possible there is no consent<br>
         You need to restart the quest and make sure to say Yes😤.`;
    }

    yes.addEventListener("click", showYes);

    // The button dodges a few times (joke), then allows a normal click.
    function dodge(){
      const box = noWrap.getBoundingClientRect();
      const maxX = Math.max(0, box.width - 140);
      const maxY = 0; // keep it horizontally playful
      const x = Math.random() * maxX;
      const y = Math.random() * maxY;
      no.style.left = x + "px";
      no.style.top = y + "px";
    }

    no.addEventListener("pointerenter", ()=>{
      if(dodgesLeft > 0){
        dodgesLeft--;
        dodge();
      }
    });

    no.addEventListener("click", ()=>{
      // If it still has dodges left, treat click as a normal “no” anyway.
      // (This preserves choice even if she manages to click early.)
      showNo();
    });

    // Always available real “no”
    realNo.addEventListener("click", (e)=>{
      e.preventDefault();
      showNo();
    });

    document.getElementById("restart")?.addEventListener("click", ()=>{
        collected = 0;
        dodgesLeft = 8;

        document.getElementById("finalResult")?.classList.remove("show");
        document.getElementById("unlockMsg")?.classList.remove("show");

        const toQ = document.getElementById("toQ");
        if (toQ) toQ.disabled = true;

        const statusEl = document.getElementById("status");
        if (statusEl) statusEl.textContent = "curious…";

        const pawCountEl = document.getElementById("pawCount");
        if (pawCountEl) pawCountEl.textContent = "Collected: 0 / 3";

        document.querySelectorAll(".paw").forEach(p=>p.classList.remove("hit"));

        const no = document.getElementById("no");
        if (no){
        no.style.left = "0px";
        no.style.top = "0px";
        }

        show("s1");

    });

    // simple emoji burst
    function burst(){
      const layer = document.createElement("div");
      layer.style.position="fixed";
      layer.style.inset="0";
      layer.style.pointerEvents="none";
      document.body.appendChild(layer);
      const bits = ["💖","✨","🐾","💗","🌙","⭐"];
      for(let i=0;i<42;i++){
        const b=document.createElement("div");
        b.textContent = bits[Math.floor(Math.random()*bits.length)];
        b.style.position="absolute";
        b.style.left=(50+(Math.random()*24-12))+"vw";
        b.style.top=(44+(Math.random()*16-8))+"vh";
        b.style.fontSize=(14+Math.random()*22)+"px";
        b.style.transition="transform 900ms ease, opacity 900ms ease";
        layer.appendChild(b);
        const dx=(Math.random()*2-1)*360;
        const dy=(Math.random()*2-1)*240-120;
        requestAnimationFrame(()=>{
          b.style.transform=`translate(${dx}px, ${dy}px) rotate(${Math.random()*180}deg)`;
          b.style.opacity="0";
        });
      }
      setTimeout(()=>layer.remove(), 950);
    }
  </script>
</body>
</html>
