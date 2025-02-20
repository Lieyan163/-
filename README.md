# 个人空间
lieyan.github.io
<!DOCTYPE html>
<html>
<head>
    <title>Lieyan 的个人空间</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            min-height: 100vh;
            background: white;
            font-family: Arial, sans-serif;
            overflow: hidden;
        }

        .container {
            position: relative;
            z-index: 2;
            padding: 50px 20px;
        }

        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 40px;
        }

        .links-section {
            max-width: 500px;
            margin: 0 auto;
        }

        .link-block {
            background: rgba(245, 245, 245, 0.9);
            margin: 15px;
            padding: 20px;
            border-radius: 10px;
            transition: all 0.5s;
            cursor: pointer;
            position: relative;
        }

        .link-block:hover {
            transform: scale(1.3);
            z-index: 3;
        }

        .links-section:hover .link-block:not(:hover) {
            filter: blur(3px) brightness(0.7);
        }

        footer {
            text-align: center;
            padding: 30px;
            color: #666;
            position: relative;
            z-index: 2;
        }

        #canvas {
            position: fixed;
            top: 0;
            left: 0;
            z-index: 1;
        }

        .github-link {
            color: #666;
            text-decoration: none;
            font-weight: bold;
            transition: all 0.3s;
        }

        .github-link:hover {
            color: #333;
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    
    <div class="container">
        <h1>Lieyan 的个人空间</h1>
        
        <div class="links-section">
            <div class="link-block" onclick="window.open('https://space.bilibili.com/687731566')">
                <h2>📺bilbil</h2>
            </div>
            <div class="link-block" onclick="window.open('https://fanqienovel.com/author-page/3244024389706810-7412638058287207705')">
                <h2>📖番茄小说</h2>
            </div>
        </div>
    </div>

    <footer>
        <p>给岁月以文明，给时光以生命。</p>
        <a href="https://github.com/Lieyan163" class="github-link">GitHub</a>
    </footer>

    <script>
        // 鼠标拖尾效果
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        let particles = [];
        const particleCount = 20;

        class Particle {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.size = Math.random() * 5 + 2;
                this.speedX = Math.random() * 3 - 1.5;
                this.speedY = Math.random() * 3 - 1.5;
                this.color = `hsl(${Math.random() * 360}, 50%, 50%)`;
            }

            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.size *= 0.95;
            }

            draw() {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        // 鼠标移动事件
        document.addEventListener('mousemove', (e) => {
            for (let i = 0; i < particleCount; i++) {
                particles.push(new Particle(e.clientX, e.clientY));
            }
        });

        // 点击效果
        document.addEventListener('click', (e) => {
            for (let i = 0; i < 30; i++) {
                particles.push(new Particle(e.clientX, e.clientY));
            }
        });

        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            
            particles.forEach((particle, index) => {
                particle.update();
                particle.draw();
                if (particle.size <= 0.5) {
                    particles.splice(index, 1);
                }
            });
            
            requestAnimationFrame(animate);
        }

        animate();
        

        // 窗口大小调整
        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
    
     // 背景变暗控制
        document.querySelectorAll('.link-item').forEach(item => {
            item.addEventListener('mouseover', () => {
                document.querySelector('.overlay').style.background = 'rgba(0,0,0,0.3)';
            });
            item.addEventListener('mouseout', () => {
                document.querySelector('.overlay').style.background = 'rgba(0,0,0,0)';
            });
        });
    </script>
</body>
</html>

