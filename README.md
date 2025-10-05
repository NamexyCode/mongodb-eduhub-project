  ## EduHub E-Learning Platform Database Project

### Project Overview
This project simulates the database backend for "EduHub," an online e-learning platform, using MongoDB as the core data store. It demonstrates proficiency in MongoDB concepts, including data modeling (using document references), CRUD operations, the Aggregation Framework, indexing for performance, and schema validation.

The system manages user profiles, course content, student enrollments, assignment submissions, and provides analytics on performance and revenue.

### Technical Stack
Database: MongoDB v8.0+
Language: Python 3.9+
Driver: PyMongo
Libraries: Pandas, datetime
Environment: Jupyter Notebook (for demonstration)

### ⚙️ Setup and Installation Guide
Follow these steps to set up the project environment and connect to your MongoDB instance.

1. Prerequisites
Before starting, ensure you have the following installed:
MongoDB Server: Running locally (default port 27017).
Python 3: (3.9 or higher recommended).
Git: For cloning the repository.
VS Code (or preferred IDE): For editing and running the code.

2. Repository and Environment Setup

Clone the Repository
Create and Activate Virtual Environment
Install Dependencies: pip install -r requirements.txt

3. Database Execution
The entire project setup, data population, and query execution are contained within the Jupyter Notebook.
Start MongoDB: Ensure your local MongoDB server is running.
Launch Jupyter: jupyter notebook notebooks/eduhub_mongodb_project.ipynb

### 📚 Database Schema Documentation
The EduHub platform uses a relational-like schema modeled in MongoDB using application-level references (e.g., storing a courseId in the enrollments document).

#### Key Data Modeling Decisions
Document References: Chosen over deep embedding to prevent document size growth in frequently updated collections (like users and courses) and to maintain consistency for highly interconnected entities.

Embedded Objects: Used for stable, logically grouped data (e.g., profile embedded within the users document).

Soft Deletes: Implemented in the users collection using the isActive boolean flag to maintain historical data and referential integrity for past enrollments.

### 📈 Performance Analysis and Indexing
Efficient data retrieval is managed through strategic indexing.

### ✅ Data Validation and Integrity
Schema Validation ($jsonSchema)
Schema validation was implemented directly on the database using the $jsonSchema operator for the primary collections (users, courses, enrollments). This ensures:

Required Fields: Documents must include essential data (e.g., a course cannot be created without an instructorId).

Data Type Enforcement: Fields maintain correct types (e.g., price is a number, dateJoined is a date).

Enum Restrictions: Values are limited to predefined lists (e.g., role must be 'student' or 'instructor').

#### Error Handling
PyMongo's exception handling was used to gracefully manage common database errors, preventing application crashes and providing informative feedback:
DuplicateKeyError: Handled during user registration attempts with a pre-existing email (due to the unique index).
OperationFailure: Caught during insertion attempts that violate the $jsonSchema rules (e.g., inserting an integer into a field defined as a string, or missing a required field).

### 📂 Deliverables Structure
This repository contains all required project files:

mongodb-eduhub-project/
├── README.md                 <-- This document
├── requirements.txt          <-- Project dependencies
├── notebooks/
│   └── eduhub_mongodb_project.ipynb  <-- Primary submission: All code and results
├── src/
│   └── eduhub_queries    <-- Backup Python code file (commented)
├── data/
│   ├── sample_data.json      <-- Exported documents from all collections
│   └── schema_validation.json<-- JSON definitions of the validation rules
└── docs/
    ├── performance_analysis.md<-- Detailed performance test documentation
    └── presentation.pptx     <-- Project design presentation
