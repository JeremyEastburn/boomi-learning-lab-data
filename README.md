# Boomi Learning Lab - Mock Data Repository

## Overview
This repository contains mock Higher Education data files for the Boomi Platform Learning Lab. The data simulates a university's integrated systems including Student Information System (SIS), Learning Management System (LMS), HR, Finance, and academic planning systems.

## Repository Structure

```
boomi-learning-lab-data/
├── module1-integration/
│   ├── sis-students.csv              # 50 student records with academic info
│   ├── lms-enrollments.xml           # 200+ course enrollment records
│   ├── hr-faculty.xml                # 30 faculty members with teaching assignments
│   └── finance-billing.csv           # 50 student financial records
│
├── module3-hub/
│   ├── students-dirty-data.csv       # 20 records with data quality issues
│   └── duplicate-records.csv         # 15 duplicate student scenarios
│
├── module4-agentstudio/
│   ├── course-catalog.xml            # 40 courses with details
│   ├── degree-requirements.xml       # 10 degree program requirements
│   ├── course-prerequisites.csv      # 40 prerequisite relationships
│   └── advisor-assignments.csv       # 50 student-advisor pairings
│
└── module5-flow/
    ├── university-majors.xml         # 20 available majors
    └── new-applications.xml          # Application template & sample
```

## Data Interconnections

### Key Relationships
- **Student IDs (10000001-10000050)**: Connect students across SIS, enrollments, billing, and advisor assignments
- **Course IDs (DEPT###-LEVEL)**: Link faculty teaching assignments, enrollments, prerequisites, and degree requirements
- **Faculty IDs (F001-F030)**: Connect faculty records to course instruction
- **Department Codes**: Consistent across faculty, courses, majors, and degree programs

### Data Flow Through Modules

#### Module 1 → Module 2
- Raw CSV/XML files are retrieved via Integration processes
- Integration transforms data to JSON
- APIM wraps Integration processes to expose REST APIs

#### Module 2 → Module 3
- APIM endpoints provide clean, standardized data to Hub
- Hub creates master records from APIM-exposed data
- Dirty/duplicate data handled separately for data quality learning

#### Module 3 → Module 4
- Hub provides clean master data for AgentStudio
- Agent uses both Hub data and additional APIM endpoints
- Academic rules inform intelligent advising capabilities

#### Module 4 → Module 5
- Flow interfaces consume data through Integration processes
- Integration processes call APIM endpoints
- New applications posted back through the same pattern

## APIM Endpoint Mapping

| Source File | APIM Endpoint | Description |
|------------|---------------|-------------|
| sis-students.csv | GET /api/students | Student records |
| lms-enrollments.xml | GET /api/enrollments | Course enrollments |
| hr-faculty.xml | GET /api/faculty | Faculty information |
| finance-billing.csv | GET /api/billing | Financial records |
| course-catalog.xml | GET /api/courses | Course offerings |
| degree-requirements.xml | GET /api/requirements | Degree requirements |
| course-prerequisites.csv | GET /api/prerequisites | Course prerequisites |
| advisor-assignments.csv | GET /api/advisors | Advisor assignments |
| university-majors.xml | GET /api/majors | Available majors |
| new-applications.xml | POST /api/applications | Application submission |

## Data Statistics

- **Total Students**: 50 (+ 20 dirty + 15 duplicates)
- **Total Faculty**: 30
- **Total Courses**: 40
- **Total Enrollments**: 200+
- **Departments**: 30+
- **Degree Programs**: 10
- **Majors Available**: 20
- **Semesters Covered**: Fall 2021 - Spring 2025

## Data Consistency Rules

- All dates use ISO format (YYYY-MM-DD) in clean data
- Student IDs are 8-digit numbers starting with 10000001
- Course IDs follow pattern: DEPT###-LEVEL (e.g., CS101-100)
- Faculty IDs use format: F### (e.g., F001)
- GPA range: 0.0-4.0 (except in dirty data)
- Credits are integers (except in dirty data)

## Notes for Instructors

- Data is intentionally inconsistent between modules to teach transformation
- Prerequisite chains are realistic but simplified for learning
- Financial data is simplified (no complex fee structures)
- All PII is fictional and generated for educational purposes

## License
This mock data is provided for educational purposes as part of the Boomi Learning Lab project.
