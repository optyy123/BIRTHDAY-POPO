
<html>
<head>
    <title>Countdown to Your Special Day! 🎉</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            background-color: #ffe4e1;
            background-image: url('https://your-link-to-background-image.com');
            background-size: cover;
            overflow: hidden;
            position: relative;
            height: 100vh; /* Full view height */
        }
        h1 {
            color: #ff69b4;
            font-size: 3em;
        }
        #countdown {
            font-size: 2em;
            color: #ff4500;
        }
        .hidden {
            display: none;
        }
        button {
            background-color: #ff69b4;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #ff1493;
        }
        .emoji {
            position: absolute;
            font-size: 2em;
            user-select: none;
            cursor: pointer;
            transition: transform 5s ease, opacity 0.5s ease;
        }
    </style>
    <script>
        // Countdown timer variables
        var countDownDate = new Date("Oct 18, 2024 00:00:00").getTime();

        // Update the countdown every second
        var countdownFunction = setInterval(function() {
            var now = new Date().getTime();
            var distance = countDownDate - now;
            var days = Math.floor(distance / (1000 * 60 * 60 * 24));
            var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            var seconds = Math.floor((distance % (1000 * 60)) / 1000);
            document.getElementById("countdown").innerHTML = days + "d " + hours + "h " +
            minutes + "m " + seconds + "s ";

            if (distance < 0) {
                clearInterval(countdownFunction);
                document.getElementById("countdown").style.display = "none";
                document.getElementById("revealMessage").style.display = "block";
            }
        }, 1000);

        // Emojis array with balloons, confetti, and heart emojis
        const emojis = ['🎈', '🎉', '❤️', '💖', '💘'];

        // Function to apply slow, paper-like floating motion
        function applySlowFloating(emoji) {
            let velocityY = Math.random() * -2 - 3; // Very slow upward velocity
            let velocityX = (Math.random() - 0.5) * 2; // Slow horizontal movement
            const gravity = 0.2; // Small gravity factor for paper-like floating
            const drag = 0.98; // Drag for slight slowing effect

            function updatePosition() {
                // Apply gravity and drag for slow floating
                velocityY += gravity;
                velocityX *= drag;

                // Update the emoji's position
                const currentTop = parseFloat(emoji.style.top) || 0;
                const currentLeft = parseFloat(emoji.style.left) || 0;
                emoji.style.top = (currentTop + velocityY) + 'px';
                emoji.style.left = (currentLeft + velocityX) + 'px';

                // Remove emoji after 1 minute
                setTimeout(() => {
                    emoji.remove();
                }, 60000);

                // Keep applying physics for smooth floating
                requestAnimationFrame(updatePosition);
            }
            updatePosition();
        }

        // Function to throw emojis with slow floating behavior
        function throwEmojis() {
            const emojiContainer = document.createElement('div');
            document.body.appendChild(emojiContainer);

            // Generate a random number of emojis between 3 and 10
            const emojiCount = Math.floor(Math.random() * 8) + 3;

            for (let i = 0; i < emojiCount; i++) {
                setTimeout(() => {
                    const emoji = document.createElement('div');
                    emoji.innerText = emojis[Math.floor(Math.random() * emojis.length)];
                    emoji.classList.add('emoji');

                    // Set random initial position at the bottom
                    emoji.style.left = Math.random() * window.innerWidth + 'px';
                    emoji.style.top = window.innerHeight - 50 + 'px'; // Start near the bottom

                    // Make the emoji draggable/throwable
                    let isDragging = false;
                    let startX, startY;

                    // Mouse or touch start
                    emoji.addEventListener('mousedown', (e) => {
                        isDragging = true;
                        startX = e.clientX - parseInt(emoji.style.left);
                        startY = e.clientY - parseInt(emoji.style.top);
                    });

                    document.addEventListener('mousemove', (e) => {
                        if (isDragging) {
                            emoji.style.left = e.clientX - startX + 'px';
                            emoji.style.top = e.clientY - startY + 'px';
                        }
                    });

                    document.addEventListener('mouseup', () => {
                        if (isDragging) {
                            isDragging = false;
                            applySlowFloating(emoji); // Apply slow floating after it's thrown
                        }
                    });

                    // Touch events for mobile
                    emoji.addEventListener('touchstart', (e) => {
                        isDragging = true;
                        const touch = e.touches[0];
                        startX = touch.clientX - parseInt(emoji.style.left);
                        startY = touch.clientY - parseInt(emoji.style.top);
                    });

                    document.addEventListener('touchmove', (e) => {
                        if (isDragging) {
                            const touch = e.touches[0];
                            emoji.style.left = touch.clientX - startX + 'px';
                            emoji.style.top = touch.clientY - startY + 'px';
                        }
                    });

                    document.addEventListener('touchend', () => {
                        if (isDragging) {
                            isDragging = false;
                            applySlowFloating(emoji); // Apply slow floating after it's thrown
                        }
                    });

                    // Append emoji to container
                    emojiContainer.appendChild(emoji);

                    // Apply initial slow floating effect
                    applySlowFloating(emoji);
                }, Math.random() * 1000); // Delay the emoji launches for more randomness
            }
        }

        // Start throwing emojis immediately
        throwEmojis();
        setInterval(throwEmojis, 5000); // Re-throw emojis every 5 seconds
    </script>
</head>
<body>
    <h1>Countdown to Your Birthday! 🎂🎈</h1>
    <p>I'm so excited for your special day!</p>
    
    <div id="countdown"></div>

    <div id="revealMessage" class="hidden reveal">
        <p>🎉 The wait is over! 🎉</p>
        <p>I'm bringing you something special for your birthday!</p>
        <img src="https://eshop.thrustmaster.com/media/catalog/product/cache/2cc11eadbe5979a7883b6a1bf56c2150/t/c/tcasidestickairbusedition.webp" alt="Gift Image" style="max-width: 300px;">
        <p>Can’t wait to see your reaction! ❤️</p>
    </div>
</body>
</html>
