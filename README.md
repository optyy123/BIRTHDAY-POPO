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
        /* Styles for all reward images */
        .reward-image {
            display: none;
            opacity: 0;
            transition: opacity 1s ease-in-out;
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
            bottom: 20px;
            max-width: 300px;
            background: transparent;
        }

        /* Fade-in and show class */
        .reward-image.show {
            display: block;
            opacity: 1;
        }

        /* Fade-out animation for the last image */
        .reward-image.hide {
            opacity: 0;
            transition: opacity 1s ease-in-out;
        }

        .emoji {
            position: absolute;
            font-size: 3em;
            user-select: none;
            cursor: pointer;
            transition: transform 0.5s ease, opacity 0.5s ease;
            padding: 15px;
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
    
    <!-- Reward images -->
    <img id="reward-image-1" class="reward-image" src="https://i.imgur.com/2hjw8IS.png" alt="Reward Image 1">
    <img id="reward-image-2" class="reward-image" src="https://i.imgur.com/Dna92xG.png" alt="Reward Image 2">
    <img id="reward-image-3" class="reward-image" src="https://i.imgur.com/2LJDX4X.png" alt="Reward Image 3">

    <div id="notification" class="notification"></div>

    <script>
        const countDownDate = new Date("Oct 18, 2024 00:00:00").getTime();
        const counterElement = document.getElementById('counter');
        const rewardImage1 = document.getElementById('reward-image-1');
        const rewardImage2 = document.getElementById('reward-image-2');
        const rewardImage3 = document.getElementById('reward-image-3');

        let counter = 0;

        // Countdown Timer
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
                    showRewardImage(rewardImage1);
                } else if (counter === 10) {
                    showRewardImage(rewardImage2);
                } else if (counter === 13) {
                    showRewardImage(rewardImage3);
                    setTimeout(() => {
                        hideRewardImage(rewardImage3);
                    }, 5000);
                }
            });

            document.body.appendChild(emoji);
            animateEmoji(emoji);

            setTimeout(() => emoji.remove(), 10000);
        }

        function animateEmoji(emoji) {
            const gravity = 0.01; 
            let velocityY = Math.random() * -2 - 3; 
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

        function showRewardImage(imageElement) {
            imageElement.classList.add('show');
        }

        function hideRewardImage(imageElement) {
            imageElement.classList.add('hide');
            setTimeout(() => {
                imageElement.style.display = 'none';
            }, 1000); // Fade out duration matches CSS transition
        }

        // Generate random emojis
        setInterval(() => {
            const emojiCount = Math.floor(Math.random() * 2) + 1;
            for (let i = 0; i < emojiCount; i++) {
                createEmoji();
            }
        }, Math.random() * 1000 + 1000);
    </script>
</body>
</html>
