
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Memory Lane Game</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f7f0f9;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            overflow: hidden;
            position: relative;
        }

        .container {
            background-color: #fff;
            border-radius: 15px;
            padding: 20px;
            box-shadow: 0px 4px 20px rgba(0, 0, 0, 0.1);
            text-align: center;
            width: 90%;
            max-width: 500px;
        }

        .container h1 {
            font-size: 24px;
            color: #ff69b4;
            margin-bottom: 20px;
        }

        .question-input {
            margin: 10px 0;
            width: 100%;
            padding: 10px;
            border: 2px solid #ff69b4;
            border-radius: 10px;
        }

        button {
            background-color: #ff69b4;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 10px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s ease;
        }

        button:hover {
            background-color: #ff4786;
        }

        .game-screen {
            display: none;
        }

        .question-display {
            font-size: 20px;
            margin-bottom: 20px;
        }

        #reset-btn {
            position: absolute;
            top: 10px;
            left: 10px;
            background-color: transparent;
            border: none;
            cursor: pointer;
            font-size: 14px;
            color: #ff69b4;
            padding: 5px;
        }
    </style>
</head>
<body>

    <div class="container" id="input-screen">
        <h1>Memory Lane Game</h1>
        <p>Enter 5 questions about your memories:</p>

        <!-- Question inputs -->
        <input class="question-input" type="text" id="q1" placeholder="Question 1">
        <input class="question-input" type="text" id="q2" placeholder="Question 2">
        <input class="question-input" type="text" id="q3" placeholder="Question 3">
        <input class="question-input" type="text" id="q4" placeholder="Question 4">
        <input class="question-input" type="text" id="q5" placeholder="Question 5">

        <!-- Submit button -->
        <button id="submit-btn">Submit Questions</button>
    </div>

    <div class="container game-screen" id="game-screen">
        <h1>Memory Lane Game</h1>
        <div class="question-display" id="question-display"></div>
        <button id="next-btn">Next Question</button>
    </div>

    <!-- Reset button -->
    <button id="reset-btn">Reset</button>

    <script>
        // Variables to store questions
        let playerQuestions = [];
        let currentQuestionIndex = 0;
        let otherPlayerSubmitted = false;

        const inputScreen = document.getElementById('input-screen');
        const gameScreen = document.getElementById('game-screen');
        const questionDisplay = document.getElementById('question-display');
        const submitBtn = document.getElementById('submit-btn');
        const nextBtn = document.getElementById('next-btn');
        const resetBtn = document.getElementById('reset-btn');

        // Submit Questions
        submitBtn.addEventListener('click', function () {
            const q1 = document.getElementById('q1').value.trim();
            const q2 = document.getElementById('q2').value.trim();
            const q3 = document.getElementById('q3').value.trim();
            const q4 = document.getElementById('q4').value.trim();
            const q5 = document.getElementById('q5').value.trim();

            if (q1 && q2 && q3 && q4 && q5) {
                playerQuestions = [q1, q2, q3, q4, q5];
                inputScreen.style.display = 'none';
                
                // Wait for the other player (simulate with a flag here)
                if (otherPlayerSubmitted) {
                    startGame();
                } else {
                    alert("Waiting for the other player to submit questions...");
                    otherPlayerSubmitted = true;
                }
            } else {
                alert("Please enter all 5 questions.");
            }
        });

        // Start the Game
        function startGame() {
            gameScreen.style.display = 'block';
            showQuestion();
        }

        // Show current question
        function showQuestion() {
            if (currentQuestionIndex < playerQuestions.length) {
                questionDisplay.textContent = playerQuestions[currentQuestionIndex];
            } else {
                questionDisplay.textContent = "Game over! You've answered all the questions!";
                nextBtn.style.display = 'none';
            }
        }

        // Next question button
        nextBtn.addEventListener('click', function () {
            currentQuestionIndex++;
            showQuestion();
        });

        // Reset button
        resetBtn.addEventListener('click', function () {
            location.reload();
        });
    </script>

</body>
</html>
