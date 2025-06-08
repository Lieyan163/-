<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>昀泷RainD - 个人主页</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: url('https://i.postimg.cc/GpTxfYmZ/Image-1748766443466.png');
            background-size: cover;
            background-attachment: fixed;
            background-position: center;
            min-height: 100vh;
            overflow-x: hidden;
            cursor: none;
        }

        /* 自定义光标 */
        .cursor {
            position: fixed;
            width: 20px;
            height: 20px;
            background: radial-gradient(circle, rgba(255,255,255,0.8) 0%, rgba(255,255,255,0.2) 70%, transparent 100%);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9999;
            mix-blend-mode: difference;
            transition: transform 0.1s ease;
        }

        .cursor-trail {
            position: fixed;
            width: 6px;
            height: 6px;
            background: rgba(255,255,255,0.4);
            border-radius: 50%;
            pointer-events: none;
            z-index: 9998;
        }

        /* 页面扭曲效果 */
        .distortion-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 1;
            mix-blend-mode: screen;
            opacity: 0.3;
        }

        .container {
            position: relative;
            z-index: 2;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* 标题区域 */
        .header {
            text-align: center;
            padding: 4rem 2rem 2rem;
            position: relative;
        }

        .title {
            font-size: 4rem;
            font-weight: bold;
            color: white;
            text-shadow: 0 0 20px rgba(255,255,255,0.3);
            margin-bottom: 1rem;
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4, #45b7d1, #96ceb4);
            background-size: 400% 400%;
            -webkit-background-clip: text;
            background-clip: text;
            -webkit-text-fill-color: transparent;
            animation: gradientShift 4s ease-in-out infinite;
        }

        @keyframes gradientShift {
            0%, 100% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
        }

        /* GitHub按钮 */
        .github-btn {
            position: fixed;
            top: 2rem;
            right: 2rem;
            width: 60px;
            height: 60px;
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            text-decoration: none;
            font-size: 1.5rem;
            transition: all 0.3s ease;
            z-index: 1000;
        }

        .github-btn:hover {
            transform: scale(1.1);
            background: rgba(255,255,255,0.2);
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }

        /* QQ群按钮 */
        .qq-group {
            position: fixed;
            right: 2rem;
            top: 50%;
            transform: translateY(-50%);
            writing-mode: vertical-rl;
            text-orientation: mixed;
            z-index: 1000;
        }

        .qq-group a {
            display: block;
            padding: 1rem 0.5rem;
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 25px;
            color: white;
            text-decoration: none;
            font-size: 1rem;
            transition: all 0.3s ease;
            margin: 0.5rem 0;
        }

        .qq-group a:hover {
            background: rgba(255,165,0,0.3);
            transform: scale(1.05);
        }

        /* 主要内容区域 */
        .main-content {
            flex: 1;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem;
            gap: 3rem;
            flex-wrap: wrap;
        }

        .card {
            width: 280px;
            height: 180px;
            background: rgba(255,255,255,0.1);
            backdrop-filter: blur(15px);
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-decoration: none;
            color: white;
            font-size: 1.5rem;
            font-weight: bold;
            transition: all 0.5s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
            box-shadow: 0 8px 32px rgba(0,0,0,0.1);
        }

        .card::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1), transparent);
            transform: translateX(-100%) translateY(-100%) rotate(45deg);
            transition: transform 0.6s ease;
        }

        .card:hover::before {
            transform: translateX(100%) translateY(100%) rotate(45deg);
        }

        .card:hover {
            transform: scale(1.15) translateY(-10px);
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            border-color: rgba(255,255,255,0.4);
        }

        .card:active {
            transform: scale(1.05) translateY(-5px);
        }

        /* 模糊效果 */
        .blur-others .card:not(:hover) {
            filter: blur(5px) brightness(0.5);
            transform: scale(0.95);
        }

        .blur-others .card:hover {
            filter: none;
        }

        /* 友情链接 */
        .friends-links {
            padding: 2rem;
            text-align: center;
        }

        .friends-title {
            color: white;
            font-size: 1.5rem;
            margin-bottom: 1rem;
            text-shadow: 0 0 10px rgba(255,255,255,0.3);
        }

        .friends-container {
            display: flex;
            justify-content: center;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .friend-link {
            padding: 0.8rem 1.5rem;
            background: rgba(255,255,255,0.08);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255,255,255,0.15);
            border-radius: 15px;
            color: white;
            text-decoration: none;
            font-size: 0.9rem;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .friend-link::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.1), transparent);
            transform: translateX(-100%) translateY(-100%) rotate(45deg);
            transition: transform 0.6s ease;
        }

        .friend-link:hover::before {
            transform: translateX(100%) translateY(100%) rotate(45deg);
        }

        .friend-link:hover {
            background: rgba(255,255,255,0.15);
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        /* 底部文字 */
        .footer {
            text-align: center;
            padding: 2rem;
            color: #ff8c00;
            font-size: 1.1rem;
            font-weight: 500;
            text-shadow: 0 0 10px rgba(255,140,0,0.3);
        }

        /* 点击效果 */
        .click-ripple {
            position: absolute;
            pointer-events: none;
            z-index: 9999;
        }

        .firework-particle {
            position: absolute;
            width: 4px;
            height: 4px;
            border-radius: 50%;
            pointer-events: none;
        }

        @keyframes firework {
            0% {
                transform: scale(1);
                opacity: 1;
            }
            100% {
                transform: scale(0);
                opacity: 0;
            }
        }

        @keyframes sparkle {
            0%, 100% {
                transform: scale(0) rotate(0deg);
                opacity: 0;
            }
            50% {
                transform: scale(1) rotate(180deg);
                opacity: 1;
            }
        }

        /* 响应式设计 */
        @media (max-width: 768px) {
            .title {
                font-size: 2.5rem;
            }
            .main-content {
                flex-direction: column;
                gap: 2rem;
            }
            .card {
                width: 240px;
                height: 150px;
            }
            .qq-group {
                right: 1rem;
                font-size: 0.9rem;
            }
            .friends-container {
                gap: 0.5rem;
            }
            .friend-link {
                padding: 0.6rem 1rem;
                font-size: 0.8rem;
            }
        }
    </style>
</head>
<body>
    <canvas class="distortion-canvas" id="distortionCanvas"></canvas>
    <div class="cursor" id="cursor"></div>
    
    <div class="container">
        <header class="header">
            <h1 class="title">昀泷RainD</h1>
        </header>

        <a href="https://github.com/Lieyan163" class="github-btn" target="_blank" rel="noopener">
            <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor">
                <path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/>
            </svg>
        </a>

        <div class="qq-group">
            <a href="https://qm.qq.com/cgi-bin/qm/qr?authKey=9aH0ELnL3gfgs%2F%2BZjaHKevQJzwyYHG1lu%2FbwWdbBoOKRZCJ8XHvfTsQl9bY%2BuC3b&k=9GyGg_wzGJnW8G_-WlsOhxORjR6vC815&noverify=0" target="_blank" rel="noopener">
                读者QQ群
            </a>
        </div>

        <main class="main-content" id="mainContent">
            <a href="https://space.bilibili.com/687731566" class="card" target="_blank" rel="noopener">
                <div>哔哩哔哩</div>
            </a>
            
            <a href="https://fanqienovel.com/author-page/3244024389706810-7475358655399859481" class="card" target="_blank" rel="noopener">
                <div>番茄小说</div>
            </a>
            
            <a href="https://www.qidian.com/book/1043967187/" class="card" target="_blank" rel="noopener">
                <div>起点中文网</div>
            </a>
        </main>

        <section class="friends-links">
            <h2 class="friends-title">友情链接</h2>
            <div class="friends-container">
                <a href="https://localsend.org/zh-CN/download" class="friend-link" target="_blank" rel="noopener">LocalSend</a>
                <a href="https://login.123pan.com/" class="friend-link" target="_blank" rel="noopener">123网盘</a>
                <a href="https://msdn.itellyou.cn/" class="friend-link" target="_blank" rel="noopener">MSDN</a>
                <a href="https://www.microsoft.com/zh-cn/" class="friend-link" target="_blank" rel="noopener">Microsoft</a>
                <a href="https://www.apple.com.cn/" class="friend-link" target="_blank" rel="noopener">Apple</a>
            </div>
        </section>

        <footer class="footer">
            给岁月以文明，给时光以生命。
        </footer>
    </div>

    <script>
        // 自定义光标
        const cursor = document.getElementById('cursor');
        const trails = [];
        const trailLength = 10;

        // 创建光标拖尾
        for (let i = 0; i < trailLength; i++) {
            const trail = document.createElement('div');
            trail.className = 'cursor-trail';
            trail.style.opacity = (i + 1) / trailLength * 0.5;
            document.body.appendChild(trail);
            trails.push(trail);
        }

        let mouseX = 0, mouseY = 0;
        let trailX = [], trailY = [];

        for (let i = 0; i < trailLength; i++) {
            trailX[i] = 0;
            trailY[i] = 0;
        }

        document.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
            cursor.style.left = mouseX - 10 + 'px';
            cursor.style.top = mouseY - 10 + 'px';
        });

        // 更新拖尾
        function updateTrails() {
            trailX[0] = mouseX;
            trailY[0] = mouseY;

            for (let i = 0; i < trailLength; i++) {
                if (i > 0) {
                    trailX[i] += (trailX[i-1] - trailX[i]) * 0.3;
                    trailY[i] += (trailY[i-1] - trailY[i]) * 0.3;
                }
                
                trails[i].style.left = trailX[i] - 3 + 'px';
                trails[i].style.top = trailY[i] - 3 + 'px';
            }
            
            requestAnimationFrame(updateTrails);
        }
        updateTrails();

        // 模糊效果
        const mainContent = document.getElementById('mainContent');
        const cards = document.querySelectorAll('.card');

        cards.forEach(card => {
            card.addEventListener('mouseenter', () => {
                mainContent.classList.add('blur-others');
            });
            
            card.addEventListener('mouseleave', () => {
                mainContent.classList.remove('blur-others');
            });
        });

        // 点击烟花效果
        document.addEventListener('click', (e) => {
            const colors = ['#ff6b6b', '#4ecdc4', '#45b7d1', '#96ceb4', '#feca57', '#ff9ff3', '#54a0ff'];
            const particleCount = 20;
            
            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.className = 'firework-particle';
                
                const color = colors[Math.floor(Math.random() * colors.length)];
                particle.style.backgroundColor = color;
                particle.style.boxShadow = `0 0 10px ${color}`;
                
                const angle = (i / particleCount) * 2 * Math.PI;
                const velocity = Math.random() * 100 + 50;
                const startX = e.clientX;
                const startY = e.clientY;
                
                particle.style.left = startX + 'px';
                particle.style.top = startY + 'px';
                
                document.body.appendChild(particle);
                
                const endX = startX + Math.cos(angle) * velocity;
                const endY = startY + Math.sin(angle) * velocity;
                
                particle.animate([
                    {
                        transform: 'translate(0, 0) scale(1)',
                        opacity: 1
                    },
                    {
                        transform: `translate(${endX - startX}px, ${endY - startY}px) scale(0)`,
                        opacity: 0
                    }
                ], {
                    duration: 800 + Math.random() * 400,
                    easing: 'cubic-bezier(0.25, 0.46, 0.45, 0.94)'
                });
                
                setTimeout(() => {
                    particle.remove();
                }, 1200);
            }
            
            // 添加星光闪烁效果
            for (let i = 0; i < 5; i++) {
                setTimeout(() => {
                    const sparkle = document.createElement('div');
                    sparkle.innerHTML = '✨';
                    sparkle.style.position = 'absolute';
                    sparkle.style.left = (e.clientX + (Math.random() - 0.5) * 60) + 'px';
                    sparkle.style.top = (e.clientY + (Math.random() - 0.5) * 60) + 'px';
                    sparkle.style.fontSize = '20px';
                    sparkle.style.pointerEvents = 'none';
                    sparkle.style.zIndex = '9999';
                    
                    document.body.appendChild(sparkle);
                    
                    sparkle.animate([
                        {
                            transform: 'scale(0) rotate(0deg)',
                            opacity: 0
                        },
                        {
                            transform: 'scale(1) rotate(180deg)',
                            opacity: 1
                        },
                        {
                            transform: 'scale(0) rotate(360deg)',
                            opacity: 0
                        }
                    ], {
                        duration: 1000,
                        easing: 'ease-out'
                    });
                    
                    setTimeout(() => {
                        sparkle.remove();
                    }, 1000);
                }, i * 100);
            }
        });

        // 页面扭曲效果
        const canvas = document.getElementById('distortionCanvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const particles = [];
        const particleCount = 50;

        class Particle {
            constructor() {
                this.reset();
                this.life = Math.random() * 100;
            }

            reset() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.vx = (Math.random() - 0.5) * 2;
                this.vy = (Math.random() - 0.5) * 2;
                this.life = 100;
                this.decay = Math.random() * 0.02 + 0.005;
            }

            update() {
                this.x += this.vx;
                this.y += this.vy;
                this.life -= this.decay;

                if (this.life <= 0 || this.x < 0 || this.x > canvas.width || this.y < 0 || this.y > canvas.height) {
                    this.reset();
                }
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.life / 100 * 0.1;
                ctx.fillStyle = '#ffffff';
                ctx.beginPath();
                ctx.arc(this.x, this.y, 2, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }
        }

        for (let i = 0; i < particleCount; i++) {
            particles.push(new Particle());
        }

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            particles.forEach(particle => {
                particle.update();
                particle.draw();
            });

            requestAnimationFrame(animate);
        }
        animate();

        // 窗口大小调整
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        });

        // 鼠标移动扭曲效果
        document.addEventListener('mousemove', (e) => {
            const mouseInfluence = 50;
            particles.forEach(particle => {
                const dx = e.clientX - particle.x;
                const dy = e.clientY - particle.y;
                const distance = Math.sqrt(dx * dx + dy * dy);
                
                if (distance < mouseInfluence) {
                    const force = (mouseInfluence - distance) / mouseInfluence;
                    particle.vx += (dx / distance) * force * 0.1;
                    particle.vy += (dy / distance) * force * 0.1;
                }
            });
        });
    </script>
</body>
</html>
