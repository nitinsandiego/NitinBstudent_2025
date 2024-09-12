---
toc: false
layout: post
title: Flight Tracker
description: Enter a flight number to get the current status.
type: collab
permalink: /flight-tracker
courses: {csa: {week: 3}}
---

<style>
    .flight-container {
        background: rgba(255, 255, 255, 0.9);
        padding: 30px;
        border-radius: 10px;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
        width: 100%;
        max-width: 600px;
        text-align: center;
    }
    h2 {
        margin-bottom: 20px;
        font-size: 2em;
        color: #555;
    }
    input {
        width: 100%;
        padding: 10px;
        margin-bottom: 20px;
        border-radius: 5px;
        border: 1px solid #ccc;
        font-size: 1em;
    }
    button {
        padding: 10px 20px;
        border: none;
        background: #007BFF;
        color: #fff;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1.1em;
        transition: background 0.3s;
    }
    button:hover {
        background: #0056b3;
    }
    .flight-info {
        margin-top: 20px;
        font-size: 1.2em;
    }
</style>

<div class="flight-container">
    <h2>Flight Tracker</h2>
    <input type="text" id="flightNumber" placeholder="Enter flight number (e.g., AA100)" />
    <button onclick="fetchFlightData()">Track Flight</button>
    <div id="flightResults" class="flight-info"></div>
</div>

<script>
    function fetchFlightData() {
        const flightNumber = document.getElementById("flightNumber").value.trim();
        if (!flightNumber) {
            alert("Please enter a valid flight number.");
            return;
        }

        const apiKey = "d27bdb73e72cd6a6d730b42bdac02ebf"; // Replace with your actual API key
        const apiUrl = `http://api.aviationstack.com/v1/flights?access_key=${apiKey}&flight_iata=${flightNumber}`;

        fetch(apiUrl)
            .then(response => response.json())
            .then(data => {
                const flightData = data.data[0];
                const flightResults = document.getElementById("flightResults");

                if (flightData) {
                    flightResults.innerHTML = `
                        <h3>Flight Status: ${flightData.flight_status}</h3>
                        <p><strong>Airline:</strong> ${flightData.airline.name}</p>
                        <p><strong>Flight Number:</strong> ${flightData.flight.iata}</p>
                        <p><strong>Departure:</strong> ${flightData.departure.airport} (${flightData.departure.iata})</p>
                        <p><strong>Arrival:</strong> ${flightData.arrival.airport} (${flightData.arrival.iata})</p>
                        <p><strong>Scheduled Departure:</strong> ${new Date(flightData.departure.scheduled).toLocaleString()}</p>
                        <p><strong>Scheduled Arrival:</strong> ${new Date(flightData.arrival.scheduled).toLocaleString()}</p>
                    `;
                } else {
                    flightResults.innerHTML = "<p>No data available for this flight. Please check the flight number and try again.</p>";
                }
            })
            .catch(error => {
                console.error("Error fetching flight data:", error);
                document.getElementById("flightResults").innerHTML = "<p>Failed to fetch flight data. Please try again later.</p>";
            });
    }
</script>
