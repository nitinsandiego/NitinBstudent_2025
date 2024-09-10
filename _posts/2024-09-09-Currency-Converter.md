---
toc: false
layout: post
title: Currency Converter
description: Input two currencies and my code will give you the current exchange rate.
type: ccc
permalink: /currency-converter
courses: {csa: {week: 3}}
---

<style>
    .converter-container {
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
        background: #28a745;
        color: #fff;
        border-radius: 5px;
        cursor: pointer;
        transition: background 0.3s;
    }
    button:hover {
        background: #218838;
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


<div class="converter-container">
    <label for="currencyFrom">Convert from (currency code, e.g., USD):</label>
    <input type="text" id="currencyFrom" placeholder="Enter source currency">
    <label for="currencyTo" style="margin-top: 15px;">Convert to (currency code, e.g., EUR):</label>
    <input type="text" id="currencyTo" placeholder="Enter target currency">
    <button onclick="convertCurrency()">Convert</button>
    <div id="conversion-result"></div>
</div>

<script>
    function convertCurrency() {
        const currencyFrom = document.getElementById("currencyFrom").value.trim().toUpperCase();
        const currencyTo = document.getElementById("currencyTo").value.trim().toUpperCase();

        if (!currencyFrom || !currencyTo) {
            alert("Please enter both currencies.");
            return;
        }

        const apiKey = "2ee9c8b9bd607482664e667e";
        const apiUrl = `https://v6.exchangerate-api.com/v6/${apiKey}/pair/${currencyFrom}/${currencyTo}`;

        fetch(apiUrl)
            .then(response => response.json())
            .then(data => {
                if (data.result === "success") {
                    const rate = data.conversion_rate;
                    const resultContainer = document.getElementById("conversion-result");
                    resultContainer.innerHTML = `
                        <h2>Exchange Rate: ${currencyFrom} to ${currencyTo}</h2>
                        <p>1 ${currencyFrom} = ${rate} ${currencyTo}</p>
                    `;
                } else {
                    console.error("Error fetching conversion rate.");
                    alert("Invalid currency codes or data unavailable.");
                }
            })
            .catch(error => {
                console.error("Error fetching conversion rate:", error);
                alert("There was an error processing your request.");
            });
    }
</script>
