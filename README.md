<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>Lieyan 的个人空间</title>
    <style>
        :root {
            --blur-intensity: 10px;
            --brightness-value: 0.5;
            --transition-time: 0.5s;
        }

        body {
            margin: 0;
            min-height: 100vh;
            font-family: 'Arial', sans-serif;
            overflow-x: hidden;
            background: url('https://wallpaperm.cmcm.com/da915804aeab435636dd9bd1c9b39722.jpg') center/cover fixed;
            position: relative;
            transition: background 0.5s;
        }

      
        body::after {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.3);
            z-index: -1;
        }

        .blur-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            backdrop-filter: blur(0px);
            transition: all var(--transition-time) cubic-bezier(0.4, 0, 0.2, 1);
            pointer-events: none;
            z-index: 0;
        }

        .blur-active .blur-overlay {
            backdrop-filter: blur(20px);
            background: rgba(0, 0, 0, 0.4);
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 2rem;
            position: relative;
            z-index: 2;
        }

        .links-section {
            display: grid;
            gap: 2rem;
            perspective: 1200px;
        }

.link-item {
    padding: 2rem;
    background: linear-gradient(145deg, rgba(255, 255, 255, 0.9), rgba(245, 245, 245, 0.95));
    border-radius: 16px;
    transition: all 0.6s cubic-bezier(0.23, 1, 0.32, 1);
    cursor: pointer;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.15);
    transform: translateZ(0);
    position: relative;
    overflow: hidden;
    filter: brightness(var(--brightness-value));
}


.link-item:hover {
    transform: scale(1.1) translateZ(20px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.25);
    z-index: 3;
    filter: blur(0px) brightness(1); 
}


.blur-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    backdrop-filter: blur(0px); 
    transition: all var(--transition-time) cubic-bezier(0.4, 0, 0.2, 1);
    pointer-events: none;
    z-index: 0;
}

.blur-active .blur-overlay {
    backdrop-filter: blur(12px); 
    background: rgba(0, 0, 0, 0.4);
}document.querySelectorAll('.link-item').forEach(item => {
    item.addEventListener('click', () => {
    
        document.querySelectorAll('.link-item').forEach(link => {
            link.classList.remove('active');
        });
        
     
        item.classList.add('active');
        
       
        document.body.classList.add('blur-active');
    });

    item.addEventListener('mouseenter', () => {
     
        if (!item.classList.contains('active')) {  
            document.body.classList.add('blur-active');
        }
    });

    item.addEventListener('mouseleave', () => {
   
        if (![...document.querySelectorAll('.link-item')].some(item => item.classList.contains('active'))) {
            document.body.classList.remove('blur-active');
        }
    });
});

 

     
        .link-item::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border: 3px solid rgba(255, 255, 255, 0.3);
            border-radius: 16px;
            transition: all 0.3s ease;
            opacity: 0;
            transform: scale(0.95);
        }

  
        .link-item:hover {
            transform: scale(1.1) translateZ(20px);
            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.25);
            z-index: 3;
            filter: blur(0px) brightness(1);
        }

    
        .link-item:active {
            transform: scale(1.05) translateZ(15px);
            box-shadow: 0 10px 35px rgba(0, 0, 0, 0.3);
            transition: transform 0.2s ease, box-shadow 0.3s ease;
        }

      
        
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <div class="blur-overlay"></div>
    
    <div class="container">
        <h1>Lieyan 的个人空间</h1>
        
        <div class="links-section">
            <div class="link-item" onclick="window.open('https://space.bilibili.com/687731566')">
                <h2>哔哩哔哩</h2>
            </div>
            
            <div class="link-item" onclick="window.open('https://fanqienovel.com/author-page/3244024389706810-7412638058287207705')">
                <h2>番茄小说</h2>
            </div>
        </div>
	
	 <div class="link-item" onclick="window.open('https://lieyan163.github.io/NO-/')">
                <h2>无聊按钮</h2>
            </div>
        </div>


        <footer>
            <p style="margin-bottom: 2rem;">给岁月以文明，给时光以生命。</p>
            <p onclick="window.open('https://github.com/Lieyan163')" 
               style="cursor: pointer; color: #666; margin-top: 1.5rem;">
                GitHub
	 	<p onclick="window.open('https://qm.qq.com/q/92zmnf0xmo')" 
               style="cursor: pointer; color: #EF7D31; margin-top: 1.5rem;font-size: 20px;font-weight: bold;">
		
               加入群聊：煊铭的小窝
		

            </p>
        </footer>
    </div>

    <script>
      
        class Particle {
            constructor(x, y) {
                this.x = x;
                this.y = y;
                this.size = Math.random() * 8 + 2;
                this.speedX = (Math.random() - 0.5) * 6;
                this.speedY = (Math.random() - 0.5) * 6;
                this.color = `hsl(${Math.random() * 360}, 70%, 60%)`;
                this.alpha = 1;
                this.life = 1;
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                this.alpha -= 0.015;
                this.size *= 0.96;
                this.life -= 0.02;
                return this.life > 0;
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

     
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        let particles = [];

      
        function animate() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles = particles.filter(particle => {
                particle.draw();
                return particle.update();
            });
            requestAnimationFrame(animate);
        }
        animate();

     document.addEventListener('mousemove', (e) => {
        const offsetX = window.pageXOffset;
        const offsetY = window.pageYOffset; 
        for (let i = 0; i < 4; i++) {
            particles.push(new Particle(
                e.clientX + Math.random() * 10 - 5 + offsetX, 
                e.clientY + Math.random() * 10 - 5 + offsetY  
            ));
        }
    });

   
    document.addEventListener('click', (e) => {
        const offsetX = window.pageXOffset;
        const offsetY = window.pageYOffset; 
        for (let i = 0; i < 30; i++) {
            const angle = Math.PI * 2 * i / 30;
            const speed = Math.random() * 8 + 2;
            const p = new Particle(e.clientX + offsetX, e.clientY + offsetY); 
            p.speedX = Math.cos(angle) * speed;
            p.speedY = Math.sin(angle) * speed;
            p.size = Math.random() * 8 + 3;
            particles.push(p);
            }
        });

     
        let activeHover = false;
        document.querySelectorAll('.link-item').forEach(item => {
            item.addEventListener('mouseenter', () => {
                document.body.classList.add('blur-active');
                activeHover = true;
            });
            item.addEventListener('mouseleave', () => {
                document.body.classList.remove('blur-active');
                activeHover = false;
            });
        });

     
        document.addEventListener('mousemove', (e) => {
            if(activeHover) {
                const x = (e.clientX - window.innerWidth/2) * 0.03;
                const y = (e.clientY - window.innerHeight/2) * 0.03;
                document.querySelector('.links-section').style.transform = 
                    `perspective(1200px) rotateY(${x}deg) rotateX(${-y}deg)`;
            }
        });
    </script>
</body>
</html>
