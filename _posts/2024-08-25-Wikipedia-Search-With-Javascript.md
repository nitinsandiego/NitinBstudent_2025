---
layout: post
title: Wikipedia Summary Search with JavaScript
courses: {csa: {week: 0}}
type: collab
permalink: /wikipediasummary
toc: false
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
<body>
    <input type="text" id="topicInput" placeholder="Enter a topic">
    <button id="fetchButton">Fetch Summary</button>
    <div id="summaryContainer"></div>

<script>
        document.addEventListener("DOMContentLoaded", () => {
            const fetchButton = document.getElementById("fetchButton");
            const topicInput = document.getElementById("topicInput");
            const summaryContainer = document.getElementById("summaryContainer");

            fetchButton.addEventListener("click", () => {
                const topic = topicInput.value;
                if (topic) {
                    fetchSummary(topic);
                }
            });

            function fetchSummary(topic) {
                const apiUrl = `https://en.wikipedia.org/api/rest_v1/page/summary/${encodeURIComponent(topic)}`;

                fetch(apiUrl)
                    .then(response => response.json())
                    .then(data => {
                        if (data.extract) {
                            summaryContainer.innerHTML = `<br><h2>${data.title}</h2><p>${data.extract}</p>`;
                        } else {
                            summaryContainer.innerHTML = "<br><p>Summary not found.</p>";
                        }
                    })
                    .catch(error => {
                        console.error("Error fetching data:", error);
                        summaryContainer.innerHTML = "<br><p>An error occurred while fetching data.</p>";
                    });
            }
        });
</script>
</body>
</html>
