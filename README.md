
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
            justify-content: center;
            align-items: center;
            height: 100vh;
            overflow: hidden;
            position: relative;
            border: 10px solid #ff69b4;
            border-radius: 15px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
        }

        h1 {
            font-size: 3em;
            color: #ff69b4;
            margin-bottom: 0.5em;
        }

        #countdown {
            font-size: 2.5em;
            color: #ff1493;
            background-color: white;
            padding: 10px 20px;
            border-radius: 15px;
            box-shadow: 0 0 10px rgba(255, 20, 147, 0.6);
            margin-bottom: 20px;
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
            animation: float 10s linear infinite;
            pointer-events: all;
        }

        @keyframes float {
            to {
                transform: translateY(-100vh);
            }
        }

        .fly-away {
            animation: flyAway 1s ease-in-out forwards;
        }

        @keyframes flyAway {
            to {
                transform: translate(300px, -200px) scale(0);
                opacity: 0;
            }
        }

        #emoji-counter {
            position: fixed;
            top: 10px;
            left: 10px;
            background-color: #ff1493;
            color: white;
            font-size: 1.5em;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(255, 20, 147, 0.5);
            transition: transform 0.3s ease;
        }

        #emoji-counter.animated {
            transform: scale(1.1);
        }

        #popup-message {
            position: fixed;
            top: 50px;
            left: 50%;
            transform: translateX(-50%);
            background-color: #ff69b4;
            color: white;
            font-size: 1.5em;
            padding: 15px;
            border-radius: 15px;
            display: none;
            animation: fadeInOut 1s forwards, fadeOut 5s forwards;
        }

        @keyframes fadeInOut {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes fadeOut {
            from { opacity: 1; }
            to { opacity: 0; }
        }

        #puzzle-game {
            display: none;
            background-color: #f8f8ff;
            padding: 20px;
            border: 2px solid #ff69b4;
            border-radius: 10px;
            margin-top: 20px;
            text-align: center;
        }

        .puzzle-piece {
            display: inline-block;
            background-color: #ff69b4;
            width: 50px;
            height: 50px;
            margin: 5px;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        .puzzle-piece.solved {
            background-color: #ff1493;
        }

        .popup-text {
            position: absolute;
            color: #ff69b4;
            font-size: 1.8em;
            font-weight: bold;
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

    <div id="popup-message">The gift is more than two 😉</div>

    <div id="puzzle-game">
        <h2>Solve the Puzzle 💖</h2>
        <div id="puzzle">
            <div class="puzzle-piece" data-piece="1"></div>
            <div class="puzzle-piece" data-piece="2"></div>
            <div class="puzzle-piece" data-piece="3"></div>
            <div class="puzzle-piece" data-piece="4"></div>
            <div class="puzzle-piece" data-piece="5"></div>
            <div class="puzzle-piece" data-piece="6"></div>
            <div class="puzzle-piece" data-piece="7"></div>
            <div class="puzzle-piece" data-piece="8"></div>
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
                setTimeout(() => emoji.remove(), 1000);

                emojiCounter++;
                const emojiCounterElement = document.getElementById("emoji-counter");
                emojiCounterElement.innerText = `Touched Emojis: ${emojiCounter}`;
                emojiCounterElement.classList.add("animated");

                setTimeout(() => emojiCounterElement.classList.remove("animated"), 300);

                if (emojiCounter === 5) {
                    document.getElementById("puzzle-game").style.display = "block";
                    const popupMessage = document.getElementById("popup-message");
                    popupMessage.style.display = "block";
                    setTimeout(() => {
                        popupMessage.style.display = "none";
                    }, 5000);
                }
            });

            emojiContainer.appendChild(emoji);

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
            setTimeout(() => randomMessage.remove(), 3000);
        }, 3000);

        // Puzzle game interaction
        const puzzlePieces = document.querySelectorAll(".puzzle-piece");
        let solvedPieces = 0;
        puzzlePieces.forEach(piece => {
            piece.addEventListener("click", () => {
                piece.classList.add("solved");
                solvedPieces++;
                if (solvedPieces === puzzlePieces.length) {
                    alert("Puzzle Solved! 🎉");
                }
            });
        });
    </script>
</body>
</html>
