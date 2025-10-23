This repository, `beta-org-for-pustak/College-ERP`, presents a Django-based college management system designed to facilitate interactions between students and teachers, with a focus on academic administration.

---

## 1. Project Purpose and Goals

The primary purpose of the College-ERP system is to provide a comprehensive management solution for academic institutions. Its main goal is to streamline and automate core administrative tasks related to student and teacher interactions, specifically focusing on attendance tracking, marks management, and timetable display. It aims to offer dedicated interfaces for both student and teacher roles, backed by a robust administrative panel for system configuration and data management.

## 2. Key Features

The College-ERP system offers the following key functionalities:

*   **User Management & Roles:**
    *   Support for multiple user roles: Students, Teachers, and System Administrators.
    *   Default login credentials provided for easy testing (e.g., `samarth` for student, `trisila` for teacher, `admin` for administrator, all with password `project123`).
    *   Ability to create new student and teacher accounts via the Django admin panel.
    *   Admins can create new superusers using `python manage.py createsuperuser`.
*   **Core Academic Management:**
    *   **Attendance:** Teachers can record and manage student attendance. Students can view their attendance records.
    *   **Marks:** Teachers can add and view student marks. Students can view their academic marks.
    *   **Timetable:** Functionality for managing and displaying class timetables (implied by description).
*   **Administrative Control:**
    *   Comprehensive Django Admin interface accessible at `/admin`.
    *   Admins have full control to modify and manage all core college entities, including Students, Teachers, Departments, Courses, and Classes.
    *   Specialized feature to reset attendance data: An "Attendance Range" tool in the Django Admin allows administrators to define a new attendance period (Start Date, End Date). This action deletes all existing attendance data and generates new attendance objects for the specified range, providing a way to manage academic terms or semesters.
*   **User Interfaces:**
    *   Separate dashboards and functionalities tailored for Teacher and Student users.
    *   Screenshots showcase interfaces for teachers to view attendance, add marks, and view marks, suggesting a web-based user experience. (Note: Student page screenshot link was truncated).
*   **API Capabilities (Potential):**
    *   The presence of `serializers.py` in the `apis` app suggests that the system might expose RESTful API endpoints, allowing for integration with other systems or a decoupled frontend.

## 3. Technology Stack

*   **Framework:** Django (Python Web Framework)
*   **Programming Language:** Python
*   **Database:** Django's default ORM and database support (typically SQLite for development, configurable for production databases like PostgreSQL, MySQL, etc.)
*   **Frontend:** Standard Django templating (implied), no specific modern JavaScript framework is mentioned.
*   **API Layer:** Potentially Django REST Framework, inferred from `serializers.py` within an `apis` application.

## 4. Getting Started Guide

To get the College-ERP system up and running, follow these steps:

1.  **Prerequisites:**
    *   Ensure Python is installed on your system.
    *   Install Django:
        ```bash
        pip install django
        ```
2.  **Clone the Repository:**
    *   (Assumed step, as the prompt only provided file paths, not clone instructions. In a real scenario, this would be `git clone <repo_url>`).
3.  **Navigate to Project Directory:**
    *   Change your current directory to the `College-ERP` folder (the one containing `manage.py`).
4.  **Run the Server:**
    *   Start the Django development server:
        ```bash
        python manage.py runserver
        ```
5.  **Access the Application:**
    *   Open your web browser and navigate to:
        `http://127.0.0.1:8000/`
6.  **Login Information:**
    *   **Student/Teacher Login:**
        *   URL: `http://127.0.0.1:8000/` (main page)
        *   Example Usernames: `samarth` (student), `trisila` (teacher)
        *   Password for everyone: `project123`
    *   **Admin Login:**
        *   URL: `http://127.0.0.1:8000/admin`
        *   Username: `admin`
        *   Password: `project123`
    *   **Create a New Admin User (Optional):**
        *   If the default `admin` user doesn't exist or you want a new one, stop the server and run:
            ```bash
            python manage.py createsuperuser
            ```
            Follow the prompts to create a new superuser.
7.  **Managing Users and Data:**
    *   Log in to the Django admin page (`/admin`) to add new students, teachers, departments, courses, classes, and manage other system data.

*(Note: Typically, after cloning a Django project, you would also run `python manage.py migrate` to apply database migrations, especially if it's the first time setting up the project or if new migrations have been added. The README does not explicitly state this, but it's a standard Django setup step.)*

## 5. Project Structure Overview

The repository follows a typical Django project structure, consisting of a main project configuration and multiple Django applications.

```
College-ERP/                    # Main project root directory
├── CollegeERP/                 # Main Django project configuration
│   ├── __init__.py
│   ├── settings.py             # Project settings (database, installed apps, etc.)
│   ├── urls.py                 # Main URL routing for the project
│   └── wsgi.py                 # WSGI configuration for deployment
│
├── apis/                       # Django Application: Likely handles API endpoints
│   ├── migrations/             # Database migration files for the 'apis' app
│   │   └── __init__.py
│   ├── __init__.py
│   ├── admin.py                # Admin interface customization for 'apis' models
│   ├── apps.py                 # Application configuration
│   ├── models.py               # Database models for the 'apis' app
│   ├── serializers.py          # Django REST Framework serializers (suggests API functionality)
│   ├── tests.py                # Unit tests for the 'apis' app
│   ├── urls.py                 # URL routing for the 'apis' app
│   └── views.py                # View functions/classes for the 'apis' app
│
├── info/                       # Django Application: Core data models for college entities
│   ├── migrations/             # Extensive database migration files for the 'info' app
│   │   ├── 0001_initial.py
│   │   ├── ... (many migration files, indicating complex data structure evolution)
│   │   └── 0016_auto_20210820_1553.py
│   ├── __init__.py
│   ├── admin.py                # Admin interface customization for 'info' models
│   ├── apps.py                 # Application configuration (implied, common for Django apps)
│   ├── models.py               # Database models for students, teachers, courses, attendance, etc.
│   ├── urls.py                 # URL routing for the 'info' app (implied)
│   └── views.py                # View functions/classes for the 'info' app (implied)
│
└── manage.py                   # Django's command-line utility
```

The `CollegeERP` directory contains the main project-level settings and URL configurations. The system leverages at least two distinct Django applications: `apis` (potentially for REST APIs) and `info` (likely housing the core models for students, teachers, courses, attendance, and other college-specific data, given its numerous migration files and reference in the admin URL).