<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pesan Rahasia Untukmu 💖</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@400;600;800&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Nunito', sans-serif;
            margin: 0;
            overflow: hidden; /* Mencegah scroll saat ada animasi */
            background: linear-gradient(135deg, #fce4ec 0%, #f3e5f5 50%, #f8bbd0 100%);
            height: 100vh;
        }

        /* Floating Background Hearts */
        .bg-hearts {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        .bg-heart {
            position: absolute;
            font-size: 24px;
            color: rgba(255, 105, 180, 0.4);
            animation: floatUp 10s linear infinite;
            bottom: -50px;
        }
        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-120vh) rotate(360deg); opacity: 0; }
        }

        /* Main Container Content */
        .content-wrapper {
            position: relative;
            z-index: 10;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100%;
            padding: 20px;
        }

        /* Glassmorphism Card */
        .glass-card {
            background: rgba(255, 255, 255, 0.6);
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border: 2px solid rgba(255, 255, 255, 0.8);
            box-shadow: 0 8px 32px 0 rgba(255, 105, 180, 0.2);
            border-radius: 2rem;
            padding: 2rem;
            max-width: 400px;
            width: 100%;
            text-align: center;
            transition: all 0.3s ease;
        }

        /* Cute CSS Bear */
        .bear-container {
            margin: 0 auto 20px auto;
            animation: bounce 3s ease-in-out infinite;
        }
        .bear {
            width: 120px;
            height: 120px;
            background: #d4a373;
            border-radius: 50%;
            position: relative;
            margin: 0 auto;
            box-shadow: inset -10px -10px 20px rgba(0,0,0,0.1), 0 10px 20px rgba(212, 163, 115, 0.3);
        }
        .bear::before, .bear::after {
            content: ''; position: absolute;
            width: 45px; height: 45px;
            background: #d4a373;
            border-radius: 50%; top: -5px; z-index: -1;
            box-shadow: inset -5px -5px 10px rgba(0,0,0,0.1);
        }
        .bear::before { left: -10px; }
        .bear::after { right: -10px; }
        
        .bear-snout {
            position: absolute;
            width: 55px; height: 40px;
            background: #faedcd;
            border-radius: 50%;
            bottom: 20px; left: 32.5px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.05);
        }
        .bear-nose {
            position: absolute;
            width: 16px; height: 10px;
            background: #5c4033;
            border-radius: 50%;
            top: 5px; left: 19.5px;
        }
        .bear-eye {
            position: absolute;
            width: 12px; height: 12px;
            background: #5c4033;
            border-radius: 50%;
            top: 45px;
            animation: blink 4s infinite;
        }
        .bear-eye.left { left: 35px; }
        .bear-eye.right { right: 35px; }
        .bear-blush {
            position: absolute;
            width: 20px; height: 12px;
            background: #ffb5a7;
            border-radius: 50%;
            top: 60px;
            filter: blur(2px);
            opacity: 0.8;
        }
        .bear-blush.left { left: 15px; }
        .bear-blush.right { right: 15px; }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        @keyframes blink {
            0%, 96%, 98%, 100% { transform: scaleY(1); }
            97%, 99% { transform: scaleY(0.1); }
        }

        /* Text Animations */
        .message-text {
            font-size: 1.25rem;
            color: #704264;
            font-weight: 700;
            min-height: 80px;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: opacity 0.5s ease, transform 0.5s ease;
            opacity: 1;
            transform: scale(1);
        }
        .message-text.fade-out {
            opacity: 0;
            transform: scale(0.95);
        }

        /* Bubbly Button */
        .btn-bubbly {
            background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 99%, #fecfef 100%);
            color: #b73a62;
            font-weight: 800;
            padding: 12px 24px;
            border-radius: 50px;
            border: none;
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.4);
            cursor: pointer;
            transition: all 0.2s ease;
            position: relative;
            overflow: hidden;
            animation: pulseBtn 2s infinite;
            display: inline-block;
            margin-top: 15px;
        }
        .btn-bubbly:active {
            transform: scale(0.95);
        }
        @keyframes pulseBtn {
            0% { box-shadow: 0 0 0 0 rgba(255, 154, 158, 0.7); }
            70% { box-shadow: 0 0 0 15px rgba(255, 154, 158, 0); }
            100% { box-shadow: 0 0 0 0 rgba(255, 154, 158, 0); }
        }

        /* Canvas for Confetti */
        #confetti-canvas {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 100;
        }
    </style>
</head>
<body>

    <!-- Background Floating Hearts -->
    <div class="bg-hearts" id="bg-hearts"></div>

    <!-- Explosion Canvas -->
    <canvas id="confetti-canvas"></canvas>

    <div class="content-wrapper">
        <div class="glass-card">
            
            <!-- CSS Character (Cute Bear) -->
            <div class="bear-container">
                <div class="bear">
                    <div class="bear-eye left"></div>
                    <div class="bear-eye right"></div>
                    <div class="bear-blush left"></div>
                    <div class="bear-blush right"></div>
                    <div class="bear-snout">
                        <div class="bear-nose"></div>
                    </div>
                </div>
            </div>

            <!-- Message Area -->
            <div id="message-container" class="message-text">
                <!-- Text will be injected here -->
            </div>

            <!-- Action Button -->
            <button id="action-btn" class="btn-bubbly">
                Ada pesan rahasia nih...
            </button>

        </div>
    </div>

    <script>
        // --- 1. Background Floating Hearts Generator ---
        const bgHeartsContainer = document.getElementById('bg-hearts');
        const heartEmojis = ['💖', '💕', '🌸', '✨', '🤍'];
        
        for(let i = 0; i < 20; i++) {
            let heart = document.createElement('div');
            heart.classList.add('bg-heart');
            heart.innerText = heartEmojis[Math.floor(Math.random() * heartEmojis.length)];
            heart.style.left = Math.random() * 100 + 'vw';
            heart.style.animationDuration = (Math.random() * 10 + 8) + 's';
            heart.style.animationDelay = (Math.random() * 10) + 's';
            heart.style.fontSize = (Math.random() * 20 + 15) + 'px';
            bgHeartsContainer.appendChild(heart);
        }

        // --- 2. Story / Messages Logic ---
        const messages = [
            'Halo kesayangannya Fajri yang lagi sibuk kerja! 👩‍💻',
            'Semangat terus ya, Bu Planner kebanggaan Sikur, Lombok! 🏙️✨',
            'Jangan lupa minum air putih dan senyum hari ini.',
            'Walaupun kita lagi LDR...',
            'Aku cuma mau bilang...',
            'I miss you so much and I am so proud of you! ❤️'
        ];

        let currentIndex = -1; // Starts at -1 so the first click shows the first message
        const messageContainer = document.getElementById('message-container');
        const actionBtn = document.getElementById('action-btn');

        // Initial empty state text guide
        messageContainer.innerHTML = "<em>(Klik tombol di bawah)</em>";

        actionBtn.addEventListener('click', () => {
            // If it's the first click, change button text
            if(currentIndex === -1) {
                actionBtn.innerText = "Lanjut 💕";
                actionBtn.style.animation = "none"; // stop initial pulse to be less distracting
            }

            currentIndex++;

            // Fade out current text
            messageContainer.classList.add('fade-out');

            setTimeout(() => {
                if (currentIndex < messages.length) {
                    messageContainer.innerHTML = messages[currentIndex];
                    messageContainer.classList.remove('fade-out');
                }

                // If it's the last message
                if (currentIndex === messages.length - 1) {
                    actionBtn.style.display = 'none'; // Hide button
                    triggerExplosion(); // TRIGGER BOOM
                }
            }, 500); // Wait for fade out transition (0.5s)
        });

        // --- 3. Canvas Confetti/Heart Explosion Logic ---
        const canvas = document.getElementById('confetti-canvas');
        const ctx = canvas.getContext('2d');
        let particles = [];
        let w, h;

        function resizeCanvas() {
            w = canvas.width = window.innerWidth;
            h = canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        function triggerExplosion() {
            const explosionEmojis = ['❤️', '💖', '💘', '✨', '🥰', '🌸'];
            const particleCount = 150; // Massive explosion
            
            // Start from center of the screen
            const startX = w / 2;
            const startY = h / 2;

            for (let i = 0; i < particleCount; i++) {
                particles.push({
                    x: startX,
                    y: startY,
                    emoji: explosionEmojis[Math.floor(Math.random() * explosionEmojis.length)],
                    size: Math.random() * 25 + 15,
                    speedX: (Math.random() - 0.5) * 20, // Spread wide
                    speedY: (Math.random() - 0.5) * 20 - 5, // Slight upward bias
                    gravity: 0.2, // Fall down
                    rotation: Math.random() * 360,
                    rotationSpeed: (Math.random() - 0.5) * 10,
                    opacity: 1
                });
            }

            animateExplosion();
        }

        function animateExplosion() {
            ctx.clearRect(0, 0, w, h);
            
            let aliveParticles = false;

            for (let i = 0; i < particles.length; i++) {
                let p = particles[i];
                if (p.opacity <= 0) continue;

                aliveParticles = true;

                // Physics update
                p.x += p.speedX;
                p.y += p.speedY;
                p.speedY += p.gravity; // Apply gravity
                p.rotation += p.rotationSpeed;
                
                // Fade out near the bottom or over time
                if (p.y > h - 100) {
                    p.opacity -= 0.02;
                } else if (Math.abs(p.speedX) < 1 && p.speedY > 5) {
                    p.opacity -= 0.01;
                }

                // Draw
                ctx.save();
                ctx.translate(p.x, p.y);
                ctx.rotate(p.rotation * Math.PI / 180);
                ctx.globalAlpha = Math.max(0, p.opacity);
                ctx.font = p.size + 'px Arial';
                ctx.textAlign = 'center';
                ctx.textBaseline = 'middle';
                ctx.fillText(p.emoji, 0, 0);
                ctx.restore();
            }

            if (aliveParticles) {
                requestAnimationFrame(animateExplosion);
            }
        }
    </script>
</body>
</html>
