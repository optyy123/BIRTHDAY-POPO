
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

        /* Puzzle styles */
        #puzzle-container {
            display: flex;
            justify-content: center;
            margin: 30px;
        }

        .draggable {
            width: 100px;
            height: 100px;
            margin: 10px;
            background-color: #ff69b4;
            border: 2px solid #000;
            display: inline-block;
            cursor: grab;
            font-size: 24px;
            color: white;
            display: flex;
            align-items: center;
            justify-content: center;
            user-select: none;
        }

        #puzzle-target {
            width: 350px;
            height: 100px;
            background-color: #fff;
            border: 2px dashed #4682b4;
            display: inline-block;
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

        /* Feedback Text */
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
        <div id="puzzle-instructions">Drag the blocks to complete the puzzle!</div>
        <div id="puzzle-container">
            <!-- Puzzle pieces -->
            <div class="draggable" draggable="true" id="piece1">A</div>
            <div class="draggable" draggable="true" id="piece2">B</div>
            <div class="draggable" draggable="true" id="piece3">C</div>
            <div class="draggable" draggable="true" id="piece4">D</div>
        </div>
        <!-- Puzzle Target -->
        <div id="puzzle-target"></div>
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

        /* Puzzle functionality */
        const pieces = document.querySelectorAll('.draggable');
        const target = document.getElementById('puzzle-target');
        let solved = false;

        pieces.forEach(piece => {
            piece.addEventListener('dragstart', dragStart);
            piece.addEventListener('dragend', dragEnd);
        });

        target.addEventListener('dragover', dragOver);
        target.addEventListener('drop', drop);

        function dragStart(e) {
            e.dataTransfer.setData('text', e.target.id);
        }

        function dragEnd() {
            // You can add visual feedback for dropping
        }

        function dragOver(e) {
            e.preventDefault();
        }

        function drop(e) {
            e.preventDefault();
            const pieceId = e.dataTransfer.getData('text');
            const piece = document.getElementById(pieceId);
            target.appendChild(piece);
            checkPuzzle();
        }

        function checkPuzzle() {
            if (target.children.length === 4) {
                // Puzzle is solved
                document.getElementById('win-message').style.display = 'block';
            }
        }
    </script>
</body>
</html>
