<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>বাংলা কুইজ</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+Bengali:wght@400;500;700&display=swap');

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Noto Sans Bengali', sans-serif;
    background: #0f0e17;
    color: #fffffe;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1.5rem;
  }

  .container {
    width: 100%;
    max-width: 640px;
  }

  .header {
    text-align: center;
    margin-bottom: 2rem;
  }

  .header h1 {
    font-size: 2rem;
    font-weight: 700;
    letter-spacing: -0.5px;
    color: #ff8906;
  }

  .header p {
    font-size: 0.9rem;
    color: #a7a9be;
    margin-top: 4px;
  }

  .card {
    background: #1a1a2e;
    border: 1px solid #2e2e4a;
    border-radius: 20px;
    padding: 2rem;
  }

  .progress-wrap {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 1.5rem;
  }

  .progress-bg {
    flex: 1;
    height: 6px;
    background: #2e2e4a;
    border-radius: 99px;
    overflow: hidden;
  }

  .progress-fill {
    height: 6px;
    background: linear-gradient(90deg, #ff8906, #f25f4c);
    border-radius: 99px;
    transition: width 0.5s cubic-bezier(.4,0,.2,1);
  }

  .progress-text {
    font-size: 13px;
    color: #a7a9be;
    white-space: nowrap;
  }

  .question-text {
    font-size: 1.15rem;
    font-weight: 500;
    line-height: 1.6;
    color: #fffffe;
    margin-bottom: 1.5rem;
  }

  .options {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .opt-btn {
    background: #0f0e17;
    border: 1px solid #2e2e4a;
    border-radius: 12px;
    padding: 14px 18px;
    font-family: 'Noto Sans Bengali', sans-serif;
    font-size: 0.95rem;
    color: #fffffe;
    cursor: pointer;
    text-align: left;
    transition: all 0.15s;
    display: flex;
    align-items: center;
    gap: 12px;
  }

  .opt-btn .label {
    width: 28px;
    height: 28px;
    border-radius: 50%;
    border: 1px solid #2e2e4a;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 12px;
    font-weight: 700;
    flex-shrink: 0;
    transition: all 0.15s;
  }

  .opt-btn:hover:not(:disabled) {
    border-color: #ff8906;
    background: #1a1a2e;
  }

  .opt-btn:hover:not(:disabled) .label {
    background: #ff8906;
    border-color: #ff8906;
    color: #0f0e17;
  }

  .opt-btn.correct {
    background: #0d2b1f;
    border-color: #2d9e6a;
    color: #5dde9a;
  }

  .opt-btn.correct .label {
    background: #2d9e6a;
    border-color: #2d9e6a;
    color: #fff;
  }

  .opt-btn.wrong {
    background: #2b0d0d;
    border-color: #9e2d2d;
    color: #de5d5d;
  }

  .opt-btn.wrong .label {
    background: #9e2d2d;
    border-color: #9e2d2d;
    color: #fff;
  }

  .opt-btn:disabled { cursor: default; }

  .explanation {
    margin-top: 1.25rem;
    padding: 14px 16px;
    background: #0f0e17;
    border-radius: 12px;
    border-left: 3px solid #ff8906;
    font-size: 0.9rem;
    color: #a7a9be;
    line-height: 1.6;
    display: none;
  }

  .next-btn {
    margin-top: 1.25rem;
    padding: 12px 28px;
    background: #ff8906;
    color: #0f0e17;
    border: none;
    border-radius: 12px;
    font-family: 'Noto Sans Bengali', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    cursor: pointer;
    display: none;
    transition: background 0.15s, transform 0.1s;
  }

  .next-btn:hover { background: #e07a00; transform: translateY(-1px); }

  /* Result */
  .result-wrap { text-align: center; padding: 1rem 0; }
  .result-ring {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    background: conic-gradient(#ff8906 var(--pct), #2e2e4a 0);
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 0 auto 1.5rem;
    position: relative;
  }
  .result-ring::after {
    content: '';
    width: 90px;
    height: 90px;
    border-radius: 50%;
    background: #1a1a2e;
    position: absolute;
  }
  .result-score {
    font-size: 2rem;
    font-weight: 700;
    color: #ff8906;
    position: relative;
    z-index: 1;
  }
  .result-msg { font-size: 1.1rem; font-weight: 500; margin-bottom: 0.5rem; }
  .result-sub { font-size: 0.9rem; color: #a7a9be; margin-bottom: 1.5rem; }
  .restart-btn {
    padding: 12px 28px;
    background: #ff8906;
    color: #0f0e17;
    border: none;
    border-radius: 12px;
    font-family: 'Noto Sans Bengali', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    cursor: pointer;
    transition: background 0.15s;
  }
  .restart-btn:hover { background: #e07a00; }
</style>
</head>
<body>

<div class="container">
  <div class="header">
    <h1>বাংলা কুইজ</h1>
    <p>সাধারণ জ্ঞান — ১০টি প্রশ্ন</p>
  </div>
  <div class="card" id="quiz-area"></div>
</div>

<script>
const questions = [
  { q: "'সোমপ্রকাশ' পত্রিকাটি কে সম্পাদনা করতেন?", opts: ["রাজা রামমোহন রায়","মাইকেল মধুসূদন দত্ত","ঈশ্বরচন্দ্র বিদ্যাসাগর","রবীন্দ্রনাথ ঠাকুর"], ans: 2, exp: "'সোমপ্রকাশ' বিখ্যাত পত্রিকাটি পণ্ডিত ঈশ্বরচন্দ্র বিদ্যাসাগর সম্পাদনা করতেন।" },
  { q: "আন্দিজ পর্বতমালা কোন মহাদেশে অবস্থিত?", opts: ["এশিয়া","উত্তর আমেরিকা","দক্ষিণ আমেরিকা","আফ্রিকা"], ans: 2, exp: "বিশ্বের দীর্ঘতম পর্বতমালাগুলির অন্যতম আন্দিজ পর্বতমালা দক্ষিণ আমেরিকা মহাদেশে অবস্থিত।" },
  { q: "কোন মোগল সম্রাট 'দীন-ই-ইলাহি' প্রচলন করেন?", opts: ["শাহজাহান","হুমায়ুন","জাহাঙ্গীর","আকবর"], ans: 3, exp: "মোগল সম্রাট আকবর সমস্ত ধর্মের সারমর্ম নিয়ে 'দীন-ই-ইলাহি' নামক নতুন ধর্মমত প্রচলন করেছিলেন।" },
  { q: "কোষের 'সুইসাইড ব্যাগ' কোন অঙ্গাণুকে বলা হয়?", opts: ["সেন্ট্রোজোম","মাইটোকনড্রিয়া","লাইসোজোম","রাইবোজোম"], ans: 2, exp: "লাইসোজোমকে তার ধ্বংসাত্মক উৎসেচকের কারণে কোষের 'সুইসাইড ব্যাগ' বলা হয়।" },
  { q: "'জালিয়ানওয়ালা বাগ'-এর ঘটনা কোন সালে হয়েছিল?", opts: ["১৯১৯","১৭৮৯","১৯২৮","১৭৫০"], ans: 0, exp: "জালিয়ানওয়ালা বাগের মর্মান্তিক হত্যাকাণ্ডটি ১৯১৯ সালে সংঘটিত হয়েছিল।" },
  { q: "নীচের কোনটিকে 'বাদামী কয়লা' (brown coal) বলা হয়?", opts: ["বিটুমিনাস","কোক","অ্যানথ্রাসাইট","লিগনাইট"], ans: 3, exp: "কার্বনের পরিমাণের ওপর ভিত্তি করে লিগনাইট শ্রেণির কয়লাকে 'বাদামী কয়লা' বলা হয়।" },
  { q: "'ভারী জল' (Heavy water) বলতে কী বোঝায়?", opts: ["ওজোন গ্যাস মিশ্রিত জল","ভারী ধাতুর খনিজ মিশ্রিত জল","খনিজ মিশ্রিত জল","হাইড্রোজেনের আইসোটোপ দ্বারা তৈরি জল"], ans: 3, exp: "হাইড্রোজেনের আইসোটোপ 'ডয়টেরিয়াম' দ্বারা তৈরি জলকে বিজ্ঞানের ভাষায় 'ভারী জল' বলা হয়।" },
  { q: "'সীমান্ত গান্ধী' নামে কোন স্বাধীনতা সংগ্রামী পরিচিত ছিলেন?", opts: ["সৈয়দ আহমেদ খান","দাদাভাই নওরোজী","খান আবদুল গফ্ফর খান","মহম্মদ ইকবাল"], ans: 2, exp: "খান আবদুল গফ্ফর খান অহিংস ভূমিকার জন্য 'সীমান্ত গান্ধী' নামে পরিচিত ছিলেন।" },
  { q: "বক্সা ব্যাঘ্র সংরক্ষণ প্রকল্প পশ্চিমবঙ্গের কোন জেলায় অবস্থিত?", opts: ["জলপাইগুড়ি","আলিপুরদুয়ার","দার্জিলিং","দক্ষিণ ২৪ পরগনা"], ans: 1, exp: "পশ্চিমবঙ্গের আলিপুরদুয়ার জেলায় বক্সা ব্যাঘ্র সংরক্ষণ প্রকল্পটি অবস্থিত।" },
  { q: "স্পঞ্জ (Sponge) কী?", opts: ["উদ্ভিদ (Plant)","জীবদেহ (Animal)","জীবাশ্ম (Fossil)","ছত্রাক (Fungus)"], ans: 1, exp: "বিজ্ঞানসম্মতভাবে স্পঞ্জ হলো এক প্রকার বহুকোষী জলজ জীবদেহ বা প্রাণী (Animal)।" },
];

let current = 0, score = 0, answered = false;
const labels = ['A','B','C','D'];

function render() {
  const area = document.getElementById('quiz-area');
  if (current >= questions.length) {
    const pct = Math.round((score / questions.length) * 100);
    let msg = pct === 100 ? "অসাধারণ! পারফেক্ট স্কোর! 🎉" : pct >= 70 ? "বেশ ভালো করেছেন! 👏" : pct >= 40 ? "আরও একটু পড়লে ভালো হবে। 📚" : "আবার চেষ্টা করুন! 💪";
    let sub = `${questions.length}টি প্রশ্নের মধ্যে ${score}টি সঠিক (${pct}%)`;
    area.innerHTML = `<div class="result-wrap">
      <div class="result-ring" style="--pct: ${pct * 3.6}deg">
        <span class="result-score">${score}/${questions.length}</span>
      </div>
      <div class="result-msg">${msg}</div>
      <div class="result-sub">${sub}</div>
      <button class="restart-btn" onclick="restart()">আবার খেলুন</button>
    </div>`;
    return;
  }
  const q = questions[current];
  const pct = (current / questions.length) * 100;
  area.innerHTML = `
    <div class="progress-wrap">
      <div class="progress-bg"><div class="progress-fill" style="width:${pct}%"></div></div>
      <span class="progress-text">${current + 1}/${questions.length}</span>
    </div>
    <div class="question-text">${q.q}</div>
    <div class="options">
      ${q.opts.map((o, i) => `<button class="opt-btn" id="opt${i}" onclick="choose(${i})"><span class="label">${labels[i]}</span>${o}</button>`).join('')}
    </div>
    <div class="explanation" id="exp">💡 ${q.exp}</div>
    <button class="next-btn" id="nextbtn" onclick="next()">${current === questions.length - 1 ? 'ফলাফল দেখুন →' : 'পরের প্রশ্ন →'}</button>
  `;
  answered = false;
}

function choose(i) {
  if (answered) return;
  answered = true;
  const q = questions[current];
  for (let j = 0; j < q.opts.length; j++) {
    const btn = document.getElementById('opt' + j);
    btn.disabled = true;
    if (j === q.ans) btn.classList.add('correct');
    else if (j === i) btn.classList.add('wrong');
  }
  if (i === q.ans) score++;
  document.getElementById('exp').style.display = 'block';
  document.getElementById('nextbtn').style.display = 'inline-block';
}

function next() { current++; render(); }
function restart() { current = 0; score = 0; render(); }

render();
</script>
</body>
</html>
