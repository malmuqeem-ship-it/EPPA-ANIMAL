<!doctype html>
<html lang="ar">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width,initial-scale=1">
  <title>لعبة أسئلة</title>
  <style>
    body{font-family:Tahoma,Arial;direction:rtl;padding:20px;background:#f7f7f7}
    .card{background:#fff;padding:20px;border-radius:8px;max-width:700px;margin:20px auto;box-shadow:0 2px 8px rgba(0,0,0,0.08)}
    h1{text-align:center}
    .options button{display:block;width:100%;margin:8px 0;padding:12px;border-radius:6px;border:1px solid #ddd;background:#fafafa;cursor:pointer}
    .options button.correct{background:#d4edda;border-color:#c3e6cb}
    .options button.wrong{background:#f8d7da;border-color:#f5c6cb}
    .meta{display:flex;justify-content:space-between;margin-top:10px;color:#555}
    #next{margin-top:12px}
  </style>
</head>
<body>
  <div class="card">
    <h1>لعبة أسئلة وأجوبة</h1>
    <div id="game">
      <div id="questionArea">
        <p id="questionText">...جاري التحميل</p>
        <div class="options" id="options"></div>
      </div>
      <div class="meta">
        <div>السؤال <span id="qIndex">0</span>/<span id="qTotal">0</span></div>
        <div>النقاط: <span id="score">0</span></div>
      </div>
      <button id="next" style="display:none">التالي</button>
    </div>
    <div id="result" style="display:none;text-align:center">
      <h2>انتهت اللعبة!</h2>
      <p>النقاط الكلية: <span id="finalScore"></span></p>
      <button id="restart">إعادة اللعب</button>
    </div>
  </div>

  <script>
    // قاعدة أسئلة بسيطة (يمكن تحميلها من ملف JSON خارجي)
    const questions = [
      { q: "ما عاصمة الإمارات؟", choices: ["دبي","أبو ظبي","الشارقة","عجمان"], a:1 },
      { q: "أكبر قارة من حيث المساحة؟", choices: ["أفريقيا","آسيا","أوروبا","أمريكا"], a:1 },
      { q: "هل الشمس نجم؟", choices: ["نعم","لا"], a:0 }
    ];

    let index = 0, score = 0;
    const qTotal = questions.length;
    document.getElementById('qTotal').textContent = qTotal;

    function showQuestion() {
      const q = questions[index];
      document.getElementById('questionText').textContent = q.q;
      const opts = document.getElementById('options');
      opts.innerHTML = '';
      q.choices.forEach((ch,i)=>{
        const btn = document.createElement('button');
        btn.textContent = ch;
        btn.onclick = () => selectAnswer(i, btn);
        opts.appendChild(btn);
      });
      document.getElementById('qIndex').textContent = index+1;
      document.getElementById('next').style.display = 'none';
    }

    function selectAnswer(i, btn) {
      const correct = questions[index].a;
      // منع النقر المتكرر
      Array.from(document.getElementById('options').children).forEach(b=>b.disabled=true);
      if (i === correct) {
        btn.classList.add('correct');
        score += 10; // نقاط لكل إجابة صحيحة
        document.getElementById('score').textContent = score;
      } else {
        btn.classList.add('wrong');
        // إبراز الإجابة الصحيحة
        const buttons = document.getElementById('options').children;
        buttons[correct].classList.add('correct');
      }
      // إظهار زر التالي أو النتيجة
      if (index < qTotal - 1) {
        document.getElementById('next').style.display = 'inline-block';
      } else {
        setTimeout(showResult, 800);
      }
    }

    document.getElementById('next').addEventListener('click', ()=>{
      index++;
      showQuestion();
    });

    function showResult(){
      document.getElementById('game').style.display='none';
      document.getElementById('finalScore').textContent = score;
      document.getElementById('result').style.display='block';
    }

    document.getElementById('restart').addEventListener('click', ()=>{
      index = 0; score = 0;
      document.getElementById('score').textContent = score;
      document.getElementById('game').style.display='block';
      document.getElementById('result').style.display='none';
      showQuestion();
    });

    // بدء اللعب
    showQuestion();
  </script>
</body>
</html>
