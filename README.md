<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tip Tracker.AI</title> <!-- Custom title for GitHub Pages -->
    <style>
        body {
            margin: 0;
            padding: 0;
            background: #000;
            overflow: hidden;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Orbitron', sans-serif;
        }

        .text {
            color: #fff;
            font-size: clamp(2rem, 10vw, 10rem);
            font-weight: 900;
            text-transform: uppercase;
            letter-spacing: clamp(2px, 1vw, 8px);
            opacity: 0;
            position: absolute;
            text-align: center;
            width: 100%;
            padding: 0 10px;
            box-sizing: border-box;
            font-family: 'Montserrat', sans-serif;
        }

        .logo-container {
            opacity: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            position: absolute;
        }

        .logo-text {
            font-size: clamp(2rem, 6vw, 4rem);
            font-weight: 700;
            letter-spacing: 2px;
            color: #fff;
            position: relative;
            text-transform: lowercase;
            animation: shimmerText 2s infinite ease-in-out;
        }

        .ai-part {
            position: relative;
            display: inline-block;
        }

        .star-dot {
            position: absolute;
            top: -2mm; /* ~7.5px above "AI" */
            left: 85%; /* Moved further right over "AI" */
            transform: translateX(-50%);
            width: clamp(20px, 3vw, 40px);
            height: clamp(20px, 3vw, 40px);
            background: #fff;
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            animation: flicker 0.5s infinite ease-in-out;
        }

        @keyframes flicker {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.7; transform: scale(1.2); }
        }

        @keyframes explodeStar {
            0% { transform: scale(1) translateX(-50%); box-shadow: 0 0 15px #fff; opacity: 1; }
            100% { transform: scale(10) translateX(-50%); box-shadow: 0 0 2000px #fff; opacity: 0; }
        }

        @keyframes fadeIn {
            0% { opacity: 0; transform: translateY(20px); }
            100% { opacity: 1; transform: translateY(0); }
        }

        @keyframes fadeOut {
            0% { opacity: 1; }
            100% { opacity: 0; }
        }

        @keyframes shimmerText {
            0% { text-shadow: 0 0 10px #ff00ff; }
            50% { text-shadow: 0 0 20px #00ffff; }
            100% { text-shadow: 0 0 10px #ff00ff; }
        }

        @keyframes screenFade {
            0% { background: #000; }
            10% { background: #fff; } /* Quick white peak */
            40% { background: #d0d0d0; } /* Lighter gray for subtle fade */
            70% { background: #404040; } /* Darker gray */
            100% { background: #000; } /* Smooth back to black */
        }
    </style>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@900&family=Orbitron:wght@700&display=swap" rel="stylesheet">
</head>
<body>
    <div class="text" id="introText">No Tax on Tips</div>
    <div class="logo-container" id="logoContainer">
        <div class="logo-text">
            tiptracker.<span class="ai-part">ai</span>
            <div class="star-dot" id="starDot"></div>
        </div>
    </div>

    <script>
        const introText = document.getElementById('introText');
        const logoContainer = document.getElementById('logoContainer');
        const starDot = document.getElementById('starDot');
        const body = document.body;

        function runSequence() {
            // Reset everything
            introText.style.animation = 'none';
            introText.style.opacity = '0';
            introText.style.display = 'block';
            logoContainer.style.animation = 'none';
            logoContainer.style.opacity = '0';
            starDot.style.animation = 'flicker 0.5s infinite ease-in-out';
            body.style.animation = 'none';
            body.style.background = '#000';

            // Black screen for 1s
            setTimeout(() => {
                introText.style.animation = 'fadeIn 0.5s ease-out forwards';
            }, 1000);

            // Intro text stays for 3.5s, then fades out
            setTimeout(() => {
                introText.style.animation = 'fadeOut 0.5s ease-in forwards';
                setTimeout(() => {
                    introText.style.display = 'none';
                    logoContainer.style.animation = 'fadeIn 0.5s ease-out forwards';
                }, 500);
            }, 4600); // 1s black + 3.5s + 0.1s = 4.6s

            // Star explodes (0.1s), logo fades out early, then screen fades
            setTimeout(() => {
                logoContainer.style.animation = 'fadeOut 0.05s ease-in forwards'; // Fades out in 0.05s
                starDot.style.animation = 'explodeStar 0.1s ease-in forwards';
                setTimeout(() => {
                    body.style.animation = 'screenFade 1s ease-in forwards';
                }, 100); // Fade after explosion
            }, 8100); // Logo stays 3s, explode at 8.1s

            // Restart sequence
            setTimeout(runSequence, 9100); // Total: 9.1s
        }

        // Start the loop
        runSequence();
    </script>
</body>
</html>
