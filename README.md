# 🪪 Diving Center Management Pro & AI Automated Workflow

> A multi-tenant SaaS-style web application for diving center management, featuring real-time client ID/passport scanning powered by **n8n and AI**, secure role-based access control, daily operations tracking, and executive analytics.

---

## 🏗️ System Architecture & Tech Stack

This project integrates frontend web technologies, serverless logic, workflow automation, and cloud spreadsheets into a unified architecture:

```
[ Frontend (HTML5, Vanilla JS, Tailwind/CSS, Chart.js) ]
            │
            ├────── (REST GET/POST) ──────► [ Google Apps Script (Backend & API Router) ] ──────► [ Google Sheets Database ]
            │
            └────── (Multipart Form) ─────► [ n8n Workflow Automation Webhook ] ──► [ AI Model (Vision/OCR) ] ──► [ Google Sheets ]

```

* **Frontend:** HTML5, CSS3, JavaScript (ES6+), Chart.js (for executive analytics), XLSX (for CSV exports), Crypto-JS (for secure client-side SHA-256 password hashing).
* **Backend & API:** Google Apps Script (`doGet` / `doPost`), handling multi-tenant isolation, user authentication, company registration, booking management, and status updates.
* **Workflow Automation & AI Engine:** **n8n** automation platform handling webhook requests, processing passport/ID uploads, and extracting structured client data via AI vision/OCR.
* **Database & Storage:** Google Sheets (partitioned by unique company IDs for secure data multi-tenancy).

---

## 🚀 Project Components

### 1. Frontend Dashboard (`index_8.html`)

* **Authentication Overlay:** Secure multi-tenant login system supporting role-based dashboards (`Manager` and `Sales`) with SHA-256 password encryption.
* **Company Registration:** Dynamic self-service registration form allowing new diving centers to provision isolated company accounts (`Company ID`, Manager & Sales credentials).
* **Daily Operations Tab:** Manages real-time customer bookings, automated voucher generation, client ID lookup, and live activity filtering.
* **ID & Licenses Tab:** Document management interface with drag-and-drop file upload capabilities for passports and identification cards.
* **Executive Analytics Tab:** Manager-exclusive dashboard featuring real-time KPI metric cards and interactive charts built with **Chart.js** (Weekly Client Acquisition, Activity Popularity, and Payment Collection status).

### 2. Google Apps Script Backend (`script_7.py` / `Code.gs`)

* **`doGet(e)`:** Handles secure data retrieval with strict row-level filtering based on `companyID`. Automatically provisions the `Users` database table with default secure admin accounts on first initialization.
* **`doPost(e)`:** Processes state-changing requests using concurrency locks (`LockService`) to prevent race conditions. Handles company registration payloads, creates new booking rows in `Sheet2` with a default `Pending` status, and updates booking approval statuses (`Accepted` / `Cancelled`).

### 3. n8n Automation Workflow (`n8n Webhook Pipeline`)

* **Webhook Trigger:** Receives POST requests containing uploaded passport or ID documents from the frontend interface.
* **AI Processing Node:** Analyzes document visuals/text to extract standardized client records (Full Name, ID Number, Issuing Authority/Nationality).
* **Data Sink:** Automatically appends structured results into the designated Google Sheets data storage.

---

## 🔒 Security & Multi-Tenancy Features

* **Data Isolation:** Every read and write query enforces strict `companyID` filtering, ensuring complete data privacy between different diving center organizations.
* **Password Hashing:** Client passwords are cryptographically hashed using **SHA-256** via Crypto-JS before transmission and database comparison.
* **Role-Based Access Control (RBAC):**
* *Sales Role:* Handles bookings, views client directories, and registers daily operations.
* *Manager Role:* Accesses Executive Analytics, reviews/approves pending bookings, and oversees company records.



---

## 📊 Available API Endpoints & Actions

| Method | Target Sheet / Action | Description |
| --- | --- | --- |
| **GET** | `?sheet=Users` | Retrieves authentication and user credential records. |
| **GET** | `?sheet=الورقة1&companyID=XXX` | Fetches registered client documents filtered by company ID. |
| **GET** | `?sheet=Sheet2&companyID=XXX` | Fetches daily booking entries filtered by company ID. |
| **POST** | `action: "registerCompany"` | Provisions a new company workspace along with Manager and Sales credentials. |
| **POST** | `voucherNo` / New Booking | Creates a new booking entry with `Pending` status. |
| **POST** | `action: "updateStatus"` | Updates booking status (`Accepted` or `Cancelled`) by voucher number (Manager privilege). |# 🪪 Diving Center Management Pro & AI Automated Workflow

> A multi-tenant SaaS-style web application for diving center management, featuring real-time client ID/passport scanning powered by **n8n and AI**, secure role-based access control, daily operations tracking, and executive analytics.

---

## 🏗️ System Architecture & Tech Stack

This project integrates frontend web technologies, serverless logic, workflow automation, and cloud spreadsheets into a unified architecture:

```
[ Frontend (HTML5, Vanilla JS, Tailwind/CSS, Chart.js) ]
            │
            ├────── (REST GET/POST) ──────► [ Google Apps Script (Backend & API Router) ] ──────► [ Google Sheets Database ]
            │
            └────── (Multipart Form) ─────► [ n8n Workflow Automation Webhook ] ──► [ AI Model (Vision/OCR) ] ──► [ Google Sheets ]

```

* **Frontend:** HTML5, CSS3, JavaScript (ES6+), Chart.js (for executive analytics), XLSX (for CSV exports), Crypto-JS (for secure client-side SHA-256 password hashing).
* **Backend & API:** Google Apps Script (`doGet` / `doPost`), handling multi-tenant isolation, user authentication, company registration, booking management, and status updates.
* **Workflow Automation & AI Engine:** **n8n** automation platform handling webhook requests, processing passport/ID uploads, and extracting structured client data via AI vision/OCR.
* **Database & Storage:** Google Sheets (partitioned by unique company IDs for secure data multi-tenancy).

---

## 🚀 Project Components

### 1. Frontend Dashboard (`index_8.html`)

* **Authentication Overlay:** Secure multi-tenant login system supporting role-based dashboards (`Manager` and `Sales`) with SHA-256 password encryption.
* **Company Registration:** Dynamic self-service registration form allowing new diving centers to provision isolated company accounts (`Company ID`, Manager & Sales credentials).
* **Daily Operations Tab:** Manages real-time customer bookings, automated voucher generation, client ID lookup, and live activity filtering.
* **ID & Licenses Tab:** Document management interface with drag-and-drop file upload capabilities for passports and identification cards.
* **Executive Analytics Tab:** Manager-exclusive dashboard featuring real-time KPI metric cards and interactive charts built with **Chart.js** (Weekly Client Acquisition, Activity Popularity, and Payment Collection status).

### 2. Google Apps Script Backend (`script_7.py` / `Code.gs`)

* **`doGet(e)`:** Handles secure data retrieval with strict row-level filtering based on `companyID`. Automatically provisions the `Users` database table with default secure admin accounts on first initialization.
* **`doPost(e)`:** Processes state-changing requests using concurrency locks (`LockService`) to prevent race conditions. Handles company registration payloads, creates new booking rows in `Sheet2` with a default `Pending` status, and updates booking approval statuses (`Accepted` / `Cancelled`).

### 3. n8n Automation Workflow (`n8n Webhook Pipeline`)

* **Webhook Trigger:** Receives POST requests containing uploaded passport or ID documents from the frontend interface.
* **AI Processing Node:** Analyzes document visuals/text to extract standardized client records (Full Name, ID Number, Issuing Authority/Nationality).
* **Data Sink:** Automatically appends structured results into the designated Google Sheets data storage.

---

## 🔒 Security & Multi-Tenancy Features

* **Data Isolation:** Every read and write query enforces strict `companyID` filtering, ensuring complete data privacy between different diving center organizations.
* **Password Hashing:** Client passwords are cryptographically hashed using **SHA-256** via Crypto-JS before transmission and database comparison.
* **Role-Based Access Control (RBAC):**
* *Sales Role:* Handles bookings, views client directories, and registers daily operations.
* *Manager Role:* Accesses Executive Analytics, reviews/approves pending bookings, and oversees company records.



---

## 📊 Available API Endpoints & Actions

| Method | Target Sheet / Action | Description |
| --- | --- | --- |
| **GET** | `?sheet=Users` | Retrieves authentication and user credential records. |
| **GET** | `?sheet=الورقة1&companyID=XXX` | Fetches registered client documents filtered by company ID. |
| **GET** | `?sheet=Sheet2&companyID=XXX` | Fetches daily booking entries filtered by company ID. |
| **POST** | `action: "registerCompany"` | Provisions a new company workspace along with Manager and Sales credentials. |
| **POST** | `voucherNo` / New Booking | Creates a new booking entry with `Pending` status. |
<<<<<<< HEAD
| **POST** | `action: "updateStatus"` | Updates booking status (`Accepted` or `Cancelled`) by voucher number (Manager privilege). |
=======
| **POST** | `action: "updateStatus"` | Updates booking status (`Accepted` or `Cancelled`) by voucher number (Manager privilege). |

>>>>>>> f94d8a6 (Add Supplier management feature and multi-tenancy support)
