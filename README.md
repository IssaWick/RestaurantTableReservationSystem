# 🍽️ Restaurant Table Reservation System

A desktop-based **Restaurant Table Reservation System** built with **Java Swing**, following the **MVC (Model-View-Controller)** architecture. The application allows customers to register, log in, and reserve restaurant tables with support for multiple booking types, while administrators can manage tables, customers, and generate PDF reports.

---

## 📋 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Technical Tools & Technologies](#technical-tools--technologies)
- [Project Architecture](#project-architecture)
- [Database Schema](#database-schema)
- [How to Run](#how-to-run)
- [External Libraries](#external-libraries)

---

## 📖 About the Project

This project is a **Java Swing desktop application** designed to streamline the process of reserving tables at a restaurant. It provides separate interfaces for **Customers** and **Administrators**, each with role-specific functionalities. The system manages table availability in real-time, supports multiple reservation types, and generates downloadable PDF reports for administrators.

---

## ✨ Features

### Customer Side
- **User Registration & Login** — Customers can sign up with their personal details (Name, NIC, Email, Contact Number, Password) and log in securely.
- **My Account** — View and update personal profile information.
- **Make a Reservation** — Reserve tables with three booking types:
  - **Single Day Booking** — Reserve a table for a specific date and time slot.
  - **Continuous Booking** — Reserve a table across a continuous range of dates.
  - **Specific Days Booking** — Reserve a table for selected days of the week within a date range.
- **View My Reservations** — View upcoming and past booking details.
- **Cancel Reservation** — Cancel an existing upcoming reservation.
- **View Table Details** — Browse available restaurant tables with seat count and pricing.
- **View Reservation Schedule** — See current reservation schedule to check table availability.

### Administrator Side
- **Customer Management** — View, search, and delete customer records.
- **Table Management** — Add, update, search, and delete restaurant tables (Table ID, Number of Seats, Charges Per Hour).
- **Reservation Management** — View all upcoming and past reservations, add reservations on behalf of customers, and cancel reservations.
- **PDF Report Generation** — Generate and download PDF reports:
  - Daily Reservation Report (filtered by date)
  - Customer Details Report
  - Table Details Report

### UI/UX
- **Animated Splash Screen** — Custom splash screen with gradient curves, progress bar, and loading animation on application startup.
- **Custom UI Components** — Gradient buttons, custom tabbed panes, and shadow-rendered panels for a polished look.

---

## 🛠️ Technical Tools & Technologies

| Category              | Technology / Tool                                                     |
|-----------------------|-----------------------------------------------------------------------|
| **Programming Language** | Java (JDK 20)                                                     |
| **GUI Framework**     | Java Swing (`javax.swing`)                                            |
| **GUI Layout**        | Java AWT (`java.awt`) & Swing GroupLayout                             |
| **IDE**               | Apache NetBeans (NetBeans Project Structure)                          |
| **Build Tool**        | Apache Ant (`build.xml`)                                              |
| **Database**          | SQLite (`ResturantTableReservationSystem.db`)                         |
| **JDBC Driver**       | SQLite JDBC Driver v3.41.0.0 (`sqlite-jdbc-3.41.0.0.jar`)            |
| **PDF Generation**    | iTextPDF v5.5.13 (`itextpdf-5.5.13.jar`)                             |
| **Date Picker**       | LGoodDatePicker v11.2.1 (`LGoodDatePicker-11.2.1.jar`)               |
| **ResultSet to Table**| rs2xml (`rs2xml (1).jar`) — Maps SQL ResultSets to JTable models      |
| **Architecture**      | MVC (Model-View-Controller) Design Pattern                            |
| **Java APIs Used**    | `java.sql`, `java.time` (LocalDate, LocalTime, DayOfWeek), `java.io` |
| **Version Control**   | Git                                                                   |

---

## 🏗️ Project Architecture

The project follows the **MVC (Model-View-Controller)** design pattern:

```
src/
├── Animations/                        # Custom UI animation components
│   ├── ButtonGradient.java            # Gradient-styled button component
│   ├── CurvesPanel.java              # Animated curves background panel
│   ├── GradientPanel.java            # Gradient panel component
│   ├── ProgressBarCustom.java        # Custom progress bar
│   ├── ShadowRenderer.java           # Shadow rendering utility
│   ├── SplashScreen.java             # Animated splash screen on startup
│   ├── TabbedPaneCustom.java         # Custom tabbed pane component
│   └── TabbedPaneCustomUI.java       # Custom tabbed pane UI delegate
│
├── Controller/                        # Business logic & database operations
│   ├── AdministratorController.java   # Admin CRUD operations & report queries
│   ├── CustomerController.java       # Customer auth, CRUD & reservation ops
│   └── ReservationController.java    # Reservation validation & availability checks
│
├── DatabaseConnection/                # Database connectivity
│   └── DBConnection.java             # SQLite JDBC connection manager
│
├── Model/                             # Data model classes (POJOs)
│   ├── Customer.java                  # Customer entity (id, name, NIC, email, contact, password)
│   ├── Reservation.java              # Reservation entity (dates, times, type, table, customer)
│   └── Table.java                     # Table entity (tableID, seats, charges per hour)
│
└── ResturantTableReservationSystem/   # View layer (Swing GUI forms)
    ├── CustomerLogin.java             # Customer login screen (Main Entry Point)
    ├── SignupCustomer.java            # Customer registration form
    ├── CustomerMainMenu.java         # Customer dashboard / main menu
    ├── MyAccount.java                 # Customer profile management
    ├── makeReservation.java           # Customer reservation form
    ├── ViewMyBookingDetails.java     # Customer's reservation history
    ├── AdministratorMainMenu.java    # Administrator dashboard
    ├── CustomerDetails.java          # Admin — customer management view
    ├── TableDetailsView.java         # Admin — table management view
    ├── AddReservation.java           # Admin — add reservation form
    ├── ViewReservationDetails.java   # Admin — all reservations view
    ├── GenerateDailyReservationReport.java  # Admin — PDF report generator
    ├── TableView.java                 # Table availability view
    ├── ReservationView.java          # Reservation schedule view
    └── Images/                        # UI image assets
```

---

## 🗄️ Database Schema

The application uses an **SQLite** database with the following tables:

### `Customer`
| Column      | Type    | Description            |
|-------------|---------|------------------------|
| `cusID`     | INTEGER | Primary Key (Auto)     |
| `Name`      | TEXT    | Customer full name     |
| `NIC`       | TEXT    | National Identity Card |
| `Email`     | TEXT    | Email address          |
| `ContactNO` | TEXT   | Phone number           |
| `Password`  | TEXT    | Account password       |

### `ResturantTables`
| Column           | Type    | Description              |
|------------------|---------|--------------------------|
| `tableID`        | TEXT    | Primary Key              |
| `NoOfSeats`      | INTEGER | Number of seats          |
| `ChargesPerHour` | REAL    | Hourly charge rate       |

### `Reservation`
| Column            | Type    | Description                                       |
|-------------------|---------|---------------------------------------------------|
| `ReservationID`   | INTEGER | Primary Key (Auto)                                |
| `CustomerID`      | INTEGER | Foreign Key → Customer                            |
| `TableID`         | TEXT    | Foreign Key → ResturantTables                     |
| `ReservationType` | TEXT    | Single / Continuous / Specific Days               |
| `StartDate`       | TEXT    | Reservation start date                            |
| `StartTime`       | TEXT    | Reservation start time                            |
| `EndTime`         | TEXT    | Reservation end time                              |
| `EndDate`         | TEXT    | Reservation end date                              |
| `ReservationDate` | TEXT    | Date the reservation was made                     |

---

## 🚀 How to Run

### Prerequisites
- **Java JDK 20** or later installed
- **Apache NetBeans IDE** (recommended) or any Java IDE

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/IssaWick/RestaurantTableReservationSystem.git
   ```

2. **Open in NetBeans**
   - Open NetBeans → `File` → `Open Project` → Select the project folder.

3. **Update the database path**
   - Open `src/DatabaseConnection/DBConnection.java`
   - Update the `url` variable to point to the `ResturantTableReservationSystem.db` file on your system.

4. **Ensure libraries are added**
   - The following JAR files must be in the project classpath:
     - `sqlite-jdbc-3.41.0.0.jar`
     - `itextpdf-5.5.13.jar`
     - `LGoodDatePicker-11.2.1.jar`
     - `rs2xml (1).jar`

5. **Run the application**
   - Right-click the project → `Run`, or press `F6`.
   - The application starts with the **Customer Login** screen.

---

## 📦 External Libraries

| Library                          | Version  | Purpose                                                |
|----------------------------------|----------|--------------------------------------------------------|
| **SQLite JDBC**                  | 3.41.0.0 | JDBC driver for SQLite database connectivity           |
| **iTextPDF**                     | 5.5.13   | PDF document generation for reports and booking slips  |
| **LGoodDatePicker**             | 11.2.1   | Swing-based date picker component for date selection   |
| **rs2xml**                       | —        | Converts SQL `ResultSet` into `JTable` `TableModel`   |
| **AbsoluteLayout** (NetBeans)    | —        | NetBeans layout library for form-based GUI design      |

---

> **Note:** This project was developed as an academic project (AS2022432) demonstrating practical application of Java desktop development, MVC architecture, database management with SQLite, and PDF report generation using iTextPDF.
