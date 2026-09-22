<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Сапалық және сандық есептер — қысым</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,600;9..144,700&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
:root{
  --navy-deep:#0e1b2b;
  --navy-panel:#152640;
  --navy-line:#2a3f5c;
  --cream:#f1ece1;
  --cream-dim:#c7bfae;
  --gauge-orange:#e2732c;
  --gauge-orange-dim:#a4562a;
  --teal:#3aa89a;
  --teal-dim:#245e56;
  --wrong:#c0524a;
}
*{box-sizing:border-box;}
html,body{margin:0;padding:0;}
body{
  background:var(--navy-deep);
  background-image:
    radial-gradient(circle at 15% 0%, rgba(58,168,154,0.10), transparent 45%),
    radial-gradient(circle at 90% 20%, rgba(226,115,44,0.08), transparent 40%);
  color:var(--cream);
  font-family:'Inter', sans-serif;
  line-height:1.55;
  padding:0 0 80px 0;
}
.wrap{max-width:760px;margin:0 auto;padding:0 20px;}

.hero{
  padding:48px 20px 36px 20px;
  border-bottom:1px solid var(--navy-line);
  margin-bottom:44px;
}
.hero-inner{max-width:760px;margin:0 auto;display:flex;gap:32px;align-items:center;flex-wrap:wrap;}
.hero-text{flex:1 1 320px;min-width:260px;}
.eyebrow-topic{color:var(--teal);font-size:14px;letter-spacing:0.02em;margin-bottom:10px;}
h1{
  font-family:'Fraunces', serif;
  font-weight:600;
  font-size:clamp(28px,4.4vw,40px);
  line-height:1.15;
  margin:0 0 14px 0;
  color:var(--cream);
}
.hero-desc{color:var(--cream-dim);font-size:15.5px;max-width:46ch;}
.gauge-box{flex:0 0 auto;display:flex;flex-direction:column;align-items:center;gap:8px;}
#gaugeScore{font-family:'Fraunces',serif;font-size:15px;color:var(--cream-dim);}
#gaugeScore b{color:var(--gauge-orange);font-size:19px;}

.task{
  background:var(--navy-panel);
  border:1px solid var(--navy-line);
  border-radius:4px;
  padding:28px 26px;
  margin:0 0 22px 0;
  position:relative;
}
.task-head{display:flex;align-items:baseline;gap:14px;margin-bottom:16px;}
.task-num{
  font-family:'Fraunces',serif;
  font-size:26px;
  color:var(--gauge-orange-dim);
  min-width:34px;
}
.task-title{
  font-family:'Fraunces',serif;
  font-weight:600;
  font-size:20px;
  color:var(--cream);
}
.task-body{color:var(--cream-dim);font-size:15px;}
.task-body p{margin:0 0 14px 0;}

.opt-list{display:flex;flex-direction:column;gap:9px;margin-top:14px;}
.opt{
  text-align:left;
  background:transparent;
  border:1px solid var(--navy-line);
  color:var(--cream);
  padding:11px 14px;
  border-radius:3px;
  font-family:'Inter',sans-serif;
  font-size:14.5px;
  cursor:pointer;
  transition:border-color .15s ease, background .15s ease;
}
.opt:hover{border-color:var(--teal);}
.opt.correct{border-color:var(--teal);background:rgba(58,168,154,0.14);}
.opt.wrong{border-color:var(--wrong);background:rgba(192,82,74,0.14);}
.opt:disabled{cursor:default;}

.feedback{margin-top:12px;font-size:14px;padding:10px 12px;border-radius:3px;display:none;}
.feedback.show{display:block;}
.feedback.ok{background:rgba(58,168,154,0.12);color:#8fd9cd;border:1px solid var(--teal-dim);}
.feedback.bad{background:rgba(192,82,74,0.12);color:#e6a29d;border:1px solid var(--wrong);}

.sim-row{display:flex;gap:20px;flex-wrap:wrap;align-items:flex-start;margin-top:6px;}
canvas#pressCanvas{background:#0a1420;border:1px solid var(--navy-line);border-radius:3px;}
.sim-controls{flex:1 1 200px;min-width:200px;}
.sim-controls label{font-size:13.5px;color:var(--cream-dim);display:block;margin-bottom:6px;}
input[type=range]{width:100%;accent-color:var(--gauge-orange);}
.sim-readout{margin-top:14px;font-size:14px;}
.sim-readout .num{color:var(--gauge-orange);font-family:'Fraunces',serif;font-size:22px;}

select.blank, input.blank{
  background:var(--navy-deep);
  border:1px solid var(--navy-line);
  color:var(--cream);
  padding:5px 8px;
  border-radius:3px;
  font-family:'Inter',sans-serif;
  font-size:14.5px;
  margin:0 3px;
}
select.blank:focus, input.blank:focus{outline:1px solid var(--teal);}

.calc-row{display:flex;gap:10px;align-items:center;margin-top:8px;flex-wrap:wrap;}
input.numans{width:110px;}
button.check{
  background:var(--gauge-orange);
  color:var(--navy-deep);
  border:none;
  font-weight:600;
  padding:9px 18px;
  border-radius:3px;
  cursor:pointer;
  font-family:'Inter',sans-serif;
  font-size:14px;
}
button.check:hover{background:#ef8340;}

.match-cols{display:flex;gap:26px;flex-wrap:wrap;margin-top:10px;}
.match-col{flex:1 1 220px;display:flex;flex-direction:column;gap:8px;}
.match-item{
  border:1px solid var(--navy-line);
  padding:10px 12px;
  border-radius:3px;
  font-size:14px;
  cursor:pointer;
  transition:border-color .15s ease;
}
.match-item.selected{border-color:var(--teal);color:#8fd9cd;}
.match-item.paired{border-color:var(--gauge-orange-dim);opacity:0.55;cursor:default;}
.match-item.wrongflash{border-color:var(--wrong);}

.tf-item{
  border-top:1px solid var(--navy-line);
  padding:14px 0;
}
.tf-item:first-of-type{border-top:none;padding-top:0;}
.tf-stmt{font-size:14.5px;margin-bottom:10px;}
.tf-btns{display:flex;gap:8px;}
.tf-btns button{
  background:transparent;
  border:1px solid var(--navy-line);
  color:var(--cream-dim);
  padding:6px 16px;
  border-radius:3px;
  cursor:pointer;
  font-size:13.5px;
}
.tf-btns button.correct{border-color:var(--teal);color:#8fd9cd;background:rgba(58,168,154,0.12);}
.tf-btns button.wrong{border-color:var(--wrong);color:#e6a29d;background:rgba(192,82,74,0.12);}

.press-diagram{display:flex;justify-content:center;margin:14px 0;}
svg text{font-family:'Inter',sans-serif;}

footer.foot{max-width:760px;margin:0 auto;padding:0 20px;color:var(--cream-dim);font-size:13px;text-align:center;}
</style>
</head>
<body>

<div class="hero">
  <div class="hero-inner">
    <div class="hero-text">
      <div class="eyebrow-topic">7.3.1.3 — есептер шығаруда қатты дененің қысымының формуласын қолдану</div>
      <h1>Сапалық және сандық есептер шығару</h1>
      <p class="hero-desc">Қысым формуласын (P = F / S) сапалық ойлауда да, сандық есептеуде де қолдануды жаттықтыратын жеті тапсырма. Әр тапсырманы өз бетіңше орында — дұрыс жауап манометр көрсеткішін жылжытады.</p>
    </div>
    <div class="gauge-box">
      <svg width="120" height="90" viewBox="0 0 120 90">
        <path d="M 10 80 A 50 50 0 0 1 110 80" fill="none" stroke="#2a3f5c" stroke-width="10"/>
        <path id="gaugeArc" d="M 10 80 A 50 50 0 0 1 110 80" fill="none" stroke="#e2732c" stroke-width="10" stroke-dasharray="157" stroke-dashoffset="157"/>
        <line id="needle" x1="60" y1="80" x2="60" y2="32" stroke="#f1ece1" stroke-width="2" style="transform-origin:60px 80px; transform:rotate(-90deg); transition:transform .5s ease;"/>
        <circle cx="60" cy="80" r="4" fill="#f1ece1"/>
      </svg>
      <div id="gaugeScore">Нәтиже: <b id="scoreNum">0</b> / 7</div>
    </div>
  </div>
</div>

<div class="wrap">

  <!-- TASK 1: qualitative concept -->
  <div class="task">
    <div class="task-head"><span class="task-num">1</span><span class="task-title">Сапалық есеп: пышақ неге өткір болғанда жақсы кеседі?</span></div>
    <div class="task-body">
      <p>Пышақтың жүзі өткірленген сайын, ол затты неге оңай кеседі?</p>
      <div class="opt-list" data-task="1">
        <button class="opt" data-correct="false">Өткір жүз ауырырақ болады, сондықтан күш көп түседі</button>
        <button class="opt" data-correct="true">Өткір жүздің ауданы кішірейеді, сол себепті бірдей күш кішкене ауданға түсіп, қысым артады</button>
        <button class="opt" data-correct="false">Өткір жүз затпен үйкелісі азаяды, сондықтан қысымға қатысы жоқ</button>
        <button class="opt" data-correct="false">Өткір жүз жеңілірек болғандықтан оңай кеседі</button>
      </div>
      <div class="feedback" id="fb1"></div>
    </div>
  </div>

  <!-- TASK 2: interactive simulation — area vs pressure -->
  <div class="task">
    <div class="task-head"><span class="task-num">2</span><span class="task-title">Зертхана: аудан мен қысым</span></div>
    <div class="task-body">
      <p>Бірдей салмақты дене әртүрлі аудандағы табанға қойылды. Тұтқаны жылжытып, табан ауданын өзгерт те, қысымның қалай өзгеретінін бақыла (күш F = 60 Н тұрақты).</p>
      <div class="sim-row">
        <canvas id="pressCanvas" width="260" height="200"></canvas>
        <div class="sim-controls">
          <label for="areaSlider">Табан ауданы, S (см²)</label>
          <input type="range" id="areaSlider" min="10" max="100" value="40" step="1">
          <div class="sim-readout">Есептелген қысым: <span class="num" id="pressureReadout">—</span> Па</div>
        </div>
      </div>
      <p style="margin-top:16px;">Тәжірибе нәтижесі бойынша: аудан кішірейгенде қысым қалай өзгереді?</p>
      <div class="opt-list" data-task="2">
        <button class="opt" data-correct="true">Артады — бірдей күш кішірек ауданға түседі</button>
        <button class="opt" data-correct="false">Кемиді — аудан кіші болған сайын қысым да азаяды</button>
        <button class="opt" data-correct="false">Өзгермейді — аудан қысымға әсер етпейді</button>
      </div>
      <div class="feedback" id="fb2"></div>
    </div>
  </div>

  <!-- TASK 3: fill blanks -->
  <div class="task">
    <div class="task-head"><span class="task-num">3</span><span class="task-title">Анықтаманы толықтыр</span></div>
    <div class="task-body">
      <p>Бос орындарды дұрыс сөздермен толтыр:</p>
      <p style="font-size:15.5px;color:var(--cream);line-height:2.1;">
        Қысым — бетке перпендикуляр түсірілген
        <select class="blank" id="blank1">
          <option value="">— таңда —</option>
          <option value="kush">күштің</option>
          <option value="massa">массаның</option>
          <option value="jyldamdyk">жылдамдықтың</option>
        </select>
        сол бет ауданына қатынасы. Аудан кемісе, бірдей күш кезінде қысым
        <select class="blank" id="blank2">
          <option value="">— таңда —</option>
          <option value="artady">артады</option>
          <option value="azayady">азаяды</option>
          <option value="ozgermeidi">өзгермейді</option>
        </select>
        . Қысымның өлшем бірлігі —
        <select class="blank" id="blank3">
          <option value="">— таңда —</option>
          <option value="pa">паскаль (Па)</option>
          <option value="n">ньютон (Н)</option>
          <option value="m2">шаршы метр (м²)</option>
        </select>
        .
      </p>
      <button class="check" onclick="checkTask3()">Тексеру</button>
      <div class="feedback" id="fb3"></div>
    </div>
  </div>

  <!-- TASK 4: quantitative calculation -->
  <div class="task">
    <div class="task-head"><span class="task-num">4</span><span class="task-title">Сандық есеп: қысымды тап</span></div>
    <div class="task-body">
      <p>Салмағы 400 Н жәшік ауданы 2 м² еденге тұр. Жәшіктің еденге түсіретін қысымын есепте (P = F / S).</p>
      <div class="calc-row">
        <input type="number" class="numans" id="ans4" placeholder="P = ?">
        <span style="color:var(--cream-dim);">Па</span>
        <button class="check" onclick="checkTask4()">Тексеру</button>
      </div>
      <div class="feedback" id="fb4"></div>
    </div>
  </div>

  <!-- TASK 5: matching -->
  <div class="task">
    <div class="task-head"><span class="task-num">5</span><span class="task-title">Ұғымдарды сәйкестендір</span></div>
    <div class="task-body">
      <p>Сол жақтан бір ұғымды, содан кейін оң жақтан сәйкес анықтама немесе формуланы бас.</p>
      <div class="match-cols">
        <div class="match-col" id="matchTerms">
          <div class="match-item" data-key="a">Қысым (P)</div>
          <div class="match-item" data-key="b">Күш (F)</div>
          <div class="match-item" data-key="c">Аудан (S)</div>
          <div class="match-item" data-key="d">Паскаль (Па)</div>
        </div>
        <div class="match-col" id="matchDefs">
          <div class="match-item" data-key="c">Дене табанының бетке тиетін бөлігінің көлемі, м² өлшенеді</div>
          <div class="match-item" data-key="a">Бетке перпендикуляр түсірілген күштің сол бет ауданына қатынасы</div>
          <div class="match-item" data-key="d">1 м² ауданға 1 Н күш перпендикуляр түсіргендегі қысымға тең өлшем бірлік</div>
          <div class="match-item" data-key="b">Бір дененің екінші денеге әсер ету шамасы, ньютонмен өлшенеді</div>
        </div>
      </div>
      <div class="feedback" id="fb5"></div>
    </div>
  </div>

  <!-- TASK 6: true/false -->
  <div class="task">
    <div class="task-head"><span class="task-num">6</span><span class="task-title">Дұрыс па, бұрыс па?</span></div>
    <div class="task-body">
      <div id="tfList"></div>
      <div class="feedback" id="fb6"></div>
    </div>
  </div>

  <!-- TASK 7: applied comprehensive problem -->
  <div class="task">
    <div class="task-head"><span class="task-num">7</span><span class="task-title">Қолданбалы есеп: трактор дөңгелегі</span></div>
    <div class="task-body">
      <p>Салмағы 12 000 Н трактор жерге 3 000 Па қысым түсіруі тиіс (жер батпай қалу үшін). Трактордың дөңгелектерінің жермен жанасатын жалпы ауданы қандай болуы керек? (S = F / P)</p>
      <div class="press-diagram">
        <svg width="260" height="140" viewBox="0 0 260 140">
          <rect x="20" y="105" width="220" height="12" fill="#0a1420" stroke="#2a3f5c"/>
          <rect x="70" y="45" width="120" height="45" rx="4" fill="#152640" stroke="#3aa89a"/>
          <circle cx="95" cy="100" r="17" fill="#0a1420" stroke="#e2732c" stroke-width="3"/>
          <circle cx="165" cy="100" r="17" fill="#0a1420" stroke="#e2732c" stroke-width="3"/>
          <text x="130" y="35" fill="#c7bfae" font-size="11" text-anchor="middle">F = 12 000 Н</text>
          <text x="130" y="128" fill="#c7bfae" font-size="10" text-anchor="middle">S = ?</text>
        </svg>
      </div>
      <p style="font-size:13.5px;color:var(--cream-dim);">Ескерту: S = F / P формуласын қолдан.</p>
      <div class="calc-row">
        <input type="number" class="numans" id="ans7" placeholder="S = ?">
        <span style="color:var(--cream-dim);">м²</span>
        <button class="check" onclick="checkTask7()">Тексеру</button>
      </div>
      <div class="feedback" id="fb7"></div>
    </div>
  </div>

</div>

<footer class="foot">7.3.1.3 — есептер шығаруда қатты дененің қысымының формуласын қолдану</footer>

<script>
let score = 0;
let completed = new Set();

function markDone(taskId, isCorrect){
  if(!completed.has(taskId)){
    completed.add(taskId);
    if(isCorrect) score++;
    updateGauge();
  }
}

function updateGauge(){
  document.getElementById('scoreNum').textContent = score;
  const frac = score/7;
  const offset = 157 - (157*frac);
  document.getElementById('gaugeArc').style.strokeDashoffset = offset;
  const angle = -90 + (180*frac);
  document.getElementById('needle').style.transform = `rotate(${angle}deg)`;
}

function setupChoice(taskNum){
  const list = document.querySelector(`.opt-list[data-task="${taskNum}"]`);
  const btns = list.querySelectorAll('.opt');
  btns.forEach(btn=>{
    btn.addEventListener('click', ()=>{
      const correct = btn.dataset.correct === 'true';
      btns.forEach(b=>b.disabled=true);
      btn.classList.add(correct ? 'correct' : 'wrong');
      if(!correct){
        list.querySelector('[data-correct="true"]').classList.add('correct');
      }
      const fb = document.getElementById('fb'+taskNum);
      fb.classList.add('show', correct ? 'ok' : 'bad');
      fb.textContent = correct
        ? 'Дұрыс! ' + (taskNum==1 ? 'Аудан кішірейген сайын, бірдей күш кезінде қысым артады.' : 'Аудан кемігенде бірдей күш кішкене бетке түсіп, қысым артады.')
        : 'Дұрыс жауап жасыл түспен белгіленді.';
      markDone('t'+taskNum, correct);
    });
  });
}
setupChoice(1);
setupChoice(2);

// TASK 2 simulation: fixed force, variable area -> pressure changes; visualize as shrinking footprint with dot density
const canvas = document.getElementById('pressCanvas');
const ctx = canvas.getContext('2d');
const F_CONST = 60; // N

function drawSim(){
  const sCm2 = parseFloat(document.getElementById('areaSlider').value);
  const sM2 = sCm2 / 10000;
  const pressure = F_CONST / sM2;
  document.getElementById('pressureReadout').textContent = Math.round(pressure);

  ctx.clearRect(0,0,canvas.width,canvas.height);
  // ground line
  ctx.strokeStyle = '#2a3f5c';
  ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.moveTo(10, 170);
  ctx.lineTo(250, 170);
  ctx.stroke();

  // footprint size scales with area slider (visual only)
  const maxSide = 120, minSide = 30;
  const side = minSide + (maxSide-minSide) * ((sCm2-10)/(100-10));
  const x = canvas.width/2 - side/2;
  const y = 170 - side;

  // color intensity reflects pressure (higher pressure -> more orange/intense)
  const frac = Math.min(1, (pressure-600)/(5400));
  const r = Math.round(58 + frac*(226-58));
  const g = Math.round(168 + frac*(115-168));
  const b = Math.round(154 + frac*(44-154));
  ctx.fillStyle = `rgb(${r},${g},${b})`;
  ctx.globalAlpha = 0.75;
  ctx.fillRect(x, y, side, side);
  ctx.globalAlpha = 1;
  ctx.strokeStyle = '#f1ece1';
  ctx.lineWidth = 1;
  ctx.strokeRect(x, y, side, side);

  // force arrow above
  ctx.strokeStyle = '#f1ece1';
  ctx.lineWidth = 2;
  ctx.beginPath();
  ctx.moveTo(canvas.width/2, y-45);
  ctx.lineTo(canvas.width/2, y-5);
  ctx.stroke();
  ctx.beginPath();
  ctx.moveTo(canvas.width/2, y-5);
  ctx.lineTo(canvas.width/2-6, y-15);
  ctx.lineTo(canvas.width/2+6, y-15);
  ctx.closePath();
  ctx.fillStyle = '#f1ece1';
  ctx.fill();
  ctx.fillStyle = '#c7bfae';
  ctx.font = '12px Inter, sans-serif';
  ctx.textAlign = 'center';
  ctx.fillText('F = 60 Н', canvas.width/2, y-52);
  ctx.fillText('S = ' + sCm2 + ' см²', canvas.width/2, 188);
}
document.getElementById('areaSlider').addEventListener('input', drawSim);
drawSim();

// TASK 3
function checkTask3(){
  const b1 = document.getElementById('blank1').value;
  const b2 = document.getElementById('blank2').value;
  const b3 = document.getElementById('blank3').value;
  const correct = (b1==='kush' && b2==='artady' && b3==='pa');
  const fb = document.getElementById('fb3');
  fb.classList.add('show', correct?'ok':'bad');
  fb.textContent = correct
    ? 'Дұрыс! Бұл — қысымның дәл анықтамасы.'
    : 'Тағы бір рет тексеріп көр: барлық үш бос орынды дұрыс таңда.';
  markDone('t3', correct);
}

// TASK 4
function checkTask4(){
  const val = parseFloat(document.getElementById('ans4').value);
  const correct = Math.abs(val - 200) < 1;
  const fb = document.getElementById('fb4');
  fb.classList.add('show', correct?'ok':'bad');
  fb.textContent = correct
    ? 'Дұрыс! P = F/S = 400 Н / 2 м² = 200 Па.'
    : 'Қате. Формула: P = F/S = 400 / 2 = 200 Па.';
  markDone('t4', correct);
}

// TASK 5 matching
let selectedTerm = null;
let pairsFound = 0;
document.getElementById('matchTerms').querySelectorAll('.match-item').forEach(el=>{
  el.addEventListener('click', ()=>{
    if(el.classList.contains('paired')) return;
    document.getElementById('matchTerms').querySelectorAll('.match-item').forEach(x=>x.classList.remove('selected'));
    el.classList.add('selected');
    selectedTerm = el;
  });
});
document.getElementById('matchDefs').querySelectorAll('.match-item').forEach(el=>{
  el.addEventListener('click', ()=>{
    if(el.classList.contains('paired') || !selectedTerm) return;
    if(el.dataset.key === selectedTerm.dataset.key){
      el.classList.add('paired');
      selectedTerm.classList.add('paired');
      selectedTerm.classList.remove('selected');
      selectedTerm = null;
      pairsFound++;
      if(pairsFound === 4){
        const fb = document.getElementById('fb5');
        fb.classList.add('show','ok');
        fb.textContent = 'Керемет! Барлық ұғым дұрыс сәйкестендірілді.';
        markDone('t5', true);
      }
    } else {
      el.classList.add('wrongflash');
      setTimeout(()=>el.classList.remove('wrongflash'), 450);
    }
  });
});

// TASK 6 true/false
const tfData = [
  {stmt:'Бірдей күш кезінде аудан кішірейсе, қысым артады.', answer:true},
  {stmt:'Қысымның өлшем бірлігі — ньютон (Н).', answer:false},
  {stmt:'Кең табанды аяқ киім қар үстінде батпай жүруге көмектеседі, себебі қысым аз болады.', answer:true},
  {stmt:'Қысым тек дененің салмағына байланысты, ауданға тәуелді емес.', answer:false}
];
const tfList = document.getElementById('tfList');
let tfCorrectCount = 0;
let tfAnswered = 0;
tfData.forEach((item)=>{
  const div = document.createElement('div');
  div.className = 'tf-item';
  div.innerHTML = `
    <div class="tf-stmt">${item.stmt}</div>
    <div class="tf-btns">
      <button data-val="true">Дұрыс</button>
      <button data-val="false">Бұрыс</button>
    </div>`;
  tfList.appendChild(div);
  const btns = div.querySelectorAll('button');
  btns.forEach(btn=>{
    btn.addEventListener('click', ()=>{
      if(btn.disabled) return;
      const chosen = btn.dataset.val === 'true';
      const isCorrect = chosen === item.answer;
      btns.forEach(b=>b.disabled=true);
      btn.classList.add(isCorrect?'correct':'wrong');
      if(!isCorrect){
        div.querySelector(`[data-val="${item.answer}"]`).classList.add('correct');
      }
      tfAnswered++;
      if(isCorrect) tfCorrectCount++;
      if(tfAnswered === tfData.length){
        const fb = document.getElementById('fb6');
        const allCorrect = tfCorrectCount === tfData.length;
        fb.classList.add('show', allCorrect?'ok':'bad');
        fb.textContent = `Нәтиже: ${tfCorrectCount} / ${tfData.length} дұрыс.`;
        markDone('t6', allCorrect);
      }
    });
  });
});

// TASK 7
function checkTask7(){
  const val = parseFloat(document.getElementById('ans7').value);
  const correct = Math.abs(val - 4) < 0.05;
  const fb = document.getElementById('fb7');
  fb.classList.add('show', correct?'ok':'bad');
  fb.textContent = correct
    ? 'Дұрыс! S = F/P = 12000 / 3000 = 4 м².'
    : 'Қате. Формула: S = F/P = 12000 / 3000 = 4 м².';
  markDone('t7', correct);
}
</script>
</body>
</html>
