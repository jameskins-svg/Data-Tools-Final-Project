# Data-Tools-Final-Project

<div align="center">
  <!-- You are encouraged to replace this logo with your own! Otherwise you can also remove it. -->
  <img width="314" height="285" alt="image" src="https://github.com/jameskins-svg/hello_world/blob/main/image_2025-09-30_111733297.png" />
  <br/>

  <h3><b>Mwai's ReadME Template</b></h3>

</div>

# Hospital SQL Project

<a name="readme-top"></a>

<!-- TABLE OF CONTENTS -->

# 📗 Table of Contents

- [My SQL Project](#about-project)
- [📗 Table of Contents](#-table-of-contents)
- [📖 My SQL Project](#about-project)
  - [🛠 Built With ](#-built-with-)
    - [Tech Stack ](#tech-stack-)
    - [Key Features ](#key-features-)
  - [💻 Getting Started ](#-getting-started-)
    - [Prerequisites](#prerequisites)
    - [Setup](#setup)
    - [Usage](#usage)
  - [👥 Authors ](#-authors-)
  - [🔭 Future Features ](#-future-features-)
  - [🤝 Contributing ](#-contributing-)

<!-- PROJECT DESCRIPTION -->

# 📖 My SQL Project <a name="about-project"></a>

**My Hospital SQL Project** is a simple Database that uses SQL, Postgres via Supabase and R to create, query and secure a **Hospital** database.

## 🛠 Built With <a name="built-with"></a>

### Tech Stack <a name="tech-stack"></a>
- SQL
- Postgres DB

<!-- Features -->

### Key Features <a name="key-features"></a>

- [ ] **Tables**
- [ ] **Schema**
- [ ] **Access control**

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- GETTING STARTED -->

## 💻 Getting Started <a name="getting-started"></a>

To rebuild this DB, follow these steps.

### Prerequisites

To run this project, you need:
- [A Supabase account](https://supabase.com/)
- [Knowledge on SQL](https://www.w3schools.com/sql/)
- A schema for creating your tables in the DB


### DB Schema

- The DB is made up of 3 tables. Eaach table has 5 entries.
- To create the table, you will need a schema as shown below:

```sql
-- Create Patients table
CREATE TABLE Patients (
    patient_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    date_of_birth DATE,
    gender VARCHAR(10),
    contact_info VARCHAR(100)
);

-- Create Doctors table
CREATE TABLE Doctors (
    doctor_id VARCHAR(10) PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    specialty VARCHAR(50),
    contact_info VARCHAR(100)
);

-- Create Appointments table
CREATE TABLE Appointments (
    appointment_id VARCHAR(10) PRIMARY KEY,
    patient_id VARCHAR(10) REFERENCES Patients(patient_id),
    doctor_id VARCHAR(10) REFERENCES Doctors(doctor_id),
    appointment_date DATE,
    appointment_time TIME,
    reason_for_visit VARCHAR(255),
    appointment_status VARCHAR(50) -- Column to indicate the status of the appointment
);

-- Create Treatments table
CREATE TABLE Treatments (
    treatment_id VARCHAR(10) PRIMARY KEY,
    appointment_id VARCHAR(10) REFERENCES Appointments(appointment_id),
    treatment_description VARCHAR(255),
    treatment_date DATE,
    treatment_cost DECIMAL(10, 2)
);


-- Insert sample data into Patients table
INSERT INTO Patients (patient_id, first_name, last_name, date_of_birth, gender, contact_info) VALUES
('P001', 'John', 'Kamau', '1980-01-15', 'Male', '0798532678'),
('P002', 'Jane', 'Wanjiku', '1990-02-25', 'Female', '0720867589'),
('P003', 'Alice', 'Mwangi', '2000-03-10', 'Female', '0739236490'),
('P004', 'Bob', 'Otieno', '1975-04-05', 'Male', '074377901'),
('P005', 'Charlie', 'Njoroge', '1985-05-20', 'Male', '0755566012'),
('P006', 'Grace', 'Achieng', '1995-06-30', 'Female', '0763324563'),
('P007', 'Peter', 'Kariuki', '1988-07-25', 'Male', '0778426334'),
('P008', 'Joy', 'Mutua', '1992-08-15', 'Female', '07833578345'),
('P009', 'Brian', 'Omondi', '1982-09-10', 'Male', '07901006456'),
('P010', 'Aisha', 'Ali', '1998-10-05', 'Female', '0701481167');


-- Insert sample data into Doctors table
INSERT INTO Doctors (doctor_id, first_name, last_name, specialty, contact_info) VALUES
('D001', 'Dr. Emily', 'Wangari', 'Cardiology', '0717384678'),
('D002', 'Dr. Michael', 'Oluoch', 'Neurology', '0711956789'),
('D003', 'Dr. Sarah', 'Kilonzo', 'Pediatrics', '0796357890'),
('D004', 'Dr. David', 'Mutiso', 'Orthopedics', '0745046901'),
('D005', 'Dr. Laura', 'Kariuki', 'Dermatology', '0754672512'),
('D006', 'Dr. James', 'Mwangi', 'General Surgery', '0765096423'),
('D007', 'Dr. Anne', 'Ndungu', 'Gynecology', '0711468534'),
('D008', 'Dr. Peter', 'Omondi', 'ENT', '0785499845');


-- Insert sample data into Appointments table
INSERT INTO Appointments (appointment_id, patient_id, doctor_id, appointment_date, appointment_time, reason_for_visit, appointment_status) VALUES
('A001', 'P001', 'D001', '2025-09-01', '09:00:00', 'Routine Checkup', 'Completed'),
('A002', 'P002', 'D002', '2025-09-15', '10:00:00', 'Headache', 'Completed'),
('A003', 'P003', 'D003', '2025-09-20', '11:00:00', 'Fever', 'Missed'),
('A004', 'P004', 'D004', '2025-09-25', '12:00:00', 'Back Pain', 'Pending'),
('A005', 'P005', 'D005', '2025-09-30', '13:00:00', 'Skin Rash', 'Completed'),
('A006', 'P006', 'D006', '2025-10-05', '14:00:00', 'Stomach Ache', 'Pending'),
('A007', 'P007', 'D007', '2025-10-10', '15:00:00', 'Pregnancy Checkup', 'Pending'),
('A008', 'P008', 'D008', '2025-10-15', '16:00:00', 'Ear Infection', 'Pending'),
('A009', 'P009', 'D001', '2025-10-20', '17:00:00', 'Chest Pain', 'Pending'),
('A010', 'P010', 'D002', '2025-10-25', '18:00:00', 'Migraine', 'Pending');


-- Insert sample data into Treatments table
INSERT INTO Treatments (treatment_id, appointment_id, treatment_description, treatment_date, treatment_cost) VALUES
('T001', 'A001', 'Blood Test', '2025-09-01', 1000.00),
('T002', 'A002', 'MRI Scan', '2025-09-15', 5000.00),
('T003', 'A003', 'Medication', '2025-09-20', 500.00),
('T004', 'A004', 'Physical Therapy', '2025-09-25', 2000.00),
('T005', 'A005', 'Skin Biopsy', '2025-09-30', 1500.00),
('T006', 'A006', 'Endoscopy', '2025-10-05', 3000.00),
('T007', 'A007', 'Ultrasound', '2025-10-10', 2500.00),
('T008', 'A008', 'Ear Cleaning', '2025-10-15', 800.00),
('T009', 'A009', 'ECG', '2025-10-20', 1200.00),
('T010', 'A010', 'CT Scan', '2025-10-25', 4000.00);

```

- The Tables look like this in Supabase:

Patients:
<img width="1920" height="895" alt="image" src="https://github.com/user-attachments/assets/ae7cc756-9cb7-4b20-8254-77de6651a7ad" />

Doctors:
<img width="1920" height="895" alt="image" src="https://github.com/user-attachments/assets/94fb553c-a604-4437-bbb1-c74ebcfd53aa" />

Appointments:
<img width="1920" height="895" alt="image" src="https://github.com/user-attachments/assets/ce120764-fdbc-4b0c-8210-fe70b45f8c7d" />

Treatments:
<img width="1920" height="899" alt="image" src="https://github.com/user-attachments/assets/c3741e19-4990-4265-8b18-2e5be89b0019" />

- The ERD screenshot from Supabase looks like this: 
<img width="1918" height="891" alt="image" src="https://github.com/user-attachments/assets/99718701-55ff-43e5-a266-ed27872ef9c7" />

- To test the table, I used two queries: 

```sql
SELECT * FROM orders
WHERE name = "Nadine Gordimer"
````

```sql
SELECT * FROM books
WHERE in_stock = "TRUE"
````

- Here are the results of the queries:
<img width="1460" height="791" alt="image" src="https://github.com/user-attachments/assets/37cf0a4e-ca92-4d8d-8888-2cca0165d32b" />

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- AUTHORS -->

## 👥 Authors <a name="authors"></a>

👤 **Joy Phoebe**

- GitHub: [@joyapisi](https://github.com/joyapisi)
- Twitter: [@joyphoebe300](https://twitter.com/joyphoebe300)
- LinkedIn: [@joyapisi](https://linkedin.com/in/joyapisi)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- FUTURE FEATURES -->

## 🔭 Future Features <a name="future-features"></a>

- [ ] **Add security**
- [ ] **Link DB to R for visualisation purposes and further analyses**

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- CONTRIBUTING -->

## 🤝 Contributing <a name="contributing"></a>

Contributions, issues, and feature requests are welcome!

Feel free to check the [issues page](../../issues/).

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- SUPPORT -->
