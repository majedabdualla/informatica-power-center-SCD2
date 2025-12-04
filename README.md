# 📌 SCD Type 2 Implementation in Informatica PowerCenter

## 📝 Overview
This project demonstrates a complete implementation of **Slowly Changing Dimension Type 2 (SCD2)** using **Informatica PowerCenter**.  
The goal is to track historical changes in dimension data while preserving all previous versions of each record.

This repository includes:
- ETL mappings for SCD2
- Lookup & Update Strategy logic
- Sample source and target data
- Workflow to run and validate the SCD2 process

---

## 📚 What is SCD Type 2?
**Slowly Changing Dimensions (SCD)** represent data that changes slowly over time in a data warehouse.

### 🔹 SCD Type 2
SCD Type 2 keeps the **full history** of changes.  
When a change occurs:
1. The old record is **closed** (`End_Date` updated, `Is_Current = 0`)
2. A **new record is inserted** with updated values
3. The new record becomes the **current active version** (`Is_Current = 1`, `Start_Date = current date`)

## ⚙️ Implementation Steps

### 1️⃣ Extract
Data is extracted from the source file and loaded into a staging area.

### 2️⃣ Compare
A **Lookup transformation** compares source records with the target dimension table to determine if:
- The record is **new**
- The record **exists but has changed**
- The record **exists with no changes**

### 3️⃣ Apply SCD2 Logic
Using **Router** + **Update Strategy**:
- **New record → INSERT**
- **Changed record → Close old record + INSERT new version**
- **Unchanged record → REJECT**

### 4️⃣ Load
Records are loaded into the target dimension table with proper versioning fields.

##  Technologies Used
- Informatica PowerCenter  
- SQL  
-  SQL Server  
  

 ## 🖼️ Project Screenshots

### 📍 1. SCD2 Mapping (Informatica PowerCenter)
<img src="./scd2_mapping.png" width="900"/>

---

### 📍 2. Session 
<img src="./session.png" width="900"/>

---

### 📍 3. Output After SCD2 Load
<img src="./output.png" width="900"/>

