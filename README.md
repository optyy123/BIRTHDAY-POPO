<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Memory Lane Game</title>
    <link rel="stylesheet" href="styles.css"> <!-- Add your styles if needed -->
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-database.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f0f0;
            color: #333;
            text-align: center;
            padding: 20px;
        }

        #inputScreen {
            display: block;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            width: 300px;
        }

        input {
            width: 90%;
            padding: 10px;
            margin: 10px 0;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        button {
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            background-color: #007bff;
            color: #fff;
            cursor: pointer;
        }

        button:hover {
            background-color: #0056b3;
        }

        #questionDisplay {
            display: none;
            margin-top: 20px;
        }
    </style>
</head>
<body>

<h1>Memory Lane Game</h1>

<div id="inputScreen">
    <h2>Enter Your Questions</h2>
    <input type="text" id="q1" placeholder="Question 1" required>
    <input type="text" id="q2" placeholder="Question 2" required>
    <input type="text" id="q3" placeholder="Question 3" required>
    <input type="text" id="q4" placeholder="Question 4" required>
    <input type="text" id="q5" placeholder="Question 5" required>
    <button id="submitBtn">Submit Questions</button>
</div>

<div id="questionDisplay">
    <h2>Your Questions</h2>
    <p id="currentQuestion"></p>
    <button id="nextQuestion">Next Question</button>
    <button id="resetGame" style="display:none;">Reset Game</button>
</div>

<script>
// Your web app's Firebase configuration
const firebaseConfig = {
    apiKey: "AIzaSyCqAhFMKIlVqRrEOAyIuQijkEQ7-3y_khw",
    authDomain: "birthdaypopo-d0d0f.firebaseapp.com",
    databaseURL: "https://birthdaypopo-d0d0f-default-rtdb.firebaseio.com",
    projectId: "birthdaypopo-d0d0f",
    storageBucket: "birthdaypopo-d0d0f.appspot.com",
    messagingSenderId: "105525599505",
    appId: "1:105525599505:web:cf78dce1f7e474067cc0b0",
    measurementId: "G-BM5B8NFJDN"
};

// Initialize Firebase
const app = firebase.initializeApp(firebaseConfig);
const db = firebase.database();

let playerId = "player" + Date.now(); // Unique player ID
let questionsSubmitted = false;
let questionsArray = [];
let currentQuestionIndex = 0;

document.getElementById('submitBtn').addEventListener('click', function () {
    const q1 = document.getElementById('q1').value.trim();
    const q2 = document.getElementById('q2').value.trim();
    const q3 = document.getElementById('q3').value.trim();
    const q4 = document.getElementById('q4').value.trim();
    const q5 = document.getElementById('q5').value.trim();

    if (q1 && q2 && q3 && q4 && q5) {
        // Store questions in an array
        questionsArray = [q1, q2, q3, q4, q5];

        // Write to Firebase under the player's ID
        db.ref('memoryGame/players/' + playerId).set({
            questions: questionsArray
        });

        // Hide input screen and show question display
        document.getElementById('inputScreen').style.display = 'none';
        document.getElementById('questionDisplay').style.display = 'block';
        document.getElementById('currentQuestion').innerText = questionsArray[currentQuestionIndex];
        questionsSubmitted = true;
    } else {
        alert("Please enter all 5 questions.");
    }
});

// Next question button
document.getElementById('nextQuestion').addEventListener('click', function () {
    currentQuestionIndex++;
    if (currentQuestionIndex < questionsArray.length) {
        document.getElementById('currentQuestion').innerText = questionsArray[currentQuestionIndex];
    } else {
        document.getElementById('currentQuestion').innerText = "No more questions.";
        document.getElementById('nextQuestion').style.display = 'none';
        document.getElementById('resetGame').style.display = 'block';
    }
});

// Reset game button
document.getElementById('resetGame').addEventListener('click', function () {
    // Reset the game state
    currentQuestionIndex = 0;
    questionsSubmitted = false;
    questionsArray = [];
    document.getElementById('inputScreen').style.display = 'block';
    document.getElementById('questionDisplay').style.display = 'none';
    document.getElementById('resetGame').style.display = 'none';
    document.getElementById('currentQuestion').innerText = "";
    document.querySelectorAll('input').forEach(input => input.value = '');
});
</script>
</body>
</html>
