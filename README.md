<p align="right">
  <img src="Student Course Registration System Report/Asset/Image/Datakirk logo.jpg" alt="Datakirk logo" width="150">
</p>
<h1 align="center">SALAWUDEEN IBRAHIM</h1>

<h2 align="center">Project Introduction</h2>

This project presents the **design** and **implementation of a Student Course Registration System using a relational database model**. It aims to simulate how a fictional university manages student registrations, course offerings, instructor assignments, prerequisites, and academic records. The system is built entirely with **SQL**, covering schema design, table creation, constraints enforcement, and data manipulation.

To reflect real-world scenarios, the dataset includes **manually generated dummy data featuring null values, empty fields, and duplicate entries, enabling a realistic environment for practicing data analysis and integrity checks**. Core components of the project include an **Entity-Relationship Diagram (ERD)**, **SQL scripts for database creation**, **sample data population**, and **practical query operations**. The project emphasizes **data integrity**, **normalization, and the use of SQL for efficient information retrieval and validation**, making it a strong foundation for understanding database systems in academic or enterprise environments.

## 🎯 Aim
To design and implement a robust relational database system that effectively manages student registrations, course offerings, instructor assignments, and academic performance, while simulating real-world data scenarios involving missing values, nulls, and duplicate records, using SQL for data modeling, manipulation, and analysis.

## 🧩 Problem Statement
Modern universities manage thousands of students, courses, instructors, and class enrollments each semester. Without a centralized system, tracking course offerings, managing student registrations, assigning instructors, and recording grades becomes inefficient and error-prone. This project aims to design and implement a relational database that addresses these challenges by providing a structured way to:

- Store and manage student information.

- Maintain a catalog of courses and prerequisites.

- Track course offerings for each semester.

- Record instructor assignments.

- Handle student course registrations and grades.

## ✅ Objectives

### 1. Analyze the Problem Domain

- **Identify key entities (e.g., Students, Courses, Enrollments) and define their relationships and data requirements.**
  
  | Entity              | Description                                                        | Key Attributes                                         |
| ------------------- | ------------------------------------------------------------------ | ------------------------------------------------------ |
| **Students**        | Individuals who enroll in the university and register for courses. | StudentID, FirstName, LastName, Email, Major, Year     |
| **Courses**         | Abstract course definitions offered by departments.                | CourseID, CourseCode, Title, Credits, Department       |
| **Instructors**     | Faculty members responsible for teaching courses.                  | InstructorID, FirstName, LastName, Email, Department   |
| **CourseOfferings** | Specific instances of courses taught in a semester.                | OfferingID, CourseID, Semester, InstructorID, Schedule |
| **Enrollments**     | Records of students registering for specific course offerings.     | EnrollmentID, StudentID, OfferingID, Grade, Date       |
| **Prerequisites**   | Courses that must be completed before enrolling in another course. | CourseID, PrerequisiteID                               |



  1. Students ↔ Enrollments
     Type: One-to-Many
     Explanation: A single student can enroll in multiple course offerings, but each enrollment record refers to only one student.
     Implementation: StudentID in Enrollments is a foreign key referencing Students.

  2. Courses ↔ CourseOfferings
     Type: One-to-Many
     Explanation: Each course can be offered in different semesters (e.g., CS101 may be offered in Fall and Spring).
     Implementation: CourseID in CourseOfferings is a foreign key referencing Courses.

  3. Instructors ↔ CourseOfferings
     Type: One-to-Many
     Explanation: One instructor can teach multiple course offerings.
     Implementation: InstructorID in CourseOfferings is a foreign key referencing Instructors.

  4. CourseOfferings ↔ Enrollments
     Type: One-to-Many
     Explanation: A course offering can have many students enrolled, but each enrollment belongs to only one offering.
     Implementation: OfferingID in Enrollments is a foreign key referencing CourseOfferings.

  5. Courses ↔ Prerequisites
     Type: Many-to-Many (Self-Referencing)
     Explanation: A course can have multiple prerequisites, and a course can be a prerequisite for multiple other courses.
     Implementation: Prerequisites table acts as a bridge with composite keys CourseID and PrerequisiteID.
     

    | Relationship                       | Type         |
| ---------------------------------- | -----------------|
| **Student → Enrollments**             | One-to-Many   |
| **Course → CourseOfferings**           | One-to-Many  |
| **Instructor → CourseOfferings**       | One-to-Many  |
| **CourseOffering → Enrollments**       | One-to-Many  |
| **Course ↔ Prerequisites (Self-join)** | Many-to-Many |

     

   
     | Relationship                                | Type                          | Description                                                                       |
|---------------------------------------------|-------------------------------|-----------------------------------------------------------------------------|
| **Student → Enrollments**                   | One-to-Many                   | A student can be enrolled in multiple course offerings.                     |
| **Student → CourseOfferings**               | Many-to-Many (via Enrollments) | Students register for course offerings through the Enrollments table.       |
| **Student → Courses**                       | Many-to-Many (via CourseOfferings & Enrollments) | Students take courses indirectly through course offerings and enrollments. |
| **Student → Prerequisites (via Courses)**   | Indirect                      | Students must complete prerequisite courses before enrolling in some courses. |
| **Student → Instructors**                   | Indirect (via CourseOfferings) | Students are taught by instructors assigned to course offerings they enroll in. |


- **Data understanding**
  
  To simulate a realistic environment for the Student Course Registration System, synthetic data was manually generated for each table. Each table contains 500 rows, designed to include various data quality challenges such as null values, empty cells, and duplicates, 
  which reflect real-world database inconsistencies and provide a solid foundation for data integrity enforcement and validation through SQL.
  Below is a breakdown of each table, its key attributes, and its structure:
  

  | Table Name       | Number of Rows | Number of Columns  |  Key Columns                                                  |
|--------------------|----------------|--------------------|---------------------------------------------------------------|
| **Students**        | 500            | 7                  | StudentID, FirstName, LastName, Email, Phone, Major, Year    |
| **Courses**         | 500            | 5                  | CourseID, CourseCode, Title, Credits, Department             |
| **Instructors**     | 500            | 5                  | InstructorID, FirstName, LastName, Email, Department         |
| **CourseOfferings** | 500            | 5                  | OfferingID, CourseID, Semester, InstructorID, Schedule       |
| **Enrollments**     | 500            | 5                  | EnrollmentID, StudentID, OfferingID, EnrollmentDate, Grade   |
| **Prerequisites**   | 500            | 2                  | CourseID, PrerequisiteID                                     |


<sub>Click the image to view the next table</sub>

<div align="center"> <details> <summary>📸 Click here to cycle through the data table images</summary> <img src="Student Course Registration System Report/Asset/Image/Student.jpg" width="600" alt="Excel Table for Student" onclick="this.src='Student Course Registration System Report/Asset/Image/Course.jpg'"> <img src="Student Course Registration System Report/Asset/Image/Course.jpg" width="600" alt="Excel Table for Course" hidden> <img src="Student Course Registration System Report/Asset/Image/Instructor.jpg" width="600" alt="Excel Table for Instructor" hidden> <img src="Student Course Registration System Report/Asset/Image/CourseOffering.jpg" width="600" alt="Excel Table for CourseOffering" hidden> <img src="Student Course Registration System Report/Asset/Image/Enrollment.jpg" width="600" alt="Excel Table for Enrollment" hidden> <img src="Student Course Registration System Report/Asset/Image/Prerequites.jpg" width="600" alt="Excel Table for Prerequisites" hidden> <p><strong>🔁 Click images above to cycle through all data tables</strong></p> </details> </div>


### 2.  Design an ERD (Entity-Relationship Diagram)

- Create a logical model representing how the entities interact, including one-to-many and many-to-many relationships.

### 3. Implement the Relational Schema in SQL

- Write CREATE TABLE scripts with appropriate data types, primary keys, foreign keys, and constraints (e.g., UNIQUE, CHECK).

### 4. Simulate Real-World Data Challenges

- Populate tables with manually generated dummy data that includes:

- Empty fields and NULL values

- Duplicate entries

### 5. Inconsistent or edge-case values (e.g., invalid grades, blank emails)

- Ensure Data Integrity and Validation

- Apply business rules using constraints (e.g., valid grade ranges, mandatory fields) to enforce data quality and consistency.

### 6. Write and Execute SQL Queries for Analysis

- Develop queries to:

- Retrieve student transcripts

- Identify enrollment trends

- Detect data issues (e.g., duplicates, missing prerequisites)

- Summarize course loads for instructors and departments

### 7. Optional: Create SQL Views for Abstraction

- Build virtual tables (views) for simplified access to complex joins, such as:

- StudentTranscriptView

- InstructorScheduleView

### 8. Reflect on Data Cleaning Needs

- Use SQL to identify and potentially isolate records that need cleaning or manual correction.

## 9. Scope of the Project

- Includes: Student registration, course enrollment, instructor assignment, grade recording.

- Excludes: Payment processing, learning content delivery, real-time notifications.

## 10. Methodology
For this SQL project, this include:

- Schema design using ER diagrams

- SQL implementation (CREATE, INSERT, SELECT, etc.)

- Manual data generation (including nulls, duplicates)

- Query writing for analysis

## 11. System Design / Architecture

- ERD (Entity Relationship Diagram)

- Normalization process

- Table relationships and structure

## 12. Challenges and Limitations

- Manually generating realistic data

- Handling large CSV imports with null/duplicate values

## 13. Results / Output Samples
Show some SQL query outputs, insights gathered from the analysis, or screenshots (optional).

## 14. Conclusion
Summarize what you achieved, what went well, and what could be improved.

## 15. Future Work / Recommendations

- Integrate with front-end UI

- Add stored procedures and triggers

- Real-time dashboard using BI tools




