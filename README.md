<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta
  name="viewport"
  content="width=device-width, initial-scale=1.0"
/>

<title>Cinematic Video Showcase</title>

<style>
/* =========================================================
   RESET
========================================================= */

*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

html,
body{
  width:100%;
  height:100%;
  overflow:hidden;
  background:#0a0a0c;
  font-family:
    "Segoe UI",
    Roboto,
    Helvetica,
    Arial,
    sans-serif;
  color:#fff;
}

/* =========================================================
   DESIGN TOKENS
========================================================= */

:root{
  --bg-primary:#0a0a0c;
  --bg-secondary:#111111;
  --surface:#18181b;

  --accent-a:#ff0055;
  --accent-b:#7a00ff;

  --text-primary:#ffffff;
  --text-secondary:#aaaaaa;
  --text-muted:#666666;

  --glass-border:rgba(255,255,255,0.08);

  --transition:
    cubic-bezier(0.22,1,0.36,1);

  --glow:
    0 0 80px rgba(255,0,85,.16);

  --radius:24px;
}

/* =========================================================
   APP ROOT
========================================================= */

body{
  position:relative;
}

/* =========================================================
   BACKGROUND FX
========================================================= */

#bg-layer{
  position:fixed;
  inset:0;
  overflow:hidden;
  z-index:0;
  background:
    radial-gradient(
      circle at top left,
      rgba(255,0,85,.12),
      transparent 35%
    ),
    radial-gradient(
      circle at bottom right,
      rgba(122,0,255,.15),
      transparent 40%
    ),
    var(--bg-primary);
}

#bg-layer::before{
  content:"";
  position:absolute;
  inset:-20%;
  background:
    linear-gradient(
      135deg,
      rgba(255,0,85,.08),
      rgba(122,0,255,.08)
    );
  filter:blur(100px);
  animation:bgFloat 12s ease-in-out infinite alternate;
}

#bg-layer::after{
  content:"";
  position:absolute;
  inset:0;
  background-image:
    url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='120' height='120' viewBox='0 0 120 120'%3E%3Cg fill='white' fill-opacity='0.03'%3E%3Ccircle cx='2' cy='2' r='2'/%3E%3C/g%3E%3C/svg%3E");
  opacity:.25;
  pointer-events:none;
}

@keyframes bgFloat{
  0%{
    transform:translateY(-20px) scale(1);
  }
  100%{
    transform:translateY(20px) scale(1.08);
  }
}

/* =========================================================
   GLOBAL SCREEN BASE
========================================================= */

.screen{
  position:absolute;
  inset:0;
  display:flex;
  align-items:center;
  justify-content:center;
  transition:
    opacity 1.2s var(--transition),
    transform 1.2s var(--transition);
}

/* =========================================================
   LANDING SCREEN
========================================================= */

#landing-screen{
  z-index:5;
  flex-direction:column;
  gap:28px;
  padding:40px;
  text-align:center;
}

.landing-badge{
  padding:10px 18px;
  border-radius:999px;
  background:rgba(255,255,255,.04);
  border:1px solid rgba(255,255,255,.08);
  color:var(--text-secondary);
  font-size:.82rem;
  letter-spacing:2px;
  text-transform:uppercase;
  backdrop-filter:blur(20px);
}

.landing-title{
  font-size:clamp(3rem,9vw,7rem);
  line-height:.95;
  font-weight:700;
  max-width:1000px;
  letter-spacing:-4px;
}

.gradient-text{
  background:
    linear-gradient(
      135deg,
      var(--accent-a),
      var(--accent-b)
    );
  -webkit-background-clip:text;
  -webkit-text-fill-color:transparent;
}

.landing-subtitle{
  max-width:700px;
  color:var(--text-secondary);
  line-height:1.8;
  font-size:1rem;
}

.enter-btn{
  position:relative;
  overflow:hidden;
  border:none;
  outline:none;
  cursor:pointer;

  padding:18px 34px;
  border-radius:999px;

  background:
    linear-gradient(
      135deg,
      var(--accent-a),
      var(--accent-b)
    );

  color:#fff;
  font-size:1rem;
  font-weight:600;
  letter-spacing:1px;

  transition:
    transform .5s var(--transition),
    box-shadow .5s var(--transition);

  box-shadow:var(--glow);
}

.enter-btn:hover{
  transform:translateY(-3px) scale(1.02);
}

.enter-btn::before{
  content:"";
  position:absolute;
  inset:0;
  background:
    linear-gradient(
      120deg,
      transparent,
      rgba(255,255,255,.2),
      transparent
    );
  transform:translateX(-120%);
  animation:shine 3s infinite;
}

@keyframes shine{
  to{
    transform:translateX(120%);
  }
}

/* =========================================================
   INTRO SCREEN
========================================================= */

#intro-screen{
  z-index:4;
  opacity:0;
  pointer-events:none;
  flex-direction:column;
  text-align:center;
}

.intro-logo{
  width:140px;
  height:140px;
  border-radius:50%;
  position:relative;

  background:
    linear-gradient(
      135deg,
      var(--accent-a),
      var(--accent-b)
    );

  display:flex;
  align-items:center;
  justify-content:center;

  font-size:3rem;
  font-weight:700;

  box-shadow:
    0 0 120px rgba(255,0,85,.3);

  animation:pulse 3s infinite;
}

.intro-logo::after{
  content:"";
  position:absolute;
  inset:-12px;
  border-radius:50%;
  border:1px solid rgba(255,255,255,.08);
}

@keyframes pulse{
  0%{
    transform:scale(1);
  }
  50%{
    transform:scale(1.04);
  }
  100%{
    transform:scale(1);
  }
}

.intro-title{
  margin-top:40px;
  font-size:clamp(2rem,6vw,5rem);
  font-weight:700;
  letter-spacing:-2px;
}

.intro-line{
  width:240px;
  height:2px;
  margin-top:28px;
  background:
    linear-gradient(
      90deg,
      transparent,
      var(--accent-a),
      var(--accent-b),
      transparent
    );
}

.intro-tag{
  margin-top:24px;
  color:var(--text-secondary);
  letter-spacing:4px;
  text-transform:uppercase;
  font-size:.8rem;
}

/* =========================================================
   DASHBOARD
========================================================= */

#video-dashboard{
  z-index:3;
  opacity:0;
  pointer-events:none;
  padding:30px;
}

.dashboard-shell{
  width:100%;
  height:100%;
  border-radius:32px;

  background:
    linear-gradient(
      180deg,
      rgba(255,255,255,.04),
      rgba(255,255,255,.02)
    );

  border:1px solid rgba(255,255,255,.06);

  backdrop-filter:blur(30px);

  overflow:hidden;

  display:flex;
  flex-direction:column;

  box-shadow:
    0 20px 80px rgba(0,0,0,.45);
}

/* =========================================================
   TOPBAR
========================================================= */

.topbar{
  height:88px;
  flex-shrink:0;

  display:flex;
  align-items:center;
  justify-content:space-between;

  padding:0 34px;

  border-bottom:
    1px solid rgba(255,255,255,.06);
}

.brand{
  display:flex;
  align-items:center;
  gap:16px;
}

.brand-dot{
  width:14px;
  height:14px;
  border-radius:50%;

  background:
    linear-gradient(
      135deg,
      var(--accent-a),
      var(--accent-b)
    );

  box-shadow:var(--glow);
}

.brand-name{
  font-size:1.05rem;
  letter-spacing:2px;
  font-weight:600;
}

.top-actions{
  display:flex;
  align-items:center;
  gap:14px;
}

.glass-btn{
  border:none;
  cursor:pointer;

  width:48px;
  height:48px;

  border-radius:16px;

  background:
    rgba(255,255,255,.04);

  border:
    1px solid rgba(255,255,255,.06);

  color:#fff;

  font-size:1rem;

  transition:
    transform .4s var(--transition),
    background .4s;
}

.glass-btn:hover{
  transform:translateY(-2px);
  background:rgba(255,255,255,.08);
}

/* =========================================================
   CONTENT
========================================================= */

.dashboard-content{
  flex:1;
  display:flex;
  padding:24px;
  gap:24px;
  min-height:0;
}

/* =========================================================
   VIDEO PANEL
========================================================= */

.video-panel{
  flex:1;
  position:relative;
  overflow:hidden;
  border-radius:28px;
  background:#000;
}

.video-panel video{
  width:100%;
  height:100%;
  object-fit:cover;
  background:#000;
}

.video-overlay{
  position:absolute;
  inset:0;
  pointer-events:none;

  background:
    linear-gradient(
      to top,
      rgba(0,0,0,.7),
      transparent 45%
    );
}

.video-meta{
  position:absolute;
  left:34px;
  bottom:30px;
  z-index:3;
}

.video-title{
  font-size:2rem;
  font-weight:700;
  letter-spacing:-1px;
}

.video-desc{
  margin-top:10px;
  color:var(--text-secondary);
  max-width:580px;
  line-height:1.7;
}

/* =========================================================
   SIDEBAR
========================================================= */

.sidebar{
  width:360px;
  display:flex;
  flex-direction:column;
  gap:20px;
}

.panel{
  background:
    rgba(255,255,255,.03);

  border:
    1px solid rgba(255,255,255,.06);

  border-radius:24px;

  padding:24px;

  backdrop-filter:blur(20px);
}

.panel-title{
  font-size:.85rem;
  letter-spacing:3px;
  text-transform:uppercase;
  color:var(--text-secondary);
  margin-bottom:18px;
}

.stat-grid{
  display:grid;
  grid-template-columns:1fr 1fr;
  gap:16px;
}

.stat-card{
  background:
    rgba(255,255,255,.03);

  border:
    1px solid rgba(255,255,255,.05);

  border-radius:18px;

  padding:18px;
}

.stat-value{
  font-size:1.4rem;
  font-weight:700;
}

.stat-label{
  margin-top:6px;
  color:var(--text-muted);
  font-size:.8rem;
}

.timeline{
  display:flex;
  flex-direction:column;
  gap:16px;
}

.timeline-item{
  display:flex;
  gap:14px;
}

.timeline-dot{
  width:10px;
  height:10px;
  margin-top:7px;
  border-radius:50%;
  background:
    linear-gradient(
      135deg,
      var(--accent-a),
      var(--accent-b)
    );
}

.timeline-content h4{
  font-size:.95rem;
}

.timeline-content p{
  margin-top:5px;
  color:var(--text-secondary);
  line-height:1.6;
  font-size:.88rem;
}

/* =========================================================
   STATES
========================================================= */

body.phase-intro #landing-screen{
  opacity:0;
  transform:scale(1.05);
  pointer-events:none;
}

body.phase-intro #intro-screen{
  opacity:1;
  pointer-events:auto;
}

body.phase-dashboard #intro-screen{
  opacity:0;
  transform:scale(.96);
  pointer-events:none;
}

body.phase-dashboard #video-dashboard{
  opacity:1;
  pointer-events:auto;
}

/* =========================================================
   LOADER
========================================================= */

.loader{
  position:absolute;
  inset:0;
  display:flex;
  align-items:center;
  justify-content:center;
  z-index:100;
  background:#000;
  transition:opacity 1s ease;
}

.loader.hidden{
  opacity:0;
  pointer-events:none;
}

.loader-ring{
  width:90px;
  height:90px;
  border-radius:50%;

  border:
    2px solid rgba(255,255,255,.08);

  border-top:
    2px solid var(--accent-a);

  animation:spin 1s linear infinite;
}

@keyframes spin{
  to{
    transform:rotate(360deg);
  }
}

/* =========================================================
   RESPONSIVE
========================================================= */

@media(max-width:1100px){

  .dashboard-content{
    flex-direction:column;
  }

  .sidebar{
    width:100%;
    flex-direction:row;
  }

  .panel{
    flex:1;
  }

}

@media(max-width:768px){

  .topbar{
    padding:0 20px;
  }

  .dashboard-content{
    padding:16px;
  }

  .sidebar{
    flex-direction:column;
  }

  .landing-title{
    letter-spacing:-2px;
  }

  .video-title{
    font-size:1.4rem;
  }

}

/* =========================================================
   REDUCED MOTION
========================================================= */

@media(prefers-reduced-motion:reduce){

  *,
  *::before,
  *::after{
    animation:none !important;
    transition:none !important;
  }

}
</style>
</head>

<body>

<!-- ======================================================
     BACKGROUND
====================================================== -->

<div id="bg-layer"></div>

<!-- ======================================================
     LOADER
====================================================== -->

<div class="loader" id="loader">
  <div class="loader-ring"></div>
</div>

<!-- ======================================================
     LANDING SCREEN
====================================================== -->

<section
  id="landing-screen"
  class="screen"
>

  <div class="landing-badge">
    PREMIUM CINEMATIC EXPERIENCE
  </div>

  <h1 class="landing-title">
    Experience<br>
    Motion In<br>
    <span class="gradient-text">
      Pure Form
    </span>
  </h1>

  <p class="landing-subtitle">
    A cinematic showcase interface crafted
    with immersive motion, refined lighting,
    and premium visual architecture designed
    for high-end media presentation.
  </p>

  <button
    class="enter-btn"
    id="enterBtn"
  >
    ENTER EXPERIENCE
  </button>

</section>

<!-- ======================================================
     INTRO SCREEN
====================================================== -->

<section
  id="intro-screen"
  class="screen"
>

  <div class="intro-logo">
    V
  </div>

  <h2 class="intro-title">
    VISUAL DESIGN SYSTEM
  </h2>

  <div class="intro-line"></div>

  <div class="intro-tag">
    cinematic showcase engine
  </div>

</section>

<!-- ======================================================
     DASHBOARD
====================================================== -->

<main id="video-dashboard">

  <div class="dashboard-shell">

    <!-- TOPBAR -->

    <header class="topbar">

      <div class="brand">
        <div class="brand-dot"></div>

        <div class="brand-name">
          VISUALFRAME
        </div>
      </div>

      <div class="top-actions">

        <button
          class="glass-btn"
          id="playToggle"
        >
          ▶
        </button>

        <button
          class="glass-btn"
          id="muteToggle"
        >
          🔊
        </button>

      </div>

    </header>

    <!-- CONTENT -->

    <div class="dashboard-content">

      <!-- VIDEO -->

      <section class="video-panel">

        <!--
          REPLACE THE VIDEO SOURCE BELOW
          WITH YOUR OWN VIDEO FILE
        -->

        <video
          id="heroVideo"
          autoplay
          muted
          playsinline
          preload="auto"
          loop
        >
          <source
            src="https://files.catbox.moe/wp2eq7.mp4"
            type="video/mp4"
          />
        </video>

        <div class="video-overlay"></div>

        <div class="video-meta">

          <h2 class="video-title">
            Cinematic Motion Reel
          </h2>

          <p class="video-desc">
            Premium motion design presentation
            built with a fully self-contained
            visual architecture utilizing
            immersive transitions, cinematic
            glow systems, and fluid media
            orchestration.
          </p>

        </div>

      </section>

      <!-- SIDEBAR -->

      <aside class="sidebar">

        <!-- PANEL 1 -->

        <div class="panel">

          <div class="panel-title">
            Showcase Metrics
          </div>

          <div class="stat-grid">

            <div class="stat-card">
              <div class="stat-value">
                4K
              </div>

              <div class="stat-label">
                Ultra Quality
              </div>
            </div>

            <div class="stat-card">
              <div class="stat-value">
                60FPS
              </div>

              <div class="stat-label">
                Smooth Motion
              </div>
            </div>

            <div class="stat-card">
              <div class="stat-value">
                HDR
              </div>

              <div class="stat-label">
                Dynamic Range
              </div>
            </div>

            <div class="stat-card">
              <div class="stat-value">
                LIVE
              </div>

              <div class="stat-label">
                Rendering
              </div>
            </div>

          </div>

        </div>

        <!-- PANEL 2 -->

        <div class="panel">

          <div class="panel-title">
            Experience Flow
          </div>

          <div class="timeline">

            <div class="timeline-item">

              <div class="timeline-dot"></div>

              <div class="timeline-content">
                <h4>
                  Landing Experience
                </h4>

                <p>
                  Minimal cinematic entry
                  interface with immersive
                  motion pacing.
                </p>
              </div>

            </div>

            <div class="timeline-item">

              <div class="timeline-dot"></div>

              <div class="timeline-content">
                <h4>
                  Designer Splash
                </h4>

                <p>
                  Branded motion reveal with
                  atmospheric visual layering.
                </p>
              </div>

            </div>

            <div class="timeline-item">

              <div class="timeline-dot"></div>

              <div class="timeline-content">
                <h4>
                  Media Dashboard
                </h4>

                <p>
                  High-fidelity playback
                  environment with modern
                  glass interface systems.
                </p>
              </div>

            </div>

          </div>

        </div>

      </aside>

    </div>

  </div>

</main>

<!-- ======================================================
     SCRIPT
====================================================== -->

<script>

/* =========================================================
   APP STATE
========================================================= */

const APP_STATE = {
  phase: "landing",
  introPlayed: false,
  playing: true,
  muted: true
};

/* =========================================================
   ELEMENTS
========================================================= */

const body = document.body;

const loader = document.getElementById("loader");

const enterBtn =
  document.getElementById("enterBtn");

const heroVideo =
  document.getElementById("heroVideo");

const playToggle =
  document.getElementById("playToggle");

const muteToggle =
  document.getElementById("muteToggle");

/* =========================================================
   LOADER
========================================================= */

window.addEventListener("load", () => {

  setTimeout(() => {
    loader.classList.add("hidden");
  }, 1200);

});

/* =========================================================
   TRANSITION ENGINE
========================================================= */

function transitionTo(phase){

  APP_STATE.phase = phase;

  body.classList.remove(
    "phase-intro",
    "phase-dashboard"
  );

  if(phase === "intro"){
    body.classList.add("phase-intro");
  }

  if(phase === "dashboard"){
    body.classList.add("phase-dashboard");
  }

}

/* =========================================================
   EXPERIENCE FLOW
========================================================= */

enterBtn.addEventListener("click", async () => {

  transitionTo("intro");

  try{
    await heroVideo.play();
  }catch(err){
    console.log(
      "Autoplay blocked:",
      err
    );
  }

  setTimeout(() => {

    transitionTo("dashboard");

  }, 4200);

});

/* =========================================================
   VIDEO CONTROLS
========================================================= */

playToggle.addEventListener("click", () => {

  if(heroVideo.paused){

    heroVideo.play();

    APP_STATE.playing = true;

    playToggle.innerHTML = "❚❚";

  }else{

    heroVideo.pause();

    APP_STATE.playing = false;

    playToggle.innerHTML = "▶";

  }

});

muteToggle.addEventListener("click", () => {

  heroVideo.muted = !heroVideo.muted;

  APP_STATE.muted = heroVideo.muted;

  muteToggle.innerHTML =
    heroVideo.muted ? "🔇" : "🔊";

});

/* =========================================================
   KEYBOARD SHORTCUTS
========================================================= */

window.addEventListener("keydown", (e) => {

  if(e.code === "Space"){

    e.preventDefault();

    playToggle.click();

  }

  if(e.key.toLowerCase() === "m"){

    muteToggle.click();

  }

});

/* =========================================================
   SAFETY AUTOPLAY
========================================================= */

heroVideo.addEventListener(
  "canplay",
  async () => {

    try{
      await heroVideo.play();
    }catch(e){
      console.log("Playback waiting.");
    }

  }
);

</script>

</body>
</html>
