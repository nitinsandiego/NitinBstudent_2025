---
layout: page
title: About
permalink: /about/
---


<style>
    /* Style looks pretty compact, trace grid-container and grid-item in the code */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 200px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }
    .image-gallery {
        display: flex;
        flex-wrap: nowrap;
        overflow-x: auto;
        gap: 10px;
        }
    .image-gallery img {
        max-height: 250px;
        object-fit: cover;
        border-radius: 5px;
    }
    img{
        max-height:350px;
        display: block;
        margin-left: auto;
        margin-right: auto;
    }
</style>

<!-- This grid_container class is for the CSS styling, the id is for JavaScript connection -->
# My Interests

<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container");

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var favorite_teams = [
        {"team": "https://upload.wikimedia.org/wikipedia/en/thumb/e/eb/Manchester_City_FC_badge.svg/632px-Manchester_City_FC_badge.svg.png?20180205235525", "name": "Manchester City FC", "description": "Favorite Premier League Team", "link": "{{ site.baseurl }}/manchester-city-quiz"},
        {"team": "https://upload.wikimedia.org/wikipedia/commons/2/21/Mercedes-Benz_in_Formula_One_logo.svg", "name": "Mercedes F1", "description": "Favorite Formula 1 Team", "link": "{{ site.baseurl }}/mercedes-f1-quiz"},
        {"team": "https://upload.wikimedia.org/wikipedia/en/a/a7/Paris_Saint-Germain_F.C..svg", "name": "PSG", "description": "Favorite Ligue 1 Team", "link": "{{ site.baseurl }}/psg-quiz"},
        {"team": "https://upload.wikimedia.org/wikipedia/en/4/44/Denver_Broncos_logo.svg", "name": "Denver Broncos", "description": "Favorite NFL Team", "link": "{{ site.baseurl }}/denver-broncos-quiz"},
    ]; 
    
    // 3. Build grid items inside of our container for each row of data
    for (const team of favorite_teams) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";

        // Create an anchor tag with the href attribute
        var link = document.createElement("a");
        link.href = team.link;

        // Add "img" HTML tag for the team
        var img = document.createElement("img");
        img.src = team.team;
        img.alt = team.name + " Team";

        // Append img to the link
        link.appendChild(img);

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = team.description;

        // Append the link and description to the grid item DIV
        gridItem.appendChild(link);
        gridItem.appendChild(description);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>

![alt text](/NitinBstudent_2025/images/A3FA4A7B-3DC5-4890-8EF4-1A12097C9AE2_1_105_c.jpeg)

- 🇬🇧 ⚽️ My favorite Premier League team is Manchester City F.C. They have the won the last 4 Premier League titles.
- 🏎️ 🏁 My favorite F1 team Mercedes AMG Petronas F1 Team. They have won 8 Constructors World Championships and 7 Drivers World Championship.
- 🇫🇷 ⚽️ My favorite Ligue One team is Paris Saint-Germain F.C. PSG has won the most Ligue One titles with 12 titles.
- ⛰️ 🏈 My favorite NFL team is the Denver Broncos. They have won 3 Super Bowls.


<div class="image-gallery">
    <img src="{{site.baseurl}}/images/fae3f0b0-a4c4-49ee-90a5-a2b5c47005ed-aad7165e-56aa-423a-9453-3d85bd7bd67c.jpeg" alt="Image 1">
    <img src="{{site.baseurl}}/images/mercedes-amgwins-formula-1-champions_8.jpg" alt="Image 2">
    <img src="{{site.baseurl}}/images/Paris-Saint-Germain-celebration-PSG-vs-Dijon-Ligue-1-2019.jpg" alt="Image 3">
    <img src="{{site.baseurl}}/images/103369676-GettyImages-508989972.jpg" alt="Image 4">
</div>