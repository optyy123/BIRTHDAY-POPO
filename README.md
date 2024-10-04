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
            font-size: 2.5em;
            color: white;
            background-color: #ff69b4;
            padding: 10px 20px;
            border-radius: 50px;
            margin-top: 20px;
            display: inline-block;
            box-shadow: 0 0 10px rgba(255, 105, 180, 0.5);
        }
        .notification {
            font-size: 1.5em;
            color: #ffffff;
            background-color: #32CD32;
            padding: 10px;
            border-radius: 10px;
            margin-top: 20px;
            display: none;
        }
        .hidden {
            display: none;
        }
        .emoji {
            position: absolute;
            font-size: 2.5em;
            width: 120px; /* Larger hitbox */
            height: 120px;
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
                font-size: 2em;
                width: 100px;
                height: 100px;
            }
            #counter {
                font-size: 2em;
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
        let missedEmojis = 0;

        // Function to apply slow floating behavior
        function applySlowFloating(emoji) {
            let velocityY = Math.random() * -3 - 3; // Slow upward velocity
            let velocityX = (Math.random() - 0.5) * 3; // Slight horizontal movement
            const gravity = 0.02; // Slower fall due to gravity

            function updatePosition() {
                velocityY += gravity;
                velocityX *= 0.995;

                // Update the emoji's position
                const currentTop = parseFloat(emoji.style.top) || 0;
                const currentLeft = parseFloat(emoji.style.left) || 0;
                emoji.style.top = (currentTop + velocityY) + 'px';
                emoji.style.left = (currentLeft + velocityX) + 'px';

                // Remove emoji if it reaches the bottom of the screen (untouched)
                if (parseFloat(emoji.style.top) > window.innerHeight) {
                    emoji.remove();
                    missedEmojis++;
                    if (counter > 0) { // Only decrement if counter is above 0
                        counter--;
                        document.getElementById('counter').innerText = `Touched Emojis: ${counter}`;
                    }
                }

                requestAnimationFrame(updatePosition);
            }
            updatePosition();
        }

        // Function to throw emojis
        function throwEmojis() {
            const emojiContainer = document.createElement('div');
            document.body.appendChild(emojiContainer);

            // Reduce the number of emojis to between 1 and 2
            const emojiCount = Math.floor(Math.random() * 2) + 1;

            for (let i = 0; i < emojiCount; i++) {
                setTimeout(() => {
                    const emoji = document.createElement('div');
                    emoji.innerText = emojis[Math.floor(Math.random() * emojis.length)];
                    emoji.classList.add('emoji');

                    // Set random initial position at the bottom
                    emoji.style.left = Math.random() * window.innerWidth + 'px';
                    emoji.style.top = window.innerHeight - 50 + 'px';

                    // Click or touch event to increment counter and add sparkle
                    emoji.addEventListener('click', () => {
                        emoji.style.transition = 'transform 0.5s ease, opacity 0.5s ease';
                        emoji.style.transform = 'scale(1.5) translateY(-150px)';
                        emoji.style.opacity = '0';

                        // Show sparkle emoji and remove after sparkle
                        setTimeout(() => {
                            emoji.innerText = '✨';
                            setTimeout(() => {
                                emoji.remove();
                            }, 500);
                        }, 500);

                        // Increment counter
                        counter++;
                        document.getElementById('counter').innerText = `Touched Emojis: ${counter}`;

                        // Show notification after 5 touches
                        if (counter === 5) {
                            document.getElementById('notification').style.display = 'block';
                        }
                    });

                    // Append emoji to container
                    emojiContainer.appendChild(emoji);

                    applySlowFloating(emoji);
                }, Math.random() * 1500);
            }
        }

        // Start throwing emojis
        throwEmojis();
        setInterval(throwEmojis, 5000);
    </script>
</head>
<body>
    <h1>Countdown to Your Birthday! 🎂🎈</h1>
    <p>I'm so excited for your special day!</p>
    
    <div id="countdown"></div>

    <div id="counter">Touched Emojis: 0</div>

    <div id="notification" class="notification">
        There will be hints! 🔍🎁
    </div>

    <div id="revealMessage" class="hidden reveal">
        <p>🎉 The wait is over! 🎉</p>
        <p>I'm bringing you something special for your birthday!</p>
        <img src="https://eshop.thrustmaster.com/media/catalog/product/cache/2cc11eadbe5979a7883b6a1bf56c2150/t/c/tcasidestickairbusedition.webp" alt="Gift Image" style="max-width: 300px;">
        <p>Can’t wait to see your reaction! ❤️</p>
    </div>
</body>
</html>
