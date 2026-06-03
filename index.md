---
layout: default
title: DigiDhruv - Master Your Multiplication Tables
description: Interactive gamified learning experience for multiplication tables 5-16
---

# 🎮 Missing Tables Game

Welcome to **DigiDhruv's** interactive multiplication tables game! Master your skills through engaging, bite-sized lessons designed for quick mastery.

---

## ✨ Game Features

- 🌱 **Three Difficulty Levels** - Progress from beginner to expert
- 🎯 **Instant Feedback** - Know your answers right away
- 🎵 **Sound Effects** - Audio cues for engagement
- 🏆 **Leaderboard** - Track your top 5 scores
- 📱 **Fully Responsive** - Works on all devices
- ⚡ **No External Dependencies** - Pure HTML, CSS, and JavaScript

---

## 📊 How It Works

| Level | Name | Questions | Difficulty |
|-------|------|-----------|------------|
| 1 | 🌱 Very Easy | Tables 1-4 (5-16) | Beginner |
| 2 | 🌿 Medium | Tables 5-8 (5-16) | Intermediate |
| 3 | 🔥 Super | Tables 9-12 (5-16) | Expert |

---

## 🎮 Start Playing

Ready to test your skills? Click the button below to begin!

<div id="game-container" class="game-wrapper">
    <div id="start-screen" class="start-screen">
        <p class="start-text">Master tables 5 to 16!</p>
        <button onclick="startGame()" class="start-btn">🚀 Start Game</button>
    </div>
    
    <div id="game-ui" style="display:none;">
        <div id="level" class="level"></div>
        <div id="question" class="question"></div>
        <input type="number" id="answer" placeholder="?" class="answer-input" onkeydown="if(event.key==='Enter') checkAnswer()">
        <br>
        <button onclick="checkAnswer()" class="submit-btn">Submit Answer</button>
        <div id="feedback" class="feedback-box"></div>
    </div>
</div>

---

## 💡 Tips for Success

1. **Focus** - Take your time to think about each problem
2. **Practice** - Repetition helps build muscle memory
3. **Track Progress** - Keep playing to improve your scores
4. **Challenge Yourself** - Move through the levels strategically

---

<script>
const audioCtx = new (window.AudioContext || window.webkitAudioContext)();

function playSound(type) {
    try {
        const osc = audioCtx.createOscillator();
        const gain = audioCtx.createGain();
        osc.connect(gain);
        gain.connect(audioCtx.destination);

        if (type === 'correct') {
            osc.frequency.setValueAtTime(523.25, audioCtx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(880, audioCtx.currentTime + 0.1);
            gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
            osc.start();
            osc.stop(audioCtx.currentTime + 0.3);
        } else if (type === 'wrong') {
            osc.frequency.setValueAtTime(150, audioCtx.currentTime);
            gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
            gain.gain.exponentialRampToValueAtTime(0.01, audioCtx.currentTime + 0.3);
            osc.start();
            osc.stop(audioCtx.currentTime + 0.3);
        } else if (type === 'levelUp') {
            osc.frequency.setValueAtTime(440, audioCtx.currentTime);
            osc.frequency.exponentialRampToValueAtTime(880, audioCtx.currentTime + 0.5);
            gain.gain.setValueAtTime(0.1, audioCtx.currentTime);
            osc.start();
            osc.stop(audioCtx.currentTime + 0.5);
        }
    } catch (e) {
        console.log('Audio context not available');
    }
}

const levels = [
    { name: "🌱 Very Easy Level", questions: [] },
    { name: "🌿 Medium Level", questions: [] },
    { name: "🔥 Super Level", questions: [] }
];

let tables = [5,6,7,8,9,10,11,12,13,14,15,16];
let currentLevel = 0;
let currentQuestion = 0;
let score = 0;

function generateQuestions() {
    levels.forEach(l => l.questions = []);
    
    tables.forEach(t => {
        for (let i=1; i<=12; i++) {
            let q = { table: t, multiplier: i, answer: t*i };
            if (i <= 4) levels[0].questions.push(q);
            else if (i <= 8) levels[1].questions.push(q);
            else levels[2].questions.push(q);
        }
    });

    levels.forEach(level => {
        level.questions = level.questions.sort(() => 0.5 - Math.random()).slice(0,5);
    });
}

function startGame() {
    document.getElementById("start-screen").style.display = "none";
    document.getElementById("game-ui").style.display = "block";
    generateQuestions();
    loadQuestion();
}

function loadQuestion() {
    document.getElementById("level").innerText = levels[currentLevel].name;
    let q = levels[currentLevel].questions[currentQuestion];
    document.getElementById("question").innerText = `${q.table} × ${q.multiplier} = ?`;
    document.getElementById("answer").value = "";
    document.getElementById("answer").focus();
    document.getElementById("feedback").innerHTML = "";
}

function checkAnswer() {
    let q = levels[currentLevel].questions[currentQuestion];
    let userAns = document.getElementById("answer").value;

    if (userAns === "") return;

    const feedback = document.getElementById("feedback");
    if (parseInt(userAns) === q.answer) {
        score++;
        playSound('correct');
        const items = ["🌸", "🍎", "🌻", "🍓", "🍊"];
        const words = ["Correct", "Good", "Nice", "Excellent", "Perfect"];
        let randItem = items[Math.floor(Math.random() * items.length)];
        let randWord = words[Math.floor(Math.random() * words.length)];
        feedback.innerHTML = `<div class='correct'>${randItem} ${randWord}!</div>`;
    } else {
        playSound('wrong');
        feedback.innerHTML = `<div class='wrong'>❌ Wrong! It was ${q.answer}</div>`;
    }

    currentQuestion++;

    setTimeout(() => {
        if (currentQuestion >= 5) {
            currentLevel++;
            currentQuestion = 0;
            if (currentLevel < 3) playSound('levelUp');

            if (currentLevel >= 3) {
                showScore();
                return;
            }
        }
        loadQuestion();
    }, 1500);
}

function showScore() {
    let name = prompt("Amazing! Enter your name for the Score Card:", "Player");
    if (!name) name = "Player";

    let leaderboard = JSON.parse(localStorage.getItem("tableLeaderboard")) || [];
    leaderboard.push({ name: name, score: score });
    leaderboard.sort((a, b) => b.score - a.score);
    leaderboard = leaderboard.slice(0, 5);
    localStorage.setItem("tableLeaderboard", JSON.stringify(leaderboard));

    let list = leaderboard.map((s) => `<li>${s.name}: ${s.score}/15</li>`).join("");

    document.getElementById("game-container").innerHTML = `
        <h2 style="text-align: center;">🏆 Final Score Card</h2>
        <div style="font-size: 24px; margin: 20px 0; text-align: center;">
            <strong>${name}</strong>, you scored <br>
            <span style="font-size: 48px; color: #3498db;">${score} / 15</span>
        </div>
        <hr>
        <h3 style="text-align: center;">📊 Top 5 Leaderboard</h3>
        <ol style="display: inline-block;">${list}</ol>
        <br><br>
        <div style="text-align: center;">
            <button onclick="location.reload()">🔁 Play Again</button>
        </div>
    `;
}
</script>
