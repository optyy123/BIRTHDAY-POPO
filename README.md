
<html>
<head>
    <title>Countdown to Your Special Day! 🎉</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            background-color: #FFFFFF;
            background-image: url('');
            background-size: cover;
            overflow: hidden;
        }
        h1 {
            color: #ff69b4;
            font-size: 3em;
        }
        #countdown {
            font-size: 2em;
            color: #008B8B;
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
            bottom: -50px; /* Start below the screen */
            animation: floatUp 5s linear forwards;
        }
        @keyframes floatUp {
            0% {
                transform: translateY(0);
            }
            100% {
                transform: translateY(-100vh); /* Float upwards across the screen */
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

        // Function to throw random balloons and confetti from the bottom
        function throwEmojis() {
            const emojis = ['🎈', '🎉']; // Balloons and confetti
            const emojiContainer = document.createElement('div');
            document.body.appendChild(emojiContainer);

            // Generate a random number of emojis between 5 and 15
            const emojiCount = Math.floor(Math.random() * 11) + 5;

            for (let i = 0; i < emojiCount; i++) {
                const emoji = document.createElement('div');
                emoji.innerText = emojis[Math.floor(Math.random() * emojis.length)];
                emoji.classList.add('emoji');

                // Set random horizontal position for each emoji
                emoji.style.left = Math.random() * window.innerWidth + 'px';

                // Append emoji to the container
                emojiContainer.appendChild(emoji);

                // Remove the emoji after 5 seconds to avoid clutter
                setTimeout(() => {
                    emoji.remove();
                }, 5000);
            }
        }

        // Throw emojis every 5 seconds
        setInterval(throwEmojis, 5000);
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
