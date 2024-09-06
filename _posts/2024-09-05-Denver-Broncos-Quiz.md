---
toc: false
layout: post
title: Denver Broncos Quiz
type: ccc
permalink: /denver-broncos-quiz
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
        background-color: #0033a0; /* Denver Broncos' navy blue color */
        color: white;
        border: none;
        padding: 10px 20px;
        border-radius: 4px;
        cursor: pointer;
        font-size: 16px;
        margin: 5px;
    }

    button:hover {
        background-color: #002c77;
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
                question: "In which year did the Denver Broncos win their first Super Bowl?",
                options: ["1997", "1998", "2000", "2015"],
                answer: "1997"
            },
            {
                question: "Who holds the record for the most career touchdown passes for the Broncos?",
                options: ["Peyton Manning", "John Elway", "Jake Plummer", "Tim Tebow"],
                answer: "Peyton Manning"
            },
            {
                question: "Which stadium is the home of the Denver Broncos?",
                options: ["Mile High Stadium", "Empower Field at Mile High", "Sports Authority Field", "Coors Field"],
                answer: "Empower Field at Mile High"
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