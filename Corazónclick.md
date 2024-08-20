<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Corazones y Efectos</title>
    <style>
        body {
            margin: 0;
            overflow: hidden;
            background-color: #282c34;
            color: white;
            font-family: Arial, sans-serif;
        }
        .heart {
            position: absolute;
            width: 30px;
            height: 30px;
            background: red;
            clip-path: polygon(50% 0%, 100% 50%, 50% 100%, 0% 50%);
            transform: rotate(-45deg);
            opacity: 0.8;
        }
        .star {
            position: absolute;
            width: 10px;
            height: 10px;
            background: white;
            clip-path: polygon(50% 0%, 61% 35%, 98% 35%, 68% 57%, 79% 91%, 50% 70%, 21% 91%, 32% 57%, 2% 35%, 39% 35%);
            opacity: 0.8;
            animation: twinkle 1s infinite;
        }
        @keyframes twinkle {
            0% { opacity: 0.8; }
            50% { opacity: 0.2; }
            100% { opacity: 0.8; }
        }
    </style>
</head>
<body>
    <script>
        let clickCount = 0;

        function createHeart(x, y) {
            const heart = document.createElement('div');
            heart.className = 'heart';
            heart.style.left = `${x}px`;
            heart.style.top = `${y}px`;
            document.body.appendChild(heart);
        }

        function createStar(x, y) {
            const star = document.createElement('div');
            star.className = 'star';
            star.style.left = `${x}px`;
            star.style.top = `${y}px`;
            document.body.appendChild(star);
        }

        function handleClick(event) {
            clickCount++;
            const { clientX: x, clientY: y } = event;
            createHeart(x - 15, y - 15);

            if (clickCount === 100) {
                for (let i = 0; i < 100; i++) {
                    setTimeout(() => {
                        const angle = Math.random() * 2 * Math.PI;
                        const distance = Math.random() * 200;
                        const xOffset = Math.cos(angle) * distance;
                        const yOffset = Math.sin(angle) * distance;
                        createHeart(x + xOffset - 15, y + yOffset - 15);
                    }, i * 20);
                }
                for (let i = 0; i < 200; i++) {
                    setTimeout(() => {
                        const angle = Math.random() * 2 * Math.PI;
                        const distance = Math.random() * 400;
                        const xOffset = Math.cos(angle) * distance;
                        const yOffset = Math.sin(angle) * distance;
                        createStar(x + xOffset - 5, y + yOffset - 5);
                    }, i * 10);
                }
            }

            if (clickCount >= 200 && clickCount % 10 === 0) {
                const questions = [
                    "¿Cuál es tu color favorito?",
                    "¿Qué música te gusta?",
                    "¿Cuál es tu película favorita?",
                    "¿Qué lugar te gustaría visitar?",
                    "¿Tienes alguna mascota?",
                ];
                const question = questions[Math.floor(Math.random() * questions.length)];
                alert(question);
            }
        }

        document.addEventListener('click', handleClick);
    </script>
</body>
</html>
