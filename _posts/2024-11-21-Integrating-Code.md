---
toc: false
layout: post
title: Integration Code
type: ccc
permalink: /integrationcode
courses: {csa: {week: 13}}
---

# My Feature 

## **Get Student Details Feature**

It takes the student's name and returns all their Github details, allowing Mr. Mortenson and others to quickly and seamlessly check the analytics of specific students.

### Backend Work

- Gets the details, which contain the GitHub username, of one specific student

```java
@RestController
@RequestMapping("/api/students")
public class StudentApiController {
    @Getter
    public static class CriteriaDto {
        private String name;
        private String course;
        private int trimester;
        private int period; 
    }

    @PostMapping("/find")
    public ResponseEntity<Student> getStudentByCriteria(
            @RequestBody CriteriaDto criteriaDto) {
        
        List<Student> students = studentJPARepository.findByNameCourseTrimesterPeriod(criteriaDto.getName(), criteriaDto.getCourse(), criteriaDto.getTrimester(), criteriaDto.getPeriod());
        
        if (students.isEmpty()) {
            return ResponseEntity.notFound().build();
        } else {
            return ResponseEntity.ok(students.get(0));
        }
    }
}
```

- JPA that connects to SQL database to person query
```java
public interface StudentJPARepository extends JpaRepository<Student, Long> {
    @Query(
        value = "SELECT * FROM students WHERE name = :name AND course = :course AND trimester = :trimester AND period = :period",
        nativeQuery = true
    )
    List<Student> findByNameCourseTrimesterPeriod(
        @Param("name") String name, 
        @Param("course") String course, 
        @Param("trimester") int trimester, 
        @Param("period") int period
    );
}
```

### Frontend Work

- One section in the homepage page contains input box

```html
<body>
  <!-- Search Bar -->
  <div class="search-container">
    <input type="text" id="searchName" placeholder="Enter student name">
    <button onclick="searchStudent()">Search</button>
  </div>
<script>
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

- Page to display student details

```html
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
```