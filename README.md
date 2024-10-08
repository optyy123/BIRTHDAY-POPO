
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown to Her Birthday 🎉</title>
    <style>
        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            background-color: #fff0f5;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            text-align: center;
            border: 10px solid #ff69b4;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
        }

        h1 {
            font-size: 3em;
            color: #ff69b4;
            margin-bottom: 0.5em;
        }

        #countdown, #emoji-counter {
            font-size: 2.5em;
            color: #ff1493;
            background-color: white;
            padding: 10px 20px;
            border-radius: 15px;
            box-shadow: 0 0 10px rgba(255, 20, 147, 0.6);
            margin: 10px;
        }

        #emoji-container {
            position: absolute;
            bottom: 0;
            width: 100%;
            pointer-events: none;
        }

        .emoji {
            font-size: 2.5em;
            position: absolute;
            bottom: -50px;
            animation: floaty 8s ease-in-out infinite;
            pointer-events: all;
            transition: transform 0.8s ease-in-out, opacity 0.8s ease-in-out;
        }

        .fly-away {
            transform: translateY(-150vh) rotate(720deg) scale(0.5);
            opacity: 0;
        }

        @keyframes floaty {
            0% {
                transform: translateY(0);
            }
            50% {
                transform: translateY(-20px);
            }
            100% {
                transform: translateY(-100vh);
            }
        }

        /* Centered countdown and counter */
        #countdown-container {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        /* Glass-like popup background */
        .popup-text {
            position: absolute;
            color: #ff69b4;
            font-size: 1.8em;
            font-weight: bold;
            background: rgba(255, 255, 255, 0.2);
            backdrop-filter: blur(10px);
            border-radius: 10px;
            padding: 10px 20px;
            box-shadow: 0 0 10px rgba(255, 182, 193, 0.6);
            animation: disappear 3s linear forwards;
        }

        @keyframes disappear {
            0%, 70% { opacity: 1; }
            100% { opacity: 0; }
        }

        /* Notification for after the puzzle is solved */
        #gift-message {
            position: absolute;
            top: 100px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #ff69b4;
            color: white;
            font-size: 1.5em;
            padding: 15px;
            border-radius: 15px;
            display: none;
            animation: fadeIn 1s forwards;
            text-align: center;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        #puzzle-game {
            display: none;
            background-color: #f8f8ff;
            padding: 20px;
            border: 2px solid #ff69b4;
            border-radius: 10px;
            margin-top: 20px;
        }

        /* Puzzle game */
        .puzzle-piece {
            display: inline-block;
            background-color: #ff69b4;
            width: 60px;
            height: 60px;
            margin: 5px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .puzzle-piece.correct {
            background-color: #ff1493;
        }
    </style>
</head>
<body>
    <h1>Countdown to Your Birthday 🎂</h1>

    <div id="countdown-container">
        <div id="countdown">...</div>
        <div id="emoji-counter">Touched Emojis: 0</div>
    </div>

    <div id="emoji-container"></div>

    <div id="gift-message">The gift is more than two 😉🎁🎈</div>

    <div id="puzzle-game">
        <h2>Solve the Puzzle 💖</h2>
        <div id="puzzle">
            <!-- Example puzzle: Arrange numbers in ascending order -->
            <div class="puzzle-piece" data-piece="4">4</div>
            <div class="puzzle-piece" data-piece="1">1</div>
            <div class="puzzle-piece" data-piece="3">3</div>
            <div class="puzzle-piece" data-piece="2">2</div>
        </div>
    </div>

    <script>
        // Countdown Timer
        const countdownDate = new Date("Oct 18, 2024 00:00:00").getTime();
        const countdownElement = document.getElementById("countdown");

        const countdown = setInterval(() => {
            const now = new Date().getTime();
            const distance = countdownDate - now;

            const days = Math.floor(distance / (1000 * 60 * 60 * 24));
            const hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((distance % (1000 * 60)) / 1000);

            countdownElement.innerHTML = `${days}d ${hours}h ${minutes}m ${seconds}s`;

            if (distance < 0) {
                clearInterval(countdown);
                countdownElement.innerHTML = "It's your birthday! 🎁";
                document.body.innerHTML = "<h1>Happy Birthday! 🎉</h1><img src='path-to-gift-image.jpg' alt='Gifts'>";
            }
        }, 1000);

        // Floating emojis
        const emojiContainer = document.getElementById("emoji-container");
        const emojiList = ['❤️', '🎈', '🎁'];
        let emojiCounter = 0;

        setInterval(() => {
            const emoji = document.createElement("div");
            emoji.innerHTML = emojiList[Math.floor(Math.random() * emojiList.length)];
            emoji.classList.add("emoji");
            emoji.style.left = `${Math.random() * 100}%`;

            emoji.addEventListener("click", () => {
                emoji.classList.add("fly-away");

                setTimeout(() => emoji.remove(), 800);  // Remove emoji after it flies away

                emojiCounter++;
                document.getElementById("emoji-counter").innerText = `Touched Emojis: ${emojiCounter}`;

                if (emojiCounter === 5) {
                    document.getElementById("puzzle-game").style.display = "block";
                }
            });

            emojiContainer.appendChild(emoji);

            setTimeout(() => emoji.remove(), 10000); // Remove emoji after 10 seconds if not clicked
        }, 1500);

        // Random pop-up text with glass effect
        const popUpMessages = ["You are my everything 💖", "I love you 💕", "You make my heart flutter 💘"];

        setInterval(() => {
            const randomMessage = document.createElement("div");
            randomMessage.innerText = popUpMessages[Math.floor(Math.random() * popUpMessages.length)];
            randomMessage.classList.add("popup-text");
            randomMessage.style.top = `${Math.random() * 80}%`;
            randomMessage.style.left = `${Math.random() * 80}%`;

            document.body.appendChild(randomMessage);
            setTimeout(() => randomMessage.remove(), 3000);
        }, 3000);

        // Puzzle game logic (simple reordering puzzle)
        const puzzlePieces = document.querySelectorAll(".puzzle-piece");
        let currentOrder = [];

        puzzlePieces.forEach(piece => {
            piece.addEventListener("click", () => {
                currentOrder.push(parseInt(piece.dataset.piece));

                // Check if the order is correct
                if (currentOrder.length === 4) {
                    const isCorrect = JSON.stringify(currentOrder) === JSON.stringify([1, 2, 3, 4]);
                    if (isCorrect) {
                        document.getElementById("gift-message").style.display = "block";
                    }
                    currentOrder = [];  // Reset the order after checking
                }
            });
        });
    </script>
</body>
</html>
