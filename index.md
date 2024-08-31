---
layout: base
title: Nitin Balaji 
description: This is Nitin Balaji's page
hide: true
---

<style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
            color: #333; /* Ensures text is visible */
        }
        .intro {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            color: #333; /* Ensures text is visible */
        }
        .gallery {
            display: flex;
            justify-content: space-around;
            margin-top: 20px;
        }
        .gallery img {
            width: 30%;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        .projects {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            color: #333; /* Ensures text is visible */
        }
        .projects h2 {
            color: #333; /* Ensures text is visible */
            margin-bottom: 10px;
        }
        .projects ul {
            list-style-type: disc;
            padding-left: 20px;
        }
        .projects ul li {
            margin-bottom: 8px;
        }
    </style>
# Nitin Balaji's Page

Go to my [Github account](https://github.com/nitinsandiego) !!

## About Me

<div class="into">
    <p>
Hi! This is Nitin Balaji. I am 16 years old. I am an aspiring coder and my dream job is to work as a software engineer. A little about is I am a huge fan of Formula 1 and my favorite F1 Team is Mercedes AMG Petronas Formual 1 Team, and my favorite driver is Lewis Hamilton. Not only am I avid Formula 1 fan, I am also a fan of NFL and my favorite NFL team is the Denver Broncos. Also, I am a sneaker head and love collecting shoes. I am really excited to be taking AP CSA and also excited to take future software courses.
    </p>
</div>

### My Interests
![MercedesAMGF1](images/MercedesAMGF1.jpg)
![LewisHamilton](images/LewisHamilton.png)
![Shoes](images/Shoes.png)


<h1>Rock, Paper, Scissors Game</h1>
<p>Choose your move:</p>
<button onclick="playGame('rock')">Rock</button>
<button onclick="playGame('paper')">Paper</button>
<button onclick="playGame('scissors')">Scissors</button>
<p id="result"></p>
<p id="rounds">Rounds played: 0</p>
<script>
    var rounds = 0;
    function playGame(playerChoice) {
        var choices = ["rock", "paper", "scissors"];
        var computerChoice = choices[Math.floor(Math.random() * 3)];
        rounds++;
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
        document.getElementById("rounds").textContent = "Rounds played: " + rounds;
    }
</script>
