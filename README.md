# Employee Management System (EMS)

A lightweight, modern, and self-contained web-based **Employee Management System (EMS)** designed for HR teams and team leads to manage personnel, attendance, leaves, payroll, recruitment, and performance reviews with zero external dependencies.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Quick Start](#quick-start)
- [Module Breakdown](#module-breakdown)
- [Customization](#customization)
- [Roadmap & Future Enhancements](#roadmap--future-enhancements)
- [License](#license)

---

## 🌟 Overview

The **Employee Management System** is built as a clean, single-page application (SPA) architecture in pure vanilla web technologies. It provides a comprehensive company dashboard and HR administration suite without requiring complex toolchains, package installations, or build pipelines.

### Highlights:
- **Zero Dependencies**: Pure HTML5, modern CSS3, and ES6+ JavaScript.
- **Instant Setup**: Runs immediately by opening the file in any modern web browser.
- **Adaptive Theming**: Automatically detects and adapts to system light/dark mode preferences (`prefers-color-scheme: dark`) with CSS variables.
- **Responsive Layout**: Seamless transition between desktop sidebar navigation and mobile-optimized horizontal scrolling navigation.

---

## ✨ Key Features

| Module | Description |
| :--- | :--- |
| **📊 Dashboard** | High-level KPI cards (Total headcount, Today's attendance ratio, Pending leave requests, Open applicants) and a recent leave activity table. |
| **👥 Employees** | Searchable directory detailing employee names, departments, designated roles, and employment statuses (Active, On Leave). |
| **⏱️ Attendance** | Daily log tracking employee check-in times, check-out times, and punctuality flags (`On time`, `Late`, `Absent`). |
| **🏖️ Leave Management** | Tracks employee leave requests across categories (Sick leave, Vacation, Personal) with date ranges and approval statuses (`Approved`, `Pending`). |
| **💵 Payroll** | Monthly compensation breakdown summarizing gross pay, deductions, and net payouts for team members. |
| **🎯 Recruitment** | Candidate pipeline and open vacancies tracker featuring stage indicators (`Screening`, `Interviewing`, `Offer sent`) and applicant counts. |
| **⭐ Performance** | Performance appraisal cycle management showing review ratings (`Exceeds`, `Meets`) and assigned reviewers. |
| **📈 Reports** | Pre-configured reporting categories for headcount analytics, attendance rollups, payroll cost breakdowns, and employee turnover. |
| **⚙️ Settings** | Configuration hub for company profiles, roles & permissions, notification preferences, and system audit logs. |

---

## 💻 Tech Stack

- **HTML5**: Semantic document structure with accessibility considerations and mobile viewport meta configuration.
- **CSS3**:
  - CSS Custom Properties (CSS variables) for streamlined theming and dark mode.
  - CSS Grid and Flexbox for fluid, responsive layouts.
  - Safe area inset handling (`env(safe-area-inset-top)`, `env(safe-area-inset-bottom)`) for edge-to-edge mobile screens.
- **JavaScript (ES6+)**:
  - State-driven DOM rendering functions.
  - Dynamic component templating with template literals.
  - Clean separation of mock data models and rendering logic.

---

## 📁 Project Structure

```text
Employee Management system/
├── Employee Management system.html   # Main self-contained application file
└── README.md                         # Project documentation and guide
```

---

## 🚀 Quick Start

### Method 1: Direct File Execution (Easiest)
1. Navigate to the project directory:
   ```text
   d:\AI\Employee Management system\
   ```
2. Double-click `Employee Management system.html` or right-click and choose **Open with > Google Chrome / Microsoft Edge / Mozilla Firefox / Safari**.

### Method 2: Local Static Web Server

If you prefer serving the application over HTTP (useful for testing or network preview):

- **Using Python 3:**
  ```bash
  python -m http.server 8000
  ```
  Open `http://localhost:8000/Employee Management system.html` in your browser.

- **Using Node.js (`npx serve`):**
  ```bash
  npx serve .
  ```

- **Using VS Code Live Server:**
  Open the project folder in VS Code, right-click `Employee Management system.html`, and click **"Open with Live Server"**.

---

## 🔍 Module Breakdown

### 1. Data Models
All sample records are defined in JavaScript arrays within the `<script>` block in `Employee Management system.html`:
- `sections`: Defines active navigation items and IDs.
- `employees`: Array of staff records with attributes `name`, `dept`, `role`, and `status`.
- `attendance`: Daily entry records containing check-in, check-out, and status.
- `leaveRequests`: Requested leaves with types, date ranges, and approval status.
- `payslips`: Financial breakdown showing gross salary, deductions, and net compensation.
- `jobs`: Recruitment job requisitions, candidate count, and hiring stages.
- `reviews`: Performance review cycles and evaluations.

### 2. Status Badge Engine
A centralized `badge(status)` helper maps status strings to color-coded badge classes:
- 🟢 **Green (`.b-green`)**: `Active`, `On time`, `Approved`, `Exceeds`
- 🟡 **Amber (`.b-amber`)**: `On Leave`, `Pending`, `Late`, `Meets`, `Interviewing`, `Screening`
- 🔴 **Red (`.b-red`)**: `Absent`

### 3. Rendering Pipeline
The application uses a lightweight reactive-like rendering pattern:
```javascript
function render(activeSection) {
  // 1. Updates navigation items with active states
  // 2. Renders the corresponding section HTML from the content map
  // 3. Attaches navigation click handlers
}
```

---

## 🎨 Customization

### Changing Theme Colors
You can adjust the CSS custom variables in the `<style>` block to match your company branding:

```css
:root {
  --bg: #f5f7f8;          /* Light slate-tinted background */
  --surface: #ffffff;     /* Crisp white card & table surfaces */
  --surface2: #edf2f4;    /* Secondary surface (headers/hovers) */
  --border: #d8e2e6;      /* Slategrey border strokes */
  --text: #1e2930;        /* Primary typography */
  --text2: #708090;       /* Slategrey secondary typography & labels */
  --accent: #008080;      /* Teal brand accent color */
  --accent-hover: #006666;/* Darker teal button hover */
  --accent-bg: #e6f2f2;   /* Soft teal pill & badge backgrounds */
  --radius: 10px;         /* Corner rounding */
}
```

### Adding a New Section
1. Add an entry to the `sections` array:
   ```javascript
   { id: 'training', label: 'Training' }
   ```
2. Add a corresponding view generator to the `content` dictionary:
   ```javascript
   training: () => `
     <h2>Training & Certifications</h2>
     <div class="sub">Employee development programs</div>
     <!-- HTML content / table -->
   `
   ```

---

## 🗺️ Roadmap & Future Enhancements

- [ ] **Interactive Modals**: Form modals for "+ Add employee" and "+ Request leave".
- [ ] **Live Search & Filter**: Real-time filtering for the employee directory and attendance logs.
- [ ] **Data Persistence**: Integrate `localStorage` or `IndexedDB` to persist changes between sessions.
- [ ] **Backend Integration**: Connect to a REST or GraphQL API backend (Node.js/Express, Python/FastAPI, Go, or Firebase).
- [ ] **Export Options**: Export payroll slips and attendance logs to CSV or printable PDF formats.
- [ ] **User Authentication & Role-Based Access Control (RBAC)**: Distinct permissions for Admin, HR, Manager, and Employee roles.

---

## 📄 License

This project is open-source and available under the [MIT License](https://opensource.org/licenses/MIT). You are free to modify, extend, and use it for commercial and personal projects.
