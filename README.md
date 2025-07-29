# 404
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>M_in_X.Tech</title>
    <style>
        body {
            margin: 0;
            background-color: black;
            overflow: hidden;
        }

        #canvas {
            width: 100%;
            height: 100vh;
            display: block;
        }
    </style>
</head>
<body>
    <canvas id="canvas"></canvas>
    <script>
        const canvas = document.getElementById('canvas');
        const ctx = canvas.getContext('2d');

        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;

        const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ123456789@                        
        const charactersLength = characters.length;

        function generateRandomCharacter() {
            return characters.charAt(Math.floor(Math.random() * charactersLength));
        }

        class Stream {
            constructor(x, y, speed) {
                this.x = x;
                this.y = y;
                this.speed = speed;
                this.text = '';
                this.interval = null;
            }

            draw() {
                ctx.font = '20px monospace';
                ctx.fillStyle = 'rgba(0, 255, 70, 0.8)';
                ctx.fillText(this.text, this.x, this.y);
            }

            update() {
                this.text = '';
                for (let i = 0; i < Math.floor(Math.random() * 10) + 5; i++) {
                    this.text += generateRandomCharacter();
                }
                this.y += this.speed;
                if (this.y > canvas.height) {
                    this.y = 0;
                }
            }
        }

        const streams = [];
        for (let i = 0; i < canvas.width / 20; i++) {
            streams.push(new Stream(i * 20, Math.random() * canvas.height, Math.random() * 5 + 2));
        }

        function animate() {
            ctx.fillStyle = 'rgba(0, 0, 0, 0.05)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            streams.forEach(stream => {
                stream.update();
                stream.draw();
            });
            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>
