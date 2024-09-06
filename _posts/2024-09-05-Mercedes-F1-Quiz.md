---
toc: false
layout: post
title: Mercedes F1 Quiz
type: ccc
permalink: /mercedes-f1-quiz
courses: {csa: {week: 2}}
---

<style>

    h1 {
        margin: 0;
    }

    #quiz-container, #result-container {
        background: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }

    button {
        background-color: #00d2be; /* Mercedes F1 color */
        color: white;
        border: none;
        padding: 10px 20px;
        border-radius: 4px;
        cursor: pointer;
        font-size: 16px;
        margin: 5px;
    }

    button:hover {
        background-color: #00a89c;
    }

    .hidden {
        display: none;
    }

    #question-container {
        margin-bottom: 20px;
    }
</style>
<main>
    <section id="quiz-container">
        <div id="question-container">
            <!-- Questions will be added here dynamically -->
        </div>
        <button id="next-button">Next</button>
    </section>
    <section id="result-container" class="hidden">
        <h2>Quiz Results</h2>
        <p id="result-text"></p>
        <button id="restart-button">Restart Quiz</button>
    </section>
</main>

<script>
    document.addEventListener("DOMContentLoaded", function () {
        const questions = [
            {
                question: "When did Mercedes AMG Petronas win their first Constructors' Championship?",
                options: ["2014", "2015", "2016", "2017"],
                answer: "2014"
            },
            {
                question: "Who is the Mercedes F1 Team's most successful driver?",
                options: ["Nico Rosberg", "Lewis Hamilton", "Valtteri Bottas", "Michael Schumacher"],
                answer: "Lewis Hamilton"
            },
            {
                question: "What color is the Mercedes F1 car primarily painted?",
                options: ["Black", "Silver", "White", "Green"],
                answer: "Silver"
            }
        ];

        let currentQuestionIndex = 0;
        let score = 0;

        const questionContainer = document.getElementById("question-container");
        const nextButton = document.getElementById("next-button");
        const resultContainer = document.getElementById("result-container");
        const resultText = document.getElementById("result-text");
        const restartButton = document.getElementById("restart-button");

        function loadQuestion() {
            const question = questions[currentQuestionIndex];
            questionContainer.innerHTML = `
                <h2>${question.question}</h2>
                ${question.options.map((option) => `
                    <button class="option-button">${option}</button>
                `).join('')}
            `;
            document.querySelectorAll('.option-button').forEach(button => {
                button.addEventListener('click', handleOptionClick);
            });
        }

        function handleOptionClick(event) {
            const selectedAnswer = event.target.textContent;
            if (selectedAnswer === questions[currentQuestionIndex].answer) {
                score++;
            }
            currentQuestionIndex++;
            if (currentQuestionIndex < questions.length) {
                loadQuestion();
            } else {
                showResult();
            }
        }

        function showResult() {
            questionContainer.classList.add("hidden");
            resultContainer.classList.remove("hidden");
            resultText.textContent = `You scored ${score} out of ${questions.length}.`;
        }

        function restartQuiz() {
            currentQuestionIndex = 0;
            score = 0;
            questionContainer.classList.remove("hidden");
            resultContainer.classList.add("hidden");
            loadQuestion();
        }

        nextButton.addEventListener('click', loadQuestion);
        restartButton.addEventListener('click', restartQuiz);

        loadQuestion(); // Load the first question
    });
</script>
