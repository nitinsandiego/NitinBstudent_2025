---
toc: false
layout: post
title: Backend Code
type: collab
permalink: /backendcode
courses: {csa: {week: 11}}
---

# Student Class
```java
package com.nighthawk.spring_portfolio.mvc.student;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import jakarta.annotation.PostConstruct;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import jakarta.persistence.UniqueConstraint;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

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
    private ArrayList<String> completed;
    private int trimester;
    private int period;
    private String project;

    public Student(String name, String username, int tableNumber, String course, ArrayList<String> tasks, ArrayList<String> completed, int trimester, int period, String project) {
        this.name = name;
        this.username = username;
        this.tableNumber = tableNumber;
        this.course = course;
        this.tasks = tasks;
        this.completed = completed;
        this.trimester = trimester;
        this.period = period;
        this.project = project;
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
            students.add(new Student("Akhil Singamneni", "Akhil353", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), new ArrayList<String>(Arrays.asList("Completed 1", "Completed 2")), 1, 3, "Class Management"));
            students.add(new Student("Srinivas Nampalli", "SrinivasNampalli", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), new ArrayList<String>(Arrays.asList("Completed 1", "Completed 2")), 1, 3, "Class Management"));
            students.add(new Student("Aditya Samavedam", "adityasamavedam", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), new ArrayList<String>(Arrays.asList("Completed 1", "Completed 2")), 1, 3, "Class Management"));
            students.add(new Student("Nitin Balaji", "nitinsandiego", 4, "CSA", new ArrayList<String>(Arrays.asList("Task 1", "Task 2")), new ArrayList<String>(Arrays.asList("Completed 1", "Completed 2")), 1, 3, "Class Management"));

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

        public List<Student> findByNameCourseTrimesterPeriod(String name, String course, int trimester, int period) {
            return studentJPARepository.findByNameCourseTrimesterPeriod(name, course, trimester, period);
        }

        public Student createStudent(Student student) {
            // Check if a student with the same username already exists to avoid duplicates
            Optional<Student> existingStudent = studentJPARepository.findByUsername(student.getUsername());
            if (existingStudent.isPresent()) {
                throw new RuntimeException("A student with this username already exists.");
            }
            return studentJPARepository.save(student);
        }

        public void deleteById(Long id) {
            studentJPARepository.deleteById(id);
        }

        public Optional<Student> findByUsername(String username) {
            return studentJPARepository.findByUsername(username);
        }
        
        public List<Student> findTeam(String course, int trimester, int period, int table) {
            return studentJPARepository.findTeam(course, trimester, period, table);
        }

        public List<Student> findPeriod(String course, int trimester, int period) {
            return studentJPARepository.findPeriod(course, trimester, period);
        }

        
    }
}
```

# Student JPA Repository
```java
package com.nighthawk.spring_portfolio.mvc.student;

import java.util.List;
import java.util.Optional;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.query.Param;

// JPA is an object-relational mapping (ORM) to persistent data, originally relational databases (SQL). Today JPA implementations has been extended for NoSQL.
public interface StudentJPARepository extends JpaRepository<Student, Long> {
    Optional<Student> findByUsername(String username);
    Optional<Student> findByName(String name);
    @Query(
        value = "SELECT * FROM students WHERE course = :course AND trimester = :trimester AND period = :period AND table_number = :table",
        nativeQuery = true
    )
    List<Student> findTeam(
        @Param("course") String course, 
        @Param("trimester") int trimester, 
        @Param("period") int period,
        @Param("table") int table
    );

    @Query(
        value = "SELECT * FROM students WHERE course = :course AND trimester = :trimester AND period = :period",
        nativeQuery = true
    )
    List<Student> findPeriod(
        @Param("course") String course, 
        @Param("trimester") int trimester, 
        @Param("period") int period
    );



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

# Student API Controller
```java
package com.nighthawk.spring_portfolio.mvc.student;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import lombok.Getter;

@RestController
@RequestMapping("/api/students")
public class StudentApiController {
    
    @Autowired
    private StudentJPARepository studentJPARepository;

    @GetMapping("/all")
    public ResponseEntity<Iterable<Student>> getAllStudents() {
        return ResponseEntity.ok(studentJPARepository.findAll());
    }

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

    @PostMapping("/create")
    public ResponseEntity<Student> createStudent(@RequestBody Student student) {
        try {
            Optional<Student> existingStudents = studentJPARepository.findByUsername(student.getUsername());
            if (!existingStudents.isEmpty()) {
                throw new RuntimeException("A student with this GitHub ID already exists.");
            }
            Student createdStudent = studentJPARepository.save(student);
            return ResponseEntity.ok(createdStudent);
        } catch (RuntimeException e) {
            return ResponseEntity.badRequest().body(null);
        }
    }

    @PostMapping("/delete")
    public ResponseEntity<String> deleteStudentByUsername(@RequestParam String username) {
        Optional<Student> student = studentJPARepository.findByUsername(username);
        
        if (student.isPresent()) {
            studentJPARepository.deleteById(student.get().getId());  // Delete student by ID
            return ResponseEntity.ok("Student with username '" + username + "' has been deleted.");
        } else {
            return ResponseEntity.status(404).body("Student with username '" + username + "' not found.");
        }
    }

    @Getter
    public static class TeamDto {
        private String course;
        private int trimester;
        private int period; 
        private int table;
    }

    @PostMapping("/find-team")
    public ResponseEntity<Iterable<Student>> getTeamByCriteria(
            @RequestBody TeamDto teamDto) {
        
        List<Student> students = studentJPARepository.findTeam(teamDto.getCourse(), teamDto.getTrimester(), teamDto.getPeriod(), teamDto.getTable());
        
        if (students.isEmpty()) {
            return ResponseEntity.notFound().build();
        } else {
            return ResponseEntity.ok(students);
        }
    }


    @Getter 
    public static class StudentDto {
        private String username;
        private ArrayList<String> tasks;
    }


    @PostMapping("/update-tasks")
    public ResponseEntity<Student> updateTasks(@RequestBody StudentDto studentDto) {
        String username =  studentDto.getUsername();
        ArrayList<String> tasks = studentDto.getTasks();


        Optional<Student> student = studentJPARepository.findByUsername(username);

        if (student.isPresent()) {
            Student student1 = student.get();
            ArrayList<String> newTasks = student1.getTasks();
            
            for (String task: tasks) {
                newTasks.add(task);
            }
            
            student1.setTasks(newTasks);
            studentJPARepository.save(student1);
            return ResponseEntity.ok(student1);
        }

        return new ResponseEntity<>(HttpStatus.NOT_FOUND);
}
@Getter
public static class TasksDto {
    private String username;
    private String task;
}

@PostMapping("/complete-task")
public ResponseEntity<String> completeTask(@RequestBody TasksDto tasksDto) {
    Optional<Student> optionalStudent = studentJPARepository.findByUsername(tasksDto.getUsername());
    String task = tasksDto.getTask();

    if (optionalStudent.isPresent()) {
        Student student = optionalStudent.get();
        if (student.getCompleted() == null) {
            student.setCompleted(new ArrayList<>()); 
        }

        if (student.getTasks().contains(task)) {
            student.getTasks().remove(task);
            student.getCompleted().add(task + " - Completed");
            studentJPARepository.save(student);
            return ResponseEntity.ok("Task marked as completed.");
        } else {
            return ResponseEntity.badRequest().body("Task not found in the student's task list.");
        }
    } else {
        return ResponseEntity.status(404).body("Student not found.");
    }
}

    @Getter 
    public static class PeriodDto {
        private String course;
        private int trimester;
        private int period;
    }

    @PostMapping("/find-period")
    public ResponseEntity<Iterable<Student>> getPeriodByTrimester(
        @RequestBody PeriodDto periodDto) {
            
        List<Student> students = studentJPARepository.findPeriod(periodDto.getCourse(), periodDto.getTrimester(), periodDto.getPeriod());

        if (students.isEmpty()) {
            return ResponseEntity.notFound().build();
        } else {
            return ResponseEntity.ok(students);
        }
    }


}
```