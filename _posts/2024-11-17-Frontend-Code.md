---
toc: false
layout: post
title: Frontend Code
type: collab
permalink: /frontendcode
courses: {csa: {week: 12}}
---

# Home Page
```html
<head>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      background-color: #ffffff;
    }
    /* Navigation Bar */
    .navbar {
      display: flex;
      justify-content: center;
      background-color: #121212;
      padding: 10px 0;
      font-size: 18px;
    }
    .navbar a {
      margin: 0 15px;
      color: #333;
      text-decoration: none;
    }
    /* Period Header */
    .period-header {
      background-color: #FFFFFF;
      color: black;
      text-align: center;
      padding: 20px;
      font-size: 36px;
      font-weight: bold;
    }
    /* Container for Tables using Grid */
    .container {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-template-rows: repeat(3, auto);
      gap: 20px;
      justify-content: center;
      height: calc(100vh - 150px);
      padding-top: 20px;
    }
    /* Table Icon (4 chairs) */
    .table-icon {
      position: relative;
      width: 200px;
      height: 200px;
    }
    .table {
      position: absolute;
      top: 50%;
      left: 50%;
      width: 100px;
      height: 100px;
      background-color: #8B4513; /* Brown color for the table */
      transform: translate(-50%, -50%);
      border-radius: 5px;
    }
    .chair {
      position: absolute;
      width: 30px;
      height: 30px;
      background-color: #333; /* Dark color for the chairs */
      border-radius: 50%;
    }
    .chair1 { top: 5px; left: 50%; transform: translateX(-50%); }
    .chair2 { bottom: 5px; left: 50%; transform: translateX(-50%); }
    .chair3 { left: 35px; top: 50%; transform: translateY(-50%); }
    .chair4 { right: 35px; top: 50%; transform: translateY(-50%); }
    .table-icon:hover .chair {
      background-color: #FFD700; /* Change chair color to yellow on hover */
    }
    /* Button Styling */
    .table-button {
      width: 160px;
      height: 160px;
      background-color: #FFFFFF !important;
      border: none;
      border-radius: 5px;
      font-size: 18px;
      color: black !important;
      text-align: center;
      cursor: pointer;
      position: relative;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }
    /* Button Grid Placement */
    #button1 { grid-area: 1 / 1; }
    #button2 { grid-area: 2 / 1; }
    #button3 { grid-area: 3 / 1; }
    #button4 { grid-area: 4 / 2; }
    #button5 { grid-area: 3 / 3; }
    #button6 { grid-area: 2 / 3; }
    /* Search Bar Styling */
    .search-container {
      display: flex;
      justify-content: center;
      padding: 20px;
    }
    .search-container input[type="text"] {
      width: 300px;
      padding: 8px;
      border-radius: 4px;
      border: 1px solid #ccc;
      font-size: 16px;
    }
    .search-container button {
      margin-left: 10px;
      padding: 8px 12px;
      font-size: 16px;
      cursor: pointer;
      border: none;
      background-color: #121212;
      color: white;
      border-radius: 4px;
    }
  </style>
</head>
<body>

  <!-- Navigation Bar -->
  <div class="navbar">
    <a href="#">Period 1</a>
    <a href="#">Period 3</a>
  </div>

  <!-- Period Header -->
  <div class="period-header">
    Period 3
  </div>

  <!-- Search Bar -->
  <div class="search-container">
    <input type="text" id="searchName" placeholder="Enter student name">
    <button onclick="searchStudent()">Search</button>
  </div>

  <!-- Container for Tables -->
  <div class="container">
    <button id="button1" class="table-button" onclick="fetchRequest(1)">
      <div class="table-icon">
        <div class="table"></div>
        <div class="chair chair1"></div>
        <div class="chair chair2"></div>
        <div class="chair chair3"></div>
        <div class="chair chair4"></div>
      </div>
      Table 1
    </button>
    <button id="button2" class="table-button" onclick="fetchRequest(2)">
      <div class="table-icon">
        <div class="table"></div>
        <div class="chair chair1"></div>
        <div class="chair chair2"></div>
        <div class="chair chair3"></div>
        <div class="chair chair4"></div>
      </div>
      Table 2
    </button>
    <button id="button3" class="table-button" onclick="fetchRequest(3)">
      <div class="table-icon">
        <div class="table"></div>
        <div class="chair chair1"></div>
        <div class="chair chair2"></div>
        <div class="chair chair3"></div>
        <div class="chair chair4"></div>
      </div>
      Table 3
    </button>
    <button id="button4" class="table-button" onclick="fetchRequest(4)">
      <div class="table-icon">
        <div class="table"></div>
        <div class="chair chair1"></div>
        <div class="chair chair2"></div>
        <div class="chair chair3"></div>
        <div class="chair chair4"></div>
      </div>
      Table 4
    </button>
    <button id="button5" class="table-button" onclick="fetchRequest(5)">
      <div class="table-icon">
        <div class="table"></div>
        <div class="chair chair1"></div>
        <div class="chair chair2"></div>
        <div class="chair chair3"></div>
        <div class="chair chair4"></div>
      </div>
      Table 5
    </button>
    <button id="button6" class="table-button" onclick="fetchRequest(6)">
      <div class="table-icon">
        <div class="table"></div>
        <div class="chair chair1"></div>
        <div class="chair chair2"></div>
        <div class="chair chair3"></div>
        <div class="chair chair4"></div>
      </div>
      Table 6
    </button>
  </div>

  <script>
    function fetchRequest(tableNumber) {
      // Redirect to tableDetails.html with the table number in the URL
      window.location.href = `/student_2025/tabledetails?table=${tableNumber}`;
    }

    function searchStudent() {
      const name = document.getElementById("searchName").value;

      const criteriaDto = {
        name: name,
        course: "CSA",
        trimester: 1,
        period: 3
      };

      fetch("http://localhost:8181/api/students/find", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(criteriaDto)
      })
      .then(response => {
        if (!response.ok) {
          throw new Error("Network response was not ok");
        }
        return response.json();
      })
      .then(data => {
        const params = new URLSearchParams({
          name: data.name,
          course: data.course,
          trimester: data.trimester,
          period: data.period
        });
        window.location.href = "/student_2025/student-info?" + params.toString();
      })
      .catch(error => {
        console.error("There was a problem with the fetch operation:", error);
        alert("Student not found.");
      });
    }
  </script>
</body>
```

# Table Details Page
```html
<style>
  h2 {
      color: white;
  }
  #student-cards-container {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
      margin-top: 20px;
      justify-content: center;
  }
  .student-card {
      background-color: #fff;
      border: 1px solid #ddd;
      border-radius: 5px;
      padding: 20px;
      width: 280px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      text-align: center;
      display: flex;
      flex-direction: column;
      align-items: center;
  }
  .student-card h3 {
      margin: 10px 0;
      font-size: 20px;
      color: black;
  }
  .student-card p {
      margin: 5px 0;
      font-size: 16px;
      color: black;
  }
  .student-image {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      margin-bottom: 10px;
  }
  .delete-button, .add-task-button {
      margin-top: 10px;
      padding: 8px 12px;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
  }
  .delete-button {
      background-color: #ff4d4d;
  }
  .add-task-button {
      background-color: #28a745;
  }
  .create-button {
      margin: 20px auto;
      padding: 10px 30px;
      background-color: #007BFF;
      color: white;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      display: block;
      font-size: 16px;
      font-weight: bold;
  }
</style>
<body>
  <h2 id="page-title">Students in Table</h2>
  <div id="student-cards-container"></div>
  <button class="create-button" onclick="createStudent()">Create Student</button>

  <script>
    document.addEventListener("DOMContentLoaded", function() {
      const urlParams = new URLSearchParams(window.location.search);
      const tableNumber = urlParams.get('table');

      if (tableNumber) {
        fetch("http://localhost:8181/api/students/find-team", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            course: "CSA",
            trimester: 1,
            period: 3,
            table: parseInt(tableNumber)
          })
        })
        .then(response => {
          if (!response.ok) throw new Error("Network response was not ok");
          return response.json();
        })
        .then(data => {
          const container = document.getElementById("student-cards-container");
          container.innerHTML = "";

          // Set the project name in the title using the first student in the list (assuming same project for the table)
          if (data.length > 0) {
            document.getElementById("page-title").textContent = `Project: ${data[0].project} - Students in Table ${tableNumber}`;
          }

          data.forEach(student => {
            const card = document.createElement("div");
            card.className = "student-card";
            
            // Fetch GitHub profile picture
            fetch(`https://api.github.com/users/${student.username}`)
              .then(response => response.json())
              .then(githubData => {
                const imageUrl = githubData.avatar_url || "default-image-url.jpg";
                card.innerHTML = `
                  <img src="${imageUrl}" alt="${student.username}'s Profile Picture" class="student-image">
                  <h3>${student.name}</h3>
                  <p>Username: ${student.username}</p>
                  <p>Table Number: ${student.tableNumber}</p>
                  <p>Course: ${student.course}</p>
                  <p>Trimester: ${student.trimester}</p>
                  <p>Period: ${student.period}</p>
                  <p>Tasks: ${student.tasks.join(", ")}</p>
                  <button class="add-task-button" onclick="addTask('${student.username}')">Add Task</button>
                  <button class="delete-button" onclick="deleteStudent('${student.username}')">Delete</button>
                `;
              })
              .catch(error => {
                console.error("GitHub profile fetch error:", error);
                card.innerHTML = `
                  <img src="default-image-url.jpg" alt="Default Profile Picture" class="student-image">
                  <h3>${student.name}</h3>
                  <p>Username: ${student.username}</p>
                  <p>Table Number: ${student.tableNumber}</p>
                  <p>Course: ${student.course}</p>
                  <p>Trimester: ${student.trimester}</p>
                  <p>Period: ${student.period}</p>
                  <p>Tasks: ${student.tasks.join(", ")}</p>
                  <button class="add-task-button" onclick="addTask('${student.username}')">Add Task</button>
                  <button class="delete-button" onclick="deleteStudent('${student.username}')">Delete</button>
                `;
              });
            container.appendChild(card);
          });
        })
        .catch(error => console.error("There was a problem with the fetch operation:", error));
      } else {
        document.getElementById("student-cards-container").innerHTML = "<p>No table selected.</p>";
      }
    });
function addTask(username) {
      const newTask = prompt("Enter a new task:");
      if (newTask) {
        fetch("http://localhost:8181/api/students/update-tasks", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            username: username,
            tasks: [newTask]
          })
        })
        .then(response => {
          if (!response.ok) throw new Error("Failed to add task");
          return response.json();
        })
        .then(student => {
          alert("Task added successfully!");
          location.reload();
        })
        .catch(error => console.error("There was a problem with the add task operation:", error));
      } else {
        alert("Task cannot be empty.");
      }
    }
        function createStudent() {
      const name = prompt("Enter student name:");
      const username = prompt("Enter student username:");
      const tableNumber = prompt("Enter table number:");
      const course = "CSA";
      const trimester = 1;
      const period = 3;
      const tasks = []; // Initial empty tasks

      if (name && username && tableNumber) {
        fetch("http://127.0.0.1:8181/api/students/create", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({
            name: name,
            username: username,
            tableNumber: parseInt(tableNumber),
            course: course,
            trimester: trimester,
            period: period,
            tasks: tasks
          })
        })
        .then(response => {
          if (!response.ok) throw new Error("Failed to create student");
          return response.json();
        })
        .then(student => {
          alert("Student created successfully!");
          location.reload();
        })
        .catch(error => console.error("There was a problem with the create operation:", error));
      } else {
        alert("Please fill in all fields to create a student.");
      }
    }

    function deleteStudent(username) {
      fetch(`http://127.0.0.1:8181/api/students/delete?username=${encodeURIComponent(username)}`, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        mode: "cors"
      })
      .then(response => {
        if (!response.ok) throw new Error("Failed to delete student with username: " + username);
        return response.text();
      })
      .then(message => {
        console.log(message);
        alert(message);
        location.reload();
      })
      .catch(error => console.error("There was a problem with the delete operation:", error));
    }
  </script>
</body>
```

# Student Details Page
```html
<html>
<head>
  <title>Student GitHub Profile</title>
  <style>
    #details-container {
      display: flex;
      align-items: center;
      gap: 20px;
      background-color: #3a3a3a;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
      max-width: 700px;
    }
    #profile-pic {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      border: 2px solid #ddd;
    }
    .details-content {
      display: flex;
      flex-direction: column;
      gap: 5px;
    }
    .details-content a {
      color: #b0d4ff;
      text-decoration: none;
    }
    .details-content p {
      margin: 2px 0;
      font-size: 16px;
    }
  </style>
</head>
<body>

<div id="details-container">
  <img id="profile-pic" src="" alt="Profile Picture">
  <div class="details-content">
    <p><strong>Username:</strong> <span id="githubUsername"></span></p>
    <p><strong>Profile URL:</strong> <a id="githubProfile" href="" target="_blank"></a></p>
    <p><strong>Issues:</strong> <span id="githubIssues"></span></p>
    <p><strong>Pull Requests:</strong> <span id="githubPulls"></span></p>
    <p><strong>Commits:</strong> <span id="githubCommits"></span></p>
    <p><strong>Public Repos:</strong> <span id="githubRepos"></span></p>
    <p><strong>Public Gists:</strong> <span id="githubGists"></span></p>
    <p><strong>Followers:</strong> <span id="githubFollowers"></span></p>
  </div>
</div>

<script>
  async function fetchStudentDetails() {
    const urlParams = new URLSearchParams(window.location.search);
    const name = urlParams.get("name");
    const course = urlParams.get("course");
    const trimester = urlParams.get("trimester");
    const period = urlParams.get("period");

    const criteriaDto = {
      name: name,
      course: course,
      trimester: parseInt(trimester),
      period: parseInt(period)
    };

    try {
      // Fetch student data from your backend
      const studentResponse = await fetch("http://localhost:8181/api/students/find", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(criteriaDto)
      });

      if (!studentResponse.ok) throw new Error("Student not found");

      const student = await studentResponse.json();
      const githubUsername = student.username;

      // Fetch GitHub user profile
      const githubResponse = await fetch(`https://api.github.com/users/${githubUsername}`);
      if (!githubResponse.ok) throw new Error("GitHub profile not found");
      const githubData = await githubResponse.json();

      // Fetch GitHub user events for issues, PRs, and commits data
      const eventsResponse = await fetch(`https://api.github.com/users/${githubUsername}/events`);
      if (!eventsResponse.ok) throw new Error("GitHub events not found");
      const eventsData = await eventsResponse.json();

      // Define the start date for filtering events
      const startDate = new Date("2024-08-01T00:00:00Z");

      // Count events occurring after the start date
      const commitsCount = eventsData.filter(event => 
        event.type === "PushEvent" && new Date(event.created_at) >= startDate
      ).length;

      const prsCount = eventsData.filter(event => 
        event.type === "PullRequestEvent" && new Date(event.created_at) >= startDate
      ).length;

      const issuesCount = eventsData.filter(event => 
        event.type === "IssuesEvent" && new Date(event.created_at) >= startDate
      ).length;

      // Populate the details on the page
      document.getElementById("profile-pic").src = githubData.avatar_url;
      document.getElementById("githubUsername").innerText = githubData.login;
      document.getElementById("githubProfile").href = githubData.html_url;
      document.getElementById("githubProfile").innerText = githubData.html_url;
      document.getElementById("githubRepos").innerText = githubData.public_repos;
      document.getElementById("githubGists").innerText = githubData.public_gists;
      document.getElementById("githubFollowers").innerText = githubData.followers;

      // Display the filtered event data
      document.getElementById("githubIssues").innerText = issuesCount;
      document.getElementById("githubPulls").innerText = prsCount;
      document.getElementById("githubCommits").innerText = commitsCount;

    } catch (error) {
      console.error("Error:", error);
      alert(error.message);
    }
  }

  window.onload = fetchStudentDetails;
</script>

</body>
</html>
```