# Server Log Data Extraction and User History Database Update

## 📌 Project Overview

This project focuses on extracting email addresses and their corresponding dates from a server log file (`mbox.txt`), transforming the extracted information into a structured format, and storing it in MongoDB and SQLite databases.

The project implements a data extraction and transformation pipeline using Python, Regular Expressions, MongoDB, and SQL.

The processed data is used to analyze email activity, identify unique email addresses, track email history, and generate useful insights through SQL queries.

## 🎯 Problem Statement

The objective is to extract all email addresses and their associated dates from a server log file, clean and transform the extracted data, and upload it into a user history database.

The project ensures that the extracted information is structured, accurate, and accessible for further analysis and historical tracking.

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python | Data extraction and processing |
| Regular Expressions (Regex) | Extract email addresses |
| MongoDB | Store processed data |
| SQLite | Relational database storage |
| SQL | Data analysis and querying |
| PyMongo | Python-MongoDB connectivity |

## 🏗️ Project Architecture

```text
Server Log File (mbox.txt)
          |
          v
    Python Script
          |
          v
   Data Extraction
   (Email + Date)
          |
          v
   Data Transformation
   (Cleaning + Formatting)
          |
          v
       MongoDB
   (user_history)
          |
          v
    Data Migration
          |
          v
       SQLite
   (user_history)
          |
          v
      SQL Analysis
          |
          v
    Insights & Reports
```

## 📂 Project Structure

```text
Server-Log-Data-Extraction/
│
├── data/
│   └── mbox.txt
│
├── database/
│   └── user_history.db
│
├── main.py
│
├── requirements.txt
│
├── README.md
│
└── .gitignore
```

*Note: This is a suggested repository structure. Adjust filenames according to your actual implementation.*

## ⚙️ Project Workflow

### 1. Data Extraction

- Read the server log file (`mbox.txt`).
- Identify email addresses using Python Regular Expressions.
- Extract the corresponding dates associated with each email.
- Collect the extracted information into structured records.

### 2. Data Transformation

- Clean the extracted records.
- Remove invalid or incomplete records where appropriate.
- Convert dates into a standard format:

```text
YYYY-MM-DD HH:MM:SS
```

- Prepare structured data for database insertion.

### 3. Store Data in MongoDB

- Establish a connection between Python and MongoDB using PyMongo.
- Create or access the `user_history` collection.
- Insert the extracted email addresses and dates into MongoDB.

### 4. Database Migration to SQLite

- Retrieve records from the MongoDB collection.
- Connect Python to SQLite.
- Create a relational table named `user_history`.
- Define a primary key and relevant constraints.
- Insert the processed records into SQLite.

### 5. SQL Data Analysis

Execute SQL queries to analyze the extracted information.

## 📊 SQL Analysis

The project includes the following analytical questions:

**1. List all unique email addresses.**

```sql
SELECT DISTINCT email
FROM user_history;
```

**2. Count the number of emails received per day.**

```sql
SELECT DATE(email_date), COUNT(*)
FROM user_history
GROUP BY DATE(email_date);
```

**3. Find the first and last email date for each email address.**

```sql
SELECT
    email,
    MIN(email_date) AS first_email,
    MAX(email_date) AS last_email
FROM user_history
GROUP BY email;
```

**4. Count total emails from each domain.**

```sql
SELECT
    SUBSTR(email, INSTR(email, '@') + 1) AS domain,
    COUNT(*) AS total_emails
FROM user_history
GROUP BY domain;
```

**5. Find the total number of email records.**

```sql
SELECT COUNT(*) AS total_records
FROM user_history;
```

**6. Find email addresses that appear more than once.**

```sql
SELECT email, COUNT(*) AS email_count
FROM user_history
GROUP BY email
HAVING COUNT(*) > 1;
```

**7. Find the earliest email record.**

```sql
SELECT *
FROM user_history
ORDER BY email_date ASC
LIMIT 1;
```

**8. Find the latest email record.**

```sql
SELECT *
FROM user_history
ORDER BY email_date DESC
LIMIT 1;
```

**9. Count emails received per month.**

```sql
SELECT
    STRFTIME('%Y-%m', email_date) AS month,
    COUNT(*) AS total_emails
FROM user_history
GROUP BY month
ORDER BY month;
```

**10. Find the top 5 email domains.**

```sql
SELECT
    SUBSTR(email, INSTR(email, '@') + 1) AS domain,
    COUNT(*) AS total_emails
FROM user_history
GROUP BY domain
ORDER BY total_emails DESC
LIMIT 5;
```

## 💻 Installation and Setup

### Prerequisites

- Python 3.x
- MongoDB
- MongoDB Compass (optional)
- VS Code
- Git and GitHub

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
```

```bash
cd Server-Log-Data-Extraction
```

### Step 2: Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### Step 3: Install Dependencies

```bash
pip install pymongo
```

If using a requirements file:

```bash
pip install -r requirements.txt
```

### Step 4: Configure MongoDB

Start your MongoDB service and configure your MongoDB connection string in your Python script.

Example:

```python
MONGO_URI = "mongodb://localhost:27017/"
```

### Step 5: Add the Dataset

Place the `mbox.txt` file inside the `data` folder.

### Step 6: Execute the Project

```bash
python main.py
```

The script should execute the extraction, transformation, MongoDB storage, SQLite migration, and SQL analysis stages according to your implementation.

## 📈 Expected Outcomes

- Extract email addresses and associated dates from server log data.
- Transform unstructured log information into structured records.
- Store processed records in MongoDB.
- Transfer MongoDB records into SQLite.
- Maintain a relational table with primary key constraints.
- Perform SQL-based analysis of email activity.
- Identify email domains and historical email activity.

## 🚀 Key Learning Outcomes

- Python file handling and data processing.
- Regular Expressions for text extraction.
- Data cleaning and transformation.
- ETL pipeline development.
- MongoDB database integration using PyMongo.
- Relational database management using SQLite.
- SQL queries, aggregation, and data analysis.
- Data migration between NoSQL and SQL databases.
- Modular and maintainable Python programming.

## 🔮 Future Enhancements

- Automate log file processing.
- Implement scheduled ETL execution.
- Add data validation and error logging.
- Develop a Streamlit dashboard for visualizing email activity.
- Support large-scale log processing using PySpark.

## 👨‍💻 Author

**Tamir N**

- GitHub: [Add Your GitHub Profile]
- LinkedIn: [Add Your LinkedIn Profile]

---

⭐ If you find this project useful, feel free to star the repository!

**Project Category:** Data Engineering | ETL Pipeline | Database Management | SQL Analytics
