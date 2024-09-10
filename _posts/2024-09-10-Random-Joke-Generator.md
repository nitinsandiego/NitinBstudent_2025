---
toc: false
layout: post
title: Random Joke Generator
description: Click the button to get a random joke.
type: ccc
permalink: /random-joke-generator
courses: {csa: {week: 3}}
---

<style>
    .joke-container {
        background: rgba(255, 255, 255, 0.8);
        padding: 30px 40px;
        border-radius: 10px;
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
        width: 100%;
        max-width: 600px;
        text-align: center;
    }
    button {
        margin-top: 20px;
        padding: 10px 20px;
        border: none;
        background: #ff6347;
        color: #fff;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1.1em;
        transition: background 0.3s;
    }
    button:hover {
        background: #e5533d;
    }
    h2 {
        font-weight: 500;
        margin-bottom: 20px;
    }
    p {
        font-size: 1.2em;
        margin: 10px 0;
    }
</style>

<div class="joke-container">
    <h2>Random Joke Generator</h2>
    <p id="joke"></p>
    <button id="jokeButton">Get a Joke</button>
</div>

<script>
    window.onload = function() {
        document.getElementById("jokeButton").onclick = function() {
            fetchJoke();
        };

        function fetchJoke() {
            const apiUrl = "https://official-joke-api.appspot.com/random_joke";

            fetch(apiUrl)
                .then(response => response.json())
                .then(data => {
                    const jokeContainer = document.getElementById("joke");
                    jokeContainer.innerHTML = `
                        <p><strong>Setup:</strong> ${data.setup}</p>
                        <p><strong>Punchline:</strong> ${data.punchline}</p>
                    `;
                })
                .catch(error => {
                    console.error("Error fetching joke:", error);
                    document.getElementById("joke").textContent = "Oops! Something went wrong. Try again later.";
                });
        }
    };
</script>
