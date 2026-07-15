# Clinic Management System

## Overview
A Python application for managing patients and their medical records at a clinic, built incrementally from a domain model and unit tests up through a persistent, DAO-backed backend and finally a full PyQt graphical user interface.

The system supports two core entities:
- **Patients** — identified by Personal Health Number (PHN), with name, birth date, phone, email, and address.
- **Patient Records** — each patient has a record containing a collection of **Notes**, timestamped and identified by an auto-incremented code.

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
| 9 | Choose current patient | Set/unset the active patient by PHN for modifying patient record.
| 10 |
| 11 |
| 12 |
| 13 |
| 14 |
