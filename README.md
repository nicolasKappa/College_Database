# University Project - College Database


# Description

* The purpose of this assignment is to analyse a system and go through design steps using MySQL RDBMS, and perform very simple data entry and database backups.
* A college has decided to develop a database for “admins”, “teachers”, “students” and “courses”. 


# Features
* Feature 1 Course availability for each semester is decided by college admins and students can only see the offered courses. 

* Feature 2 Admins, assign courses to teachers.

* Feature 3 Teachers can pass or fail students.

# Usage

* The database needs to support an application that enables students to select from the offered courses. 
bash

# Table of Contents
- [Getting Started](#Getting-Started)
- [Inside Database Dump File ](#Inside-Database-Dump-File)
- [License](#License)
- [Contributing](#Contributing)





# Getting Started
1) Download mySQL:
* Download and install MySQL from the official website MySQL Downloads
* after installation, open a command prompt or terminal and run the following command to verify that MySQL is installed and running mysql --version
2) Import The dump file from MySQL Workbench

# Inside Database Dump File 
* MySQL dump 10.13  Distrib 8.0.33, for macos13 (x86_64)
--
-- Host: 127.0.0.1    Database: university
-- ------------------------------------------------------
-- Server version	8.0.33

/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!50503 SET NAMES utf8 */;
/*!40103 SET @OLD_TIME_ZONE=@@TIME_ZONE */;
/*!40103 SET TIME_ZONE='+00:00' */;
/*!40014 SET @OLD_UNIQUE_CHECKS=@@UNIQUE_CHECKS, UNIQUE_CHECKS=0 */;
/*!40014 SET @OLD_FOREIGN_KEY_CHECKS=@@FOREIGN_KEY_CHECKS, FOREIGN_KEY_CHECKS=0 */;
/*!40101 SET @OLD_SQL_MODE=@@SQL_MODE, SQL_MODE='NO_AUTO_VALUE_ON_ZERO' */;
/*!40111 SET @OLD_SQL_NOTES=@@SQL_NOTES, SQL_NOTES=0 */;

--
-- Table structure for table `Admins`
--

DROP TABLE IF EXISTS `Admins`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `Admins` (
  `AdminID` int NOT NULL DEFAULT '0',
  `Admin_Name` varchar(255) NOT NULL DEFAULT 'Enter Admin Name',
  `Admin_Email` varchar(255) NOT NULL DEFAULT 'Enter Admin Email',
  `Admin_Password` varchar(255) NOT NULL DEFAULT 'Enter Admin Password',
  `Admin_Surname` varchar(255) NOT NULL DEFAULT 'Enter  Admin Surname',
  PRIMARY KEY (`AdminID`),
  UNIQUE KEY `AdminID_UNIQUE` (`AdminID`),
  UNIQUE KEY `Admin_Email_UNIQUE` (`Admin_Email`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `Admins`
--

LOCK TABLES `Admins` WRITE;
/*!40000 ALTER TABLE `Admins` DISABLE KEYS */;
INSERT INTO `Admins` VALUES (51,'Sylvia','Sylvia123@gmail.com','Syvlia!12','Enter  Admin Surname'),(52,'Jonathan','Jona123@gmail.com','Jonathan!12','Benson'),(53,'Maria','Maria123@gmail.com','Maria!12','Jobson'),(54,'Joseph','Joseph12!@gmail.com','Joseph!12','Stalone');
/*!40000 ALTER TABLE `Admins` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `CourseAssignments`
--

DROP TABLE IF EXISTS `CourseAssignments`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
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
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `CourseAssignments`
--

LOCK TABLES `CourseAssignments` WRITE;
/*!40000 ALTER TABLE `CourseAssignments` DISABLE KEYS */;
INSERT INTO `CourseAssignments` VALUES (501,51,101,201,4020),(502,52,104,202,3040),(503,53,109,203,4021),(504,51,102,204,4022),(505,53,110,205,4023),(506,52,105,206,3041),(507,51,100,207,3042),(508,52,107,208,4025),(509,53,111,209,4027),(510,52,108,210,4026),(511,52,106,211,3043),(512,51,103,212,4028);
/*!40000 ALTER TABLE `CourseAssignments` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `CourseAvailability`
--

DROP TABLE IF EXISTS `CourseAvailability`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
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
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `CourseAvailability`
--

LOCK TABLES `CourseAvailability` WRITE;
/*!40000 ALTER TABLE `CourseAvailability` DISABLE KEYS */;
INSERT INTO `CourseAvailability` VALUES (3040,71,202,52,1),(3041,71,206,52,1),(3042,71,207,51,1),(3043,71,211,52,1),(4020,70,201,51,0),(4021,72,203,53,0),(4022,73,204,51,0),(4023,72,205,53,0),(4025,70,208,52,0),(4026,73,210,52,0),(4027,70,209,53,0),(4028,72,212,52,0);
/*!40000 ALTER TABLE `CourseAvailability` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `Courses`
--

DROP TABLE IF EXISTS `Courses`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
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
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `Courses`
--

LOCK TABLES `Courses` WRITE;
/*!40000 ALTER TABLE `Courses` DISABLE KEYS */;
INSERT INTO `Courses` VALUES (201,'Computer Science',0,70),(202,'Mathematics',1,71),(203,'Physics',0,72),(204,'Biology',0,73),(205,'Chemistry',0,72),(206,'Law',1,71),(207,'Medicine',1,71),(208,'Business',0,70),(209,'Engineering',0,70),(210,'Art ',0,73),(211,'Social Science',1,71),(212,'Management',0,72);
/*!40000 ALTER TABLE `Courses` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `Enrollments`
--

DROP TABLE IF EXISTS `Enrollments`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
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
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `Enrollments`
--

LOCK TABLES `Enrollments` WRITE;
/*!40000 ALTER TABLE `Enrollments` DISABLE KEYS */;
INSERT INTO `Enrollments` VALUES (51,1,201),(52,2,204),(53,3,212),(54,4,202),(55,5,206),(56,6,211),(57,7,208),(58,9,210),(59,10,203),(60,11,205),(61,12,209),(62,13,201),(63,14,204),(64,15,212),(65,16,202),(66,17,206),(67,18,211),(68,19,208),(69,20,210),(70,21,203),(71,22,205),(72,23,209),(73,24,201);
/*!40000 ALTER TABLE `Enrollments` ENABLE KEYS */;
**UNLOCK TABLES;

--
-- Table structure for table `Semesters`
--

DROP TABLE IF EXISTS `Semesters`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `Semesters` (
  `SemesterID` int NOT NULL DEFAULT '0',
  `SemesterName` varchar(255) NOT NULL DEFAULT 'Enter Semester Name',
  PRIMARY KEY (`SemesterID`),
  UNIQUE KEY `SemesterID_UNIQUE` (`SemesterID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `Semesters`
--

LOCK TABLES `Semesters` WRITE;
/*!40000 ALTER TABLE `Semesters` DISABLE KEYS */;
**INSERT INTO `Semesters` VALUES (70,'Winter'),(71,'Spring'),(72,'Summer'),(73,'Autumn');
/*!40000 ALTER TABLE `Semesters` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `Students`
--

DROP TABLE IF EXISTS `Students`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `Students` (
  `StudentID` int NOT NULL DEFAULT '0',
  `StudentName` varchar(255) NOT NULL DEFAULT 'Enter Student Name',
  `StudentEmail` varchar(255) NOT NULL DEFAULT 'Enter Student Email',
  `StudentPassword` varchar(255) NOT NULL DEFAULT 'Enter Student Password',
  `StudentSurname` varchar(100) NOT NULL DEFAULT 'Enter Student Surname',
  PRIMARY KEY (`StudentID`),
  UNIQUE KEY `StudentID_UNIQUE` (`StudentID`),
  UNIQUE KEY `StudentEmail_UNIQUE` (`StudentEmail`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `Students`
--

LOCK TABLES `Students` WRITE;
/*!40000 ALTER TABLE `Students` DISABLE KEYS */;
**INSERT INTO `Students` VALUES (1,'Josh','Josh@gmail.com','JoshJosh123','Bigs'),(2,'Mark','Mark@gmail.com','MarkMark123','Bans'),(3,'Jacob','Jacob@gmail.com','JacobJacob123','Doody'),(4,'Maria','Maria@gmail.com','MariaMaria123','Blosa'),(5,'Clarissa','Clarissa@gmail.com','ClarisaClarisa123','Costa'),(6,'Erica','Erica@gmai.com','EricaErica123','Suar'),(7,'Ben','BenBen@gmail.com','BenBen123','Pedri'),(9,'Cameron','Cameron@gmail.com','CameronCameron123','Koke'),(10,'Brat','Brat@gmail.com','BratBrat123','Kualre'),(11,'Julia','Julia@gmail.com','JacobJacob123','scalvini'),(12,'Ethan','Ethan@gmail.com','BenBen123','pava'),(13,'Ema','Ema@gmail.com','JacobJacob123','fuios'),(14,'Taylor','Taylor@gmail.com','BenBen123','gonio'),(15,'Liam','Liam@gmail.com','MarkMark123','bambica'),(16,'Chloe','Chloe@gmail.com','CameronCameron123','stones'),(17,'Grace','Grace@gmail.com','EricaErica123','smith'),(18,'Aiden','Aiden@gmail.com','JacobJacob123','muller'),(19,'Alexander','Alexander@gmail.com','MarkMark123','jonas'),(20,'Lucas','Lucas@gmail.com','CameronCameron123','joens'),(21,'Matthew','Mathew@gmail.com','BenBen123','haalond'),(22,'Jerry','Jerry@gmail.com','MarkMark123','silvestre'),(23,'Ross','Ross@gmail.com','EricaErica123','giacommo'),(24,'Samantha','Samantha@gmail.com','BratBrat123','Enter Student Surname');
/*!40000 ALTER TABLE `Students` ENABLE KEYS */;
#UNLOCK TABLES;

--
-- Table structure for table `TeacherDecisions`
--

DROP TABLE IF EXISTS `TeacherDecisions`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `TeacherDecisions` (
  `DecisionID` int NOT NULL DEFAULT '0',
  `DecisionName` enum('Pass','Fail','NotDecided') DEFAULT NULL,
  `Teacher_ID` int NOT NULL DEFAULT '0',
  `Student_ID` int NOT NULL DEFAULT '0',
  `Cours_ID` int NOT NULL DEFAULT '0',
  PRIMARY KEY (`DecisionID`),
  UNIQUE KEY `DecisionID_UNIQUE` (`DecisionID`),
  KEY `Cours_ID_idx` (`Cours_ID`),
  KEY `Student_ID_idx` (`Student_ID`),
  KEY `Teacher_ID_idx` (`Teacher_ID`),
  CONSTRAINT `Cours_ID` FOREIGN KEY (`Cours_ID`) REFERENCES `Courses` (`CourseID`),
  CONSTRAINT `Student_ID` FOREIGN KEY (`Student_ID`) REFERENCES `Students` (`StudentID`),
  CONSTRAINT `Teacher_ID` FOREIGN KEY (`Teacher_ID`) REFERENCES `Teachers` (`TeacherID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `TeacherDecisions`
--

LOCK TABLES `TeacherDecisions` WRITE;
/*!40000 ALTER TABLE `TeacherDecisions` DISABLE KEYS */;
INSERT INTO `TeacherDecisions` VALUES (701,'Pass',101,1,201),(702,'Pass',102,2,204),(703,'Fail',103,3,212),(704,'Fail',104,4,202),(705,'Pass',105,5,206),(706,'Pass',106,6,211),(707,'Pass',107,7,208),(708,'Fail',108,9,210),(709,'Pass',109,10,203),(710,'Fail',110,11,205),(711,'Fail',101,24,201),(712,'Fail',111,12,209),(713,'Pass',101,13,201),(714,'Pass',102,14,204),(715,'Pass',103,15,212),(716,'Pass',104,16,202),(717,'Fail',105,17,206),(718,'Fail',106,18,211),(719,'Pass',107,19,208),(720,'Pass',108,20,210),(721,'Fail',109,21,203),(722,'Pass',110,22,205),(723,'Fail',111,23,209);
/*!40000 ALTER TABLE `TeacherDecisions` ENABLE KEYS */;
UNLOCK TABLES;

--
-- Table structure for table `Teachers`
--

DROP TABLE IF EXISTS `Teachers`;
/*!40101 SET @saved_cs_client     = @@character_set_client */;
/*!50503 SET character_set_client = utf8mb4 */;
CREATE TABLE `Teachers` (
  `TeacherID` int NOT NULL DEFAULT '0',
  `TeacherName` varchar(255) NOT NULL DEFAULT 'Enter Teacher Name',
  `TeacherEmail` varchar(255) NOT NULL DEFAULT 'Enter Teacher Email',
  `TeacherPassword` varchar(255) NOT NULL DEFAULT 'Enter Teacher Password',
  `TeacherSurname` varchar(255) NOT NULL DEFAULT 'Enter Teacher Surname',
  PRIMARY KEY (`TeacherID`),
  UNIQUE KEY `TeacherID_UNIQUE` (`TeacherID`),
  UNIQUE KEY `TeacherEmail_UNIQUE` (`TeacherEmail`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci;
/*!40101 SET character_set_client = @saved_cs_client */;

--
-- Dumping data for table `Teachers`
--

LOCK TABLES `Teachers` WRITE;
/*!40000 ALTER TABLE `Teachers` DISABLE KEYS */;
INSERT INTO `Teachers` VALUES (100,'britney','brittney@gmail.com','spirsea','buala'),(101,'karla','Karla@gmail.com','karla1','fklourt'),(102,'marla','marla@gmail.com','marla1','faretu'),(103,'barla','barla@gmail.com','barla1','duioas'),(104,'charla','charla@gmail.com','charla1','husa'),(105,'darla','darla@gmail.com','darla1','sikas'),(106,'niki','niki@gmail.com','niki1','boure'),(107,'fliki','fliki@gmail.com','fliki1','smith'),(108,'cameron','cameron@gmail.com','cameron1','tetcher'),(109,'jessie','jessie@gmail.com','jessie1','hugo'),(110,'max','max@gmail.com','Enter Teacher Password','boss'),(111,'shmit','shmit@gmail.com','shmit1','santa');
/*!40000 ALTER TABLE `Teachers` ENABLE KEYS */;
UNLOCK TABLES;
/*!40103 SET TIME_ZONE=@OLD_TIME_ZONE */;

/*!40101 SET SQL_MODE=@OLD_SQL_MODE */;
/*!40014 SET FOREIGN_KEY_CHECKS=@OLD_FOREIGN_KEY_CHECKS */;
/*!40014 SET UNIQUE_CHECKS=@OLD_UNIQUE_CHECKS */;
/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
/*!40111 SET SQL_NOTES=@OLD_SQL_NOTES */;

-- Dump completed on 2023-11-27  2:44:58




# License

* This project is licensed under the MIT License.

* Feel free to customize this template according to the specifics of your project.


# Contributing

* We welcome contributions! If you want to contribute, please follow the guidelines in CONTRIBUTING.md.
