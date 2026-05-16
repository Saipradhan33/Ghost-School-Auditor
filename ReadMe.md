# 👻 Ghost School Attendance Auditor

### AI-Powered Governance & Anti-Corruption Monitoring System

> An automated fraud detection platform that identifies fake school attendance reports using RPA, identity verification, and census-based validation.

---

## 📌 Problem Statement

In many districts, fraudulent schools and manipulated attendance records continue to receive government education funding due to the lack of scalable auditing systems. Manual verification of thousands of monthly PDF attendance reports is slow, inefficient, and highly error-prone.

The **Ghost School Attendance Auditor** automates the entire audit pipeline by:

* Monitoring incoming attendance reports
* Extracting and validating student identities
* Detecting suspicious fraud patterns
* Escalating high-risk reports automatically

---

# 🚀 Project Overview

The system acts as an autonomous audit assistant for the Education Ministry.

It continuously:

1. Watches a ministry email inbox
2. Downloads attendance PDF reports automatically
3. Extracts student attendance data
4. Cross-checks names against the official district census
5. Detects anomalies and duplicate identities
6. Flags suspicious reports
7. Sends alerts to the Auditor General

---

# 🧠 Core Features

## 📥 Automated Email Monitoring (RPA)

* Continuously monitors the Education Ministry inbox
* Detects newly received Monthly Attendance Reports
* Downloads PDF attachments automatically
* Organizes reports into processing folders

### Technologies

* UiPath / Automation Anywhere / Python IMAP
* SMTP/IMAP Email Automation

---

## 📄 PDF Attendance Extraction

* Parses attendance reports from PDFs
* Extracts:

  * Student Names
  * Roll Numbers
  * Attendance Data
  * School Information

### Technologies

* PyPDF2
* pdfplumber
* OCR (if scanned PDFs)

---

## 🧾 Identity & Consistency Auditor Agent

The AI Auditor compares report data with:

* District Student Census JSON
* Official enrollment database

It validates:

* Student existence
* Duplicate identities
* Attendance consistency

---

## 🚨 Fraud Detection Engine

A report is automatically flagged if:

* More than **30%** of students:

  * Do not exist in the census
  * Appear as duplicates
  * Use manipulated identities

### Fraud Indicators

✅ Fake Students
✅ Duplicate Entries
✅ Inflated Attendance
✅ Ghost Schools
✅ Identity Mismatch

---

## 📂 Automated Fraud Escalation

When fraud is detected:

* The suspicious report is moved to:

  ```bash
  /Fraud_Investigation/
  ```

* A high-priority alert is automatically sent to:

  * Auditor General
  * Education Ministry Review Team

---

# 🏗️ System Architecture

```text
            ┌────────────────────┐
            │ Ministry Email Box │
            └─────────┬──────────┘
                      │
                      ▼
        ┌──────────────────────────┐
        │ RPA Email Monitoring Bot │
        └─────────┬────────────────┘
                  │
                  ▼
      ┌─────────────────────────────┐
      │ Attendance PDF Downloader   │
      └─────────┬───────────────────┘
                │
                ▼
     ┌──────────────────────────────┐
     │ PDF Extraction & OCR Engine  │
     └─────────┬────────────────────┘
               │
               ▼
   ┌──────────────────────────────────┐
   │ Identity & Consistency Auditor   │
   └─────────┬────────────────────────┘
             │
             ▼
      ┌───────────────────────┐
      │ Fraud Detection Logic │
      └───────┬───────────────┘
              │
      ┌───────┴────────┐
      ▼                ▼
 Legitimate       Fraud Detected
 Reports             │
                     ▼
       ┌─────────────────────────┐
       │ Fraud Investigation Box │
       └──────────┬──────────────┘
                  ▼
      High Priority Alert System
```

---

# ⚙️ Tech Stack

| Component       | Technology                 |
| --------------- | -------------------------- |
| RPA Workflow    | UiPath / Python Automation |
| Backend         | Python                     |
| PDF Parsing     | pdfplumber, PyPDF2         |
| OCR             | Tesseract OCR              |
| Data Processing | Pandas                     |
| Fraud Logic     | Custom Rule Engine         |
| Database        | JSON / SQLite / PostgreSQL |
| Alerts          | SMTP Email Service         |
| Logging         | Python Logging Module      |

---

# 📂 Project Structure

```bash
Ghost-School-Attendance-Auditor/
│
├── census/
│   └── district_student_census.json
│
├── incoming_reports/
│
├── processed_reports/
│
├── fraud_investigation/
│
├── alerts/
│
├── src/
│   ├── email_monitor.py
│   ├── pdf_extractor.py
│   ├── auditor_agent.py
│   ├── fraud_detector.py
│   ├── alert_system.py
│   └── utils.py
│
├── logs/
│
├── requirements.txt
│
└── README.md
```

---

# 🧪 Fraud Detection Logic

## Detection Rule

```python
if invalid_students_percentage > 30:
    flag_report = True
```

## Validation Steps

* Match names with census
* Detect duplicate names
* Check attendance irregularities
* Verify enrollment authenticity

---

# 📊 Example Workflow

## Input

Monthly Attendance PDF:

```text
School: Sunrise Public School

Students:
- Rahul Das
- Ankit Roy
- Fake Student 1
- Fake Student 2
```

## Census Data

```json
[
  "Rahul Das",
  "Ankit Roy"
]
```

## Output

```text
⚠ FRAUD DETECTED

Reason:
- 50% students absent from census
- Duplicate identity patterns found

Action Taken:
✔ Report moved to Fraud_Investigation
✔ Alert sent to Auditor General
```

---

# 🔒 Security & Auditability

* Every action is logged
* Fraud reasoning is recorded
* Immutable audit trail maintained
* Supports future investigation workflows

---

# 📈 Evaluation Metrics

The project is evaluated on:

| Criteria             | Focus                        |
| -------------------- | ---------------------------- |
| Detection Accuracy   | Correct fraud identification |
| Workflow Reliability | Stable inbox monitoring      |
| Alert Quality        | Actionable fraud summaries   |
| Auditability         | Transparent flagging logic   |

---

# ▶️ How to Run

## 1️⃣ Clone Repository

```bash
git clone https://github.com/your-username/Ghost-School-Attendance-Auditor.git
```

## 2️⃣ Install Dependencies

```bash
pip install -r requirements.txt
```

## 3️⃣ Add Census JSON

Place district census file inside:

```bash
/census/
```

---

## 4️⃣ Configure Email Credentials

Update:

```python
email_monitor.py
```

With:

```python
EMAIL=
PASSWORD=
IMAP_SERVER=
```

---

## 5️⃣ Start the System

```bash
python src/email_monitor.py
```

---

# 🌍 Real-World Impact

This solution helps governments:

* Prevent misuse of public education funds
* Detect fake schools faster
* Reduce corruption
* Improve transparency
* Enable scalable digital governance

---

# 🔮 Future Enhancements

* AI anomaly detection models
* Dashboard for ministry officials
* Geo-verification of schools
* Blockchain audit logs
* Real-time fraud analytics
* Multi-language OCR support

---

# 👨‍💻 Team Vision

Building trustworthy digital governance systems using:

* Automation
* AI-based auditing
* Transparent fraud detection
* Data-driven accountability

---

# 📜 License

This project is developed for educational and governance innovation purposes.

---

# ⭐ Conclusion

The **Ghost School Attendance Auditor** transforms manual education auditing into a scalable, intelligent, and autonomous fraud detection ecosystem capable of protecting public funds and improving governance integrity.
