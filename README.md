# College Database Setup

This project contains the setup for a college database system. It includes multiple tables such as Admins, Teachers, Courses, Course Availability, Enrollments, and Semesters. This README provides a detailed guide on how to set up the database and its relations.

## Tables Overview

1. **Admins**: Stores details about administrators who manage the courses and assignments.
2. **Teachers**: Contains information about teachers who teach various courses.
3. **Courses**: Stores the courses offered in the college.
4. **CourseAvailability**: Tracks the availability of courses in each semester.
5. **CourseAssignments**: Associates courses with administrators, teachers, and availability.
6. **Enrollments**: Tracks which students are enrolled in which courses.
7. **Semesters**: Stores information about different academic semesters.
8. **Students**: Contains details about the students in the college.

## SQL Schema

The SQL schema includes the creation of the necessary tables, their fields, primary and foreign key constraints, and sample data for each table.

### Table 1: Admins

```
CREATE TABLE `Admins` (
  `AdminID` int NOT NULL DEFAULT '0',
  `Admin_Name` varchar(255) NOT NULL DEFAULT 'Enter Admin Name',
  `Admin_Email` varchar(255) NOT NULL DEFAULT 'Enter Admin Email',
  `Admin_Password` varchar(255) NOT NULL DEFAULT 'Enter Admin Password',
  `Admin_Surname` varchar(255) NOT NULL DEFAULT 'Enter Admin Surname',
  PRIMARY KEY (`AdminID`),
  UNIQUE KEY `AdminID_UNIQUE` (`AdminID`),
  UNIQUE KEY `Admin_Email_UNIQUE` (`Admin_Email`)
);
```
** Table 2: Teachers
```
CREATE TABLE `Teachers` (
  `TeacherID` int NOT NULL DEFAULT '0',
  `Teacher_Name` varchar(255) NOT NULL DEFAULT 'Enter Teacher Name',
  `Teacher_Email` varchar(255) NOT NULL DEFAULT 'Enter Teacher Email',
  PRIMARY KEY (`TeacherID`),
  UNIQUE KEY `Teacher_Email_UNIQUE` (`Teacher_Email`)
);
```
** Table 3: Courses
```
CREATE TABLE `Courses` (
  `CourseID` int NOT NULL DEFAULT '0',
  `CourseName` varchar(255) NOT NULL DEFAULT 'Enter Course Name',
  `Available` tinyint DEFAULT '0',
  `Semester_ID` int DEFAULT '0',
  PRIMARY KEY (`CourseID`),
  UNIQUE KEY `CourseID_UNIQUE` (`CourseID`),
  UNIQUE KEY `CourseName_UNIQUE` (`CourseName`),
  KEY `Semester_ID_idx` (`Semester_ID`),
  CONSTRAINT `Semester_ID` FOREIGN KEY (`Semester_ID`) REFERENCES `Semesters` (`SemesterID`)
);
```

** Table 4: CourseAvailability
```
CREATE TABLE `CourseAvailability` (
  `CourseAvailability_ID` int NOT NULL DEFAULT '0',
  `SemesterID` int DEFAULT NULL,
  `Courses_ID` int DEFAULT NULL,
  `Admin_id` int DEFAULT NULL,
  `IsAvailable` tinyint DEFAULT NULL,
  PRIMARY KEY (`CourseAvailability_ID`),
  UNIQUE KEY `Courses_ID_UNIQUE` (`Courses_ID`),
  KEY `Admin_id_idx` (`Admin_id`),
  KEY `SemesterID_idx` (`SemesterID`),
  CONSTRAINT `Admin_id` FOREIGN KEY (`Admin_id`) REFERENCES `Admins` (`AdminID`),
  CONSTRAINT `Courses_ID` FOREIGN KEY (`Courses_ID`) REFERENCES `Courses` (`CourseID`),
  CONSTRAINT `SemesterID` FOREIGN KEY (`SemesterID`) REFERENCES `Semesters` (`SemesterID`)
);
```

** Table 5: CourseAssignments
```
CREATE TABLE `CourseAssignments` (
  `AssignmentID` int NOT NULL DEFAULT '0',
  `AdminsID` int NOT NULL DEFAULT '0',
  `TeachID` int NOT NULL DEFAULT '0',
  `CoursesID` int NOT NULL DEFAULT '0',
  `CourseAvailabilityID` int NOT NULL DEFAULT '0',
  PRIMARY KEY (`AssignmentID`),
  UNIQUE KEY `AssignmentID_UNIQUE` (`AssignmentID`),
  KEY `AdminID_idx` (`AdminsID`),
  KEY `CourseAvailabilityID_idx` (`CourseAvailabilityID`),
  KEY `CourseID_idx` (`CoursesID`),
  KEY `TeacherID_idx` (`TeachID`),
  CONSTRAINT `AdminID` FOREIGN KEY (`AdminsID`) REFERENCES `Admins` (`AdminID`),
  CONSTRAINT `CourseAvailabilityID` FOREIGN KEY (`CourseAvailabilityID`) REFERENCES `CourseAvailability` (`CourseAvailability_ID`),
  CONSTRAINT `CoursesID` FOREIGN KEY (`CoursesID`) REFERENCES `Courses` (`CourseID`),
  CONSTRAINT `TeacherID` FOREIGN KEY (`TeachID`) REFERENCES `Teachers` (`TeacherID`)
);
```
** Table 6: Enrollments
```
CREATE TABLE `Enrollments` (
  `EnrollmentID` int NOT NULL DEFAULT '0',
  `StudentID` int DEFAULT '0',
  `Course__ID` int DEFAULT '0',
  PRIMARY KEY (`EnrollmentID`),
  UNIQUE KEY `EnrollmentID_UNIQUE` (`EnrollmentID`),
  KEY `Course__ID_idx` (`Course__ID`),
  KEY `StudentID_idx` (`StudentID`),
  CONSTRAINT `Course__ID` FOREIGN KEY (`Course__ID`) REFERENCES `Courses` (`CourseID`),
  CONSTRAINT `StudentID` FOREIGN KEY (`StudentID`) REFERENCES `Students` (`StudentID`)
);
```
** Table 7: Semesters
```
CREATE TABLE `Semesters` (
  `SemesterID` int NOT NULL DEFAULT '0',
  `SemesterName` varchar(255) NOT NULL DEFAULT 'Enter Semester Name',
  PRIMARY KEY (`SemesterID`),
  UNIQUE KEY `SemesterID_UNIQUE` (`SemesterID`)
);
```

** Table 8: Students
```
CREATE TABLE `Students` (
  `StudentID` int NOT NULL DEFAULT '0',
  `StudentName` varchar(255) NOT NULL DEFAULT 'Enter Student Name',
  `StudentEmail` varchar(255) NOT NULL DEFAULT 'Enter Student Email',
  `StudentPassword` varchar(255) NOT NULL DEFAULT 'Enter Student Password',
  `StudentSurname` varchar(100) NOT NULL DEFAULT 'Enter Student Surname',
  PRIMARY KEY (`StudentID`),
  UNIQUE KEY `StudentEmail_UNIQUE` (`StudentEmail`)
);
```


### How to Set Up

** Execute the SQL schema in MySQL Workbench or any SQL client connected to a MySQL server.
** Insert the sample data into the tables.
** Make sure the foreign key relationships are respected, as they define how data in one table is related to data in another table.

### License
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)
** This project is licensed under the MIT License.







