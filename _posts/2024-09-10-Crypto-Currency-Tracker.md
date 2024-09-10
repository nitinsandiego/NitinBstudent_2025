---
toc: false
layout: post
title: Cryptocurrency Price Tracker
description: Track real-time prices of various cryptocurrencies.
type: ccc
permalink: /crypto-price-tracker
courses: {csa: {week: 3}}
---

<style>
    .crypto-container {
        background: rgba(0, 0, 0, 0.8);
        padding: 30px 50px;
        border-radius: 10px;
        box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
        width: 100%;
        max-width: 600px;
        text-align: center;
    }
    h2 {
        margin-bottom: 20px;
        font-size: 2em;
        color: #00d9ff;
    }
    label {
        font-size: 1.1em;
        margin-top: 10px;
        display: block;
    }
    select, input {
        width: 100%;
        padding: 10px;
        margin-top: 10px;
        margin-bottom: 20px;
        border-radius: 5px;
        border: 1px solid #ccc;
        font-size: 1em;
    }
    button {
        padding: 10px 20px;
        border: none;
        background: #00d9ff;
        color: #333;
        border-radius: 5px;
        cursor: pointer;
        font-size: 1.1em;
        transition: background 0.3s;
    }
    button:hover {
        background: #00b5cc;
    }
    .crypto-info {
        margin-top: 20px;
        font-size: 1.2em;
    }
</style>

<div class="crypto-container">
    <h2>Cryptocurrency Price Tracker</h2>
    <label for="crypto">Select Cryptocurrency:</label>
    <select id="crypto">
        <option value="bitcoin">Bitcoin (BTC)</option>
        <option value="ethereum">Ethereum (ETH)</option>
        <option value="litecoin">Litecoin (LTC)</option>
    </select>

    <label for="currency">Select Currency:</label>
    <select id="currency">
        <option value="usd">US Dollar (USD)</option>
        <option value="eur">Euro (EUR)</option>
        <option value="gbp">British Pound (GBP)</option>
    </select>

    <button id="fetchPrice">Get Price</button>

    <div id="priceResult" class="crypto-info"></div>
</div>

<script>
    document.getElementById("fetchPrice").onclick = function() {
        const crypto = document.getElementById("crypto").value;
        const currency = document.getElementById("currency").value;

        const apiUrl = `https://api.coingecko.com/api/v3/simple/price?ids=${crypto}&vs_currencies=${currency}`;

        fetch(apiUrl)
            .then(response => response.json())
            .then(data => {
                const price = data[crypto][currency];
                document.getElementById("priceResult").innerHTML = `
                    <p>The current price of <strong>${crypto}</strong> in <strong>${currency.toUpperCase()}</strong> is: 
                    <span style="font-size: 1.5em; color: #00ff00;">${price}</span></p>
                `;
            })
            .catch(error => {
                console.error("Error fetching cryptocurrency data:", error);
                document.getElementById("priceResult").textContent = "Failed to fetch the price. Please try again later.";
            });
    };
</script>
