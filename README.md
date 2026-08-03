# Naija---quiz---game-
A fun Nigeria trivia quiz game 
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Naija Quiz Game 🇳🇬</title>
<style>
    * { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Arial', sans-serif; }
  body {
    background: linear-gradient(135deg, #008751, #FFFFFF, #008751);
    min-height: 100vh; display: flex; align-items: center; justify-content: center; padding: 20px;
  }
 .container {
    background: white; border-radius: 20px; padding: 25px; max-width: 500px; width: 100%;
    box-shadow: 0 10px 30px rgba(0,0,0,0.2); text-align: center;
  }
  h1 { color: #008751; margin-bottom: 10px; font-size: 28px; }
 .score { font-size: 18px; color: #333; margin-bottom: 20px; font-weight: bold; }
 .question { font-size: 20px; color: #222; margin: 20px 0; font-weight: 600; }
 .options button {
    width: 100%; padding: 15px; margin: 8px 0; border: 2px solid #008751;
    border-radius: 12px; background: white; font-size: 16px; cursor: pointer;
    transition: 0.3s;
  }
 .options button:hover { background: #008751; color: white; }
 .options button.correct { background: #4CAF50; color: white; border-color: #4CAF50; }
 .options button.wrong { background: #f44336; color: white; border-color: #f44336; }
 .next-btn {
    margin-top: 15px; padding: 12px 25px; background: #008751; color: white;
    border: none; border-radius: 10px; font-size: 16px; cursor: pointer; display: none;
  }
 .result { font-size: 22px; color: #008751; margin-top: 20px; font-weight: bold; }
</style>
</head>
<body>
<div class="container">
  <h1>Naija Quiz Game 🇳🇬</h1>
  <div class="score">Score: <span id="score">0</span>/10</div>
  <div id="quiz">
    <div class="question" id="question">Loading...</div>
    <div class="options" id="options"></div>
    <button class="next-btn" id="nextBtn" onclick="nextQuestion()">Next Question</button>
  </div>
  <div id="result" class="result" style="display:none;"></div>
</div>

<script>
const questions = [
  { q: "What is the capital of Nigeria?", options: ["Lagos", "Abuja", "Kano", "Ibadan"], answer: 1 },
  { q: "Which food is made from pounded yam?", options: ["Jollof", "Amala", "Fufu", "Eba"], answer: 2 },
  { q: "What year did Nigeria gain independence?", options: ["1950", "1960", "1970", "1980"], answer: 1 },
  { q: "Who is known as 'African Giant'?", options: ["Wizkid", "Davido", "Burna Boy", "Olamide"], answer: 2 },
  { q: "Which river is the longest in Nigeria?", options: ["River Benue", "River Niger", "River Osun", "River Kaduna"], answer: 1 },
  { q: "What is the Nigerian currency?", options: ["Dollar", "Cedi", "Naira", "Franc"], answer: 2 },
  { q: "Which city is called 'Centre of Excellence'?", options: ["Abuja", "Port Harcourt", "Lagos", "Enugu"], answer: 2 },
  { q: "What does 'How far?' mean?", options: ["Goodbye", "How are you?", "I'm hungry", "Thank you"], answer: 1 },
  { q: "Which tribe is known for Aso Oke?", options: ["Igbo", "Hausa", "Yoruba", "Ijaw"], answer: 2 },
  { q: "What is Suya mostly made from?", options: ["Fish", "Chicken", "Beef", "Goat"], answer: 2 }
];

let currentQ = 0;
let score = 0;

function loadQuestion() {
  const q = questions[currentQ];
  document.getElementById('question').innerText = `Q${currentQ + 1}: ${q.q}`;
  const optionsDiv = document.getElementById('options');
  optionsDiv.innerHTML = '';
  q.options.forEach((opt, i) => {
    const btn = document.createElement('button');
    btn.innerText = opt;
    btn.onclick = () => checkAnswer(i, btn);
    optionsDiv.appendChild(btn);
  });
  document.getElementById('nextBtn').style.display = 'none';
}

function checkAnswer(selected, btn) {
  const correct = questions[currentQ].answer;
  const buttons = document.querySelectorAll('.options button');
