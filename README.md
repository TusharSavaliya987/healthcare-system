# 🏥 Healthcare Management System

A comprehensive, full-stack healthcare management system built with **Next.js 16**, **TypeScript**, **Prisma ORM**, and **PostgreSQL**. This enterprise-grade application streamlines hospital operations including appointments, medical records, billing, and multi-role user management.

![Next.js](https://img.shields.io/badge/Next.js-16.2.6-black?style=flat&logo=next.js)
![React](https://img.shields.io/badge/React-19.2.6-blue?style=flat&logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue?style=flat&logo=typescript)
![Prisma](https://img.shields.io/badge/Prisma-6.19.3-2D3748?style=flat&logo=prisma)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-336791?style=flat&logo=postgresql)
![Clerk](https://img.shields.io/badge/Clerk-Auth-6C47FF?style=flat)

---

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [User Roles](#-user-roles)
- [System Architecture](#-system-architecture)
- [Getting Started](#-getting-started)
- [Environment Variables](#-environment-variables)
- [Database Setup](#-database-setup)
- [Project Structure](#-project-structure)
- [Key Modules](#-key-modules)
- [API Routes & Server Actions](#-api-routes--server-actions)
- [Screenshots](#-screenshots)
- [Deployment](#-deployment)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### 🎯 Core Functionality
- **Multi-Role Authentication** - Secure role-based access control (Admin, Doctor, Patient, Nurse, Lab Technician, Cashier)
- **Appointment Management** - Complete booking system with status tracking and scheduling
- **Medical Records** - Comprehensive patient health records with vital signs tracking
- **Billing & Payments** - Integrated billing system with service catalog and payment processing
- **Doctor Management** - Physician profiles with specializations and availability schedules
- **Patient Portal** - Self-service portal for patients to book appointments and view records
- **Analytics Dashboard** - Real-time statistics and trend analysis with interactive charts
- **Rating System** - Patient reviews and ratings for doctors

### 🔐 Security & Authorization
- Clerk authentication with JWT sessions
- Middleware-based route protection
- Role-based access control (RBAC)
- Secure password handling
- Session management

### 📊 Advanced Features
- **Vital Signs Tracking** - 7-day trend charts for blood pressure, heart rate, temperature
- **Diagnosis Management** - Symptoms, findings, prescriptions, and follow-up plans
- **Lab Test Integration** - Test requests, results, and status tracking
- **Service Catalog** - Reusable medical services with pricing
- **Audit Logging** - System activity tracking for compliance
- **Emergency Contacts** - Dedicated emergency contact management
- **Consent Management** - Privacy, service, and medical treatment consents

### 🎨 User Experience
- Responsive design (mobile, tablet, desktop)
- Real-time search and filtering
- Pagination for large datasets
- Toast notifications for user feedback
- Color-coded status indicators
- Profile avatars with initials fallback
- Interactive data visualizations

---

## 🛠️ Tech Stack

### Frontend
- **Framework:** Next.js 16.2.6 (App Router)
- **UI Library:** React 19.2.6
- **Language:** TypeScript 5
- **Styling:** Tailwind CSS 3.4
- **Components:** Radix UI (Dialog, Select, Popover, Checkbox, etc.)
- **Forms:** React Hook Form 7.54 + Zod validation
- **Charts:** Recharts 2.15
- **Icons:** Lucide React 0.468
- **Notifications:** Sonner 1.7
- **Date Handling:** date-fns 4.1

### Backend
- **Runtime:** Node.js
- **API:** Next.js Server Actions
- **ORM:** Prisma 6.19.3
- **Database:** PostgreSQL (Neon)
- **Authentication:** Clerk 7.4.1
- **Validation:** Zod 3.24

### Development Tools
- **Package Manager:** pnpm
- **Linting:** ESLint
- **Type Checking:** TypeScript
- **Version Control:** Git

---

## 👥 User Roles

### 1. 👨‍💼 Admin (Full System Control)
**Access:** All routes and features

**Capabilities:**
- Complete dashboard with system-wide statistics
- User management (create/delete doctors, staff, patients)
- View and manage all appointments
- Access all medical records and billing
- System settings configuration
- Service catalog management
- Generate reports and analytics

**Routes:** `/admin`, `/admin/system-settings`, `/record/*`

---

### 2. 👨‍⚕️ Doctor (Clinical & Patient Management)
**Access:** Clinical and patient routes

**Capabilities:**
- Personal dashboard with appointment statistics
- View assigned appointments and patient lists
- Add vital signs (temperature, BP, heart rate, weight, height, O2 saturation)
- Create diagnosis with prescriptions and follow-up plans
- Add medical bills for services
- View patient medical history
- Manage working schedule
- View ratings and reviews

**Routes:** `/doctor`, `/record/doctors/*`, `/record/patients`, `/record/appointments`, `/patient/*`

---

### 3. 🧑‍🤝‍🧑 Patient (Self-Service Portal)
**Access:** Personal health portal

**Capabilities:**
- Personal dashboard with appointment history
- Book appointments with available doctors
- View appointment status
- Complete patient registration with medical history
- View own medical records and treatment history
- Access billing and payment information
- Rate and review doctors
- Track vital signs and health metrics

**Routes:** `/patient`, `/patient/registration`, `/record/appointments` (own only)

---

### 4. 👩‍⚕️ Nurse (Clinical Support)
**Access:** Patient care routes

**Capabilities:**
- View patient information and appointments
- Access patient medical records
- Support doctors in patient care
- View appointment schedules

**Routes:** `/record/patients`, `/record/appointments`, `/patient/*`

---

### 5. 🔬 Lab Technician (Laboratory Services)
**Capabilities:**
- Manage lab test requests
- Record test results
- Update test status
- Link services to medical records

**Routes:** `/staff`

---

### 6. 💰 Cashier (Financial Operations)
**Capabilities:**
- Process payments
- Generate receipts
- Manage billing records
- Handle payment methods (cash/card)

**Routes:** `/staff`

---

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Client (Browser)                        │
│              Next.js 16 + React 19 + TypeScript             │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Clerk Middleware                         │
│              Authentication & Authorization                 │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                   Next.js App Router                        │
│         Server Components + Server Actions                  │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Service Layer                            │
│    (appointment, patient, doctor, medical, admin)           │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                    Prisma ORM                               │
│              Type-Safe Database Access                      │
└─────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────┐
│                  PostgreSQL Database                        │
│              (15 Models, Relational Schema)                 │
└─────────────────────────────────────────────────────────────┘
```
---

## 🔐 Environment Variables

Create a `.env` file in the root directory with the following variables:

```env
# Clerk Authentication
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key

# Database
DATABASE_URL="postgresql://USER:PASSWORD@HOST:PORT/DATABASE_NAME?schema=public"
```

### Getting Clerk Credentials

1. Sign up at [clerk.com](https://clerk.com)
2. Create a new application
3. Go to **API Keys** section
4. Copy the **Publishable Key** and **Secret Key**
5. Configure **User Metadata** to include `role` field

### Database Setup

**Option 1: Neon (Recommended for production)**
1. Sign up at [neon.tech](https://neon.tech)
2. Create a new project
3. Copy the connection string
4. Add `?sslmode=require` to the connection string

**Option 2: Local PostgreSQL**
```bash
# Install PostgreSQL
# Create a database
createdb healthcare_db

# Update DATABASE_URL
DATABASE_URL="postgresql://postgres:password@localhost:5432/healthcare_db?schema=public"
```

---

## 🗄️ Database Setup

### Prisma Commands

```bash
# Generate Prisma Client (required after schema changes)
pnpm prisma generate

# Create and apply migrations
pnpm prisma migrate dev --name init

# Open Prisma Studio (Database GUI)
pnpm prisma studio

# Reset database (WARNING: deletes all data)
pnpm prisma migrate reset

# Seed database with sample data
pnpm prisma db seed
```

### Database Schema Overview

**15 Models:**
- `Patient` - Patient demographics and medical information
- `Doctor` - Physician profiles with specializations
- `Staff` - Nurses, lab technicians, cashiers
- `WorkingDays` - Doctor availability schedule
- `Appointment` - Booking records with status tracking
- `MedicalRecords` - Central medical record per appointment
- `VitalSigns` - Patient vital measurements
- `Diagnosis` - Clinical findings and prescriptions
- `LabTest` - Laboratory test requests and results
- `Payment` - Bill headers with totals and status
- `PatientBills` - Line items for services
- `Services` - Service catalog with pricing
- `Rating` - Patient reviews for doctors
- `AuditLog` - System activity tracking

**Key Relationships:**
```
Patient → Appointments → MedicalRecords → (VitalSigns, Diagnosis, LabTest)
Appointment → Payment → PatientBills → Services
Doctor → Appointments, Diagnosis, Ratings, WorkingDays
```

---

## 📁 Project Structure

```
fullstack-healthcare/
├── app/
│   ├── (auth)/                    # Authentication pages
│   │   ├── sign-in/
│   │   └── sign-up/
│   ├── (protected)/               # Protected routes
│   │   ├── admin/                 # Admin dashboard & settings
│   │   ├── doctor/                # Doctor dashboard
│   │   ├── patient/               # Patient portal
│   │   └── record/                # Records management
│   │       ├── appointments/
│   │       ├── billing/
│   │       ├── doctors/
│   │       ├── medical-records/
│   │       ├── patients/
│   │       ├── staffs/
│   │       └── users/
│   ├── actions/                   # Server actions
│   │   ├── admin.ts
│   │   ├── appointment.ts
│   │   ├── general.ts
│   │   ├── medical.ts
│   │   └── patient.ts
│   ├── layout.tsx                 # Root layout
│   ├── page.tsx                   # Home page
│   └── globals.css                # Global styles
├── components/
│   ├── appointment/               # Appointment-specific components
│   ├── charts/                    # Chart components (Recharts)
│   ├── dialogs/                   # Modal dialogs
│   ├── forms/                     # Form components
│   ├── tables/                    # Table components
│   └── ui/                        # Reusable UI components
├── lib/
│   ├── db.ts                      # Prisma client instance
│   ├── routes.ts                  # Route access configuration
│   ├── schema.ts                  # Zod validation schemas
│   └── utils.ts                   # Utility functions
├── prisma/
│   ├── schema.prisma              # Database schema
│   └── seed.ts                    # Database seeding script
├── utils/
│   ├── roles.ts                   # Role checking utilities
│   ├── settings.ts                # App settings
│   └── services/                  # Data access layer
│       ├── admin.ts
│       ├── appointment.ts
│       ├── doctor.ts
│       ├── medical-record.ts
│       ├── patient.ts
│       ├── payments.ts
│       └── staff.ts
├── middleware.ts                  # Clerk authentication middleware
├── .env                           # Environment variables
├── package.json                   # Dependencies
├── tsconfig.json                  # TypeScript configuration
└── tailwind.config.ts             # Tailwind CSS configuration
```

---

## 🔑 Key Modules

### 📅 Appointments Module

**Features:**
- Book appointments with specific doctors
- Appointment types: General Consultation, Check-up, Antenatal, Maternity, Lab Test
- Status workflow: PENDING → SCHEDULED → COMPLETED/CANCELLED
- Time slots: 30-minute intervals (8 AM - 5 PM)
- Doctor availability based on working days
- Search & filter by patient/doctor name, status
- Pagination (10 records per page)

**Actions:**
- Schedule appointment
- Cancel appointment (with reason)
- Complete appointment
- View appointment details

**Files:**
- `app/(protected)/record/appointments/page.tsx`
- `app/actions/appointment.ts`
- `utils/services/appointment.ts`

---

### 🏥 Medical Records Module

**Features:**
- **Vital Signs Tracking:**
  - Body temperature, heart rate, blood pressure
  - Weight, height, BMI calculation
  - Respiratory rate, oxygen saturation
  - 7-day trend charts with averages

- **Diagnosis Management:**
  - Symptoms documentation
  - Diagnosis findings
  - Prescribed medications
  - Follow-up plans
  - Additional notes

- **Medical History:**
  - Complete treatment timeline
  - Past diagnoses and prescriptions
  - Lab test results
  - Vital signs history with visualizations

**Files:**
- `app/(protected)/record/medical-records/page.tsx`
- `app/actions/medical.ts`
- `utils/services/medical-record.ts`
- `components/appointment/vital-signs.tsx`
- `components/appointment/diagnosis-container.tsx`

---

### 💰 Billing & Payments Module

**Features:**
- Service catalog with predefined prices
- Line item billing (service, quantity, unit cost, total)
- Automatic total calculation
- Discount application (percentage-based)
- Payment methods: CASH, CARD
- Payment status: UNPAID, PAID, PART
- Receipt number generation
- Financial reports and outstanding payments

**Workflow:**
1. Add service line items during/after appointment
2. Calculate totals automatically
3. Apply discount percentage
4. Generate final bill
5. Mark appointment as COMPLETED
6. Process payment
7. Generate receipt

**Files:**
- `app/(protected)/record/billing/page.tsx`
- `app/actions/medical.ts`
- `utils/services/payments.ts`
- `components/appointment/bills-container.tsx`
- `components/appointment/generate-final-bill.tsx`

---

### 👨‍⚕️ Doctor Management

**Features:**
- Profile information (name, specialization, license, contact)
- Department assignment
- Profile image with color-coded avatars
- Working schedule (day-wise availability)
- Full-time vs Part-time designation
- Performance metrics (appointments, ratings)
- Patient reviews (1-5 stars)

**Files:**
- `app/(protected)/record/doctors/page.tsx`
- `app/(protected)/record/doctors/[id]/page.tsx`
- `utils/services/doctor.ts`

---

### 🧑‍🤝‍🧑 Patient Management

**Features:**
- **Comprehensive Registration:**
  - Personal: Name, DOB, gender, marital status
  - Contact: Phone, email, address
  - Emergency: Contact name, number, relation
  - Medical: Blood group, allergies, conditions, history
  - Insurance: Provider, policy number
  - Consents: Privacy, service, medical treatment

- **Patient Profile:**
  - Demographics and contact info
  - Appointment history and count
  - Last visit date
  - Medical history timeline
  - Quick links to appointments, records, bills

**Files:**
- `app/(protected)/patient/registration/page.tsx`
- `app/(protected)/record/patients/page.tsx`
- `app/(protected)/patient/[patientId]/page.tsx`
- `utils/services/patient.ts`

---

### 📊 Dashboard & Analytics

**Features:**
- **Admin Dashboard:**
  - Total patients, doctors, appointments, consultations
  - Monthly appointment trends (line chart)
  - Appointment status breakdown (pie chart)
  - Recent appointments table
  - Available doctors today

- **Doctor Dashboard:**
  - Personal statistics (patients, nurses, appointments)
  - Monthly consultation trends
  - Recent appointments
  - Available colleagues

- **Patient Dashboard:**
  - Personal appointment statistics
  - Status breakdown (pending, completed, cancelled)
  - Monthly appointment history
  - Available doctors
  - Rating submission

**Files:**
- `app/(protected)/admin/page.tsx`
- `app/(protected)/doctor/page.tsx`
- `app/(protected)/patient/page.tsx`
- `components/charts/appointment-chart.tsx`
- `components/charts/stat-summary.tsx`

---

## 🔌 API Routes & Server Actions

### Server Actions (app/actions/)

**appointment.ts**
- `createNewAppointment(data)` - Book new appointment
- `appointmentAction(id, status, reason)` - Update appointment status
- `addVitalSigns(data)` - Add patient vital signs

**medical.ts**
- `addDiagnosis(data, appointmentId)` - Create diagnosis
- `addNewBill(data)` - Add service bill
- `generateFinalBill(data)` - Generate final bill with discount
- `processPayment(data)` - Process payment

**patient.ts**
- `createPatient(data)` - Register new patient
- `updatePatient(id, data)` - Update patient information

**admin.ts**
- `createDoctor(data)` - Create doctor account
- `createStaff(data)` - Create staff account
- `addService(data)` - Add service to catalog
- `updateService(id, data)` - Update service

**general.ts**
- `deleteRecord(id, model)` - Delete any record with audit log

### Service Layer (utils/services/)

**appointment.ts**
- `getAppointmentById(id)` - Fetch single appointment
- `getPatientAppointments({ page, search, id })` - Paginated appointments
- `getAppointmentStats(userId, role)` - Dashboard statistics

**doctor.ts**
- `getAllDoctors({ page, search })` - Paginated doctors list
- `getDoctorById(id)` - Fetch doctor details
- `getAvailableDoctors()` - Doctors available today

**patient.ts**
- `getAllPatients({ page, search })` - Paginated patients list
- `getPatientById(id)` - Fetch patient details

**medical-record.ts**
- `getMedicalRecords({ page, search })` - Paginated medical records
- `getMedicalRecordByAppointment(appointmentId)` - Fetch by appointment

**payments.ts**
- `getPaymentRecords({ page, search })` - Paginated billing records
---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Your Name**
- GitHub: [TusharSavaliya987](https://github.com/TusharSavaliya987)
- LinkedIn: [tushar-savaliya](https://www.linkedin.com/in/tushar-savaliya07)
- Portfolio: [tushar-savaliya-portfolio](https://tushar-savaliya-portfolio-site.vercel.app/)

---

**⭐ If you find this project helpful, please give it a star on GitHub!**

---

*Built with ❤️ using Next.js, TypeScript, and modern web technologies*
