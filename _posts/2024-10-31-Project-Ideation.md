---
toc: false
layout: post
title: Project Ideation
type: collab
permalink: /projectideation
courses: {csa: {week: 9}}
---

**Topic**

The purpose of this project is to help Mr. Mortensen manage his CSSE, CSP, and CSA classes more easily. It will help him keep track of student information, organize group assignments, and monitor progress in different courses. This will save time, allowing Mr. Mortensen to focus more on teaching and less on keeping track of progress of each team.

**Frontend UI design**

![image](https://github.com/user-attachments/assets/4b249d9d-d2d6-4a5e-8483-3ea57b6d3041)

**Data**

| **Field Name**  | **Data Type**        | **Description**                         |
|-----------------|----------------------|-----------------------------------------|
| `id`            | `Long`               | Unique identifier for each student.     |
| `name`          | `String`             | Full name of the student.               |
| `username`      | `String`             | Unique username for the student.        |
| `tableNumber`   | `int`                | Assigned table number in the classroom. |
| `course`        | `String`             | The course the student is enrolled in (e.g., CSSE, CSP, CSA). |
| `tasks`         | `ArrayList<String>`  | List of tasks or assignments assigned to the student.  |
| `trimester`     | `int`                | Trimester during which the student is enrolled. |
| `period`        | `int`                | Class period for the student.           |

**Coding Work**

This is my code creating the Student Class and initializing some starter data into the SQL Database
```java
@Data  // Annotations to simplify writing code (ie constructors, setters)
@NoArgsConstructor
@AllArgsConstructor
@Entity // Annotation to simplify creating an entity, which is a lightweight persistence domain object. Typically, an entity represents a table in a relational database, and each entity instance corresponds to a row in that table.
@Table(name = "students" , uniqueConstraints = @UniqueConstraint(columnNames = "name"))
public class Student {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String name;
    private String username;
    private int tableNumber;
    private String course;
    private ArrayList<String> tasks;
    private int trimester;
    private int period;

    public Student(String name, String username, int tableNumber, String course, ArrayList<String> tasks, int trimester, int period) {
        this.name = name;
        this.username = username;
        this.tableNumber = tableNumber;
        this.course = course;
        this.tasks = tasks;
        this.trimester = trimester;
        this.period = period;
    }

    @Service
    public static class StudentService {

        @Autowired
        private StudentJPARepository studentJPARepository;

        @PostConstruct
        public void initializeData() { 
            if (studentJPARepository == null) {
                throw new RuntimeException("studentJPARepository is not initialized!");
            }
            List<Student> students = new ArrayList<>();
            students.add(new Student("Akhil Singamneni", "Akhil353", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), 1, 3));
            students.add(new Student("Srinivas Nampalli", "srininampalli", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), 1, 3));
            students.add(new Student("Aditya Samavedam", "adityasamavedam", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), 1, 3));
            students.add(new Student("Nitin Balaji", "nitinsandiego", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), 1, 3));

            for (Student student : students) {
            Optional<Student> existingStudent = studentJPARepository.findByUsername(student.getUsername());
            
            if (existingStudent.isEmpty()) {
                studentJPARepository.save(student);
            }
        }
        }

        public Iterable<Student> findAll() {
            return studentJPARepository.findAll();
        }
    }

}
```

This code handles the API paths. We have set a tester API path that returns all the student details in a JSON.

```java
package com.nighthawk.spring_portfolio.mvc.student;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/api/students")
public class StudentApiController {
    
    @Autowired
    private Student.StudentService studentService;

    @GetMapping("/all")
    public ResponseEntity<Iterable<Student>> getAllFlights() {
        return ResponseEntity.ok(studentService.findAll());
    }

}
```

**Evidence of Research**

Our project was inspired by the organizational tools found in platforms like Monday.com, which is a popular work management software used for team collaboration. Monday.com allows users to create detailed boards for tracking tasks, projects, and workflows. It provides a visual way to assign tasks, monitor progress, and collaborate within teams, making it a versatile tool for organizing work in an efficient manner.

Seeing the functionality of Monday.com, we decided to apply a similar concept to classroom management. The idea is to provide Mr. Mortensen with a tool to manage his CSSE, CSP, and CSA classes more effectively, similar to how Monday.com enables team management. By tracking students, assignments, and progress in one place, our project mirrors Monday.com’s ability to handle task assignments and group organization, but it tailors these features specifically for the educational context.