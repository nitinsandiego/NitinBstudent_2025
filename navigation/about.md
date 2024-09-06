---
layout: page
title: About
permalink: /about/
---

![alt text](/NitinBstudent_2025/images/A3FA4A7B-3DC5-4890-8EF4-1A12097C9AE2_1_105_c.jpeg)

Hello! My name is Nitin Balaji, and I'm 16 years old. From a young age, I've been fascinated by technology and how it shapes our world. This curiosity has driven me to pursue a path in coding, and I’m thrilled about the endless possibilities it offers. My ultimate dream is to work as a software engineer, where I can contribute to innovative projects that make a difference.

Beyond coding, I have a deep passion for Formula 1 racing. The thrill of the race, the precision of the engineering, and the sheer determination of the drivers captivate me. My favorite team is Mercedes AMG Petronas Formula 1 Team, and I admire Lewis Hamilton not just for his incredible talent on the track but also for his resilience and advocacy off it.

But my interests don’t stop there. I’m also an enthusiastic NFL fan, and you’ll often find me cheering for the Denver Broncos. The strategy, teamwork, and excitement of football make it a sport I love to follow.

Another passion of mine is collecting sneakers. As a sneakerhead, I appreciate the artistry and culture behind each pair of shoes. Every collection tells a story, and I enjoy being part of that vibrant community.

Academically, I’m currently taking AP Computer Science A (AP CSA), and I’m eager to dive deeper into software development. I look forward to expanding my knowledge through future software courses, and I’m excited about the journey ahead in the world of tech.

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
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }
</style>

<!-- This grid_container class is for the CSS styling, the id is for JavaScript connection -->
<br>
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var favorite_teams = [
        {"team": "https://upload.wikimedia.org/wikipedia/en/thumb/e/eb/Manchester_City_FC_badge.svg/632px-Manchester_City_FC_badge.svg.png?20180205235525", "name": "Manchester City FC", "description": "Favorite Premier League Team"},
        {"team": "https://upload.wikimedia.org/wikipedia/commons/2/21/Mercedes-Benz_in_Formula_One_logo.svg", "name": "Mercedes F1", "description": "Favorite Formula 1 Team"},
        {"team": "https://upload.wikimedia.org/wikipedia/en/a/a7/Paris_Saint-Germain_F.C..svg", "name": "PSG", "description":"Favorite Ligue 1 Team"},
        {"team": "https://upload.wikimedia.org/wikipedia/en/4/44/Denver_Broncos_logo.svg", "name": "Denver Broncos", "description": "Favorite NFL Team"},
    ]; 
    
    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const team of favorite_teams) {
        console.log(team); // Check the data in the console
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the team
        var img = document.createElement("img");
        img.src = team.team; // concatenate the source and team
        img.alt = team.name + " Team"; // better alt text 
        console.log("Image created:", img); // Check the image source in the console

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = team.description; // extract the description
        console.log("Description created:", description.textContent); // Debug log

        // Add "p" HTML tag for the name
        var name = document.createElement("p");
        console.log("Name created:", team.name); // Debug log
        name.textContent = team.name;  // extract the name
        console.log("Name created:", name.textContent); // Debug log

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(name);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>