# ineza_28527_runwayTrack
# Kigali Smart Airport — Runway Slot Scheduling and Conflict Prevention System

**Student Name:** Ineza Lisa Gabrielle  
**Student ID:** 28278  
**Course:** INSY 8311 · Database Development with PL/SQL  
**Instructor:** Eric Maniraguha  
**Institution:** Adventist University of Central Africa (AUCA)  

---

## 1. Project Title
**Kigali Smart Airport — Runway Slot Scheduling and Conflict Prevention System**

---

## 2. Problem Statement
Small and mid-sized international airports such as Kigali International Airport operate under high-density constraints, where multiple aircraft arrival and departure requests frequently cluster around peak traffic hours. Managing runway slots and gate allocations across disconnected spreadsheets or manual logs leads to scheduling conflicts, buffer time violations, and increased fuel burn due to unnecessary low-altitude holding patterns. Manual record-keeping also lacks automated validation for mandatory wake-turbulence separation intervals between different aircraft types (e.g., Heavy vs. Medium jets).

---

## 3. Objectives
- **Main Objective:** Develop a centralized Oracle PL/SQL database system that automates runway slot allocations and prevents double-booking conflicts in real time.
- **Specific Objectives:**
  1. Design a normalized 3NF schema to store runway availability, aircraft wake-turbulence classifications, master flight schedules, slot requests, and system audit logs.
  2. Implement PL/SQL database triggers and package procedures to enforce mandatory wake-turbulence separation buffers and block overlapping slot allocations.
  3. Build an interactive Streamlit (or APEX) user interface connected live to the Oracle database to allow air traffic controllers to manage slots and view conflict alerts.

---

## 4. Data Source
- **Dataset:** [Kaggle US Flights & Airport Operations Dataset 2024](https://www.kaggle.com/datasets/olegbogomolov/us-flights-dataset-2024-raw-data) / [Airport Operations Multi-Table Dataset](https://www.kaggle.com/datasets/sinanshereef/airport-operations-multi-table-dataset).
- **Description:** Contains flight numbers, ICAO aircraft model codes, origin/destination hubs, scheduled and actual departure/arrival timestamps, assigned gate IDs, and runway slot allocations.

---

## 5. Innovation Layer
**User Interface Layer (Python Streamlit connected directly to Oracle via `python-oracledb`):**
An interactive controller dashboard that visualizes live runway timelines, processes slot requests via PL/SQL procedures, and displays real-time conflict and audit log alerts.

---

## 6. Planned Database Tables & PL/SQL Features

### Database Schema (3NF)
- `AIRPORTS_RUNWAYS`: Stores runway physical parameters, operational statuses, and category limits.
- `AIRCRAFT_TYPES`: Stores aircraft wake turbulence categories (Heavy/Medium/Light) and minimum separation requirements.
- `FLIGHT_SCHEDULES`: Master registry holding flight arrival and departure requests.
- `RUNWAY_SLOTS`: Stores assigned time windows for runway access, clearance states, and slot flags.
- `SLOT_AUDIT_LOGS`: Audit trail logging manual overrides, slot reallocations, and blocked conflict attempts.

### Planned PL/SQL Features
- **Package (`pkg_runway_mgmt`):** Encapsulates core procedures (`assign_slot`, `reconcile_flight_delays`).
- **Functions:** `fn_check_slot_conflict` (returns BOOLEAN), `fn_calculate_wake_buffer` (returns separation minutes).
- **Triggers:** `trg_prevent_double_booking` (BEFORE INSERT/UPDATE ON `RUNWAY_SLOTS`), `trg_enforce_wake_separation`, `trg_audit_slot_changes` (AFTER INSERT/UPDATE/DELETE).
- **Cursors & Exceptions:** Explicit cursors for batch slot allocation; custom user exceptions (`e_slot_conflict`, `e_insufficient_separation`).

---

## 7. Folder Structure
```text
.
├── README.md
├── data/
│   └── raw_flights_dataset.csv
├── docs/
│   ├── proposal/
│   │   └── Phase0_Proposal_Ineza_28278.pdf
│   ├── research/
│   │   └── research_log.md
│   └── presentation/
│       └── Phase0_Presentation_Ineza_28278.pptx
└── sql/
    ├── 01_schema.sql
    └── 02_plsql_packages.sql
