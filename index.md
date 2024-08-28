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
</body>

## Overview of Hacks, Study and Tangibles
Blogging in GitHub pages is a way to learn and code at the same time. 

- Plans, Lists, [Scrum Boards](https://clickup.com/blog/scrum-board/) help you to track key events, show progress and record time.  Effort is a big part of your class grade.  Show plans and time spent!
- [Hacks(Todo)](https://levelup.gitconnected.com/six-ultimate-daily-hacks-for-every-programmer-60f5f10feae) enable you to stay in focus with key requirements of the class.  Each Hack will produce Tangibles.
- Tangibles or [Tangible Artifacts](https://en.wikipedia.org/wiki/Artifact_(software_development)) are things you accumulate as a learner and coder. 
</body>