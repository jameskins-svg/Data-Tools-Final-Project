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
    patient_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    date_of_birth DATE,
    gender VARCHAR(10),
    contact_info VARCHAR(100)
);
<img width="1920" height="901" alt="image" src="https://github.com/user-attachments/assets/9e5c22ea-532f-4158-8496-f649fdb4984a" />

-- Create Doctors table
CREATE TABLE Doctors (
    doctor_id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    specialty VARCHAR(50),
    contact_info VARCHAR(100)
);
<img width="1920" height="893" alt="image" src="https://github.com/user-attachments/assets/044da67f-729c-4552-8d32-0db17c7cf462" />

-- Create Appointments table
CREATE TABLE Appointments (
    appointment_id SERIAL PRIMARY KEY,
    patient_id INT REFERENCES Patients(patient_id),
    doctor_id INT REFERENCES Doctors(doctor_id),
    appointment_date DATE,
    appointment_time TIME,
    reason_for_visit VARCHAR(255)
);
<img width="1920" height="889" alt="image" src="https://github.com/user-attachments/assets/b4a21f9b-8460-47b0-98ea-30de4352c0ee" />

-- Create Treatments table
CREATE TABLE Treatments (
    treatment_id SERIAL PRIMARY KEY,
    appointment_id INT REFERENCES Appointments(appointment_id),
    treatment_description VARCHAR(255),
    treatment_date DATE,
    treatment_cost DECIMAL(10, 2)
);
<img width="1920" height="892" alt="image" src="https://github.com/user-attachments/assets/33ba5073-0427-4ce2-bbc0-df8958fdc31d" />


-- Insert sample data into Patients table
INSERT INTO Patients (first_name, last_name, date_of_birth, gender, contact_info) VALUES
('John', 'Kamau', '1980-01-01', 'Male', '+254-700-123456'),
('Jane', 'Wanjiku', '1990-02-02', 'Female', '+254-701-234567'),
('Alice', 'Mwangi', '2000-03-03', 'Female', '+254-702-345678'),
('Bob', 'Ochieng', '1975-04-04', 'Male', '+254-703-456789'),
('Charlie', 'Njoroge', '1985-05-05', 'Male', '+254-704-567890');
<img width="1920" height="901" alt="image" src="https://github.com/user-attachments/assets/949f4cd5-2145-433c-b72c-ad02c418951e" />

-- Insert sample data into Doctors table
INSERT INTO Doctors (first_name, last_name, specialty, contact_info) VALUES
('Dr. Emily', 'Mutua', 'Cardiology', '+254-705-678901'),
('Dr. Michael', 'Odhiambo', 'Neurology', '+254-706-789012'),
('Dr. Sarah', 'Kariuki', 'Pediatrics', '+254-707-890123'),
('Dr. David', 'Waweru', 'Orthopedics', '+254-708-901234'),
('Dr. Laura', 'Kiptoo', 'Dermatology', '+254-709-012345');
<img width="1920" height="896" alt="image" src="https://github.com/user-attachments/assets/f7d8bf61-4548-4565-b720-e68458078b75" />

-- Insert sample data into Appointments table
INSERT INTO Appointments (patient_id, doctor_id, appointment_date, appointment_time, reason_for_visit) VALUES
(1, 1, '2025-10-01', '09:00:00', 'Routine Checkup'),
(2, 2, '2025-10-02', '10:00:00', 'Headache'),
(3, 3, '2025-10-03', '11:00:00', 'Fever'),
(4, 4, '2025-10-04', '12:00:00', 'Back Pain'),
(5, 5, '2025-10-05', '13:00:00', 'Skin Rash');
<img width="1920" height="892" alt="image" src="https://github.com/user-attachments/assets/ac65003a-d1e9-48b2-8d46-388d62aca0b8" />

-- Insert sample data into Treatments table
INSERT INTO Treatments (appointment_id, treatment_description, treatment_date, treatment_cost) VALUES
(1, 'Blood Test', '2025-10-01', 100.00),
(2, 'MRI Scan', '2025-10-02', 500.00),
(3, 'Medication', '2025-10-03', 50.00),
(4, 'Physical Therapy', '2025-10-04', 200.00),
(5, 'Skin Biopsy', '2025-10-05', 150.00);
<img width="1920" height="894" alt="image" src="https://github.com/user-attachments/assets/c4ba0cc7-973f-4d4d-94a5-961ce5a92e0a" />


```

- The Tables should look like this in Supabase:
authors
<img width="1893" height="476" alt="image" src="https://github.com/user-attachments/assets/9a89f3ae-77d1-4ed2-a5c5-140db1e7e27b" />

books:
<img width="1881" height="445" alt="image" src="https://github.com/user-attachments/assets/d741319f-a0ff-416c-b50f-34c315c9af24" />

customers:
<img width="1881" height="505" alt="image" src="https://github.com/user-attachments/assets/354752e6-fa32-4aa8-a28f-bf99f98039f2" />

orders:
<img width="1902" height="517" alt="image" src="https://github.com/user-attachments/assets/fe99a68a-8950-4d87-82c1-25dcd3217a65" />

- The ERD screenshot from Supabase looks like this: 
<img width="1064" height="577" alt="image" src="https://github.com/user-attachments/assets/4b8a39b1-ff20-4bd3-be6f-f662b35ae49f" />

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
