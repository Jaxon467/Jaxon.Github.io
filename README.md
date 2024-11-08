
  <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welsh Language Quiz</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <div id="quiz-container">
        <h1>Welsh Language Quiz</h1>
        <div id="quiz-content">
            <div id="question-container">
                <!-- Question and answer choices will be inserted here dynamically -->
            </div>
            <div id="navigation">
                <button id="next-btn" onclick="nextQuestion()">Next</button>
                <button id="prev-btn" onclick="prevQuestion()">Previous</button>
            </div>
            <div id="score-container">
                <button id="submit-btn" onclick="submitQuiz()">Submit Quiz</button>
                <p id="score">Score: 0/40</p>
            </div>
        </div>
        <div id="leaderboard-container">
            <h2>Leaderboard</h2>
            <ul id="leaderboard"></ul>
        </div>
    </div>

    <script src="quiz.js"></script>
</body>
</html>

<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f4f4f4;
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }

    #quiz-container {
        background-color: #fff;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
        width: 80%;
        max-width: 600px;
    }

    h1, h2 {
        text-align: center;
        color: #4CAF50;
    }

    #question-container {
        margin-bottom: 20px;
    }

    button {
        background-color: #4CAF50;
        color: white;
        border: none;
        padding: 10px 20px;
        margin: 5px;
        cursor: pointer;
        border-radius: 5px;
        font-size: 16px;
    }

    button:hover {
        background-color: #45a049;
    }

    button:disabled {
        background-color: #ccc;
    }

    #navigation {
        display: flex;
        justify-content: space-between;
    }

    #submit-btn {
        width: 100%;
        background-color: #2196F3;
    }

    #submit-btn:hover {
        background-color: #1e88e5;
    }

    #score-container {
        text-align: center;
    }

    #leaderboard-container {
        margin-top: 30px;
    }

    #leaderboard {
        list-style-type: none;
        padding: 0;
    }

    #leaderboard li {
        background-color: #f9f9f9;
        padding: 8px;
        margin: 5px 0;
        border-radius: 5px;
    }
</style>

</style>

<script>
// Define the questions and answers, including the 7 new questions
const questions = [
    { question: "What is the Welsh word for 'hello'?", options: ["Shwmae", "Diolch", "Bore da", "Nos da"], answer: "Shwmae" },
    { question: "What is the Welsh word for 'thank you'?", options: ["Diolch", "Shwmae", "Ysgol", "Bore da"], answer: "Diolch" },
    { question: "What does 'Bore da' mean in Welsh?", options: ["Good morning", "Good night", "How are you?", "See you later"], answer: "Good morning" },
    { question: "What is the Welsh word for 'goodbye'?", options: ["Hwyl fawr", "Shwmae", "Diolch", "Nos da"], answer: "Hwyl fawr" },
    { question: "What is the Welsh word for 'school'?", options: ["Ysgol", "Cegin", "Bwyd", "Ffôn"], answer: "Ysgol" },
    { question: "What does 'Diolch' mean?", options: ["Hello", "Thank you", "Goodbye", "Please"], answer: "Thank you" },
    { question: "What is the Welsh word for 'friend'?", options: ["Ffrind", "Teulu", "Mates", "Cydweithiwr"], answer: "Ffrind" },
    { question: "How do you say 'good evening' in Welsh?", options: ["Noswaith dda", "Bore da", "Shwmae", "Nos da"], answer: "Noswaith dda" },
    { question: "Which of these is a Welsh dish?", options: ["Cawl", "Pizza", "Sushi", "Tacos"], answer: "Cawl" },
    { question: "What is the Welsh word for 'dog'?", options: ["Ci", "Cath", "Llygoden", "Ebrill"], answer: "Ci" },
    { question: "How do you say 'please' in Welsh?", options: ["Os gwelwch yn dda", "Diolch", "Shwmae", "Hwyl fawr"], answer: "Os gwelwch yn dda" },
    { question: "What is the Welsh word for 'cat'?", options: ["Cath", "Ci", "Llygoden", "Mochyn"], answer: "Cath" },
    { question: "What is the Welsh word for 'book'?", options: ["Llyfr", "Car", "Bwrdd", "Blaen"], answer: "Llyfr" },
    { question: "How do you say 'good night' in Welsh?", options: ["Nos da", "Noswaith dda", "Bore da", "Hwyl fawr"], answer: "Nos da" },
    { question: "What is the Welsh word for 'mother'?", options: ["Mam", "Tad", "Chwaer", "Brawd"], answer: "Mam" },
    { question: "What is the Welsh word for 'father'?", options: ["Tad", "Mam", "Brawd", "Chwaer"], answer: "Tad" },
    { question: "What does 'Ydw' mean?", options: ["Yes", "No", "Maybe", "Please"], answer: "Yes" },
    { question: "What is the Welsh word for 'water'?", options: ["Dwr", "Bwyd", "Cwrw", "Cwr"], answer: "Dwr" },
    { question: "What is the Welsh word for 'bread'?", options: ["Bara", "Cacen", "Bwyd", "Ffrwythau"], answer: "Bara" },
    { question: "What does 'Mwynhau' mean?", options: ["Enjoy", "Eat", "Sleep", "Work"], answer: "Enjoy" },
    { question: "What is the Welsh word for 'apple'?", options: ["Afal", "Banana", "Portocala", "Eirin"], answer: "Afal" },
    { question: "How do you say 'excuse me' in Welsh?", options: ["Esgusodwch fi", "Prynhawn da", "Shwmae", "Hwyl fawr"], answer: "Esgusodwch fi" },
    { question: "What is the Welsh word for 'sun'?", options: ["Haul", "Seren", "Eira", "Bore"], answer: "Haul" },
    { question: "How do you say 'I love you' in Welsh?", options: ["’Cariad ti", "Ti’n dda", "Ydw", "Diolch"], answer: "’Cariad ti" },
    { question: "What does 'Teulu' mean?", options: ["Family", "Friend", "School", "Book"], answer: "Family" },
    { question: "What is the Welsh word for 'mountain'?", options: ["Mynydd", "Afon", "Coed", "Mor"], answer: "Mynydd" },
    { question: "What does 'Bore' mean?", options: ["Morning", "Night", "Afternoon", "Lunch"], answer: "Morning" },
    { question: "What is the Welsh word for 'lake'?", options: ["Llyn", "Afon", "Mynydd", "Coed"], answer: "Llyn" },
    { question: "What does 'Araf' mean?", options: ["Slow", "Fast", "Stop", "Go"], answer: "Slow" },
    { question: "What is the Welsh word for 'train'?", options: ["Tren", "Bws", "Car", "Ffôn"], answer: "Tren" },
    { question: "What does 'Cwtch' mean?", options: ["Hug", "Hello", "Sleep", "Love"], answer: "Hug" },
    { question: "What is the Welsh word for 'friendship'?", options: ["Cymdeithas", "Cyfeillgarwch", "Ffrind", "Ysgol"], answer: "Cyfeillgarwch" },
    { question: "What does 'Wyt ti'n iawn?' mean?", options: ["Are you okay?", "Good morning", "How are you?", "Where are you?"], answer: "Are you okay?" }
];

let currentQuestion = 0;
let score = 0;
let userAnswers = [];

// Update the question and options displayed on the page
function loadQuestion() {
    const question = questions[currentQuestion];
    const questionContainer = document.getElementById('question-container');
    const optionsContainer = document.createElement('div');
    optionsContainer.id = "options-container";
    
    questionContainer.innerHTML = `<h2>${question.question}</h2>`;
    question.options.forEach(option => {
        const optionButton = document.createElement('button');
        optionButton.innerText = option;
        optionButton.onclick = () => selectAnswer(option);
        optionsContainer.appendChild(optionButton);
    });
    
    questionContainer.appendChild(optionsContainer);
    updateNavigation();
}

// Handle answer selection
function selectAnswer(selectedOption) {
    const question = questions[currentQuestion];
    userAnswers[currentQuestion] = selectedOption;
    if (selectedOption === question.answer) {
        score++;
    }
    updateScore();
}

// Update the score on the page
function updateScore() {
    const scoreElement = document.getElementById('score');
    scoreElement.innerText = `Score: ${score}/${questions.length}`;
}

// Move to the next question
function nextQuestion() {
    if (currentQuestion < questions.length - 1) {
        currentQuestion++;
        loadQuestion();
    }
}

// Move to the previous question
function prevQuestion() {
    if (currentQuestion > 0) {
        currentQuestion--;
        loadQuestion();
    }
}

// Submit the quiz and display results
function submitQuiz() {
    alert(`You scored ${score} out of ${questions.length}`);
    updateLeaderboard(score);
}

// Update leaderboard (basic example with local storage)
function updateLeaderboard(score) {
    let leaderboard = JSON.parse(localStorage.getItem('leaderboard')) || [];
    const playerName = prompt("Enter your name for the leaderboard:");

    leaderboard.push({ name: playerName, score: score });
    leaderboard.sort((a, b) => b.score - a.score); // Sort by score in descending order
    localStorage.setItem('leaderboard', JSON.stringify(leaderboard));
    displayLeaderboard();
}

// Display the leaderboard
function displayLeaderboard() {
    const leaderboard = JSON.parse(localStorage.getItem('leaderboard')) || [];
    const leaderboardContainer = document.getElementById('leaderboard');

    leaderboardContainer.innerHTML = '';
    leaderboard.forEach(entry => {
        const listItem = document.createElement('li');
        listItem.innerText = `${entry.name}: ${entry.score}`;
        leaderboardContainer.appendChild(listItem);
    });
}

// Initialize the quiz
loadQuestion();
displayLeaderboard();
</script>
