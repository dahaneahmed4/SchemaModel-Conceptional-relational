# 💾 Employee System SQL Studio

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white)

> **A fully interactive, browser-based SQL environment simulating the deployment of the Employee Participation System.**

## 📖 Overview

This project implements the physical database design for an Employee Management System. Instead of just providing raw text files, this solution is a **Single-Page Application (SPA)** that simulates a professional Database IDE.

It includes the full **DDL (Data Definition Language)** to create the schema and **DML (Data Manipulation Language)** to populate it with mock data, all wrapped in a GUI that visualizes the relationships and allows for simulated query execution.

---

## 🚀 Quick Start

### Prerequisites
* A modern web browser (Chrome, Firefox, Edge, or Safari).
* **No database server** (MySQL/PostgreSQL) is required; the application runs entirely in the browser using JavaScript simulation.

### Installation
1.  Download the `sql_implementation_studio.html` file.
2.  Double-click to launch the application.

---

## 🛠️ Database Schema Implementation

The system creates 4 normalized tables with strict Referential Integrity.

### 1. Department (Parent)
* **PK:** `Num_S` (INT)
* **Attributes:** `Label`, `Manager_Name`

### 2. Employee (Child)
* **PK:** `Num_E` (INT)
* **FK:** `Department_Num_S` → References `Department(Num_S)`
* **Constraint:** `ON DELETE SET NULL` (If a department is dissolved, employees remain in the system).

### 3. Project (Child)
* **PK:** `Num_P` (INT)
* **FK:** `Department_Num_S` → References `Department(Num_S)`
* **Constraint:** `ON DELETE CASCADE` (If a department is removed, its internal projects are removed).

### 4. Employee_Project (Associative)
* **PK:** Composite (`Employee_Num_E`, `Project_Num_P`)
* **FK 1:** References `Employee`
* **FK 2:** References `Project`
* **Purpose:** Handles the **Many-to-Many** relationship and stores the `Role` attribute.

---

## 🎮 Features & Usage

### 1. DDL & DML Viewers
Navigate to the sidebar to view the exact SQL scripts used to build the system.
* **Create Tables:** Shows `CREATE TABLE` statements with constraints.
* **Populate Data:** Shows `INSERT INTO` statements with 15+ mock records.

### 2. Interactive Terminal
The application includes a JavaScript-powered command line. You can type the following commands to simulate database interaction:

| Command | Description |
| :--- | :--- |
| `help` | Show available commands |
| `show tables` | List the tables in the schema |
| `select * from employee` | Display mock data for employees |
| `clear` | Clear the terminal screen |

### 3. Visual ER Diagram
Click the **"Entity Diagram"** tab to see a CSS-rendered visualization of the tables, including:
* Primary Key badges (Yellow)
* Foreign Key badges (Blue)
* Data Types (INT, VARCHAR, DATE)

---

## 📝 SQL Snippet (Core Logic)

```sql
-- Associative Table Logic
CREATE TABLE Employee_Project (
    Employee_Num_E INT,
    Project_Num_P INT,
    Role VARCHAR(255),
    
    PRIMARY KEY (Employee_Num_E, Project_Num_P),
    
    CONSTRAINT fk_ep_emp FOREIGN KEY (Employee_Num_E) 
        REFERENCES Employee(Num_E) ON DELETE CASCADE
);
