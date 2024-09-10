---
toc: false
layout: post
title: Distance Between Cities
description: Input two cities and my code will calculate the distance between them.
type: ccc
permalink: /distance-between-cities
courses: {csa: {week: 3}}
---

<style>
    .distance-container {
        background: rgba(255, 255, 255, 0.8);
        padding: 25px 40px;
        border-radius: 8px;
        box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
        width: 100%;
        max-width: 500px;
    }
    button {
        margin-top: 20px;
        padding: 10px 20px;
        border: none;
        background: #FF7F50;
        color: #fff;
        border-radius: 5px;
        cursor: pointer;
        transition: background 0.3s;
    }
    button:hover {
        background: #FF4500;
    }
    h2 {
        font-weight: 500;
    }
    p {
        font-size: 1.1em;
        margin: 5px 0;
    }
    input {
        width: 100%;
        padding: 10px;
        margin-top: 10px;
        border-radius: 5px;
        border: 1px solid #ccc;
    }
</style>

<div class="distance-container">
    <label for="cityFrom">Enter the first city:</label>
    <input type="text" id="cityFrom" placeholder="Enter the first city">
    <label for="cityTo" style="margin-top: 15px;">Enter the second city:</label>
    <input type="text" id="cityTo" placeholder="Enter the second city">
    <button id="calculateButton">Calculate Distance</button>
    <div id="distance-result"></div>
</div>

<script>
    window.onload = function() {
        document.getElementById("calculateButton").onclick = function() {
            const cityFrom = document.getElementById("cityFrom").value.trim();
            const cityTo = document.getElementById("cityTo").value.trim();

            if (!cityFrom || !cityTo) {
                alert("Please enter both cities.");
                return;
            }

            const apiKey = "2f154dace08459a35fe9522ff7de936d";
            const geocodeUrlFrom = `https://api.openweathermap.org/geo/1.0/direct?q=${cityFrom}&limit=1&appid=${apiKey}`;
            const geocodeUrlTo = `https://api.openweathermap.org/geo/1.0/direct?q=${cityTo}&limit=1&appid=${apiKey}`;

            Promise.all([fetch(geocodeUrlFrom), fetch(geocodeUrlTo)])
                .then(async ([responseFrom, responseTo]) => {
                    const [dataFrom] = await responseFrom.json();
                    const [dataTo] = await responseTo.json();

                    if (dataFrom && dataTo) {
                        const distance = calculateDistance(
                            dataFrom.lat, dataFrom.lon,
                            dataTo.lat, dataTo.lon
                        );
                        const resultContainer = document.getElementById("distance-result");
                        resultContainer.innerHTML = `
                            <h2>Distance Between ${cityFrom} and ${cityTo}</h2>
                            <p>${distance.toFixed(2)} kilometers</p>
                        `;
                    } else {
                        alert("Could not find one or both cities. Please try again.");
                    }
                })
                .catch(error => {
                    console.error("Error fetching geocoding data:", error);
                    alert("There was an error processing your request.");
                });
        };

        function calculateDistance(lat1, lon1, lat2, lon2) {
            const R = 6371; // Radius of the Earth in kilometers
            const dLat = (lat2 - lat1) * Math.PI / 180;
            const dLon = (lon2 - lon1) * Math.PI / 180;
            const a = 
                Math.sin(dLat / 2) * Math.sin(dLat / 2) +
                Math.cos(lat1 * Math.PI / 180) * Math.cos(lat2 * Math.PI / 180) *
                Math.sin(dLon / 2) * Math.sin(dLon / 2);
            const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1 - a));
            return R * c; // Distance in kilometers
        }
    };
</script>
