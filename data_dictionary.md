# 🏥 Data Dictionary – Hospital Management Schema

## Overview
This data dictionary describes all tables, columns, and relationships in the **hospital** database schema (PostgreSQL).  
The schema manages information about doctors, patients, appointments, and treatments within a healthcare setting.

---

## 📋 Tables

### 1. doctors
**Purpose:** Stores information about doctors working in the hospital.

| Column Name | Data Type | Constraints | Description |
|--------------|-----------|--------------|-------------|
| doctor_id | VARCHAR | PRIMARY KEY | Unique identifier for each doctor |
| first_name | VARCHAR | NOT NULL | Doctor's first name |
| last_name | VARCHAR | NOT NULL | Doctor's last name |
| specialty | VARCHAR | NOT NULL | Area of medical specialization (e.g., Pediatrics, Cardiology) |
| contact_info | VARCHAR | NOT NULL | Doctor's contact details (e.g., phone or email) |

---

### 2. patients
**Purpose:** Stores details about patients under medical care.

| Column Name | Data Type | Constraints | Description |
|--------------|-----------|--------------|-------------|
| patient_id | VARCHAR | PRIMARY KEY | Unique identifier for each patient |
| first_name | VARCHAR | NOT NULL | Patient's first name |
| last_name | VARCHAR | NOT NULL | Patient's last name |
| date_of_birth | DATE | NOT NULL | Patient's date of birth |
| gender | VARCHAR | CHECK (gender IN ('Male', 'Female', 'Other')) | Patient's gender |
| contact_info | VARCHAR | NOT NULL | Patient's contact details (phone or email) |
| doctor_id | VARCHAR | NOT NULL, FOREIGN KEY → doctors(doctor_id) ON DELETE CASCADE | Refers to the doctor responsible for the patient |

---

### 3. appointments
**Purpose:** Records scheduled consultations between patients and doctors.

| Column Name | Data Type | Constraints | Description |
|--------------|-----------|--------------|-------------|
| appointment_id | VARCHAR | PRIMARY KEY | Unique identifier for each appointment |
| patient_id | VARCHAR | NOT NULL, FOREIGN KEY → patients(patient_id) ON DELETE CASCADE | Patient attending the appointment |
| doctor_id | VARCHAR | NOT NULL, FOREIGN KEY → doctors(doctor_id) ON DELETE CASCADE | Doctor conducting the appointment |
| appointment_date | DATE | NOT NULL | Scheduled date of the appointment |
| appointment_time | TIME | NOT NULL | Scheduled time of the appointment |
| reason_for_visit | VARCHAR | - | Brief reason or purpose of the appointment |
| appointment_status | VARCHAR | DEFAULT 'Pending', CHECK (appointment_status IN ('Pending', 'Completed', 'Missed', 'Cancelled')) | Current status of the appointment |

---

### 4. treatments
**Purpose:** Captures details of treatments or procedures given during appointments.

| Column Name | Data Type | Constraints | Description |
|--------------|-----------|--------------|-------------|
| treatment_id | VARCHAR | PRIMARY KEY | Unique identifier for each treatment record |
| appointment_id | VARCHAR | NOT NULL, FOREIGN KEY → appointments(appointment_id) ON DELETE CASCADE | The appointment associated with this treatment |
| treatment_description | VARCHAR | NOT NULL | Description of the treatment or procedure |
| treatment_date | DATE | NOT NULL | Date when the treatment was administered |
| treatment_cost | NUMERIC | CHECK (treatment_cost >= 0) | Cost associated with the treatment |

---

## 🔗 Relationships

### Foreign Key Relationships

1. **patients.doctor_id → doctors.doctor_id**
   - **Type:** One-to-Many  
   - **Description:** Each doctor can manage multiple patients.  
   - **Action:** `ON DELETE CASCADE` (deleting a doctor removes all related patients).  

2. **appointments.patient_id → patients.patient_id**
   - **Type:** One-to-Many  
   - **Description:** Each patient can have multiple appointments.  
   - **Action:** `ON DELETE CASCADE` (deleting a patient removes their appointments).  

3. **appointments.doctor_id → doctors.doctor_id**
   - **Type:** One-to-Many  
   - **Description:** Each doctor can conduct multiple appointments.  
   - **Action:** `ON DELETE CASCADE` (deleting a doctor removes related appointments).  

4. **treatments.appointment_id → appointments.appointment_id**
   - **Type:** One-to-Many  
   - **Description:** Each appointment can have multiple treatments.  
   - **Action:** `ON DELETE CASCADE` (deleting an appointment removes its treatments).  

---

## ⚙️ Business Rules

1. Every **patient** must be linked to exactly **one doctor**.  
2. A **doctor** can manage multiple **patients** and **appointments**.  
3. An **appointment** must reference valid **doctor** and **patient** records.  
4. A **treatment** cannot exist without an associated **appointment**.  
5. `appointment_date` cannot be in the past when creating a new appointment.  
6. `treatment_date` must be on or after the related `appointment_date`.  
7. `treatment_cost` must be positive or zero.  
8. `appointment_status` must be one of: `'Pending'`, `'Completed'`, `'Missed'`, `'Cancelled'`.  
9. `gender` must be one of: `'Male'`, `'Female'`, `'Other'`.  
10. Deleting a **doctor** cascades to their **patients**, **appointments**, and **treatments**.

---

