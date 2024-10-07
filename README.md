<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown to Your Birthday! 🎉</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #fff0f5;
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
            font-size: 3em;
            margin-bottom: 0;
        }
        p {
            color: #ff1493;
            font-size: 1.5em;
        }
        #countdown {
            font-size: 2.5em;
            color: #ff4500;
            margin-bottom: 20px;
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
        .notification {
            font-size: 1.5em;
            color: white;
            background-color: #32a852;
            padding: 15px;
            border-radius: 10px;
            position: absolute;
            top: -50px;
            left: 50%;
            transform: translateX(-50%);
            opacity: 0;
            transition: opacity 1s ease-in-out, top 1s ease-in-out;
        }
        .notification.show {
            top: 20px;
            opacity: 1;
        }
        .notification.hide {
            top: -50px;
            opacity: 0;
        }
        #reward-image {
            display: none;
            margin-top: 20px;
            max-width: 300px;
        }
        .emoji {
            position: absolute;
            font-size: 3em;
            user-select: none;
            cursor: pointer;
            transition: transform 0.5s ease, opacity 0.5s ease;
            padding: 15px; /* Larger hitbox for easier clicking */
        }
        @media (max-width: 768px) {
            h1 {
                font-size: 2.5em;
            }
            p, #countdown {
                font-size: 1.5em;
            }
        }
    </style>
</head>
<body>
    <h1>Countdown to Your Birthday! 🎉</h1>
    <p>I'm so excited for your special day!</p>

    <div id="countdown"></div>
    <div id="counter">Touched Emojis: 0</div>
    
    <!-- Reward image after 8 points -->
    <img id="reward-image" src="/mnt/data/Untiatled-removebg-preview.png" alt="Reward Image">

    <div id="notification" class="notification"></div>

    <script>
        const countDownDate = new Date("Oct 18, 2024 00:00:00").getTime();
        const counterElement = document.getElementById('counter');
        const rewardImage = document.getElementById('reward-image');

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
                    emoji.innerText = '✨'; // Sparkle effect
                    setTimeout(() => emoji.remove(), 500);
                }, 300);

                counter++;
                counterElement.innerText = `Touched Emojis: ${counter}`;

                if (counter === 1) {
                    showNotification("I'm really sorry and I'm working on myself");
                } else if (counter === 5) {
                    showNotification("There will be hints! 🔍🎁");
                } else if (counter === 8) {
                    rewardImage.style.display = 'block';
                }
            });

            document.body.appendChild(emoji);
            animateEmoji(emoji);

            setTimeout(() => emoji.remove(), 10000);
        }

        function animateEmoji(emoji) {
            const gravity = 0.01; // Slower gravity for longer float
            let velocityY = Math.random() * -2 - 3; // Higher initial upward force
            let velocityX = (Math.random() - 0.5) * 2;

            function updatePosition() {
                velocityY += gravity;
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

        function showNotification(message) {
            const notification = document.getElementById('notification');
            notification.innerText = message;
            notification.classList.add('show');

            setTimeout(() => {
                notification.classList.remove('show');
            }, 5000);
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
