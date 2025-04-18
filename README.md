<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Interactive Quiz App</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #fdf2e9;
      display: flex;
      justify-content: center;
      padding: 40px;
    }
    .quiz-container {
      background: white;
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      width: 100%;
      max-width: 600px;
    }
    h1 {
      margin-bottom: 20px;
    }
    .question {
      font-size: 20px;
      margin-bottom: 15px;
    }
    .options button {
      display: block;
      margin: 8px 0;
      padding: 10px;
      width: 100%;
      font-size: 16px;
      cursor: pointer;
    }
    .feedback {
      margin-top: 15px;
      font-weight: bold;
    }
    .score {
      margin-top: 20px;
      font-size: 18px;
    }
  </style>
</head>
<body>

<div class="quiz-container">
  <h1>Interactive Quiz Application</h1>
  <div id="question" class="question"></div>
  <div class="options" id="options"></div>
  <div id="feedback" class="feedback"></div>
  <div id="score" class="score"></div>
</div>

<script>
  const quizData = [
    {
      question: "Which language runs in a web browser?",
      options: ["Java", "C", "Python", "JavaScript"],
      correct: "JavaScript"
    },
    {
      question: "What does CSS stand for?",
      options: ["Colorful Style Sheets", "Cascading Style Sheets", "Creative Style Syntax", "Computer Style Sheets"],
      correct: "Cascading Style Sheets"
    },
    {
      question: "What does HTML stand for?",
      options: ["HyperText Markup Language", "Home Tool Markup Language", "Hyperlink and Text Markup Language", "Hyper Tool Mark Language"],
      correct: "HyperText Markup Language"
    }
  ];

  let currentQuestion = 0;
  let score = 0;

  const questionEl = document.getElementById("question");
  const optionsEl = document.getElementById("options");
  const feedbackEl = document.getElementById("feedback");
  const scoreEl = document.getElementById("score");

  function loadQuestion() {
    const q = quizData[currentQuestion];
    questionEl.textContent = q.question;
    optionsEl.innerHTML = '';
    feedbackEl.textContent = '';

    q.options.forEach(option => {
      const btn = document.createElement("button");
      btn.textContent = option;
      btn.onclick = () => checkAnswer(option);
      optionsEl.appendChild(btn);
    });
  }

  function checkAnswer(selected) {
    const correct = quizData[currentQuestion].correct;
    if (selected === correct) {
      feedbackEl.textContent = "✅ Correct!";
      feedbackEl.style.color = "green";
      score++;
    } else {
      feedbackEl.textContent = `❌ Wrong! The correct answer is: ${correct}`;
      feedbackEl.style.color = "red";
    }
    scoreEl.textContent = `Score: ${score}/${quizData.length}`;

    setTimeout(() => {
      currentQuestion++;
      if (currentQuestion < quizData.length) {
        loadQuestion();
      } else {
        questionEl.textContent = "Quiz Completed!";
        optionsEl.innerHTML = '';
        feedbackEl.textContent = '';
      }
    }, 1500);
  }

  loadQuestion();
</script>

</body>
</html>
