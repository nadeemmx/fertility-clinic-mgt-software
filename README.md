<div align="center">

# 🩺 AURA IVF

### Reproductive Medicine & Assisted Conception Clinical Operating System

[![License: MIT](https://img.shields.io/badge/License-MIT-000000.svg?style=for-the-badge)](LICENSE)
[![PHP](https://img.shields.io/badge/PHP-8.2%2B-000000.svg?style=for-the-badge&logo=php)](https://php.net)
[![Framework](https://img.shields.io/badge/Framework-Laravel%2011-000000.svg?style=for-the-badge&logo=laravel)](https://laravel.com)
[![UI System](https://img.shields.io/badge/UI-100%25%20Monochrome%20Light-000000.svg?style=for-the-badge)](#-design-system--clinical-ui)

</div>

<p align="center">
  <strong>AURA IVF – Portfolio Edition</strong><br>
  A full-stack Laravel clinical management platform demonstrating enterprise-grade web application architecture, RBAC, and patient lifecycle management.
</p>

<p align="center">
  Key Features • RBAC Roles • Installation Guide • Public Edition vs Private Edition • License
</p>

<br>

## 📖 Overview

**AURA IVF Portfolio Edition** is a functionally operational, recruiter-friendly subset of the complete AURA IVF Clinical Operating System. This edition demonstrates full-stack engineering capabilities including Laravel backend architecture, Blade + Tailwind frontend implementation, role-based access control, and complete patient lifecycle management from initial inquiry through pediatric follow-up.

The public edition includes core clinical modules accessible to all authenticated users, with representative frontend components and backend implementation that showcase actual engineering work while intentionally excluding proprietary clinical modules and sensitive patient data.

---

## 🏛 Public Edition vs Private Edition

| Aspect | Public Edition (Portfolio) | Private Edition (Full) |
| :--- | :--- | :--- |
| **Purpose** | Recruiter portfolio – demonstrates engineering capabilities | Complete development repository – full clinical system |
| **Visibility** | PUBLIC on GitHub | PRIVATE on GitHub |
| **Features Included** | Core modules: Overview, Leads, Couples (basic), Cycles, Laboratory, Transfers, Failures, Overview dashboards | All 12 modules including: Antenatal Care, Deliveries, Pediatrics & Vaccinations, Cryobank, Full Settings & RBAC |
| **Authentication** | Demo accounts with sanitized credentials | Full authentication with configurable credentials |
| **Patient Data** | Anonymized/structure-focused records only | Realistic clinical patient trajectories with full demographics |
| **Clinical Features** | Core CRUD operations, metrics, and workflows | Complete embryology lab, cryobank, antenatal, delivery, and vaccination pipelines |
| **RBAC** | 3 core roles with limited tab access | 7 roles with full 12-module tab permissions |
| **Database Seeder** | Simplified seed data without PHI | Full seed data with 3 complete patient journeys |
| **Configuration** | Generic clinic settings | Clinic-specific ART registry, facility baselines, director profiles |
| **API Endpoints** | Core resource endpoints | Full endpoint suite including file uploads and specialized operations |

**Clearly documented: Features available in the public edition are intentionally functional and recruiter-accessible. Features excluded from the public edition are preserved in the private repository for continued development.**

---

## 🔐 Clinical Role-Based Access Control (Public Edition)

The public edition includes 3 core roles with restricted module access:

| Clinical Role | Accessible Modules |
| :--- | :--- |
| **Super Admin / Medical Director** | Overview, Leads, Couples (basic), Cycles, Transfers, Failures |
| **Senior Reproductive Endocrinologist** | Overview, Leads, Couples, Cycles, Transfers, Failures, Laboratory |
| **Clinic Receptionist / CRM** | Overview, Leads, Couples (basic) |

**Note:** Role-based tab permissions (`canAccessTab()`) are implemented in the `User` model and gate access to the 12 clinical workstation tabs. The public edition demonstrates the RBAC architecture with a reduced role set suitable for portfolio demonstration.

---

## 🎨 Design System & Clinical UI

* **100% Monochrome Light Theme:** High-contrast pure white (`#ffffff`) background with deep black (`#000000`) typography and crisp 1px solid borders – optimized for embryology suite visibility
* **Zero Color Distractions:** Designed to eliminate color fatigue in clinical environments
* **Regional Clinical Localization:** Pre-configured with India (`+91`) mobile phone inputs and ISO date formatting (`YYYY-MM-DD`)

**The monochrome light theme is a deliberate design choice for the target clinical demographic and demonstrates modern frontend architecture with Tailwind CSS v4 and reusable Blade components.**

---

## 🚀 Quickstart & Installation (Public Edition)

### Prerequisites

* **PHP:** >= 8.2 (Extensions: `pdo_mysql`, `mbstring`, `openssl`, `tokenizer`, `xml`, `ctype`, `json`, `bcmath`)
* **Composer:** >= 2.x
* **Database:** MySQL >= 8.0, MariaDB >= 10.4, or SQLite
* **Web Server:** Apache (XAMPP / MAMP), Nginx, or built-in PHP server
* **Node.js:** >= 18 (for Vite build development)

### 1. Clone the Repository

```bash
git clone https://github.com/nadeemmx/fertility-clinic-mgt-software.git
cd fertility-clinic-mgt-software
```

### 2. Install Dependencies

```bash
composer install --no-dev --optimize-autoloader
npm install
npm run build
```

### 3. Configure Environment

```bash
cp .env.example .env
php artisan key:generate
```

Configure your database credentials in `.env`:

```env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=ivf_public
DB_USERNAME=root
DB_PASSWORD=
```

**Important:** The public edition uses a simplified database configuration. See the "Database Setup" section below.

### 4. Run Migrations

```bash
php artisan migrate
```

The public edition migrations create the core tables: `users`, `cache`, `cache_locks`, `sessions`, `leads`, `patients`, `couples`, `ivf_cycles`, `follicular_scans`, `opu_and_lab_records`, `embryo_transfers`, `cycle_outcomes`.

### 5. Launch Workstation

```bash
php artisan serve
```

Open your browser and navigate to: `http://127.0.0.1:8000` (or `http://localhost:8000`).

**Login Credentials (Demo):**

| Clinical Role | Username / Email | Password |
| :--- | :--- | :--- |
| **Super Admin / Medical Director** | `admin@aura-ivf.com` | *generated during setup* |
| **Senior Reproductive Endocrinologist** | `endo@aura-ivf.com` | *generated during setup* |

*The seeder initializes demo accounts with generated passwords. Passwords are set during the `php artisan key:generate` and migration process.*

---

## 📁 Public Edition Project Structure

```
fertility-clinic-mgt-software/
├── app/
│   ├── Http/Controllers/
│   │   ├── AuthController.php      # Sign-in, session guards & logout
│   │   └── Controller.php          # Base controller
│   └── Models/
│       └── User.php                # Eloquent entity with RBAC canAccessTab()
├── database/
│   ├── migrations/                 # Core relational schema (8 essential migrations)
│   └── seeders/                    # Simplified seed data (no PHI)
├── resources/
│   └── views/ivf/
│       ├── layout.blade.php        # Monochrome light sidebar & top bar
│       ├── login.blade.php         # Secure login portal
│       └── index.blade.php         # Overview dashboard & KPI metrics
├── routes/
│   └── web.php                     # Protected clinical routes & authorization
├── config/
│   ├── app.php                     # Application configuration
│   ├── auth.php                    # Authentication guard configuration
│   ├── database.php                # Database connection settings
│   ├── cache.php, session.php, queue.php, logging.php
│   └── services.php                # Service endpoint configuration
├── composer.json / package.json    # Dependency declarations
├── vite.config.js                  # Vite build configuration
├── phpunit.xml                     # PHPUnit test configuration
└── README.md                       # This document
```

---

## 🗄 Database Setup

The public edition includes **8 essential migrations** creating the core relational schema:

| Table | Purpose |
| :--- | :--- |
| `users` | Staff accounts with role and status |
| `cache` / `cache_locks` | Laravel cache layer |
| `sessions` | Session storage |
| `leads` | Patient enquiries and CRM pipeline |
| `patients` | Individual female/male patient records with MRNs |
| `couples` | Couple records with consent status |
| `ivf_cycles` | Treatment cycles with protocol tracking |
| `follicular_scans` | Ultrasound follicle monitoring |
| `opu_and_lab_records` | OPU & embryology lab records |
| `embryo_transfers` | Embryo transfer procedures |
| `cycle_outcomes` | Failure RCA and re-attempt strategies |

**Note:** The public edition does not include: `antenatal_records`, `delivery_records`, `baby_records`, `vaccination_schedules`, `cryobank_storage`, or `clinic_settings` tables. These are exclusive to the private full edition.

### Seed Data

The simplified seeder creates representative records without Protected Health Information (PHI):

* Sample leads with infertility classifications
* Sample couples with basic workup data
* Sample IVF cycles with protocol types
* Sample follicular scan records
* Sample embryo transfer records with outcome tracking

**No real patient data, PHI, or identifiable information is included in the public edition seed data.**

---

## 🔑 Authentication & Authorization

The public edition uses Laravel's default session-based authentication with role gating.

### Login

```php
// Access the login page at /login
// Demo: visit http://127.0.0.1:8000/login
```

### RBAC Implementation

Module access is controlled via the `User::canAccessTab()` method. The public edition implements role-based tab permissions that gate access to the 6 core clinical tabs available in this edition.

**Authentication config** is in `config/auth.php` with the `web` guard using Eloquent user provider.

### Default Routes (Public Edition)

- `GET /login` – Login form (guest middleware)
- `POST /login` – Authenticate credentials
- `GET /logout` – Logout and invalidate session
- `GET /` – Home dashboard (auth middleware)
- Module routes under `auth` middleware

---

## 📂 API Endpoints (Public Edition)

| Endpoint | Method | Description |
| :--- | :--- | :--- |
| `/login` | GET/POST | Authentication login |
| `/logout` | POST/GET | Session termination |
| `/` | GET | Dashboard home tab |
| `/leads` | POST | Store/update/delete lead enquiries |
| `/couples` | POST | Store/update/delete couple records |
| `/cycles` | POST | Store/update/delete IVF cycles |
| `/laboratory` | POST | Store/update/delete OPU/lab records |
| `/transfers` | POST | Store/update/delete embryo transfers |
| `/failures` | POST | Store/update/delete failure RCA |
| `/settings/users` | POST | User management (Super Admin) |
| `/settings/clinic` | POST | Clinic settings (Super Admin) |

**All endpoints require authentication (`auth` middleware) except login (guest).**

---

## 🧪 Testing Instructions

Run the integrated test suite:

```bash
composer test
# or
vendor/bin/phpunit
```

The test suite includes:

* **ExampleTest** – Basic PHPUnit scaffold
* **Feature/ExampleTest** – Feature-level test definitions

Tests verify the core application bootstrap, authentication flow, and database schema integrity.

---

## 📄 License

This software is open-source and released under the [MIT License](LICENSE). You are free to use, modify, and deploy it in clinical, academic, or commercial healthcare settings.

**Public Edition:** The MIT License applies to the portfolio edition code. The Private Full Edition also uses the MIT License, with additional proprietary modules and clinical configurations maintained separately.

---

## 👤 Maintainer Information

**Project Owner / Maintainer:** Nadeem Qureshi<br>
**GitHub Account:** [nadeemmx](https://github.com/nadeemmx)<br>
**Verified Identity:** GitHub account confirmed via CLI authentication<br>
**Contact:** For professional inquiries, please reach out via LinkedIn or direct correspondence.

**Ownership:** This project is the original work of Nadeem Qureshi. The MIT License permits free use, modification, and deployment. Third-party attributions (if any) are retained per the license terms.

---

## 📬 Future Roadmap (Private Edition Roadmap)

The private full edition roadmap includes planned features not visible in the public portfolio:

* Complete Antenatal Care (ANC) monitoring with EDD calculation
* Labor & Delivery documentation with mode-of-delivery tracking
* Pediatric vaccination scheduler (WHO birth-to-15-months schedule)
* Cryobank & bio-repository management (LN2 tank hierarchy)
* Full 7-role RBAC with 12-module tab permissions
* Clinical consent management (Form ART-04, signed document uploads)
* Import/export of clinical data and report generation
* Advanced analytics and clinical benchmarks dashboard
* Integration with external clinic management systems

**These roadmap items are preserved in the private repository and not advertised as implemented in the public edition.**

---

## 📬 Contact & Maintainer

**Project Owner / Maintainer:** Nadeem Qureshi<br>
**GitHub:** [https://github.com/nadeemmx](https://github.com/nadeemmx)<br>
**Account:** Verified via GitHub CLI authentication<br>
**License:** MIT – Copyright (c) 2026