
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Birthday Countdown with Puzzle</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f0f8ff;
            text-align: center;
            margin: 0;
            padding: 20px;
        }

        h1 {
            font-size: 3em;
            color: #ff69b4;
        }

        #countdown {
            font-size: 2.5em;
            color: #ff6347;
            margin: 20px;
        }

        #emoji-counter {
            font-size: 1.5em;
            color: #4682b4;
            margin: 20px;
        }

        #puzzle-game {
            margin-top: 30px;
        }

        #puzzle-instructions {
            font-size: 1.5em;
            color: #4682b4;
        }

        /* Emoji style */
        .emoji {
            font-size: 2.5em;
            position: fixed;
            bottom: 0;
            animation: floatUp 8s ease-in-out;
            cursor: pointer;
        }

        @keyframes floatUp {
            0% {
                transform: translateY(100vh) scale(1);
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) scale(0.5);
                opacity: 0;
            }
        }

        /* Pop-up text style */
        .popup-text {
            font-size: 1.5em;
            color: #32cd32;
            position: absolute;
            opacity: 0;
            animation: popUpText 3s ease-in-out infinite;
        }

        @keyframes popUpText {
            0%, 100% {
                opacity: 0;
            }
            50% {
                opacity: 1;
            }
        }

        /* Cute border */
        body:before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            border: 10px solid #ffb6c1;
            pointer-events: none;
        }

        /* Puzzle game styles */
        #puzzle-container {
            display: flex;
            justify-content: center;
            margin: 30px;
        }

        #win-message {
            font-size: 2em;
            color: #32cd32;
            margin-top: 20px;
            display: none;
        }
    </style>
</head>
<body>

    <h1>Countdown to Your Birthday!</h1>
    <div id="countdown"></div>
    <div id="emoji-counter">Emojis Collected: <span id="counter">0</span></div>

    <!-- Puzzle Game Section -->
    <div id="puzzle-game">
        <div id="puzzle-instructions">Complete the puzzle to reveal a surprise!</div>
        <div id="puzzle-container">
            <!-- Puzzle iframe from an external puzzle maker -->
            <iframe src="https://www.jigsawexplorer.com/online-jigsaw-puzzle-player.html?puzzle-id=c0f8473cd44a" width="600" height="400"></iframe>
        </div>
        <div id="win-message">The gift is more than 2 things!</div>
    </div>

    <script>
        const targetDate = new Date('Oct 18, 2024 00:00:00').getTime();
        const countdownElement = document.getElementById('countdown');
        let emojiCounter = 0;

        function updateCountdown() {
            const now = new Date().getTime();
            const distance = targetDate - now;

            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            countdownElement.innerHTML = `${days}d ${hours}h ${minutes}m ${seconds}s`;
        }

        setInterval(updateCountdown, 1000);

        /* Emojis floating up */
        function createEmoji() {
            const emoji = document.createElement('div');
            emoji.classList.add('emoji');
            const emojis = ['🎈', '🎉', '💖', '🎁', '💙', '💗'];
            emoji.textContent = emojis[Math.floor(Math.random() * emojis.length)];
            emoji.style.left = Math.random() * window.innerWidth + 'px';
            document.body.appendChild(emoji);

            emoji.addEventListener('click', () => {
                emojiCounter++;
                document.getElementById('counter').textContent = emojiCounter;
                emoji.remove();
            });

            setTimeout(() => {
                emoji.remove();
            }, 8000);
        }

        setInterval(createEmoji, 2000);

        /* Pop-up text */
        function createPopUpText() {
            const popUp = document.createElement('div');
            popUp.classList.add('popup-text');
            const texts = ['You are my everything', 'I love you', 'So special to me!'];
            popUp.textContent = texts[Math.floor(Math.random() * texts.length)];
            popUp.style.left = Math.random() * window.innerWidth + 'px';
            popUp.style.top = Math.random() * window.innerHeight + 'px';
            document.body.appendChild(popUp);

            setTimeout(() => {
                popUp.remove();
            }, 3000);
        }

        setInterval(createPopUpText, 4000);
    </script>
</body>
</html>
