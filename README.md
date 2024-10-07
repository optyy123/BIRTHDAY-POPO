
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown to Your Birthday! 🎉</title>
    <style>
        body {
            font-family: 'Comic Sans MS', sans-serif;
            background-color: #ffe4e1;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            text-align: center;
            overflow: hidden;
        }
        h1 {
            color: #ff69b4;
            font-size: 2.8em;
            margin-bottom: 0;
            text-shadow: 2px 2px #fff;
        }
        p {
            color: #ff1493;
            font-size: 1.5em;
            margin-bottom: 20px;
        }
        #countdown {
            font-size: 2em;
            color: #ff4500;
            margin-bottom: 15px;
        }
        #counter {
            font-size: 2.5em;
            color: #ffffff;
            background-color: #ff69b4;
            padding: 10px 20px;
            border-radius: 30px;
            margin-top: 10px;
            display: inline-block;
            box-shadow: 0 0 10px rgba(255, 105, 180, 0.5);
        }
        .reward-image {
            max-width: 300px;
            opacity: 0;
            transition: opacity 1.5s ease-in-out;
            position: absolute;
            z-index: 1;
        }
        .reward-image.show {
            opacity: 1;
        }
        .hide {
            opacity: 0;
        }
        #notification {
            position: absolute;
            top: 10px;
            background-color: #ff1493;
            color: #fff;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0px 4px 8px rgba(0,0,0,0.1);
            animation: bounce 2s infinite;
        }
        .emoji {
            position: absolute;
            font-size: 3em;
            user-select: none;
            cursor: pointer;
            transition: transform 0.5s ease, opacity 0.5s ease;
            padding: 15px;
        }
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }
        @media (max-width: 768px) {
            h1 { font-size: 2.5em; }
            p, #countdown { font-size: 1.5em; }
        }
    </style>
</head>
<body>
    <h1>BIRTHDAY-POPO</h1>
    <p>Countdown to Your Birthday! 🎉</p>

    <div id="countdown"></div>
    <div id="counter">Touched Emojis: 0</div>

    <img id="image1" class="reward-image" src="https://i.imgur.com/Dna92xG.png" alt="Reward Image 1">
    <img id="image2" class="reward-image" src="https://i.imgur.com/anotherImage1.png" alt="Reward Image 2">
    <img id="image3" class="reward-image" src="https://i.imgur.com/anotherImage2.png" alt="Reward Image 3">

    <div id="notification" class="notification"></div>

    <script>
        const countDownDate = new Date("Oct 18, 2024 00:00:00").getTime();
        const counterElement = document.getElementById('counter');

        let counter = 0;

        const countdownFunction = setInterval(() => {
            const now = new Date().getTime();
            const distance = countDownDate - now;

            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            document.getElementById("countdown").innerHTML = `${days}d ${hours}h ${minutes}m ${seconds}s`;

            if (distance < 0) {
                clearInterval(countdownFunction);
                document.getElementById("countdown").innerHTML = "Happy Birthday!";
            }
        }, 1000);

        function showImage(imgElement) {
            imgElement.classList.add('show');
        }

        function hideImage(imgElement) {
            imgElement.classList.remove('show');
        }

        function handleCounter() {
            counter++;

            if (counter === 8) {
                showImage(document.getElementById('image1'));
            } else if (counter === 10) {
                hideImage(document.getElementById('image1'));
                showImage(document.getElementById('image2'));
            } else if (counter === 13) {
                hideImage(document.getElementById('image2'));
                const image3 = document.getElementById('image3');
                showImage(image3);

                setTimeout(() => {
                    hideImage(image3);
                }, 5000);
            }

            counterElement.innerText = `Touched Emojis: ${counter}`;
        }

        const emojis = ['🎈', '🎉', '❤️', '💖', '💘', '💙', '🎁'];

        function createEmoji() {
            const emoji = document.createElement('div');
            emoji.innerText = emojis[Math.floor(Math.random() * emojis.length)];
            emoji.classList.add('emoji');

            emoji.style.left = Math.random() * window.innerWidth + 'px';
            emoji.style.top = window.innerHeight - 50 + 'px';

            emoji.addEventListener('click', () => {
                emoji.style.transform = 'scale(1.5) translateY(-150px)';
                emoji.style.opacity = '0';

                setTimeout(() => {
                    emoji.remove();
                }, 500);

                handleCounter();
            });

            document.body.appendChild(emoji);
            animateEmoji(emoji);

            setTimeout(() => emoji.remove(), 10000);
        }

        function animateEmoji(emoji) {
            let velocityY = Math.random() * -2 - 3; 
            let velocityX = (Math.random() - 0.5) * 2;

            function updatePosition() {
                velocityY += 0.01;
                const currentTop = parseFloat(emoji.style.top) || 0;
                const currentLeft = parseFloat(emoji.style.left) || 0;

                emoji.style.top = (currentTop + velocityY) + 'px';
                emoji.style.left = (currentLeft + velocityX) + 'px';

                if (parseFloat(emoji.style.top) > window.innerHeight || parseFloat(emoji.style.top) < -50) {
                    emoji.remove();
                } else {
                    requestAnimationFrame(updatePosition);
                }
            }

            updatePosition();
        }

        setInterval(() => {
            const emojiCount = Math.floor(Math.random() * 2) + 1;
            for (let i = 0; i < emojiCount; i++) {
                createEmoji();
            }
        }, Math.random() * 1000 + 1000);
    </script>
</body>
</html>
