<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>EXPERIMENT</title>
    <style>
        :root {
            --primary-glow: linear-gradient(135deg, #ff0055, #7a00ff);
            --bg-color: #0a0a0c;
        }

        body, html {
            margin: 0;
            padding: 0;
            width: 100%;
            height: 100%;
            font-family: 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--bg-color);
            color: #ffffff;
            overflow: hidden;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        /* Initial Landing State */
        .landing-container {
            text-align: center;
            z-index: 10;
            transition: opacity 0.8s ease;
        }

        /* Stylish Animated Action Button */
        .action-btn {
            position: relative;
            padding: 18px 40px;
            font-size: 18px;
            font-weight: 700;
            color: #fff;
            text-transform: uppercase;
            letter-spacing: 2px;
            background: #111;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            overflow: hidden;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            box-shadow: 0 0 20px rgba(122, 0, 255, 0.2);
        }

        .action-btn::before {
            content: '';
            position: absolute;
            top: -2px; left: -2px; right: -2px; bottom: -2px;
            background: var(--primary-glow);
            z-index: -1;
            border-radius: 50px;
            transition: opacity 0.3s ease;
        }

        .action-btn:hover {
            transform: scale(1.05);
            box-shadow: 0 0 35px rgba(255, 0, 85, 0.6);
        }

        /* Splash Screen Overlay */
        .splash-screen {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: #000;
            z-index: 100;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.6s ease-in-out;
        }

        .splash-screen.active {
            opacity: 1;
            pointer-events: auto;
        }

        /* Splash Animations */
        .designer-title {
            font-size: 14px;
            text-transform: uppercase;
            letter-spacing: 6px;
            color: #888;
            margin-bottom: 10px;
            transform: translateY(20px);
            opacity: 0;
        }

        .designer-name {
            font-size: 42px;
            font-weight: 800;
            letter-spacing: 4px;
            background: var(--primary-glow);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            transform: translateY(20px);
            opacity: 0;
        }

        .active .designer-title {
            animation: fadeInUp 0.8s forwards 0.2s;
        }

        .active .designer-name {
            animation: fadeInUp 0.8s forwards 0.5s;
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        /* Glowing Loader Inside Splash */
        .loader {
            margin-top: 30px;
            width: 50px;
            height: 3px;
            background: #222;
            border-radius: 3px;
            overflow: hidden;
            position: relative;
        }

        .loader::after {
            content: '';
            position: absolute;
            left: 0; top: 0;
            height: 100%; width: 0;
            background: var(--primary-glow);
            animation: loadProgress 2s linear forwards 0.8s;
        }

        @keyframes loadProgress {
            to { width: 100%; }
        }

        /* Video Showcase Dashboard */
        .video-wrapper {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            opacity: 0;
            pointer-events: none;
            transform: scale(0.95);
            transition: opacity 0.8s ease, transform 0.8s ease;
            padding: 20px;
            box-sizing: border-box;
        }

        .video-wrapper.show {
            opacity: 1;
            pointer-events: auto;
            transform: scale(1);
        }

        .iframe-container {
            max-width: 850px;
            width: 100%;
            aspect-ratio: 16/9;
            background: #000;
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 20px 50px rgba(0,0,0,0.8), 0 0 40px rgba(122, 0, 255, 0.15);
            border: 1px solid #222;
        }

        .iframe-container iframe {
            width: 100%;
            height: 100%;
            border: none;
        }

        /* Downside Brand Tag */
        .brand-footer {
            margin-top: 30px;
            font-size: 14px;
            color: #555;
            letter-spacing: 2px;
            text-transform: uppercase;
        }

        .brand-footer span {
            color: #fff;
            font-weight: 600;
        }
    </style>
</head>
<body>

    <div class="landing-container" id="landingSection">
        <button class="action-btn" onclick="startExperience()">View Video Now</button>
    </div>

    <div class="splash-screen" id="splashScreen">
        <div class="designer-title">Presented By</div>
        <div class="designer-name" id="designerNameTag">DESIGNER NAME</div>
        <div class="loader"></div>
    </div>

    <div class="video-wrapper" id="videoSection">
        <div class="iframe-container">
            <iframe id="mainPlayer" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </div>
        <div class="brand-footer">
            Designed & Developed by: <span id="footerNameTag">DESIGNER NAME</span>
        </div>
    </div>

<script>
    // =========================================================================
    // CONFIGURATION: PASTE YOUR DATA HERE
    // =========================================================================
    const CONFIG = {
        youtubeUrl: "https://files.catbox.moe/wp2eq7.mp4", // <-- Paste your YouTube link here
        designerName: "OM K.DUBEY" // <-- Type your name here
    };
    // =========================================================================

    // Inject configuration data into presentation layers
    document.getElementById('designerNameTag').innerText = CONFIG.designerName;
    document.getElementById('footerNameTag').innerText = CONFIG.designerName;

    function extractVideoId(url) {
        const regExp = /^.*(youtu.be\/|v\/|u\/\w\/|embed\/|watch\?v=|\&v=|shorts\/)([^#\&\?]*).*/;
        const match = url.match(regExp);
        return (match && match[2].length === 11) ? match[2] : null;
    }

    function startExperience() {
        const landing = document.getElementById('landingSection');
        const splash = document.getElementById('splashScreen');
        const videoSection = document.getElementById('videoSection');
        const player = document.getElementById('mainPlayer');

        const videoId = extractVideoId(CONFIG.youtubeUrl);

        if (!videoId) {
            alert("Error: The hardcoded YouTube link in the configuration script is invalid.");
            return;
        }

        // Hide landing button frame
        landing.style.opacity = '0';
        
        setTimeout(() => {
            landing.style.display = 'none';
            // Trigger stylized splash screen sequence
            splash.classList.add('active');
        }, 400);

        // Hold splash duration, prep embed stream, then fade smoothly into the player viewport
        setTimeout(() => {
            // Using privacy-enhanced domain to minimize local file origin blocking policies
            player.src = `https://www.youtube-nocookie.com/embed/${videoId}?autoplay=1&rel=0`;
            
            splash.classList.remove('active');
            videoSection.classList.add('show');
        }, 3200); // 3.2 seconds total splash layout duration
    }
</script>

</body>
</html>
