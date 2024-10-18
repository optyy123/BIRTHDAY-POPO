<!DOCTYPE html>
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
        .question-input {
            margin: 10px 0;
            padding: 10px;
            width: 100%;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        #next-btn {
            margin-top: 20px;
        }
    </style>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.6.1/firebase-database.js"></script>
    <script>
        // Your web app's Firebase configuration
        const firebaseConfig = {
            apiKey: "AIzaSyCqAhFMKIlVqRrEOAyIuQijkEQ7-3y_khw",                      // Replace with your actual API key
            authDomain: "birthdaypopo-d0d0f.firebaseapp.com",              // Replace with your actual Auth Domain
            databaseURL: "https://birthdaypopo-d0d0f-default-rtdb.firebaseio.com",  // Your Realtime Database URL
            projectId: "birthdaypopo-d0d0f",                 // Replace with your actual Project ID
            storageBucket: "birthdaypopo-d0d0f.appspot.com",         // Replace with your actual Storage Bucket
            messagingSenderId: "105525599505", // Replace with your actual Messaging Sender ID
            appId: "1:105525599505:web:cf78dce1f7e474067cc0b0"                          // Replace with your actual App ID
        };

        // Initialize Firebase
        const app = firebase.initializeApp(firebaseConfig);
        const db = firebase.database();

        // Variables
        const submitBtn = document.getElementById('submit-btn');
        const inputScreen = document.getElementById('input-screen');
        const gameScreen = document.getElementById('game-screen');
        const questionDisplay = document.getElementById('question-display');
        const nextBtn = document.getElementById('next-btn');
        const resetBtn = document.getElementById('reset-btn');

        let playerQuestions = [];
        let currentQuestionIndex = 0;
        let questionsSubmitted = false;

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

                // Store questions in Firebase
                const playerId = Math.random().toString(36).substr(2, 9); // Unique player ID
                firebase.database().ref('memoryGame/players/' + playerId).set({
                    questions: playerQuestions
                });

                // Wait for the other player
                questionsSubmitted = true;
                checkForOtherPlayer();
            } else {
                alert("Please enter all 5 questions.");
            }
        });

        // Check if the other player has submitted
        function checkForOtherPlayer() {
            firebase.database().ref('memoryGame/players').on('value', (snapshot) => {
                const players = snapshot.val();
                if (players && Object.keys(players).length === 2 && questionsSubmitted) {
                    // Both players have submitted questions
                    startGame(players);
                }
            });
        }

        // Start the Game
        function startGame(players) {
            gameScreen.style.display = 'block';
            let allQuestions = [];

            // Combine both players' questions
            for (let player in players) {
                allQuestions = allQuestions.concat(players[player].questions);
            }
            // Show the first question
            showQuestion(allQuestions);
        }

        // Show current question
        function showQuestion(allQuestions) {
            if (currentQuestionIndex < allQuestions.length) {
                questionDisplay.textContent = allQuestions[currentQuestionIndex];
            } else {
                questionDisplay.textContent = "Game over! You've answered all the questions!";
                nextBtn.style.display = 'none';
            }
        }

        // Next question button
        nextBtn.addEventListener('click', function () {
            currentQuestionIndex++;
            showQuestion(allQuestions);
        });

        // Reset button
        resetBtn.addEventListener('click', function () {
            firebase.database().ref('memoryGame').remove(); // Clear Firebase data
            location.reload(); // Reload the page
        });
    </script>
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

    <div class="container game-screen" id="game-screen" style="display: none;">
        <h1>Memory Lane Game</h1>
        <div class="question-display" id="question-display"></div>
        <button id="next-btn">Next Question</button>
    </div>

    <!-- Reset button -->
    <button id="reset-btn" style="display: none;">Reset</button>

</body>
</html>
