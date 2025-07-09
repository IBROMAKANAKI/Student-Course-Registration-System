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


| Relationship                     | Cardinality | Description                                                   |
| -------------------------------- | ----------- | ------------------------------------------------------------- |
| **Student → Enrollments**        | 1 : Many    | One student can enroll in many course offerings               |
| **Course → CourseOfferings**     | 1 : Many    | One course can have many offerings                            |
| **Instructor → CourseOfferings** | 1 : Many    | One instructor can teach multiple offerings                   |
| **CourseOffering → Enrollments** | 1 : Many    | Each offering has many students                               |
| **Course ↔ Prerequisites**       | Many : Many | A course can have multiple prerequisites (self-join)          |
| **Student ↔ Course (indirect)**  | Many : Many | Students register for courses through offerings + enrollments |                

| **Student → CourseOfferings**               | Many-to-Many (via Enrollments)                   | Students register for course offerings through the Enrollments table.           |
| **Student → Courses**                       | Many-to-Many (via CourseOfferings & Enrollments) | Students take courses indirectly through course offerings and enrollments.      |
| **Student → Prerequisites (via Courses)**   | Indirect                                         | Students must complete prerequisite courses before enrolling in some courses.   |
| **Student → Instructors**                   | Indirect (via CourseOfferings)                   | Students are taught by instructors assigned to course offerings they enroll in. |


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


<div style="text-align: center; position: relative; display: inline-block;">

  <h3>📊 Click Through the Tables</h3>
  <p><em>Click the image to view the next table ➡️</em></p>

  <!-- Data icon badge -->
  <div style="
      position: absolute;
      top: 15px;
      left: 15px;
      background-color: rgba(255, 255, 255, 0.9);
      padding: 6px 12px;
      border-radius: 6px;
      font-size: 18px;
      font-weight: bold;
      box-shadow: 0 2px 4px rgba(0,0,0,0.2);">
    📋 Data Table
  </div>

  <!-- Image Carousel -->
  <img id="carousel" 
       src="/assets/images/tables/Student.jpg" 
       alt="Data Table" 
       width="600" 
       style="cursor: pointer; border: 2px solid #ccc; border-radius: 8px;" 
       onclick="cycleImage()" />

  <p style="margin-top: 10px;">🔁 <strong>Keep clicking to cycle through all images</strong></p>
</div>

<script>
  const imagePaths = [
    "Student Course Registration System Report/Asset/Image/Student.jpg",
    "Student Course Registration System Report/Asset/Image/Course.jpg",
    "Student Course Registration System Report/Asset/Image/Instructor.jpg",
    "Student Course Registration System Report/Asset/Image/CourseOffering.jpg", 
    "Student Course Registration System Report/Asset/Image/Enrollment.jpg",
    "Student Course Registration System Report/Asset/Image/Prerequites.jpg"
  ];

 let currentImageIndex = 0;

  function cycleImage() {
    currentImageIndex = (currentImageIndex + 1) % imagePaths.length;
    document.getElementById("carousel").src = imagePaths[currentImageIndex];
  }
</script>

### 2.  Design an ERD (Entity-Relationship Diagram)

#### Star Schema

The central fact table connects directly to multiple denormalized dimension tables. Dimension tables have redundant data but simplify queries with fewer joins while using Star Schema. use If the focus is on fast querying and reporting (like analyzing student enrollments, grades, course offerings), and simpler, flatter tables.

- Fact Table: Enrollments (records each registration with facts like Grade, EnrollmentDate)

- Dimension Tables: Students, Courses, Instructors, CourseOfferings, and Prerequites

**Note** All dimensions link directly to the fact table, and dimension tables are denormalized, meaning no further normalization (splitting) inside dimensions.


<div style="text-align: center; font-family: monospace; white-space: pre;">

         [Students]
               |
               |
[Instructors] — [Enrollments] — [Courses]
               |
           [CourseOfferings]

</div>



#### Snowflake Schema

An extension of star schema where dimension tables are normalized into multiple related tables, reducing redundancy but increasing complexity and join operations. use If a more normalized structure to save storage space or maintain data integrity is needed, especially when dimension attributes have hierarchical relationships.

- Courses split into Courses and Departments (department becomes a separate table linked to Courses)

- Students may link to Majors table rather than storing major info directly

- Instructors linked to Departments similarly

- CourseOfferings could link to Semesters as a separate table

<div style="text-align: center; font-family: monospace; white-space: pre; margin-top: 20px;">

    [Departments]
       /        \
  [Courses]   [Instructors]
       \          /
     [CourseOfferings]
           |
       [Enrollments]
           |
       [Students]
           |
      [Prerequisites]

</div>


<div style="text-align: center;">
  <img src="Student Course Registration System Report/Asset/Image/Diagram.jpg" alt="ERD DIAGRAM" style="max-width: 80%; height: auto;" />
</div>


<div style="text-align: center; font-family: monospace; white-space: pre;">

  [Students]         [Instructors]         [Courses]
    |                   |                    |
    |                   |                    |
    |                   |                    |
    |                   |                    |
[Enrollments]     [CourseOfferings] <--------/
       \               /
        \             /
         \           /
          \         /
           \       /
            \     /
             [Courses]
                 ^
                 |
                 v
   [Prerequisites (Self-Referencing)]


</div>

   
### 3. Implement the Relational Schema in SQL
A **database** is a structured collection of data stored in a way that makes it easy to retrieve, manage, and update. For example, a University Database might store data about students, courses, instructors, and enrollments. to Implement the Relational Schema in SQL a **database** needs to be create, then use then a table can be created.

- Create database

```sql
Create database STUDENT_REG;
Use STUDENT_REG;
```
**Code: Create data base**

A **table** is a fundamental unit within a database that organises data into rows and columns, much like a spreadsheet. Each table usually stores one type of data.

- **Create table**

```sql
-- a) Students Table
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    FirstName NVARCHAR(50),
    LastName NVARCHAR(50),
    Email NVARCHAR(100),
    Phone NVARCHAR(20),
    Major NVARCHAR(100),
    Year NVARCHAR(20) CHECK (Year IN ('Year 1', 'Year 2', 'Year 3', 'Year 4'))
);

-- b) Courses Table
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    CourseCode NVARCHAR(15),
    Title NVARCHAR(150),
    Credits INT CHECK (Credits > 0),
    Department NVARCHAR(150)
);

-- c) Instructors Table
CREATE TABLE Instructors (
    InstructorID INT PRIMARY KEY,
    FirstName NVARCHAR(50),
    LastName NVARCHAR(50),
    Email NVARCHAR(100),
    Department NVARCHAR(150)
);

-- d) CourseOfferings Table
CREATE TABLE CourseOfferings (
    OfferingID INT PRIMARY KEY,
    CourseID INT,
    Semester NVARCHAR(50),
    InstructorID INT,
    Schedule NVARCHAR(50),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID),
    FOREIGN KEY (InstructorID) REFERENCES Instructors(InstructorID)
);

-- e) Enrollments Table
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY,
    StudentID INT,
    OfferingID INT,
    EnrollmentDate DATE,
    Grade CHAR(1) CHECK (Grade IN ('A', 'B', 'C', 'D', 'F') OR Grade IS NULL),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (OfferingID) REFERENCES CourseOfferings(OfferingID)
);

-- f) Prerequisites Table
CREATE TABLE Prerequisites (
    CourseID INT,
    PrerequisiteID INT,
    PRIMARY KEY (CourseID, PrerequisiteID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID),
    FOREIGN KEY (PrerequisiteID) REFERENCES Courses(CourseID)
);

```

![Create table](Student Course Registration System Report/Asset/Image/table.jpg)

**Note**: PRIMARY KEY: This ensures that each StudentID is unique and not null.  
NVARCHAR(50): means it can store up to 50 Unicode characters, supporting different languages and characters (e.g., accented letters).
FOREIGN KEY: A FOREIGN KEY is a constraint in SQL that creates a relationship between two tables. It ensures referential integrity

- **View table**

```sql
Select * from Students;
Select * from Courses;
Select * from CourseOfferings;
Select * from Instructors;
Select * from Enrollments;
Select * from Prerequisites;
```

![View Table](Student Course Registration System Report/Asset/Image/table view.jpg)

- **Insert data to table**

```sql

---Student----

BULK INSERT Students
FROM "C:\Users\hp\Downloads\Students (1).csv"
WITH (
    FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '0x0a', -- Unix-style line endings
    TABLOCK,
    KEEPNULLS,
    CODEPAGE = '65001' -- Handles UTF-8
);

----Course------

BULK INSERT Courses
FROM "C:\Users\hp\Downloads\Courses (1).csv"
WITH (
    FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '0x0a', -- Unix-style line endings
    TABLOCK,
    KEEPNULLS,
    CODEPAGE = '65001' -- Handles UTF-8
);

-----Instructor---

BULK INSERT Instructors
FROM "C:\Users\hp\Downloads\Instructors (1).csv"
WITH (
    FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '0x0a', -- Unix-style line endings
    TABLOCK,
    KEEPNULLS,
    CODEPAGE = '65001' -- Handles UTF-8
);


------CourseOfferings----

BULK INSERT CourseOfferings
FROM "C:\Users\hp\Downloads\CourseOfferings (1).csv"
WITH (
    FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '0x0a', -- Unix-style line endings
    TABLOCK,
    KEEPNULLS,
    CODEPAGE = '65001' -- Handles UTF-8
);

-----Enrollments----

BULK INSERT Enrollments
FROM "C:\Users\hp\Downloads\Enrollments (1).csv"
WITH (
    FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '0x0a', -- Unix-style line endings
    TABLOCK,
    KEEPNULLS,
    CODEPAGE = '65001' -- Handles UTF-8
);

----Prerequisites------


BULK INSERT Prerequisites
FROM "C:\Users\hp\Downloads\Prerequisites (1).csv"
WITH (
    FIRSTROW = 2,
    FIELDTERMINATOR = ',',
    ROWTERMINATOR = '0x0a', -- Unix-style line endings
    TABLOCK,
    KEEPNULLS,
    CODEPAGE = '65001' -- Handles UTF-8
);

```

**BULK INSERT Students**: This command instructs SQL Server to import data from an external file into the Students table.

**FROM "C:\Users\hp\Downloads\Students (1).csv"**: Specifies the path to the CSV file importing from the computer

**FIRSTROW = 2** : Tells SQL Server to start reading from the second row. The first row is typically a header row (column names), which you needs to skip.

**FIELDTERMINATOR = ','**: Specifies that columns are separated by commas (CSV = Comma Separated Values).

**ROWTERMINATOR = '0x0a'**: This defines how each row ends. 0x0a is the Unix-style line break (Line Feed \n).

**TABLOCK**: Improves performance by locking the table during the insert operation. Recommended for large imports.

**KEEPNULLS**: If a field in the file is empty, it inserts SQL NULL instead of default values.

**CODEPAGE = '65001'**: Specifies that the file is in UTF-8 encoding. This is necessary if the CSV contains non-English characters, emojis, or accented letters.

- **Verify data insertion**

```sql
SELECT TOP 3 * FROM Students;
SELECT TOP 3 * FROM Courses;
SELECT TOP 3 * FROM CourseOfferings;
SELECT TOP 3 * FROM Instructors;
SELECT TOP 3 * FROM Enrollments;
SELECT TOP 3 * FROM Prerequisites;
```
**This code shows the first three line in each table**

![Top 3 data table](Student Course Registration System Report/Asset/Image/Top 3.jpg)



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




