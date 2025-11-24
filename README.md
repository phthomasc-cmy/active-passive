<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Active vs Passive Voice Adventure! 🌟</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600&family=Noto+Sans+TC:wght@400;700&display=swap');

        :root {
            --primary: #FF9AA2; /* Soft Pink */
            --secondary: #B5EAD7; /* Mint */
            --accent: #C7CEEA; /* Periwinkle */
            --text: #555;
            --white: #ffffff;
        }

        body {
            font-family: 'Fredoka', 'Noto Sans TC', sans-serif;
            background-color: #FFF7F8;
            color: var(--text);
            margin: 0;
            padding: 20px;
            line-height: 1.6;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        h1, h2, h3 {
            text-align: center;
            color: #FF6F91;
        }

        .card {
            background: var(--white);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 8px 20px rgba(0,0,0,0.05);
            border: 2px solid var(--secondary);
        }

        .grammar-box {
            display: flex;
            flex-direction: column;
            gap: 15px;
        }

        .concept {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
            background-color: #F3FAFF;
            padding: 15px;
            border-radius: 15px;
            font-size: 1.1em;
        }

        .highlight {
            color: #FF6F91;
            font-weight: bold;
        }

        .chinese-hint {
            color: #888;
            font-size: 0.9em;
            display: block;
            margin-top: 5px;
        }

        /* Button Styles */
        .btn {
            background-color: var(--accent);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 50px;
            font-size: 1em;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.2s;
            font-family: inherit;
            font-weight: 600;
            margin: 5px;
        }

        .btn:hover {
            transform: scale(1.05);
            background-color: #aab5e0;
        }

        .btn.active-voice { background-color: #FFB7B2; }
        .btn.passive-voice { background-color: #B5EAD7; color: #444; }

        /* Quiz Area */
        #quiz-container {
            text-align: center;
        }

        #question-text {
            font-size: 1.4em;
            margin-bottom: 10px;
            font-weight: bold;
        }

        #feedback {
            margin-top: 15px;
            font-size: 1.2em;
            min-height: 30px;
        }

        .correct { color: #6FCF97; }
        .wrong { color: #EB5757; }

        .emoji-scene {
            font-size: 3em;
            text-align: center;
            margin: 10px 0;
            animation: float 3s ease-in-out infinite;
        }

        @keyframes float {
            0% { transform: translateY(0px); }
            50% { transform: translateY(-10px); }
            100% { transform: translateY(0px); }
        }

        .formula {
            background: #FFF9C4;
            padding: 10px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            margin-top: 10px;
        }

    </style>
</head>
<body>

<div class="container">

    <!-- Header -->
    <h1>🐱 Grammar Fun: Active & Passive 🐶<br><span style="font-size:0.6em">主動語態與被動語態</span></h1>

    <!-- Learning Section -->
    <div class="card">
        <h2>📚 Let's Learn! (學習時間)</h2>
        
        <div class="grammar-box">
            <!-- Active Voice -->
            <div class="concept" style="border-left: 5px solid #FFB7B2;">
                <div>
                    <div class="emoji-scene">🐱 ➡️ 🐟</div>
                    <strong>Active Voice (主動語態):</strong><br>
                    The Subject does the action.<br>
                    <span class="chinese-hint">主詞「做」動作。</span>
                    <div class="formula">Subject + Verb + Object</div>
                    <p><em>"The cat eats the fish." (貓吃魚)</em></p>
                </div>
            </div>

            <!-- Passive Voice -->
            <div class="concept" style="border-left: 5px solid #B5EAD7;">
                <div>
                    <div class="emoji-scene">🐟 ⬅️ 🐱</div>
                    <strong>Passive Voice (被動語態):</strong><br>
                    The action happens TO the Subject.<br>
                    <span class="chinese-hint">主詞「被」做動作 (通常有 by)。</span>
                    <div class="formula">Subject + Be Verb + V3 (p.p) + by + Agent</div>
                    <p><em>"The fish is eaten by the cat." (魚被貓吃)</em></p>
                </div>
            </div>
        </div>
    </div>

    <!-- Interactive Quiz Section -->
    <div class="card" id="quiz-section">
        <h2>🎮 Mini Quiz (小測驗)</h2>
        <p style="text-align:center;">Is this Active or Passive? <br> <span class="chinese-hint">這句是主動還是被動呢？</span></p>
        
        <div id="quiz-container">
            <div class="emoji-scene" id="quiz-emoji">🧐</div>
            <div id="question-text">Loading...</div>
            <div id="question-translation" class="chinese-hint">...</div>
            
            <div style="margin-top: 20px;">
                <button class="btn active-voice" onclick="checkAnswer('active')">Active (主動) 🏃‍♂️</button>
                <button class="btn passive-voice" onclick="checkAnswer('passive')">Passive (被動) 🛌</button>
            </div>

            <div id="feedback"></div>
            <button class="btn" id="next-btn" style="display:none; background-color:#FFD166; color:#444;" onclick="nextQuestion()">Next Question ➡️</button>
        </div>
    </div>

</div>

<script>
    // 1. The Source Data (Unshuffled)
    const sourceQuestions = [
        {
            text: "The boy kicks the ball.",
            trans: "這個男孩踢球。",
            emoji: "👦 🦵 ⚽",
            type: "active"
        },
        {
            text: "The ball is kicked by the boy.",
            trans: "球被男孩踢。",
            emoji: "⚽ 💨 👦",
            type: "passive"
        },
        {
            text: "Sarah paints a picture.",
            trans: "Sarah 畫了一幅畫。",
            emoji: "🎨 🖌️",
            type: "active"
        },
        {
            text: "The cheese was eaten by the mouse.",
            trans: "起司被老鼠吃掉了。",
            emoji: "🧀 🐭",
            type: "passive"
        },
        {
            text: "The teacher loves the students.",
            trans: "老師愛學生們。",
            emoji: "👩‍🏫 ❤️ 🎓",
            type: "active"
        },
        {
            text: "The song is sung by the bird.",
            trans: "這首歌是由鳥兒唱的。",
            emoji: "🐦 🎵",
            type: "passive"
        },
        {
            text: "Mom cooks dinner.",
            trans: "媽媽煮晚餐。",
            emoji: "👩‍🍳 🥘",
            type: "active"
        },
        {
            text: "The car was washed by Dad.",
            trans: "車子被爸爸洗了。",
            emoji: "🚗 🧽 👨",
            type: "passive"
        }
    ];

    let currentQuestions = []; // This will hold the randomized list
    let currentQuestionIndex = 0;
    let score = 0;

    // DOM Elements
    const questionText = document.getElementById("question-text");
    const questionTrans = document.getElementById("question-translation");
    const quizEmoji = document.getElementById("quiz-emoji");
    const feedback = document.getElementById("feedback");
    const nextBtn = document.getElementById("next-btn");

    // 2. The Shuffle Function (Fisher-Yates Shuffle)
    function shuffleArray(array) {
        let arr = [...array]; // Create a copy
        for (let i = arr.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [arr[i], arr[j]] = [arr[j], arr[i]];
        }
        return arr;
    }

    // Initialize
    function loadQuestion() {
        const q = currentQuestions[currentQuestionIndex];
        questionText.textContent = q.text;
        questionTrans.textContent = q.trans;
        quizEmoji.textContent = q.emoji;
        feedback.textContent = "";
        nextBtn.style.display = "none";
        
        // Enable buttons again
        const buttons = document.querySelectorAll('#quiz-container .btn');
        buttons.forEach(btn => {
            if(btn.id !== 'next-btn') btn.disabled = false;
        });
    }

    function checkAnswer(userChoice) {
        const correctType = currentQuestions[currentQuestionIndex].type;
        const buttons = document.querySelectorAll('#quiz-container .btn');
        
        // Disable answer buttons to prevent double clicking
        buttons.forEach(btn => {
            if (btn.id !== "next-btn") btn.disabled = true;
        });

        if (userChoice === correctType) {
            feedback.innerHTML = "<span class='correct'>Correct! Great job! 🎉 (答對了！)</span>";
            score++;
        } else {
            feedback.innerHTML = "<span class='wrong'>Oops! Try again next time. 🥺 (答錯了...)</span>";
        }
        
        nextBtn.style.display = "inline-block";
    }

    function nextQuestion() {
        currentQuestionIndex++;
        if (currentQuestionIndex < currentQuestions.length) {
            loadQuestion();
        } else {
            // End of quiz
            quizEmoji.textContent = "🏆";
            questionText.textContent = "You finished the quiz!";
            questionTrans.textContent = `Final Score: ${score} / ${currentQuestions.length}`;
            feedback.innerHTML = "";
            
            // Hide answer buttons
            document.querySelectorAll('#quiz-container .btn').forEach(btn => {
                if(btn.id !== "next-btn") btn.style.display = "none";
            });
            
            nextBtn.textContent = "Restart (Again!) 🔄";
            nextBtn.onclick = restartQuiz;
        }
    }

    function restartQuiz() {
        currentQuestionIndex = 0;
        score = 0;
        
        // 3. Shuffle questions again on restart
        currentQuestions = shuffleArray(sourceQuestions);

        nextBtn.textContent = "Next Question ➡️";
        nextBtn.onclick = nextQuestion;
        
        // Show answer buttons again
        document.querySelectorAll('#quiz-container .btn').forEach(btn => {
            if(btn.id !== "next-btn") btn.style.display = "inline-block";
        });
        
        loadQuestion();
    }

    // Start the game (Initial Shuffle)
    restartQuiz();

</script>

</body>
</html>
