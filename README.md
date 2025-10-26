<!doctype html>
<html lang="ar">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>صدق أم إشاعة عن الحيوانات</title>
<style>
  body {
    margin: 0;
    font-family: "Tahoma", sans-serif;
    direction: rtl;
    background: linear-gradient(to bottom, #f4f1ea, #d9e7d2);
    color: #333;
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
  }
  .container {
    background: rgba(255,255,255,0.95);
    border-radius: 15px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.2);
    max-width: 700px;
    width: 90%;
    padding: 30px;
    text-align: center;
  }
  h1 {
    color: #2e7d32;
    margin-bottom: 15px;
  }
  .intro {
    font-size: 18px;
    margin-bottom: 25px;
  }
  button {
    font-size: 18px;
    padding: 12px 25px;
    margin: 10px;
    border-radius: 8px;
    border: none;
    cursor: pointer;
    transition: 0.2s;
  }
  #startBtn {
    background-color: #2e7d32;
    color: white;
  }
  #questionBox {
    display: none;
  }
  #questionBox img {
    max-width: 100%;
    border-radius: 10px;
    margin-bottom: 15px;
  }
  .choiceBtn {
    display: block;
    width: 100%;
    max-width: 300px;
    margin: 10px auto;
    background-color: #4caf50;
    color: #fff;
  }
  .choiceBtn.false {
    background-color: #f44336;
  }
  .choiceBtn:hover {
    opacity: 0.9;
  }
  #result, #explanation, #end {
    margin-top: 20px;
    font-size: 18px;
  }
  #nextBtn {
    background-color: #2e7d32;
    color: white;
    display: none;
  }
</style>
</head>
<body>
<div class="container">
  <div id="intro">
    <h1>صدق أم إشاعة عن الحيوانات</h1>
    <div class="intro">
      مرحبًا بك في لعبة صدق أم إشاعة عن الحيوانات! 🌿<br>
      اختبر معلوماتك واستمتع باكتشاف حقائق ممتعة عن عالم الصحراء.
    </div>
    <button id="startBtn">ابدأ اللعبة ▶️</button>
  </div>

  <div id="questionBox">
    <img src="https://upload.wikimedia.org/wikipedia/commons/1/18/Oryx_damma.jpg" alt="المها العربي">
    <div id="questionText">
      المها العربي لا يحتاج إلى الماء إطلاقًا ليعيش في الصحراء.
    </div>
    <button class="choiceBtn trueBtn">صدق ✅</button>
    <button class="choiceBtn falseBtn false">إشاعة ❌</button>
    <div id="result"></div>
    <div id="explanation"></div>
    <button id="nextBtn" onclick="restart()">التالي ▶️</button>
  </div>

  <div id="end" style="display:none;">
    <h2>أحسنت! 🌟</h2>
    <p>شكرًا لمشاركتك في لعبة صدق أم إشاعة عن الحيوانات.</p>
    <button onclick="restart()">إعادة اللعب 🔁</button>
  </div>
</div>

<script>
const startBtn = document.getElementById("startBtn");
const intro = document.getElementById("intro");
const questionBox = document.getElementById("questionBox");
const result = document.getElementById("result");
const explanation = document.getElementById("explanation");
const nextBtn = document.getElementById("nextBtn");
const end = document.getElementById("end");

startBtn.onclick = () => {
  intro.style.display = "none";
  questionBox.style.display = "block";
}

document.querySelector(".trueBtn").onclick = () => checkAnswer(true);
document.querySelector(".falseBtn").onclick = () => checkAnswer(false);

function checkAnswer(choice) {
  if(choice === false){
    result.textContent = "إجابة صحيحة ✅";
    explanation.textContent = "❌ إشاعة — صحيح أن المها العربي يستطيع البقاء لفترات طويلة دون شرب الماء بفضل تكيفه مع بيئة الصحراء القاسية، لكنه يشرب عندما يتوفر الماء ويستمد جزءًا من احتياجاته من النباتات التي يتغذى عليها. هذه القدرة المميزة تساعده على النجاة في أكثر المناطق جفافًا في الجزيرة العربية.";
  } else {
    result.textContent = "إجابة خاطئة ❌";
    explanation.textContent = "❌ إشاعة — صحيح أن المها العربي يستطيع البقاء لفترات طويلة دون شرب الماء بفضل تكيفه مع بيئة الصحراء القاسية، لكنه يشرب عندما يتوفر الماء ويستمد جزءًا من احتياجاته من النباتات التي يتغذى عليها. هذه القدرة المميزة تساعده على النجاة في أكثر المناطق جفافًا في الجزيرة العربية.";
  }
  nextBtn.style.display = "inline-block";
}

function restart() {
  result.textContent = "";
  explanation.textContent = "";
  nextBtn.style.display = "none";
  end.style.display = "none";
  questionBox.style.display = "block";
}
</script>
</body>
</html>