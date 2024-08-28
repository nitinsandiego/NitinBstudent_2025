---
toc: false
layout: post
title: Rock Paper Scissors Game
description: Play my rock paper wcissors game 
type: collab
permalink: /rockpaperscissors
courses: {csa: {week: 1}}
---


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            font-family: Arial, sans-serif;
        }
    </style>
</head>
<body>
    <p>Choose your move:</p>
    <button onclick="playGame('rock')">Rock</button>
    <button onclick="playGame('paper')">Paper</button>
    <button onclick="playGame('scissors')">Scissors</button>
    <p id="result"></p>

   <script>
        function playGame(playerChoice) {
            var choices = ["rock", "paper", "scissors"];
            var computerChoice = choices[Math.floor(Math.random() * 3)];
            
            if (playerChoice === computerChoice) {
                document.getElementById("result").textContent = "It's a tie!";
            } else if (
                (playerChoice === "rock" && computerChoice === "scissors") ||
                (playerChoice === "paper" && computerChoice === "rock") ||
                (playerChoice === "scissors" && computerChoice === "paper")
            ) {
                document.getElementById("result").textContent = "You win!";
            } else {
                document.getElementById("result").textContent = "Computer wins!";
            }
        }
</script>
</body>
</html>
