
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Birthday Countdown with Game</title>
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

        #minigame {
            margin-top: 30px;
        }

        #minigame-instructions {
            font-size: 1.5em;
            color: #4682b4;
        }

        #minigame-target {
            width: 100px;
            height: 100px;
            background-color: #ff6347;
            border-radius: 50%;
            display: inline-block;
            margin-top: 20px;
            cursor: pointer;
            position: relative;
            transition: all 0.3s ease;
        }

        .popup-text {
            position: absolute;
            background-color: rgba(255, 182, 193, 0.8);
            padding: 10px;
            border-radius: 10px;
            font-size: 1.2em;
            display: none;
            opacity: 0;
            transition: opacity 0.5s ease-in-out;
        }

        .popup-text.show {
            display: block;
            opacity: 1;
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

    <div id="minigame">
        <div id="minigame-instructions">Catch the red circle to win the game!</div>
        <div id="minigame-target"></div>
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

        /* Mini-game */
        const targetElement = document.getElementById('minigame-target');
        const winMessage = document.getElementById('win-message');
        let gameWon = false;

        function moveTarget() {
            if (!gameWon) {
                const randomX = Math.random() * (window.innerWidth - 100);
                const randomY = Math.random() * (window.innerHeight - 200);
                targetElement.style.left = randomX + 'px';
                targetElement.style.top = randomY + 'px';
            }
        }

        targetElement.addEventListener('click', () => {
            gameWon = true;
            targetElement.style.backgroundColor = "#32cd32";
            winMessage.style.display = 'block';
        });

        setInterval(moveTarget, 1500); // Moves target every 1.5 seconds
    </script>
</body>
</html>
