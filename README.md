# 📚 Research Projects Database

This project is a relational database design for managing **research projects**, their **funding agencies**, and the **employees** who work on them. The database uses an Entity-Relationship (ER) model and is implemented using SQL with well-structured tables and constraints.

## 📁 Database Overview

The system manages:

- Projects and their attributes (name, budget, duration, funding agency)
- Employees (SSN, name, salary)
- Funding agencies (name, address)
- Employee-project associations (many-to-many relationships)
- Project managers (each project has one manager who is also an employee)

## 🛠️ Tables Created

### 1. `Employee`
Stores employee details.

```sql
CREATE TABLE Employee (
    SSN INT PRIMARY KEY,
    Emp_Name VARCHAR(50),
    Salary DECIMAL
);
```

### 2. `FundingAgency`
Stores information about funding organizations.

```sql
CREATE TABLE FundingAgency (
    Agency_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Address VARCHAR(255)
);
```

### 3. `Project`
Each project is linked to a single funding agency.

```sql
CREATE TABLE Project (
    Project_ID INT PRIMARY KEY,
    Name VARCHAR(100),
    Duration INT,  -- Duration in months
    Budget DECIMAL(12,2)
);
```

### 4. `Employee_Project`
Junction table to show which employees work on which projects and who the manager is.

```sql
CREATE TABLE Employee_Project (
    SSN INT,
    Project_ID INT,
    Manager_SSN INT,
    PRIMARY KEY (SSN, Project_ID),
    FOREIGN KEY (SSN) REFERENCES Employee(SSN),
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
    FOREIGN KEY (Manager_SSN) REFERENCES Employee(SSN)
);
```

### 5. `Project_Manager`
Assigns one manager to each project.

```sql
CREATE TABLE Project_Manager (
    Project_ID INT PRIMARY KEY,
    Manager_SSN INT,
    FOREIGN KEY (Project_ID) REFERENCES Project(Project_ID),
    FOREIGN KEY (Manager_SSN) REFERENCES Employee(SSN)
);
```

## 📊 Sample Data

Sample records for employees, agencies, projects, and associations have been added to simulate a working environment.

### 🔹 Employee Sample
```sql
INSERT INTO Employee VALUES
(101, 'John Doe', 55000.00),
(102, 'Jane Smith', 65000.00),
(103, 'Alice Brown', 72000.00);
```

### 🔹 Funding Agencies
```sql
INSERT INTO FundingAgency VALUES
(201, 'Tech Research Fund', '123 Tech Ave, Silicon Valley, CA'),
(202, 'Innovation Grants Inc.', '456 Innovation Dr, New York, NY'),
(203, 'Global Funding Group', '789 Global St, London, UK');
```

### 🔹 Projects
```sql
INSERT INTO Project VALUES
(301, 'AI Research', 12, 200000.00),
(302, 'Cloud Migration', 18, 300000.00),
(303, 'Blockchain Platform', 24, 400000.00);
```

### 🔹 Project Managers
```sql
INSERT INTO Project_Manager VALUES
(301, 101),
(302, 102),
(303, 103);
```

### 🔹 Employee-Project Associations
```sql
INSERT INTO Employee_Project VALUES
(101, 301, 101),
(102, 302, 102),
(103, 303, 103);
```

## ✅ Features

- Supports many-to-many relationships between employees and projects
- Ensures each project has exactly one manager
- Data integrity maintained with foreign key constraints
- Flexible schema to extend with more details (e.g., tasks, departments, timelines)

## 🧠 Real-World Assumptions

- Project names are unique within each funding agency.
- Managers are regular employees who also work on projects.
- Employees can work on multiple projects.

## 📌 Use Case

Ideal for academic or enterprise use where research project tracking and funding management is needed.
![image](https://github.com/user-attachments/assets/2753da9a-74a4-4feb-b44a-47dd9b444aca)

![image](https://github.com/user-attachments/assets/ba9f13c7-b74a-4167-9942-1486663c92b7)


