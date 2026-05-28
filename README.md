<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Premium Video Experience</title>

<style>
:root{
    --primary-glow: linear-gradient(135deg,#ff0055,#7a00ff);
    --bg-color:#0a0a0c;
}

*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

body,html{
    width:100%;
    height:100%;
    overflow:hidden;
    background:var(--bg-color);
    font-family:'Segoe UI',sans-serif;
    color:#fff;
}

body{
    display:flex;
    justify-content:center;
    align-items:center;
}

/* Landing */
.landing-container{
    text-align:center;
    z-index:10;
    transition:0.8s;
}

.action-btn{
    position:relative;
    padding:18px 40px;
    font-size:18px;
    font-weight:700;
    border:none;
    border-radius:50px;
    background:#111;
    color:#fff;
    cursor:pointer;
    overflow:hidden;
    letter-spacing:2px;
    text-transform:uppercase;
    transition:0.3s;
}

.action-btn::before{
    content:'';
    position:absolute;
    inset:-2px;
    background:var(--primary-glow);
    z-index:-1;
    border-radius:50px;
}

.action-btn:hover{
    transform:scale(1.05);
    box-shadow:0 0 30px rgba(255,0,85,0.5);
}

/* Splash */
.splash-screen{
    position:fixed;
    inset:0;
    background:#000;
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    opacity:0;
    pointer-events:none;
    transition:0.6s;
}

.splash-screen.active{
    opacity:1;
    pointer-events:auto;
}

.designer-title{
    letter-spacing:6px;
    color:#777;
    margin-bottom:10px;
    animation:fadeUp 1s forwards;
}

.designer-name{
    font-size:42px;
    font-weight:800;
    background:var(--primary-glow);
    -webkit-background-clip:text;
    -webkit-text-fill-color:transparent;
    animation:fadeUp 1.3s forwards;
}

.loader{
    margin-top:30px;
    width:220px;
    height:4px;
    background:#222;
    border-radius:10px;
    overflow:hidden;
}

.loader::after{
    content:'';
    display:block;
    width:0%;
    height:100%;
    background:var(--primary-glow);
    animation:loadProgress 2s linear forwards;
}

@keyframes loadProgress{
    to{
        width:100%;
    }
}

@keyframes fadeUp{
    from{
        opacity:0;
        transform:translateY(20px);
    }
    to{
        opacity:1;
        transform:translateY(0);
    }
}

/* Video Area */
.video-wrapper{
    position:fixed;
    inset:0;
    display:flex;
    flex-direction:column;
    justify-content:center;
    align-items:center;
    opacity:0;
    pointer-events:none;
    transform:scale(0.95);
    transition:0.8s;
    padding:20px;
}

.video-wrapper.show{
    opacity:1;
    pointer-events:auto;
    transform:scale(1);
}

.video-container{
    width:100%;
    max-width:900px;
    aspect-ratio:16/9;
    border-radius:20px;
    overflow:hidden;
    background:#000;
    box-shadow:
    0 20px 60px rgba(0,0,0,0.8),
    0 0 50px rgba(122,0,255,0.2);
}

video{
    width:100%;
    height:100%;
    object-fit:contain;
    background:#000;
}

/* Typewriter Description */
.description-box{
    margin-top:25px;
    max-width:800px;
    max-height:180px;
    overflow-y:auto;
    text-align:left;
    font-size:17px;
    line-height:1.8;
    color:#ddd;
    padding:20px;
    background:rgba(255,255,255,0.04);
    border-radius:15px;
    border:1px solid rgba(255,255,255,0.08);
}

.cursor{
    display:inline-block;
    width:2px;
    background:#fff;
    animation:blink 0.7s infinite;
}

@keyframes blink{
    50%{
        opacity:0;
    }
}

.brand-footer{
    margin-top:20px;
    color:#666;
    letter-spacing:2px;
    font-size:13px;
    text-transform:uppercase;
}

.brand-footer span{
    color:#fff;
    font-weight:600;
}
</style>
</head>

<body>

<div class="landing-container" id="landingSection">
    <button class="action-btn" onclick="startExperience()">
        View Video Now
    </button>
</div>

<div class="splash-screen" id="splashScreen">
    <div class="designer-title">Presented By</div>
    <div class="designer-name" id="designerNameTag"></div>
    <div class="loader"></div>
</div>

<div class="video-wrapper" id="videoSection">

    <div class="video-container">

        <video
            id="mainPlayer"
            controls
            muted
            playsinline
            preload="auto"
        >
            <source id="videoSource" type="video/mp4">
        </video>

    </div>

    <div class="description-box">
        <span id="typewriter"></span>
        <span class="cursor"></span>
    </div>

    <div class="brand-footer">
        Designed & Developed by:
        <span id="footerNameTag"></span>
    </div>

</div>

<script>

// CONFIG
const CONFIG = {

    videoUrl:
    "https://files.catbox.moe/wp2eq7.mp4",

    designerName:
    "OM KUMAR DUBEY",

    videoDescription: `
A soil suspension contains a wide variety of microorganisms that play important roles in soil fertility and nutrient cycling.

1. Bacteria – The most abundant microorganisms in soil. They help in decomposition of organic matter, nitrogen fixation, and nutrient recycling.

2. Fungi – These microorganisms break down complex organic substances like cellulose and lignin.

3. Actinomycetes – Filamentous bacteria that decompose resistant organic materials.

4. Algae – Photosynthetic microorganisms found mainly in moist soils.

5. Protozoa – Microscopic single-celled organisms that feed on bacteria.

These microorganisms together improve soil structure, fertility, and plant growth.
`
};


// SET NAME
document.getElementById("designerNameTag").innerText =
CONFIG.designerName;

document.getElementById("footerNameTag").innerText =
CONFIG.designerName;


// TYPEWRITER EFFECT
function typeWriter(text, elementId, speed = 20){

    let i = 0;

    const element =
    document.getElementById(elementId);

    element.innerHTML = '';

    function typing(){

        if(i < text.length){

            if(text.charAt(i) === '\n'){
                element.innerHTML += '<br>';
            } else {
                element.innerHTML += text.charAt(i);
            }

            i++;

            setTimeout(typing, speed);
        }
    }

    typing();
}


// START EXPERIENCE
function startExperience(){

    const landing =
    document.getElementById('landingSection');

    const splash =
    document.getElementById('splashScreen');

    const videoSection =
    document.getElementById('videoSection');

    const player =
    document.getElementById('mainPlayer');

    const source =
    document.getElementById('videoSource');

    landing.style.opacity = '0';

    setTimeout(()=>{

        landing.style.display='none';

        splash.classList.add('active');

    },400);


    setTimeout(()=>{

        source.src = CONFIG.videoUrl;

        player.load();

        splash.classList.remove('active');

        videoSection.classList.add('show');

        player.play()
        .then(()=>{

            typeWriter(
                CONFIG.videoDescription,
                'typewriter'
            );

        })
        .catch((err)=>{

            console.log("Autoplay blocked:", err);

        });

    },3000);


    // VIDEO ERROR HANDLER
    player.addEventListener('error', () => {

        alert(
            "Video failed to load. Check MP4 link or server permissions."
        );

    });

}

</script>

</body>
</html>
