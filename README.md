<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>Lieyan 的个人空间</title>
    <style>
        body {
            margin: 0;
            min-height: 100vh;
            background: white;
            font-family: Arial, sans-serif;
            overflow-x: hidden;
            transition: background 0.5s;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 2rem;
            position: relative;
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 3rem;
        }

        .links-section {
            display: grid;
            gap: 1.5rem;
        }

        .link-item {
            padding: 1.5rem;
            background: linear-gradient(120deg, #f5f5f5, white);
            border-radius: 12px;
            transition: all 0.5s;
            cursor: pointer;
            position: relative;
            z-index: 1;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .link-item:hover {
            transform: scale(1.15);
            z-index: 3;
            background: linear-gradient(120deg, #e3f2fd, #f0f8ff);
        }

        .darken-background {
            background: rgba(0,0,0,0.1);
        }

        footer {
            text-align: center;
            margin-top: 5rem;
            color: #666;
            padding: 2rem 0;
            position: relative;
            z-index: 2;
        }

        footer p {
            margin: 1.2rem 0;
        }

        #canvas {
            position: fixed;
            top: 0;
            left: 0;
            pointer-events: none;
            z-index: -1;
        }

        .click-effect {
            position: absolute;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            animation: clickExplode 0.8s ease-out;
            pointer-events: none;
        }

        @keyframes clickExplode {
            0% { transform: scale(0); opacity: 1; }
            100% { transform: scale(5); opacity: 0; }
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <div class="container">
        <h1>Lieyan 的个人空间</h1>
        
        <div class="links-section">
            <div class="link-item" onclick="window.open('https://space.bilibili.com/687731566')">
                <h2>📺哔哩哔哩</h2>
            </div>
            
            <div class="link-item" onclick="window.open('https://fanqienovel.com/author-page/3244024389706810-7412638058287207705')">
                <h2>📖番茄小说</h2>
            </div>
        </div>

        <footer>
            <p style="margin-bottom: 2rem;">给岁月以文明，给时光以生命。</p>
            <p onclick="window.open('https://github.com/Lieyan163')" 
               style="cursor: pointer; color: #666; margin-top: 1.5rem;">
                GitHub
            </p>
        </footer>
    </div>

    <script>
        // 彩色拖尾效果
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        class Particle {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.size = Math.random() * 8 + 2;
                this.speedX = (Math.random() - 0.5) * 5;
                this.speedY = (Math.random() - 0.5) * 5;
                this.color = `hsl(${Math.random() * 360}, 70%, 60%)`;
                this.alpha = 1;
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.alpha -= 0.02;
                this.size *= 0.96;
                return this.alpha > 0;
            }
            draw() {
                ctx.save();
                ctx.globalAlpha = this.alpha;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                ctx.restore();
            }
        }

        let particles = [];
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach((particle, index) => {
                particle.draw();
                if (!particle.update()) {
                    particles.splice(index, 1);
                }
            });
            requestAnimationFrame(animate);
        }
        animate();

        // 鼠标拖尾
        document.addEventListener('mousemove', (e) => {
            for (let i = 0; i < 3; i++) {
                particles.push(new Particle(e.clientX, e.clientY));
            }
        });

        // 点击爆炸效果
        document.addEventListener('click', (e) => {
            for (let i = 0; i < 20; i++) {
                const angle = (Math.PI * 2 * i) / 20;
                const speed = Math.random() * 5 + 2;
                const clickParticle = new Particle(e.clientX, e.clientY);
                clickParticle.speedX = Math.cos(angle) * speed;
                clickParticle.speedY = Math.sin(angle) * speed;
                clickParticle.size = Math.random() * 6 + 3;
                particles.push(clickParticle);
            }
        });

        // 悬停效果
        document.querySelectorAll('.link-item').forEach(item => {
            item.addEventListener('mouseenter', () => {
                document.body.classList.add('darken-background');
            });
            item.addEventListener('mouseleave', () => {
                document.body.classList.remove('darken-background');
            });
        });
    </script>
</body>
</html>
