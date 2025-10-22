## 📊 Entity Relationships Overview

| From             | To               | Type  | Meaning                                  |
| ---------------- | ---------------- | ----- | ---------------------------------------- |
| **Doctors**      | **Patients**     | 1 → * | One doctor has many patients             |
| **Patients**     | **Appointments** | 1 → * | One patient can have many appointments   |
| **Doctors**      | **Appointments** | 1 → * | One doctor can have many appointments    |
| **Appointments** | **Treatments**   | 1 → * | One appointment can have many treatments |

<img width="1280" height="888" alt="Hospital ERD" src="https://github.com/user-attachments/assets/d9a01290-7573-4192-a491-673e8a14c324" />

---

## 🧩 Relationship Details

### 1. Doctors → Patients (One-to-Many)
- **Cardinality:** `1 : N`  
- **Description:** One doctor can be assigned to many patients, but each patient is assigned to only one doctor.  
- **Foreign Key:** `patients.doctor_id → doctors.doctor_id`  
- **Delete Rule:** `ON DELETE CASCADE` (deleting a doctor will remove all their assigned patients).  

---

### 2. Patients → Appointments (One-to-Many)
- **Cardinality:** `1 : N`  
- **Description:** Each patient can have multiple appointments scheduled with their doctor over time.  
- **Foreign Key:** `appointments.patient_id → patients.patient_id`  
- **Delete Rule:** `ON DELETE CASCADE` (deleting a patient removes all their appointments).  

---

### 3. Doctors → Appointments (One-to-Many)
- **Cardinality:** `1 : N`  
- **Description:** Each doctor can conduct many appointments with their patients.  
- **Foreign Key:** `appointments.doctor_id → doctors.doctor_id`  
- **Delete Rule:** `ON DELETE CASCADE` (deleting a doctor removes all related appointments).  

---

### 4. Appointments → Treatments (One-to-Many)
- **Cardinality:** `1 : N`  
- **Description:** A single appointment may result in multiple treatments or procedures being recorded.  
- **Foreign Key:** `treatments.appointment_id → appointments.appointment_id`  
- **Delete Rule:** `ON DELETE CASCADE` (deleting an appointment deletes its treatments).  

---

## ⚙️ Business Rules

1. Every **patient** must be assigned to **exactly one doctor** (`doctor_id` is `NOT NULL`).  
2. A **doctor** can manage multiple patients and appointments.  
3. An **appointment** must be linked to both a **valid patient** and a **valid doctor** — orphaned appointments are not allowed.  
4. A **treatment** cannot exist without an **appointment**.  
5. **Treatment cost** must be a positive decimal value.  
6. **Appointment status** must be one of: `'Pending'`, `'Completed'`, `'Missed'`, or `'Cancelled'`.  

### Date Constraints
- `appointment_date` cannot be in the past when scheduling a new appointment.  
- `treatment_date` must be on or after the related appointment date.  

### Cascading Deletions
- Deleting a **doctor** removes all their patients, appointments, and associated treatments.  
- Deleting a **patient** removes their appointments and treatments.  

### Data Validation
- `contact_info` fields must follow valid phone number format (10–12 digits).  
- `gender` should be restricted to `'Male'`, `'Female'`, or `'Other'`.  

---
