# HRMS Flask Application - README

This project implements a basic Human Resource Management System (HRMS) using Flask. The app provides functionality for managing employees, tracking attendance, and generating reports.

## Features

- **Employee Management**: 
  - Add, view, update, and delete employee records.
  - List employees and view individual employee details.
  
- **Attendance Tracking**: 
  - Mark attendance for employees.
  - Retrieve and display attendance records for specific employees.
  
- **Reporting**: 
  - Generate a department-wise report showing the count of employees in each department.

## Project Structure

- **app.py**: The main Flask application with routes for employee management, attendance tracking, and reporting.
- **database.py**: Handles database connections using SQLite.
- **schema.sql**: SQL script for creating the necessary database tables.
  
## Database Setup

### schema.sql

Run the following SQL queries to create the required tables:

```sql
CREATE TABLE emps (
    empid INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL,
    designation TEXT NOT NULL,
    department TEXT NOT NULL,
    dateofjoining TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE IF NOT EXISTS attendance (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    empid INTEGER NOT NULL,
    attendance_date DATE NOT NULL,
    status TEXT NOT NULL,
    FOREIGN KEY (empid) REFERENCES emps (empid)
);
```

The `emps` table stores employee details, and the `attendance` table records attendance data.

## Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-repo/hrms-flask.git
   cd hrms-flask
   ```

2. **Install Dependencies**:
   Install the required Python packages using `pip`:
   ```bash
   pip install flask
   ```

3. **Set Up the Database**:
   - Create a SQLite database using the schema provided in `schema.sql`.
   - You can execute the SQL script in your SQLite environment.

4. **Run the Application**:
   Start the Flask server:
   ```bash
   python app.py
   ```

   The app will be available at `http://127.0.0.1:5000/`.

## Application Routes

### Employee Management

- **Dashboard** (`/dashboard`): Displays the list of all employees.
- **Add New Employee** (`/addnewemployee`): Form to add a new employee.
- **View Single Employee** (`/singleemployee/<int:empid>`): View details of an employee.
- **Update Employee** (`/updateemployee`): Update employee details.
- **Delete Employee** (`/deleteemp/<int:empid>`): Delete an employee.

### Attendance Tracking

- **Mark Attendance** (`/mark_attendance`): Form to mark attendance for a specific employee.
- **Get Attendance** (`/get_attendance`): Retrieve attendance records for a specific employee.

### Reporting

- **Department Report** (`/report`): Displays a department-wise employee count using a bar chart.

## Code Explanation

### app.py

The main application file that defines the following routes:
- **index** (`/`): The home page.
- **dashboard** (`/dashboard`): Displays all employees.
- **addnewemployee** (`/addnewemployee`): Adds a new employee to the database.
- **singleemployee** (`/singleemployee/<int:empid>`): Displays the details of a single employee.
- **fetchone** (`/fetchone/<int:empid>`): Fetches an employee's details for updating.
- **updateemployee** (`/updateemployee`): Updates an employee's details.
- **deleteemp** (`/deleteemp/<int:empid>`): Deletes an employee.
- **report** (`/report`): Generates a report showing the employee count per department.
- **mark_attendance** (`/mark_attendance`): Marks attendance for an employee.
- **attendance_form** (`/attendance_form`): Renders the attendance retrieval form.
- **get_attendance** (`/get_attendance`): Retrieves attendance records for an employee.

### database.py

Handles SQLite database connection and ensures a persistent connection across requests using Flask's `g` object.

### schema.sql

Defines the SQL schema for the `emps` (employees) and `attendance` tables.



## License

This project is open-source and free to use.

---

This README provides a comprehensive overview of the HRMS Flask application and its structure. Feel free to modify this based on your specific setup!
