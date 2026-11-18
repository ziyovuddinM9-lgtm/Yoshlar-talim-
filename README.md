<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Intellektual Savol-Javob Viktorinasi</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: #333;
            margin: 0;
            padding: 20px;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
        }
        .container {
            background: #ffffff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 25px rgba(0,0,0,0.2);
            max-width: 500px;
            width: 100%;
            text-align: center;
        }
        h1 { color: #4a5568; margin-bottom: 10px; font-size: 24px; }
        .age-badge {
            background: #667eea;
            color: white;
            padding: 5px 15px;
            border-radius: 20px;
            font-size: 14px;
            display: inline-block;
            margin-bottom: 20px;
        }
        .question { font-size: 18px; font-weight: 600; margin-bottom: 20px; color: #2d3748; }
        .options { display: flex; flex-direction: column; gap: 10px; }
        .btn {
            background: #edf2f7;
            border: 2px solid #cbd5e0;
            padding: 12px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            transition: all 0.2s;
        }
        .btn:hover { background: #667eea; color: white; border-color: #667eea; }
        #result { font-size: 20px; font-weight: bold; color: #2f855a; }
    </style>
</head>
<body>
    <div class="container" id="app">
        <h1>Yoshlar Viktorinasi</h1>
        <div id="quiz-box">
            <div class="age-badge" id="age-group">Bosqich: 10-13 yosh</div>
            <div class="question" id="question-text">Savol yuklanmoqda...</div>
            <div class="options" id="options-box"></div>
        </div>
    </div>

    <script>
        const quizData = [
            { age: "10-13 yosh (Boshlang'ich mantiq)", q: "1 soatda necha soniya bor?", options: ["3600 soniya", "60 soniya", "1440 soniya", "2400 soniya"], correct: 0 },
            { age: "14-17 yosh (Maktab fanlari)", q: "Qaysi planetada hayot mavjud va u Quyoshdan uchinchi o'rinda turadi?", options: ["Mars", "Venera", "Yer", "Yupiter"], correct: 2 },
            { age: "18-23 yosh (Talabalik va Texnologiya)", q: "Internet tarmog'ining asosiy protokollaridan biri bo'lgan 'HTTP' so'zining ma'nosi nima?", options: ["HyperText Transfer Protocol", "High Technology Transfer Program", "Hyperlink Text Transmission Process", "Home Tool Transfer Protocol"], correct: 0 },
            { age: "24-31 yosh (Kattalar va Falsafa/Mantiq)", q: "Iqtisodiyotda 'Inflyatsiya' so'zi nimani anglatadi?", options: ["Pul qadrining tushishi va narxlar oshishi", "Ishlab chiqarishning keskin ko'payishi", "Valyuta kursining mustahkamlanishi", "Bank foizlarining pasayishi"], correct: 0 }
        ];

        let currentQuestion = 0;
        let score = 0;

        function loadQuiz() {
            if (currentQuestion < quizData.length) {
                const currentData = quizData[currentQuestion];
                document.getElementById("age-group").innerText = currentData.age;
                document.getElementById("question-text").innerText = currentData.q;
                
                const optionsBox = document.getElementById("options-box");
                optionsBox.innerHTML = "";
                
                currentData.options.forEach((opt, index) => {
                    const button = document.createElement("button");
                    button.classList.add("btn");
                    button.innerText = opt;
                    button.onclick = () => selectAnswer(index);
                    optionsBox.appendChild(button);
                });
            } else {
                document.getElementById("quiz-box").innerHTML = `
                    <h2>O'yin yakunlandi! 🎉</h2>
                    <p>Sizning umumiy natijangiz: ${score} / ${quizData.length}</p>
                    <p style="color: #4a5568; margin-top: 15px;">Siz barcha yosh bosqichlarini muvaffaqiyatli yakunladingiz!</p>
                `;
            }
        }

        function selectAnswer(index) {
            if (index === quizData[currentQuestion].correct) {
                score++;
            }
            currentQuestion++;
            loadQuiz();
        }

        loadQuiz();
    </script>
</body>
</html>
