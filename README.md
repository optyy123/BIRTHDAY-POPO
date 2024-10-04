<!DOCTYPE html>
<html>
<head>
    <title>Countdown to Your Special Day! 🎉</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            background-color: #ffe4e1;
            background-image: url('https://your-link-to-background-image.com');
            background-size: cover;
            overflow: hidden;
            margin: 0;
            padding: 0;
            height: 100vh; /* Full view height */
        }
        h1 {
            color: #ff69b4;
            font-size: 2.5em;
        }
        #countdown {
            font-size: 2em;
            color: #ff4500;
        }
        #counter {
            font-size: 2em;
            color: #32CD32;
            margin-top: 20px;
        }
        .hidden {
            display: none;
        }
        .emoji {
            position: absolute;
            font-size: 2em;
            width: 60px;
            height: 60px;
            user-select: none;
            transition: transform 8s ease, opacity 0.5s ease;
        }
        @media (max-width: 768px) {
            h1 {
                font-size: 2em;
            }
            #countdown {
                font-size: 1.5em;
            }
            .emoji {
                font-size: 1.5em;
                width: 50px;
                height: 50px;
            }
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
        let counter = 0;

        // Function to apply slower, paper-like floating behavior
        function applySlowFloating(emoji) {
            let velocityY = Math.random() * -4 - 4; // Slow upward velocity
            let velocityX = (Math.random() - 0.5) * 3; // Slight horizontal movement
            const gravity = 0.03; // Low gravity for slow floating

            function updatePosition() {
                // Apply gravity and slight drag for smooth floating
                velocityY += gravity;
                velocityX *= 0.995;

                // Update the emoji's position
                const currentTop = parseFloat(emoji.style.top) || 0;
                const currentLeft = parseFloat(emoji.style.left) || 0;
                emoji.style.top = (currentTop + velocityY) + 'px';
                emoji.style.left = (currentLeft + velocityX) + 'px';

                // Keep applying the floating effect
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

                    // Touch or click event to count and make it disappear
                    emoji.addEventListener('click', () => {
                        emoji.style.transition = 'transform 0.5s ease, opacity 0.5s ease';
                        emoji.style.transform = 'scale(1.5) translateY(-150px)'; // Quick flight upward
                        emoji.style.opacity = '0';

                        // Show sparkle emoji when it disappears
                        setTimeout(() => {
                            emoji.innerText = '✨';
                            setTimeout(() => {
                                emoji.remove();
                            }, 500); // Remove emoji after sparkle effect
                        }, 500);

                        // Increment the counter
                        counter++;
                        document.getElementById('counter').innerText = `Touched Emojis: ${counter}`;
                    });

                    // Append emoji to container
                    emojiContainer.appendChild(emoji);

                    // Apply the slow floating effect
                    applySlowFloating(emoji);
                }, Math.random() * 1500); // Delay the emoji launches for randomness
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

    <div id="counter">Touched Emojis: 0</div>

    <div id="revealMessage" class="hidden reveal">
        <p>🎉 The wait is over! 🎉</p>
        <p>I'm bringing you something special for your birthday!</p>
        <img src="https://eshop.thrustmaster.com/media/catalog/product/cache/2cc11eadbe5979a7883b6a1bf56c2150/t/c/tcasidestickairbusedition.webp" alt="Gift Image" style="max-width: 300px;">
        <p>Can’t wait to see your reaction! ❤️</p>
    </div>
</body>
</html>
