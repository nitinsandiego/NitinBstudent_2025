---
layout: base
title: Student Home 
description: Home Page
hide: true
---

# Nitin Balaji's Page

Go to my [Github account](https://github.com/nitinsandiego) !!

## About Me
Hi! This is Nitin Balaji. I am 16 years old. I am an aspiring coder and my dream job is to work as a software engineer. A little about is I am a huge fan of Formula 1 and my favorite F1 Team is Mercedes AMG Petronas Formual 1 Team, and my favorite driver is Lewis Hamilton. Not only am I avid Formula 1 fan, I am also a fan of NFL and my favorite NFL team is the Denver Broncos. Also, I am a sneaker head and love collecting shoes. I am really excited to be taking AP CSA and also excited to take future software courses.

### My Interests
![MercedesAMGF1](images/MercedesAMGF1.jpg)
![LewisHamilton](images/LewisHamilton.png)
![DenverBroncos](images/DenverBroncos.png)
![Shoes](images/Shoes.png)

## About Me Freeform Picture
My interests are coding, shoes, especially Jordans, Formula 1, and running.
![Freeform About Me](images/FreeformAboutMe.png)

<body>
    <h1>Rock, Paper, Scissors Game</h1>
    <p>Choose your move:</p>
    <button onclick="playGame('rock')">Rock</button>
    <button onclick="playGame('paper')">Paper</button>
    <button onclick="playGame('scissors')">Scissors</button>
    <p id="result"></p>
    <script>
        function playGame(playerChoice) {
            var choices = ["rock", "paper", "scissors"];
            var reuslt = "";
            for(var i = 0; i < 3; i++) {
                var computerChoice = choices[Math.floor(Math.random() * 3)];
                if(playerChoice === computerChoice) {
                    result += "Round" + (i+1) + ": It's a tie!";
                } else if (
                    (playerChoice === "rock" && computerChoice === "scissors") ||
                    (playerChoice === "paper" && computerChoice === "rock") ||
                    (playerChoice === "scissors" && computerChoice === "paper")
                ) {
                    result += "Round " + (i+1) + ": You win! ";
                } else {
                    result += "Round " + (i+1) + ": Computer wins! ";
                }
            }
        }
        document.getElementById("result").textContent = result;
    </script>
</body>