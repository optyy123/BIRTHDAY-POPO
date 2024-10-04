
<html>
<head>
    <title>Countdown to Your Special Day! 🎉</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            text-align: center;
            background-color: #ffe4e1;
            background-image: url(''); /* You can add a birthday-themed background here */
            background-size: cover;
        }
        h1 {
            color: #ff69b4;
            font-size: 3em;
        }
        #countdown {
            font-size: 2em;
            color: #00FFFF;
        }
        .balloons {
            margin-top: 20px;
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
        .reveal {
            font-size: 1.5em;
            color: #32cd32;
        }
    </style>
    <script>
        // Set the date for her birthday
        var countDownDate = new Date("Oct 4, 2024 13:20:00").getTime();

        // Update the countdown every second
        var countdownFunction = setInterval(function() {

            // Get today's date and time
            var now = new Date().getTime();

            // Find the distance between now and the countdown date
            var distance = countDownDate - now;

            // Time calculations for days, hours, minutes, and seconds
            var days = Math.floor(distance / (1000 * 60 * 60 * 24));
            var hours = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            var minutes = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
            var seconds = Math.floor((distance % (1000 * 60)) / 1000);

            // Display the result in the element with id="countdown"
            document.getElementById("countdown").innerHTML = days + "d " + hours + "h " +
            minutes + "m " + seconds + "s ";

            // If the countdown is finished, show the reveal message and image
            if (distance < 0) {
                clearInterval(countdownFunction);
                document.getElementById("countdown").style.display = "none";
                document.getElementById("revealMessage").style.display = "block";
            }
        }, 1000);
    </script>
</head>
<body>
    <h1>Countdown to Your Birthday! 🎂🎈</h1>
    <p>I'm so excited for your special day!</p>
    
    <div id="countdown"></div>
    
    <div class="balloons">
        <img src="https://purepng.com/public/uploads/large/balloons-pxn.png" alt="Balloons" style="width:200px;">
        <!-- Add more birthday decoration images like balloons, confetti, cake, etc. -->
    </div>

    <div id="revealMessage" class="hidden reveal">
        <p>🎉 The wait is over! 🎉</p>
        <p>I'm bringing you something special for your birthday!</p>
        <img src="https://eshop.thrustmaster.com/media/catalog/product/cache/2cc11eadbe5979a7883b6a1bf56c2150/t/c/tcasidestickairbusedition.webp" alt="Gift Image" style="max-width: 300px;">
        <p>Can’t wait to see your reaction! ❤️</p>
    </div>

</body>
</html>
