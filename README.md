<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel Pokémon sommeille en toi ?</title>
  <style>
    body {
      font-family: 'Verdana', sans-serif;
      background: linear-gradient(to bottom, #f5f5f5, #d1e8ff);
      color: #333;
      text-align: center;
      margin: 0;
      padding: 20px;
    }
    h1 {
      color: #e63946;
      font-size: 32px;
      margin-top: 20px;
    }
    img.logo {
      max-width: 250px;
      margin-bottom: 20px;
    }
    .question {
      background-color: #ffffff;
      border-radius: 12px;
      padding: 20px;
      margin: 20px auto;
      max-width: 600px;
      box-shadow: 0 0 10px rgba(0,0,0,0.1);
    }
    .options button {
      background-color: #48cae4;
      border: none;
      padding: 10px 20px;
      margin: 10px;
      font-size: 16px;
      cursor: pointer;
      border-radius: 8px;
      transition: background 0.3s;
    }
    .options button:hover {
      background-color: #0096c7;
      color: #fff;
    }
    .result {
      display: none;
      margin-top: 30px;
      background: #ffffff;
      padding: 20px;
      border-radius: 12px;
      max-width: 600px;
      margin-left: auto;
      margin-right: auto;
      box-shadow: 0 0 10px rgba(0,0,0,0.2);
    }
  </style>
</head>
<body>
  <img class="logo" src="https://zupimages.net/up/25/25/6rfv.png" alt="Logo Pokémon">
  <h1>Quel Pokémon sommeille en toi ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Tu es...</h2>
    <p id="result-text"></p>
    <button onclick="startQuiz()">Recommencer le quiz</button>
  </div>

  <script>
    const characters = [
      { name: "Pikachu", description: "Énergique et sociable, tu es l'étincelle de ton entourage.", score: 0 },
      { name: "Salamèche", description: "Courageux et passionné, tu avances malgré les obstacles.", score: 0 },
      { name: "Carapuce", description: "Loyal et calme, tu es toujours là pour tes amis.", score: 0 },
      { name: "Bulbizarre", description: "Posé et réfléchi, tu observes avant d’agir.", score: 0 },
      { name: "Évoli", description: "Flexible et curieux, tu évolues selon tes choix.", score: 0 },
      { name: "Mewtwo", description: "Mystérieux et puissant, ton esprit dépasse l’ordinaire.", score: 0 },
      { name: "Mew", description: "Joueur et énigmatique, tu caches un immense potentiel.", score: 0 },
      { name: "Rayquaza", description: "Serein et majestueux, tu fais respecter l’équilibre.", score: 0 },
      { name: "Lugia", description: "Protecteur discret, tu inspires le respect.", score: 0 },
      { name: "Suicune", description: "Noble et pur, tu agis toujours avec dignité.", score: 0 },
    ];

    const questions = [
      {
        question: "Quelle est ta qualité principale ?",
        answers: [
          { text: "Énergie et enthousiasme", scores: [0] },
          { text: "Détermination et feu intérieur", scores: [1] },
          { text: "Sérénité et loyauté", scores: [2, 8] },
          { text: "Discrétion et mystère", scores: [6, 7, 9] }
        ]
      },
      {
        question: "Comment réagis-tu face à un défi ?",
        answers: [
          { text: "Je fonce sans hésiter !", scores: [1] },
          { text: "Je m’adapte à la situation", scores: [4] },
          { text: "Je reste calme et j’analyse", scores: [3, 8] },
          { text: "Je fais appel à ma force intérieure", scores: [5, 6, 9] }
        ]
      },
      {
        question: "Ton élément préféré ?",
        answers: [
          { text: "Électricité", scores: [0] },
          { text: "Feu", scores: [1] },
          { text: "Eau", scores: [2, 9] },
          { text: "Air / Psy", scores: [5, 6, 7, 8] }
        ]
      },
      {
        question: "Avec qui préfères-tu passer du temps ?",
        answers: [
          { text: "Un groupe d'amis fidèles", scores: [0, 2, 4] },
          { text: "Seul avec mes pensées", scores: [5, 7] },
          { text: "Ma famille ou mes proches", scores: [1, 3] },
          { text: "Peu importe, du moment qu'on respecte mon espace", scores: [6, 8, 9] }
        ]
      }
    ];

    let currentQuestion = 0;

    function startQuiz() {
      currentQuestion = 0;
      characters.forEach(c => c.score = 0);
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;

      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';

      question.answers.forEach(answer => {
        const btn = document.createElement('button');
        btn.innerText = answer.text;
        btn.onclick = () => {
          answer.scores.forEach(i => characters[i].score++);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(btn);
      });
    }

    function showResult() {
      const best = characters.reduce((a, b) => a.score > b.score ? a : b);
      document.getElementById('result-text').innerText = `${best.name} : ${best.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    startQuiz();
  </script>
</body>
</html>
