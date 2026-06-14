<!DOCTYPE html>
<html lang="bn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Test Bazar — জীবন বিজ্ঞান | জীবনের প্রবাহমানতা | Set 1</title>
<link href="https://fonts.googleapis.com/css2?family=Tiro+Bangla&family=Syne:wght@400;600;700;800&display=swap" rel="stylesheet">
<style>
*{margin:0;padding:0;box-sizing:border-box}
body{font-family:'Syne',sans-serif;background:#f0faf4;min-height:100vh;color:#1c2e24}
.top-bar{background:#1a7a4a;padding:0.8rem 1.5rem;display:flex;justify-content:space-between;align-items:center;position:sticky;top:0;z-index:100}
.top-logo{font-size:1.1rem;font-weight:800;color:white}.top-logo span{color:#f9a825}
.timer-box{background:rgba(255,255,255,0.15);border-radius:8px;padding:0.4rem 1rem;display:flex;align-items:center;gap:6px;font-size:1rem;font-weight:700;color:white}
.timer-box.danger{background:#dc3545}
.main-container{max-width:750px;margin:2rem auto;padding:0 1rem}
.set-header{background:white;border-radius:12px;padding:1.5rem;margin-bottom:1.5rem;border:1px solid #c5dccb;box-shadow:0 4px 6px rgba(0,0,0,0.02)}
.set-header h1{font-family:'Tiro Bangla',serif;font-size:1.6rem;color:#1a7a4a;margin-bottom:0.4rem}
.set-header p{font-size:0.95rem;color:#5a7a66;font-weight:600}
.question-card{background:white;border-radius:12px;padding:1.5rem;margin-bottom:1.5rem;border:1px solid #c5dccb;box-shadow:0 4px 6px rgba(0,0,0,0.02)}
.q-title{font-size:1.1rem;font-weight:700;margin-bottom:1.2rem;line-height:1.5;color:#0f1a14}
.opts-grid{display:flex;flex-direction:column;gap:10px}
.opt{width:100%;background:#f8fdf9;border:1px solid #c5dccb;border-radius:8px;padding:0.9rem 1.2rem;display:flex;align-items:center;gap:12px;cursor:pointer;text-align:left;font-size:0.95rem;font-weight:600;color:#1c2e24;transition:0.15s}
.opt:hover{background:#e8f7ef;border-color:#2aad68}
.opt input{display:none}
.opt-circle{width:26px;height:26px;border-radius:50%;border:2px solid #c5dccb;background:white;display:flex;align-items:center;justify-content:center;font-size:0.85rem;font-weight:800;color:#5a7a66;flex-shrink:0;transition:0.15s}
.opt:hover .opt-circle{border-color:#2aad68;color:#2aad68}
.opt.selected{background:#e8f7ef;border-color:#1a7a4a}
.opt.selected .opt-circle{background:#1a7a4a;border-color:#1a7a4a;color:white}
.opt.correct-ans{background:#e8f5e9;border-color:#2e7d32;color:#1b5e20}
.opt.correct-ans .opt-circle{background:#2e7d32;border-color:#2e7d32;color:white}
.opt.wrong-ans{background:#ffebee;border-color:#c62828;color:#c62828}
.opt.wrong-ans .opt-circle{background:#c62828;border-color:#c62828;color:white}
.opt.disabled{pointer-events:none;cursor:default}
.explanation-box{display:none;margin-top:1.2rem;padding:1rem;background:#f4fbf6;border-left:4px solid #1a7a4a;border-radius:4px;font-size:0.92rem;line-height:1.6;color:#2a4a36}
.submit-area{margin-top:2rem;text-align:center}
.submit-btn{background:#1a7a4a;color:white;border:none;border-radius:8px;padding:1rem 2.5rem;font-size:1.1rem;font-weight:700;cursor:pointer;box-shadow:0 4px 12px rgba(26,122,74,0.25);transition:0.2s}
.submit-btn:hover{background:#135939;transform:translateY(-1px)}
.submit-btn:disabled{background:#a3cfb9;cursor:not-allowed;box-shadow:none;transform:none}
.result-box{display:none;background:#e8f7ef;border:2px dashed #1a7a4a;border-radius:12px;padding:2rem;text-align:center;margin-bottom:2rem}
.result-box h2{font-size:1.8rem;color:#1a7a4a;margin-bottom:0.5rem}
.result-box p {font-size:1.1rem;font-weight:600;color:#5a7a66}
</style>
</head>
<body>

<div class="top-bar">
    <div class="top-logo">Test<span>Bazar</span></div>
    <div class="timer-box" id="timerBox">⏱️ 10:00</div>
</div>

<div class="main-container">
    <div class="set-header">
        <h1>দ্বিতীয় অধ্যায়: জীবনের प्रवाहমানতা</h1>
        <p>প্র্যাকটিস সেট - ১ (কোশ বিভাজন এবং কোশ চক্র)</p>
    </div>

    <div class="result-box" id="resultBox">
        <h2>পরীক্ষার ফলাফল</h2>
        <p id="scoreText"></p>
    </div>

    <form id="quizForm">
        <div id="questionsContainer"></div>
        <div class="submit-area">
            <button type="button" class="submit-btn" id="submitBtn" onclick="submitQuiz()">খাতা জমা দিন (Submit)</button>
        </div>
    </form>
</div>

<script>
const questions = [{"q": "১. 'ক্রোমোজোম' শব্দটি প্রথম কে প্রবর্তন করেন?", "opts": ["গ্রেগর জোহান মেন্ডেল", "ওয়ালডেয়ার", "জোহানসেন", "চার্লস ডারউইন"], "ans": 1, "exp": "১৮৮৮ সালে বিজ্ঞানী ওয়ালডেয়ার প্রথম ক্রোমাটিন জালিকা থেকে সৃষ্ট দণ্ডাকার এই গঠনটির নাম দেন 'ক্রোমোজোম' (Chroma = রং এবং soma = দেহ)।"}, {"q": "২. মানুষের দেহকোশে অটোজোমের সংখ্যা কত?", "opts": ["২২টি", "৪৬টি", "৪৪টি", "২৩টি"], "ans": 2, "exp": "মানুষের প্রতিটি দেহকোশে মোট ৪৬টি (২৩ জোড়া) ক্রোমোজোম থাকে। এর মধ্যে ৪৪টি (২২ জোড়া) হলো অটোজোম (দেহজ বৈশিষ্ট্য নিয়ন্ত্রক) এবং বাকি ২টি হলো সেক্স ক্রোমোজোম বা অ্যালোজোম (লিঙ্গ নির্ধারক, যেমন- XX বা XY)।"}, {"q": "৩. DNA অণুর দ্বি-তন্ত্রী (Double helix) বা প্যাঁচানো সিঁড়ির মতো মডেল কারা আবিষ্কার করেন?", "opts": ["ওয়াটসন ও ক্রিক", "বেলিস ও স্টারলিং", "ওপারিন ও হ্যালডেন", "বোভেরি ও সাটন"], "ans": 0, "exp": "১৯৫৩ সালে বিজ্ঞানী জেমস ওয়াটসন, ফ্রান্সিস ক্রিক এবং মরিস উইলকিনস DNA-এর দ্বি-তন্ত্রী গঠন আবিষ্কার করেন, যার জন্য তাঁরা ১৯৬২ সালে নোবেল পুরস্কারও পেয়েছিলেন।"}, {"q": "৪. DNA-তে থাইমিনের (Thymine) পরিবর্তে RNA-তে কোন নাইট্রোজেনযুক্ত ক্ষারকটি থাকে?", "opts": ["সাইটোসিন", "গুয়ানিন", "ইউরাসিল", "অ্যাডিনিন"], "ans": 2, "exp": "DNA এবং RNA উভয়েই অ্যাডিনিন, গুয়ানিন ও সাইটোসিন থাকে। তবে DNA-তে পিরিমিডিন ক্ষারক হিসেবে থাইমিন (T) থাকে, কিন্তু RNA-তে থাইমিনের বদলে ইউরাসিল (U) থাকে।"}, {"q": "৫. সেন্ট্রোমিয়ারের অবস্থান ক্রোমোজোমের ঠিক মাঝখানে হলে, তাকে কী ধরনের ক্রোমোজোম বলে?", "opts": ["মেটাসেন্ট্রিক", "অ্যাক্রোসেন্ট্রিক", "টেলোসেন্ট্রিক", "সাব-মেটাসেন্ট্রিক"], "ans": 0, "exp": "সেন্ট্রোমিয়ার ক্রোমোজোমের মাঝখানে থাকলে তাকে মেটাসেন্ট্রিক ক্রোমোজোম বলে। কোশ বিভাজনের অ্যানাফেজ দশায় এটি ইংরেজি 'V' অক্ষরের মতো আকৃতি ধারণ করে।"}, {"q": "৬. কোশচক্রের কোন দশায় DNA-এর সংশ্লেষ বা প্রতিলিপি গঠন ঘটে?", "opts": ["G1 দশা", "S দশা", "G2 দশা", "M দশা"], "ans": 1, "exp": "ইন্টারফেজ দশার S দশা বা সংশ্লেষ (Synthesis) দশায় অত্যন্ত গুরুত্বপূর্ণ কাজটি ঘটে, অর্থাৎ DNA-এর নতুন প্রতিলিপি তৈরি বা DNA সংশ্লেষিত হয়।"}, {"q": "৭. ক্রোমোজোমের একদম দুই প্রান্তীয় অংশকে কী বলা হয়?", "opts": ["সেন্ট্রোমিয়ার", "স্যাটেলাইট", "কাইনেটোকোর", "টেলোমিয়ার"], "ans": 3, "exp": "ক্রোমোজোমের দুই প্রান্তভাগকে টেলোমিয়ার বলে। এটি ক্রোমোজোমের নির্দিষ্ট গঠন ও স্থায়িত্ব রক্ষা করে এবং দুটি ক্রোমোজোমকে একে অপরের সাথে জুড়ে যেতে বাধা দেয়।"}, {"q": "৮. ক্রোমোজোমের যে নির্দিষ্ট স্থানে কোশ বিভাজনকালে বেমতন্তু এসে যুক্ত হয়, তাকে কী বলে?", "opts": ["টেলোমিয়ার", "কাইনেটোকোর", "গৌণ খাঁজ", "স্যাটেলাইট"], "ans": 1, "exp": "ক্রোমোজোমের মুখ্য খাঁজ বা সেন্ট্রোমিয়ার অঞ্চলে প্রোটিন নির্মিত একটি প্যাড বা চাকতি থাকে যাকে কাইনেটোকোর বলে। এই কাইনেটোকোরের সাথেই বেমতন্তুর অনুনালিকা যুক্ত হয়।"}, {"q": "৯. কোন ধরনের ক্রোমাটিন অঞ্চলে ক্রসিং ওভার ঘটে এবং জিনগতভাবে বেশি সক্রিয় থাকে?", "opts": ["হেটারোক্রোমাটিন", "ইউক্রোমাটিন", "ক্রোমোজোম", "নিউক্লিওজোম"], "ans": 1, "exp": "ইউক্রোমাটিন হলো ক্রোমোজোমের হালকা রং ধারণকারী অংশ যা জিনগতভাবে সক্রিয়। মিয়োসিস কোশ বিভাজনের সময় এই অংশেই জিনের খণ্ডাংশ বিনিময় বা ক্রসিং ওভার ঘটে।"}, {"q": "১০. ক্রোমোজোমের গৌণ খাঁজ অঞ্চলটি কোশ বিভাজনের সময় কী গঠনে সাহায্য করে?", "opts": ["বেমযন্ত্র", "নিউক্লিওলাস", "সেন্ট্রোজোম", "কোশপর্দা"], "ans": 1, "exp": "ক্রোমোজোমের গৌণ খাঁজ অঞ্চলটি নিউক্লিওলাস সৃষ্টিতে বা সংগঠনে সক্রিয় ভূমিকা পালন করে বলে একে নিউক্লিওলার অর্গানাইজিং রিজিয়ন বা সংক্ষেপে NOR বলা হয়।"}, {"q": "১১. DNA অণুতে গুয়ানিন (G) এবং সাইটোসিন (C)-এর মধ্যে কয়টি হাইড্রোজেন বন্ড থাকে?", "opts": ["২টি", "৩টি", "৪টি", "১টি"], "ans": 1, "exp": "DNA অণুতে অ্যাডিনিন সর্বদা থাইমিনের সাথে (A=T) ২টি হাইড্রোজেন বন্ড দ্বারা যুক্ত থাকে এবং গুয়ানিন সর্বদা সাইটোসিনের সাথে (G≡C) ৩টি হাইড্রোজেন বন্ড দ্বারা যুক্ত থাকে।"}, {"q": "১২. যে সকল কোশ কখনোই বিভাজিত হয় না (যেমন স্নায়ুকোশ), তারা কোশচক্রের কোন দশায় আটকে থাকে?", "opts": ["G1 দশা", "S দশা", "G2 দশা", "G0 দশা"], "ans": 3, "exp": "স্নায়ুকোশ, পেশিকোশ বা পরিণত লোহিত রক্তকণিকা বিভাজন সংক্রান্ত সমস্ত প্রক্রিয়া থেকে নিজেকে প্রত্যাহার করে নেয় এবং ইন্টারফেজের একটি বিশেষ নিষ্ক্রিয় দশায় আটকে থাকে, যাকে G0 (জি-জিরো) দশা বলে।"}, {"q": "১৩. কোনো প্রজাতির হ্যাপ্লয়েড ক্রোমোজোম সেটে উপস্থিত জিনের সম্পূর্ণ সমষ্টিকে একত্রে কী বলা হয়?", "opts": ["জিনোটাইপ", "অ্যালিল", "জিনোম", "ক্রসিং ওভার"], "ans": 2, "exp": "কোনো প্রজাতির হ্যাপ্লয়েড সেট ক্রোমোজোমে (যেমন গ্যামেটে থাকা ক্রোমোজোমে) অবস্থিত জিনের সম্পূর্ণ সেটকে একত্রে জিনোম (Genome) বলে।"}, {"q": "১৪. যে ক্রোমোজোমের একদম প্রান্তে সেন্ট্রোমিয়ার থাকে, তাকে কী বলে?", "opts": ["টেলোসেন্ট্রিক", "মেটাসেন্ট্রিক", "সাব-মেটাসেন্ট্রিক", "অ্যাক্রোসেন্ট্রিক"], "ans": 0, "exp": "সেন্ট্রোমিয়ার ক্রোমোজোমের একপ্রান্তে থাকলে তাকে টেলোসেন্ট্রিক বলে, যা কোশ বিভাজনের অ্যানাফেজ দশায় ইংরেজি 'I' অক্ষরের মতো দেখতে হয়।"}, {"q": "১৫. ইউক্যারিওটিক ক্রোমোজোমের গঠনগত উপাদানগুলির মধ্যে কোন প্রোটিনটি 'ক্ষারীয়' প্রকৃতির হয়?", "opts": ["হিস্টোন", "নন-হিস্টোন", "স্ক্যাফল্ড", "অ্যাকটিন"], "ans": 0, "exp": "ইউক্যারিওটিক ক্রোমোজোমে থাকা হিস্টোন প্রোটিনগুলো (যেমন- H2A, H2B, H3, H4) ক্ষারীয় প্রকৃতির হয়, অন্যদিকে নন-হিস্টোন প্রোটিনগুলো সাধারণত আম্লিক প্রকৃতির হয়ে থাকে।"}];
const LABELS = ['ক', 'খ', 'গ', 'ঘ'];
let timeLeft = 600; // 10 minutes
let timerInterval;

function initQuiz() {
    const container = document.getElementById('questionsContainer');
    container.innerHTML = '';
    
    questions.forEach((q, qIdx) => {
        const card = document.createElement('div');
        card.className = 'question-card';
        card.id = `qCard_${qIdx}`;
        
        let optsHtml = '';
        q.opts.forEach((opt, oIdx) => {
            optsHtml += `
                <button type="button" class="opt" id="opt_${qIdx}_${oIdx}" onclick="selectOption(${qIdx}, ${oIdx})">
                    <div class="opt-circle">${LABELS[oIdx]}</div>
                    <div class="opt-text">${opt}</div>
                </button>
            `;
        });
        
        card.innerHTML = `
            <div class="q-title"><strong>${q.q}</strong></div>
            <div class="opts-grid">${optsHtml}</div>
            <div class="explanation-box" id="exp_${qIdx}">
                <strong>💡 ব্যাখ্যা:</strong> ${q.exp}
            </div>
        `;
        container.appendChild(card);
    });
    
    startTimer();
}

let userAnswers = new Array(questions.length).fill(null);

function selectOption(qIdx, oIdx) {
    userAnswers[qIdx] = oIdx;
    for(let i=0; i<4; i++) {
        const btn = document.getElementById(`opt_${qIdx}_${i}`);
        if(i === oIdx) {
            btn.classList.add('selected');
        } else {
            btn.classList.remove('selected');
        }
    }
}

function startTimer() {
    timerInterval = setInterval(() => {
        if (timeLeft <= 0) {
            clearInterval(timerInterval);
            submitQuiz();
        } else {
            timeLeft--;
            let mins = Math.floor(timeLeft / 60);
            let secs = timeLeft % 60;
            const timerBox = document.getElementById('timerBox');
            timerBox.textContent = `⏱️ ${mins}:${secs < 10 ? '0' : ''}${secs}`;
            if(timeLeft <= 60) {
                timerBox.classList.add('danger');
            }
        }
    }, 1000);
}

function submitQuiz() {
    clearInterval(timerInterval);
    document.getElementById('submitBtn').disabled = true;
    
    let score = 0;
    
    questions.forEach((q, qIdx) => {
        const selected = userAnswers[qIdx];
        const correct = q.ans;
        
        for(let i=0; i<4; i++) {
            const btn = document.getElementById(`opt_${qIdx}_${i}`);
            btn.classList.add('disabled');
            if(i === correct) {
                btn.classList.remove('selected');
                btn.classList.add('correct-ans');
            }
            if(selected === i && selected !== correct) {
                btn.classList.remove('selected');
                btn.classList.add('wrong-ans');
            }
        }
        
        if(selected === correct) {
            score++;
        }
        document.getElementById(`exp_${qIdx}`).style.display = 'block';
    });
    
    document.getElementById('scoreText').innerHTML = `আপনার মোট স্কোর: <strong>${score} / ${questions.length}</strong>`;
    document.getElementById('resultBox').style.display = 'block';
    window.scrollTo({top: 0, behavior: 'smooth'});
}

window.onload = initQuiz;
</script>
</body>
</html>
