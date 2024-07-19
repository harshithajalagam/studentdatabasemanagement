# studentdatabasemanagement
CREATE DATABASE StudentManagement;
USE StudentManagement;
CREATE TABLE Students (
    StudentID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    DateOfBirth DATE NOT NULL,
    Gender CHAR(1),
    Email VARCHAR(100) UNIQUE,
    PhoneNumber VARCHAR(15)
);
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY AUTO_INCREMENT,
    CourseName VARCHAR(100) NOT NULL,
    CourseDescription TEXT,
    Credits INT NOT NULL
);
CREATE TABLE Instructors (
    InstructorID INT PRIMARY KEY AUTO_INCREMENT,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE,
    PhoneNumber VARCHAR(15)
);
CREATE TABLE Enrollments (
    EnrollmentID INT PRIMARY KEY AUTO_INCREMENT,
    StudentID INT,
    CourseID INT,
    EnrollmentDate DATE,
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);
CREATE TABLE Grades (
    GradeID INT PRIMARY KEY AUTO_INCREMENT,
    EnrollmentID INT,
    Grade CHAR(1),
    FOREIGN KEY (EnrollmentID) REFERENCES Enrollments(EnrollmentID)
);
INSERT INTO Students (FirstName, LastName, DateOfBirth, Gender, Email, PhoneNumber)
VALUES 
('John', 'Doe', '2000-01-01', 'M', 'john.doe@example.com', '123-456-7890'),
('Jane', 'Smith', '2001-02-02', 'F', 'jane.smith@example.com', '098-765-4321');
INSERT INTO Courses (CourseName, CourseDescription, Credits)
VALUES 
('Mathematics', 'Introduction to Algebra', 3),
('History', 'World History', 4);
INSERT INTO Instructors (FirstName, LastName, Email, PhoneNumber)
VALUES 
('Alice', 'Brown', 'alice.brown@example.com', '111-222-3333'),
('Bob', 'Johnson', 'bob.johnson@example.com', '444-555-6666');
INSERT INTO Enrollments (StudentID, CourseID, EnrollmentDate)
VALUES 
(1, 1, '2023-09-01'),
(2, 2, '2023-09-01');
INSERT INTO Grades (EnrollmentID, Grade)
VALUES 
(1, 'A'),
(2, 'B');
SELECT * FROM Students;
SELECT * FROM Courses;
SELECT 
    E.EnrollmentID,
    S.FirstName AS StudentFirstName,
    S.LastName AS StudentLastName,
    C.CourseName,
    E.EnrollmentDate
FROM 
    Enrollments E
JOIN 
    Students S ON E.StudentID = S.StudentID
JOIN 
    Courses C ON E.CourseID = C.CourseID;
SELECT 
    G.GradeID,
    S.FirstName AS StudentFirstName,
    S.LastName AS StudentLastName,
    C.CourseName,
    G.Grade
FROM 
    Grades G
JOIN 
    Enrollments E ON G.EnrollmentID = E.EnrollmentID
JOIN 
    Students S ON E.StudentID = S.StudentID
JOIN 
    Courses C ON E.CourseID = C.CourseID;

