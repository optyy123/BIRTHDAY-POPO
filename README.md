
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Countdown to Her Birthday 🎉</title>
    <style>
        body {
            font-family: 'Comic Sans MS', cursive, sans-serif;
            background-color: #fff0f5;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            overflow: hidden;
            margin: 0;
            position: relative;
            text-align: center;
        }

        h1 {
            font-size: 3em;
            color: #ff69b4;
        }

        #countdown {
            font-size: 2em;
            color: #ff69b4;
        }

        #emoji-container {
            position: absolute;
            bottom: 0;
            width: 100%;
            pointer-events: none;
        }

        .emoji {
            font-size: 2em;
            position: absolute;
            bottom: -50px;
            animation: float 10s linear infinite;
            pointer-events: all;
        }

        @keyframes float {
            to {
                transform: translateY(-100vh);
            }
        }

        #emoji-counter {
            position: fixed;
            top: 10px;
            left: 10px;
            background-color: #ff69b4;
            color: white;
            padding: 10px;
            border-radius: 10px;
        }

        #popup-message {
            position: fixed;
            top: 50px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #ff69b4;
            color: white;
            padding: 15px;
            border-radius: 10px;
            display: none;
        }

        /* Puzzle and fade animation */
        #puzzle-game {
            display: none;
            background-color: #f8f8ff;
            padding: 20px;
            border: 2px solid #ff69b4;
            border-radius: 10px;
            margin-top: 20px;
        }

        .puzzle-piece {
            display: inline-block;
            background-color: #ff69b4;
            width: 50px;
            height: 50px;
            margin: 5px;
            border-radius: 5px;
            cursor: pointer;
        }

        /* Notification fade-in */
        .fade-in {
            animation: fadeIn 1s forwards;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }

        /* Random pop-up text */
        .popup-text {
            position: absolute;
            color: #ff69b4;
            font-size: 1.5em;
            animation: disappear 3s linear forwards;
        }

        @keyframes disappear {
            0%, 70% { opacity: 1; }
            100% { opacity: 0; }
        }
    </style>
</head>
<body>
    <h1>Countdown to Your Birthday 🎂</h1>
    <div id="countdown">...</div>

    <div id="emoji-container"></div>

    <div id="emoji-counter">Touched Emojis: 0</div>

    <div id="popup-message" class="fade-in">The gift is more than two 😉</div>

    <div id="puzzle-game">
        <h2>Solve the Puzzle 💖</h2>
        <div id="puzzle">
            <div class="puzzle-piece" data-piece="1"></div>
            <div class="puzzle-piece" data-piece="2"></div>
            <div class="puzzle-piece" data-piece="3"></div>
            <div class="puzzle-piece" data-piece="4"></div>
        </div>
    </div>

    <script>
        // Countdown timer
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
                // Show the birthday image after countdown
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
                emoji.remove();
                emojiCounter++;
                document.getElementById("emoji-counter").innerText = `Touched Emojis: ${emojiCounter}`;

                if (emojiCounter === 5) {
                    document.getElementById("puzzle-game").style.display = "block";
                    document.getElementById("popup-message").style.display = "block";
                }
            });

            emojiContainer.appendChild(emoji);

            // Remove emoji after 10 seconds
            setTimeout(() => emoji.remove(), 10000);
        }, 1500);

        // Random popup text
        const popUpMessages = ["You are my everything 💖", "I love you 💕", "You make my heart flutter 💘"];

        setInterval(() => {
            const randomMessage = document.createElement("div");
            randomMessage.innerText = popUpMessages[Math.floor(Math.random() * popUpMessages.length)];
            randomMessage.classList.add("popup-text");
            randomMessage.style.top = `${Math.random() * 80}%`;
            randomMessage.style.left = `${Math.random() * 80}%`;

            document.body.appendChild(randomMessage);

            // Remove the message after animation
            setTimeout(() => randomMessage.remove(), 3000);
        }, 3000);

        // Puzzle game interaction
        const puzzlePieces = document.querySelectorAll(".puzzle-piece");
        puzzlePieces.forEach(piece => {
            piece.addEventListener("click", () => {
                piece.style.backgroundColor = "#fff0f5";
                // Add more logic to complete the puzzle
            });
        });
    </script>
</body>
</html>
