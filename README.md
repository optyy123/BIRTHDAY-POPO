
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
            background-color: #ff69b4;
            padding: 15px;
            border-radius: 10px;
            display: none;
            position: absolute;
            top: -50px;
            left: 50%;
            transform: translateX(-50%);
            opacity: 0;
            transition: opacity 0.5s, top 0.5s;
        }
        .notification.show {
            display: block;
            top: 20px;
            opacity: 1;
        }
        .emoji {
            position: absolute;
            font-size: 3em;
            user-select: none;
            cursor: pointer;
            transition: transform 0.5s ease, opacity 0.5s ease;
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

    <div id="notification" class="notification"></div>

    <script>
        // Countdown timer setup
        const countDownDate = new Date("Oct 18, 2024 00:00:00").getTime();

        // Update the countdown every second
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

        // Emojis array
        const emojis = ['🎈', '🎉', '❤️', '💖', '💘', '💙', '🎁'];
        let counter = 0;

        // Function to generate and animate emojis
        function createEmoji() {
            const emoji = document.createElement('div');
            emoji.innerText = emojis[Math.floor(Math.random() * emojis.length)];
            emoji.classList.add('emoji');

            emoji.style.left = Math.random() * window.innerWidth + 'px';
            emoji.style.top = window.innerHeight - 50 + 'px';

            // Emoji interaction and counter update
            emoji.addEventListener('click', () => {
                emoji.style.transform = 'scale(1.5) translateY(-150px)';
                emoji.style.opacity = '0';

                setTimeout(() => {
                    emoji.innerText = '✨'; // Add sparkle effect
                    setTimeout(() => emoji.remove(), 500);
                }, 300);

                counter++;
                document.getElementById('counter').innerText = `Touched Emojis: ${counter}`;

                // Notifications for 1 and 5 touches
                const notification = document.getElementById('notification');
                if (counter === 1) {
                    showNotification(notification, "I'm really sorry and I'm working on myself");
                } else if (counter === 5) {
                    showNotification(notification, "There will be hints! 🔍🎁");
                }
            });

            document.body.appendChild(emoji);
            animateEmoji(emoji);

            // Remove emoji after a while to avoid clutter
            setTimeout(() => emoji.remove(), 10000);
        }

        // Function to animate emojis with slow float
        function animateEmoji(emoji) {
            const gravity = 0.03;
            let velocityY = Math.random() * -2 - 1;
            let velocityX = (Math.random() - 0.5) * 2;

            function updatePosition() {
                velocityY += gravity;
                const currentTop = parseFloat(emoji.style.top) || 0;
                const currentLeft = parseFloat(emoji.style.left) || 0;

                emoji.style.top = (currentTop + velocityY) + 'px';
                emoji.style.left = (currentLeft + velocityX) + 'px';

                if (parseFloat(emoji.style.top) > window.innerHeight) {
                    emoji.remove();
                } else {
                    requestAnimationFrame(updatePosition);
                }
            }

            updatePosition();
        }

        // Function to show notifications
        function showNotification(element, message) {
            element.innerText = message;
            element.classList.add('show');

            setTimeout(() => {
                element.classList.remove('show');
            }, 5000);
        }

        // Start generating emojis
        setInterval(() => {
            const emojiCount = Math.floor(Math.random() * 2) + 1;
            for (let i = 0; i < emojiCount; i++) {
                createEmoji();
            }
        }, Math.random() * 1000 + 1000); // 1 or 2 emojis every 1-2 seconds
    </script>
</body>
</html>
