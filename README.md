# Clinic Management System

## Overview
A Python application for managing patients and their medical records at a clinic, built incrementally from a domain model and unit tests up through a persistent, DAO-backed backend and finally a full PyQt graphical user interface.

The system supports three core classes:
- **Patients** — identified by Personal Health Number (PHN), with name, birth date, phone, email, and address.
- **Patient Records** — each patient has a record containing a collection of **Notes**.
- **Notes** —  individual entries in a patient record, identified by an auto-incremented code, with text content and a timestamp marking creation or last update.

## User Stories
| User Story | Title | Description |
| --- | --- | --- |
| 1 | Log in | Authenticate with a username and password. |
| 2 | Log out | End the current session. |
| 3 | Search patient | Find a patient by PHN. |
| 4 | Create new patient | Register a new patient with PHN, name, and personal data. |
| 5 | Retrieve existing patients | Search patients by (partial) name match. |
| 6 | Update existing patient | Find a patient by PHN and update their data. |
| 7 | Delete existing patient | Find a patient by PHN and remove them. |
| 8 | List all patients | Retrieve the full patient list. |
| 9 | Choose current patient | Set/unset the active patient by PHN for modifying patient record. |
| 10 | Create new note | Add a note to the current patient's record with an auto-incremented code and timestamp. |
| 11 | Retrieve existing notes | Search the current patient's notes by code. |
| 12 | Update existing note | Find a note by code and update its text. |
| 13 | Delete existing note | Find a note by code and remove it. |
| 14 | List the full patient record | List all notes for the current patient, most recent first. |

## Architecture
- Exception Handling — `Controller` raises custom exceptions (from `clinic/exception`) instead of returning `None`/`False` on invalid operations.
- DAO Layer — Collections were moved out of `Controller` and `PatientRecord` into `PatientDAOJSON` and `NoteDAOPickle`, which own their collections and CRUD logic, keeping persistence tech swappable.
- Persistence — Controlled by an autosave flag; patients load/save from `patients.json`, notes load/save per-patient from binary `.dat` files in `records/`, and users load from `users.txt`.
- Encoding — Patients are serialized to/from JSON via custom `PatientEncoder`/`PatientDecoder` classes; notes are serialized via `pickle`.
- Password Hashes — Usernames and password hashes are loaded from `users.txt`; passwords are never stored or compared in plaintext.
- User Interfaces — A CLI (`clinic/cli`) served as a reference for interacting with Controller, followed by a PyQt GUI (`clinic/gui`) implementing all user stories, with patient lists in `QTableView` and note/record views in `QPlainTextEdit`.


## Running the Application
From the project's root directory
```
# Command-line interface
python3 -m clinic cli

# Graphical interface
python3 -m clinic gui

# Sample login credentials:
# Username: user
# Password: 123456
```

Sample interface:

<img width="621" height="441" alt="Screenshot 2026-07-15 at 5 11 19 PM" src="https://github.com/user-attachments/assets/4907d534-dc6f-45a8-b266-b4c2e088ae00" />
<img width="614" height="446" alt="Screenshot 2026-07-15 at 5 11 57 PM" src="https://github.com/user-attachments/assets/7b493e6e-78c3-4354-b5ba-91c10991ea77" />


## Running tests
```
# Unit tests
python3 -m unittest tests/patient_test.py tests/patient_record_test.py tests/note_test.py

# Integration tests (in-memory, autosave=False)
python3 -m unittest integration_test.py
```
