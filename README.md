# KhaledB
# 🔧 حل مشكلة "Invalid Link"

الرابط الذي ظهر لك هو **رابط نشر مؤقت** من منصة Qwen، وهذه الروابط **تنتهي صلاحيتها تلقائياً** بعد فترة قصيرة.

## ✅ الحل: احفظ اللعبة كملف HTML على جهازك

انسخ الكود التالي واحفظه في ملف باسم `game.html` ثم افتحه بأي متصفح:

```html
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>لعبة كلمات - B.Khaled</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  
  body {
    font-family: 'Tajawal', 'Amiri', 'Segoe UI', Tahoma, sans-serif;
    overflow: hidden;
    height: 100vh;
    width: 100vw;
    transition: background 1s ease;
    background: #1a2a5e;
  }

  .screen {
    position: absolute;
    inset: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 20px;
    opacity: 0;
    pointer-events: none;
    transition: opacity 0.6s ease;
  }

  .screen.active {
    opacity: 1;
    pointer-events: all;
  }

  #welcome {
    background: linear-gradient(135deg, #0f1e4a 0%, #1a2a5e 50%, #2a3a7e 100%);
    text-align: center;
    color: white;
  }

  .welcome-logo {
    width: 260px;
    height: 260px;
    border-radius: 50%;
    background: radial-gradient(circle, #ffffff 0%, #e8e8e8 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 30px;
    box-shadow: 0 20px 60px rgba(0,0,0,0.4);
    position: relative;
    animation: floatLogo 3s ease-in-out infinite;
  }

  @keyframes floatLogo {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
  }

  .welcome-logo::before {
    content: '';
    position: absolute;
    inset: -15px;
    border-radius: 50%;
    border: 3px solid gold;
    opacity: 0.6;
  }

  .welcome-title {
    font-size: 3rem;
    font-weight: 900;
    color: #ffd700;
    text-shadow: 0 4px 20px rgba(255, 215, 0, 0.4);
    margin-bottom: 20px;
  }

  .welcome-message {
    font-size: 1.5rem;
    max-width: 600px;
    line-height: 1.8;
    margin-bottom: 40px;
    color: #f0f0f0;
  }

  .btn-start {
    background: linear-gradient(135deg, #ffd700, #ffaa00);
    color: #1a2a5e;
    border: none;
    padding: 18px 60px;
    font-size: 1.5rem;
    font-weight: 900;
    font-family: inherit;
    border-radius: 50px;
    cursor: pointer;
    box-shadow: 0 10px 30px rgba(255, 170, 0, 0.4);
    transition: all 0.3s ease;
    animation: pulse 2s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.05); }
  }

  .btn-start:hover { transform: scale(1.1); }

  .welcome-footer {
    position: absolute;
    bottom: 25px;
    color: rgba(255,255,255,0.7);
    font-size: 1rem;
  }

  #game { padding: 15px; }

  .game-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%;
    max-width: 700px;
    margin-bottom: 15px;
    color: white;
  }

  .category-badge, .score-display {
    background: rgba(255,255,255,0.2);
    backdrop-filter: blur(10px);
    padding: 8px 20px;
    border-radius: 25px;
    font-size: 1rem;
    font-weight: 700;
    border: 2px solid rgba(255,255,255,0.3);
  }

  .progress-bar {
    width: 100%;
    max-width: 700px;
    height: 8px;
    background: rgba(255,255,255,0.2);
    border-radius: 4px;
    margin-bottom: 20px;
    overflow: hidden;
  }

  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, #ffd700, #ffaa00);
    border-radius: 4px;
    transition: width 0.5s ease;
  }

  .stamp-logo {
    width: 180px;
    height: 140px;
    background: linear-gradient(180deg, #ffffff 0%, #e0e0e0 100%);
    position: relative;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 10px 30px rgba(0,0,0,0.3);
  }

  .stamp-logo-text {
    font-size: 3.5rem;
    font-weight: 900;
    color: #1a2a5e;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
  }

  .question-container {
    background: rgba(0,0,0,0.2);
    backdrop-filter: blur(10px);
    padding: 25px 35px;
    border-radius: 20px;
    margin-bottom: 30px;
    max-width: 700px;
    width: 100%;
    text-align: center;
    border: 2px solid rgba(255,255,255,0.2);
  }

  .question-text {
    font-size: 1.8rem;
    font-weight: 700;
    color: white;
    line-height: 1.6;
  }

  .answer-slots {
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-bottom: 30px;
    flex-wrap: wrap;
    max-width: 700px;
  }

  .answer-slot {
    width: 70px;
    height: 70px;
    background: linear-gradient(180deg, #ffffff 0%, #e8e8e8 100%);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    font-weight: 900;
    color: #1a2a5e;
    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .answer-slot.filled {
    background: linear-gradient(180deg, #ffd700 0%, #ffaa00 100%);
    animation: slotFill 0.4s ease;
  }

  .answer-slot.correct {
    background: linear-gradient(180deg, #4CAF50 0%, #2E7D32 100%);
    color: white;
    animation: correctPulse 0.6s ease;
  }

  .answer-slot.wrong {
    background: linear-gradient(180deg, #f44336 0%, #c62828 100%);
    color: white;
    animation: shake 0.5s ease;
  }

  @keyframes slotFill {
    0% { transform: scale(1); }
    50% { transform: scale(1.15); }
    100% { transform: scale(1); }
  }

  @keyframes correctPulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.2); }
  }

  @keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-10px); }
    75% { transform: translateX(10px); }
  }

  .letters-container {
    display: flex;
    justify-content: center;
    gap: 10px;
    flex-wrap: wrap;
    max-width: 700px;
  }

  .letter-btn {
    width: 70px;
    height: 70px;
    background: linear-gradient(180deg, #ffffff 0%, #e8e8e8 100%);
    border-radius: 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    font-weight: 900;
    color: #1a2a5e;
    cursor: pointer;
    box-shadow: 0 5px 15px rgba(0,0,0,0.3);
    transition: all 0.3s ease;
    user-select: none;
  }

  .letter-btn:hover:not(.used) {
    transform: translateY(-5px) scale(1.05);
  }

  .letter-btn.used {
    opacity: 0.3;
    cursor: not-allowed;
    transform: scale(0.9);
  }

  .controls {
    display: flex;
    gap: 15px;
    margin-top: 25px;
  }

  .btn-control {
    background: rgba(255,255,255,0.2);
    backdrop-filter: blur(10px);
    color: white;
    border: 2px solid rgba(255,255,255,0.4);
    padding: 12px 30px;
    font-size: 1.1rem;
    font-weight: 700;
    font-family: inherit;
    border-radius: 25px;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .btn-control:hover {
    background: rgba(255,255,255,0.3);
    transform: translateY(-3px);
  }

  .btn-hint {
    background: rgba(255, 215, 0, 0.3);
    border-color: #ffd700;
    color: #ffd700;
  }

  #end {
    background: linear-gradient(135deg, #0f1e4a 0%, #1a2a5e 50%, #2a3a7e 100%);
    text-align: center;
    color: white;
  }

  .end-title {
    font-size: 3rem;
    font-weight: 900;
    color: #ffd700;
    margin-bottom: 20px;
  }

  .end-score { font-size: 2rem; margin-bottom: 15px; }
  .end-message { font-size: 1.5rem; margin-bottom: 30px; color: #f0f0f0; }

  .end-footer {
    position: absolute;
    bottom: 25px;
    color: rgba(255,255,255,0.8);
    font-size: 1.1rem;
    font-weight: 700;
  }

  .end-footer span { color: #ffd700; font-weight: 900; }

  .feedback {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%) scale(0);
    font-size: 4rem;
    font-weight: 900;
    color: white;
    text-shadow: 0 5px 20px rgba(0,0,0,0.5);
    z-index: 100;
    pointer-events: none;
  }

  .feedback.show {
    animation: feedbackPop 1.5s ease forwards;
  }

  @keyframes feedbackPop {
    0% { transform: translate(-50%, -50%) scale(0); opacity: 0; }
    30% { transform: translate(-50%, -50%) scale(1.3); opacity: 1; }
    70% { transform: translate(-50%, -50%) scale(1); opacity: 1; }
    100% { transform: translate(-50%, -50%) scale(1); opacity: 0; }
  }

  .confetti {
    position: fixed;
    width: 10px;
    height: 10px;
    top: -10px;
    z-index: 99;
    animation: confettiFall 3s linear forwards;
  }

  @keyframes confettiFall {
    0% { transform: translateY(0) rotate(0deg); opacity: 1; }
    100% { transform: translateY(100vh) rotate(720deg); opacity: 0; }
  }

  @media (max-width: 600px) {
    .welcome-title { font-size: 2rem; }
    .welcome-message { font-size: 1.1rem; }
    .question-text { font-size: 1.3rem; }
    .answer-slot, .letter-btn { width: 50px; height: 50px; font-size: 1.5rem; }
    .stamp-logo { width: 140px; height: 110px; }
    .stamp-logo-text { font-size: 2.5rem; }
    .welcome-logo { width: 200px; height: 200px; }
    .feedback { font-size: 2.5rem; }
  }
</style>
</head>
<body>

<div id="welcome" class="screen active">
  <div class="welcome-logo">
    <div class="stamp-logo-text" style="font-size:3rem;">كلمات</div>
  </div>
  <div class="welcome-title">🎮 لعبة كلمات 🎮</div>
  <div class="welcome-message">
    مرحبا بيكم عند خالد،<br>
    نتمنى لكم وقت ممتع أحبائي 
  </div>
  <button class="btn-start" onclick="startGame()">ابدأ اللعب 🚀</button>
  <div class="welcome-footer">صممت هذه اللعبة من طرف <strong>B.Khaled</strong></div>
</div>

<div id="game" class="screen">
  <div class="game-header">
    <div class="category-badge" id="categoryBadge">🕌 دينية</div>
    <div class="score-display" id="scoreDisplay">النقاط: 0</div>
  </div>
  <div class="progress-bar">
    <div class="progress-fill" id="progressFill" style="width: 0%"></div>
  </div>
  <div class="stamp-logo">
    <div class="stamp-logo-text">كلمات</div>
  </div>
  <div class="question-container">
    <div class="question-text" id="questionText">السؤال هنا</div>
  </div>
  <div class="answer-slots" id="answerSlots"></div>
  <div class="letters-container" id="lettersContainer"></div>
  <div class="controls">
    <button class="btn-control btn-hint" onclick="showHint()">💡 تلميح</button>
    <button class="btn-control" onclick="resetCurrent()">🔄 إعادة</button>
  </div>
</div>

<div id="end" class="screen">
  <div class="end-title">🎉 انتهت اللعبة! </div>
  <div class="end-score" id="endScore">نتيجتك: 0 / 10</div>
  <div class="end-message" id="endMessage">أحسنت!</div>
  <button class="btn-start" onclick="restartGame()">العب مرة أخرى 🔄</button>
  <div class="end-footer">صممت هذه اللعبة من طرف <span>B.Khaled</span></div>
</div>

<div class="feedback" id="feedback"></div>

<script>
const questions = [
  { category: "دينية", icon: "🕌", question: "من هو النبي الذي لُقّب بجد العرب؟", answer: "إسماعيل", hint: "ابن إبراهيم عليه السلام" },
  { category: "دينية", icon: "🕌", question: "ما هي أول سورة في القرآن الكريم؟", answer: "الفاتحة", hint: "تسمى أم الكتاب" },
  { category: "دينية", icon: "🕌", question: "من هو خاتم الأنبياء والمرسلين؟", answer: "محمد", hint: "النبي الأمي" },
  { category: "دينية", icon: "🕌", question: "كم عدد أركان الإسلام؟", answer: "خمسة", hint: "رقم بعد 4" },
  { category: "تاريخ", icon: "📜", question: "من هو أول خليفة في الإسلام؟", answer: "أبوبكر", displayAnswer: "أبو بكر", hint: "الصديق" },
  { category: "تاريخ", icon: "📜", question: "من هو مؤسس الدولة الأموية؟", answer: "معاوية", hint: "أول الخلفاء الأمويين" },
  { category: "تاريخ", icon: "📜", question: "ما اسم المعركة الأولى في الإسلام؟", answer: "بدر", hint: "وقعت في رمضان" },
  { category: "جغرافيا", icon: "🌍", question: "ما هو أطول نهر في العالم؟", answer: "النيل", hint: "يجري في أفريقيا" },
  { category: "جغرافيا", icon: "🌍", question: "ما هي أكبر قارة في العالم؟", answer: "آسيا", hint: "تضم الصين والهند" },
  { category: "جغرافيا", icon: "", question: "ما هو أعلى جبل في العالم؟", answer: "إيفرست", hint: "يقع في نيبال" },
  { category: "عواصم", icon: "️", question: "ما هي عاصمة السعودية؟", answer: "الرياض", hint: "تقع في وسط المملكة" },
  { category: "عواصم", icon: "️", question: "ما هي عاصمة مصر؟", answer: "القاهرة", hint: "مدينة الألف مئذنة" },
  { category: "عواصم", icon: "️", question: "ما هي عاصمة فرنسا؟", answer: "باريس", hint: "مدينة النور" },
  { category: "عواصم", icon: "🏛️", question: "ما هي عاصمة اليابان؟", answer: "طوكيو", hint: "أكبر مدن اليابان" },
  { category: "رياضة", icon: "⚽", question: "كم عدد لاعبي فريق كرة القدم؟", answer: "أحدعشر", displayAnswer: "11", hint: "رقم بين 10 و 12" },
  { category: "رياضة", icon: "", question: "أين أقيمت كأس العالم 2022؟", answer: "قطر", hint: "دولة خليجية" },
  { category: "رياضة", icon: "⚽", question: "ما الرياضة التي تُلعب بالمضرب؟", answer: "تنس", hint: "Wimbledon" },
  { category: "ثقافة", icon: "", question: "كم عدد ألوان قوس قزح؟", answer: "سبعة", hint: "رقم بعد 6" },
  { category: "ثقافة", icon: "📚", question: "ما هي اللغة الأكثر تحدثاً؟", answer: "الصينية", hint: "لغة أكبر دولة سكاناً" },
  { category: "بلدان", icon: "🌐", question: "ما أكبر دولة في العالم مساحة؟", answer: "روسيا", hint: "تمتد من أوروبا لآسيا" },
  { category: "بلدان", icon: "🌐", question: "ما الدولة الملقبة ببلد المليون شهيد؟", answer: "الجزائر", hint: "دولة مغاربية" },
];

const categoryColors = {
  "دينية": "linear-gradient(135deg, #1a4a3a 0%, #0d2818 50%, #1a4a3a 100%)",
  "تاريخ": "linear-gradient(135deg, #4a2a1a 0%, #28150d 50%, #4a2a1a 100%)",
  "جغرافيا": "linear-gradient(135deg, #1a3a5e 0%, #0d1f3a 50%, #1a3a5e 100%)",
  "عواصم": "linear-gradient(135deg, #5e1a4a 0%, #3a0d28 50%, #5e1a4a 100%)",
  "رياضة": "linear-gradient(135deg, #2a5e1a 0%, #153a0d 50%, #2a5e1a 100%)",
  "ثقافة": "linear-gradient(135deg, #4a1a5e 0%, #280d3a 50%, #4a1a5e 100%)",
  "بلدان": "linear-gradient(135deg, #5e4a1a 0%, #3a280d 50%, #5e4a1a 100%)"
};

let currentQuestionIndex = 0;
let score = 0;
let currentAnswer = "";
let selectedLetters = [];
let shuffledQuestions = [];
let audioCtx = null;

function initAudio() {
  if (!audioCtx) {
    try { audioCtx = new (window.AudioContext || window.webkitAudioContext)(); } catch(e) {}
  }
}

function playTone(freq, type, duration, delay) {
  if (!audioCtx) return;
  const now = audioCtx.currentTime + delay;
  const osc = audioCtx.createOscillator();
  const gain = audioCtx.createGain();
  osc.connect(gain);
  gain.connect(audioCtx.destination);
  osc.frequency.value = freq;
  osc.type = type;
  gain.gain.setValueAtTime(0.3, now);
  gain.gain.exponentialRampToValueAtTime(0.01, now + duration);
  osc.start(now);
  osc.stop(now + duration);
}

function playCorrectSound() {
  initAudio();
  [523.25, 659.25, 783.99, 1046.50].forEach((f, i) => playTone(f, 'sine', 0.3, i * 0.1));
}

function playWrongSound() {
  initAudio();
  playTone(150, 'sawtooth', 0.4, 0);
}

function playClickSound() {
  initAudio();
  playTone(800, 'sine', 0.1, 0);
}

function shuffleArray(arr) {
  const a = [...arr];
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

function showScreen(id) {
  document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

function startGame() {
  initAudio();
  playClickSound();
  shuffledQuestions = shuffleArray(questions).slice(0, 10);
  currentQuestionIndex = 0;
  score = 0;
  showScreen('game');
  loadQuestion();
}

function restartGame() {
  playClickSound();
  startGame();
}

function loadQuestion() {
  if (currentQuestionIndex >= shuffledQuestions.length) { endGame(); return; }
  
  const q = shuffledQuestions[currentQuestionIndex];
  currentAnswer = q.answer;
  selectedLetters = [];
  
  document.body.style.background = categoryColors[q.category] || categoryColors["دينية"];
  document.getElementById('categoryBadge').textContent = q.icon + " " + q.category;
  document.getElementById('scoreDisplay').textContent = "النقاط: " + score;
  document.getElementById('progressFill').style.width = ((currentQuestionIndex / shuffledQuestions.length) * 100) + "%";
  document.getElementById('questionText').textContent = q.question;
  
  const slotsContainer = document.getElementById('answerSlots');
  slotsContainer.innerHTML = '';
  for (let i = 0; i < q.answer.length; i++) {
    const slot = document.createElement('div');
    slot.className = 'answer-slot';
    slot.dataset.index = i;
    slot.onclick = (function(idx) { return function() { removeFromSlot(idx); }; })(i);
    slotsContainer.appendChild(slot);
  }
  
  const answerLetters = q.answer.split('');
  const distractors = ['ن','ا','و','ع','س','م','ل','ي','إ','د','ت','ر','ب','ك','ح','ج','ف','ق','غ','ظ','ط','ذ','ز','ش','ض','ث','خ','ص'];
  const extraLetters = shuffleArray(distractors).slice(0, Math.max(4, 10 - answerLetters.length));
  const allLetters = shuffleArray([...answerLetters, ...extraLetters]);
  
  const lettersContainer = document.getElementById('lettersContainer');
  lettersContainer.innerHTML = '';
  allLetters.forEach((letter, i) => {
    const btn = document.createElement('div');
    btn.className = 'letter-btn';
    btn.textContent = letter;
    btn.dataset.id = i;
    btn.onclick = (function(b, l) { return function() { selectLetter(b, l); }; })(btn, letter);
    lettersContainer.appendChild(btn);
  });
}

function selectLetter(btn, letter) {
  if (btn.classList.contains('used')) return;
  if (selectedLetters.length >= currentAnswer.length) return;
  playClickSound();
  btn.classList.add('used');
  const slotIndex = selectedLetters.length;
  selectedLetters.push({ letter: letter, btn: btn });
  const slots = document.querySelectorAll('.answer-slot');
  slots[slotIndex].textContent = letter;
  slots[slotIndex].classList.add('filled');
  if (selectedLetters.length === currentAnswer.length) setTimeout(checkAnswer, 400);
}

function removeFromSlot(index) {
  if (index >= selectedLetters.length) return;
  const slots = document.querySelectorAll('.answer-slot');
  for (let i = selectedLetters.length - 1; i >= index; i--) {
    selectedLetters[i].btn.classList.remove('used');
    slots[i].textContent = '';
    slots[i].classList.remove('filled');
  }
  selectedLetters = selectedLetters.slice(0, index);
}

function checkAnswer() {
  const userAnswer = selectedLetters.map(s => s.letter).join('');
  const slots = document.querySelectorAll('.answer-slot');
  if (userAnswer === currentAnswer) {
    slots.forEach(s => s.classList.add('correct'));
    playCorrectSound();
    score++;
    document.getElementById('scoreDisplay').textContent = "النقاط: " + score;
    showFeedback('✅ صحيح!');
    createConfetti();
    setTimeout(function() { currentQuestionIndex++; loadQuestion(); }, 2000);
  } else {
    slots.forEach(s => s.classList.add('wrong'));
    playWrongSound();
    showFeedback('❌ حاول مرة أخرى');
    setTimeout(resetCurrent, 1200);
  }
}

function resetCurrent() {
  selectedLetters.forEach(function(s) { s.btn.classList.remove('used'); });
  selectedLetters = [];
  document.querySelectorAll('.answer-slot').forEach(function(s) {
    s.textContent = '';
    s.classList.remove('filled', 'correct', 'wrong');
  });
}

function showHint() {
  showFeedback('💡 ' + shuffledQuestions[currentQuestionIndex].hint);
  playClickSound();
}

function showFeedback(text) {
  const fb = document.getElementById('feedback');
  fb.textContent = text;
  fb.classList.remove('show');
  void fb.offsetWidth;
  fb.classList.add('show');
  setTimeout(function() { fb.classList.remove('show'); }, 1500);
}

function createConfetti() {
  const colors = ['#ffd700', '#ff6b6b', '#4ecdc4', '#45b7d1', '#f9ca24', '#6c5ce7'];
  for (let i = 0; i < 30; i++) {
    const conf = document.createElement('div');
    conf.className = 'confetti';
    conf.style.left = Math.random() * 100 + 'vw';
    conf.style.background = colors[Math.floor(Math.random() * colors.length)];
    conf.style.animationDuration = (2 + Math.random() * 2) + 's';
    conf.style.animationDelay = Math.random() * 0.5 + 's';
    document.body.appendChild(conf);
    setTimeout(function() { conf.remove(); }, 4000);
  }
}

function endGame() {
  showScreen('end');
  document.body.style.background = 'linear-gradient(135deg, #0f1e4a 0%, #1a2a5e 50%, #2a3a7e 100%)';
  document.getElementById('endScore').textContent = "نتيجتك: " + score + " / " + shuffledQuestions.length;
  const pct = score / shuffledQuestions.length;
  let msg = pct === 1 ? '🏆 ممتاز! أنت عبقري!' : pct >= 0.8 ? '🌟 أحسنت! أداء رائع!' : pct >= 0.6 ? ' جيد! استمر!' : pct >= 0.4 ? '💪 حاول مرة أخرى!' : '📚 تحتاج للمزيد!';
  document.getElementById('endMessage').textContent = msg;
  playCorrectSound();
  createConfetti();
}
</script>
</body>
</html>
```

