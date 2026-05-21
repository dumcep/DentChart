# DentChart

A web application designed to digitize dental workflows, integrating anamnesis, odontograms, and calendar management. Developed as a Computer Science thesis project.

**Live Demo:** [https://dentchart.vercel.app/](https://dentchart.vercel.app/)

DentChart is a comprehensive web application designed to digitize and optimize dental clinic workflows. Developed as a Computer Science thesis project in direct collaboration with a dental medicine student, the platform is tailored to meet the practical, day-to-day requirements of dental students and practitioners. 

It centralizes patient data, procedural tracking, and scheduling to reduce administrative overhead and transition traditional paper-based clinics into a unified digital environment.

---

## 🏗 Architecture Note: Live Demo vs. Production

* **Live Demo (Vercel):** The publicly accessible version is configured for client-side interaction using local browser storage and mock data. A Next.js middleware simulates the authentication flow by managing a session token locally, allowing guests to freely explore all features, interact with the charting tools, and manage schedules without modifying a live database. Data in this environment is ephemeral.
* **Production Version (Supabase):** The original, fully deployed application relies on Supabase as a Backend-as-a-Service, backed by a relational PostgreSQL database. 
  * **Multi-Tenant Architecture & RLS:** It utilizes a multi-tenant data model where records (patients, treatments, schedules) are stored centrally but isolated using PostgreSQL **Row Level Security (RLS)**. Each doctor's access is restricted via a `medic_id` foreign key.
  * **Authentication Middleware:** Supabase handles secure credential management, issuing a JWT upon login. Next.js middleware validates this JWT to protect routes and maintain the server-client session securely.
  * **Complex State Storage:** The intricate state of the interactive SVG odontograms is serialized and stored using PostgreSQL's `JSONB` format, linked directly to the patient profile and the presiding dentist.

---

## ⚙️ Technical Stack

* **Framework:** Next.js
* **Language:** TypeScript
* **Styling:** Tailwind CSS
* **Graphics:** Custom SVG rendering (utilized for the highly interactive, individual tooth components in the Odontogram)
* **Backend (Production):** Supabase (PostgreSQL, Auth, RLS)

---

## ✨ Core Features & Visual Walkthrough

### 1. Interactive Dental & Periodontal Charting (Odontogram)
The core feature of the application is a custom-built, SVG-based interactive dental chart. It allows dentists to visually map past dental work, current pathologies (e.g., caries, mobility), and planned treatments on specific tooth surfaces. It also integrates periodontal tracking.

![Odontogram View](Odontogram_Full.png)
*Detailed view of the interactive SVG odontogram and treatment journal.*

![Odontogram Compact](Odontogram_Compact.png)

### 2. Clinic Dashboard
A centralized hub providing a quick overview of the day's operations, including total patient count, upcoming appointments, and system status.

![Dashboard](Dashboard.png)

### 3. Patient Management 
A searchable database for all registered clinic patients, providing quick access to their individual files, contact information, and treatment history.

![Patients List](Pacients.png)

### 4. Medical History & GDPR Compliance (Anamnesis)
Integrated digital forms for capturing and updating patient medical backgrounds, alerting the dentist to specific conditions (e.g., cardiac issues, diabetes, pregnancy), current medications, and tracking GDPR consent signatures.

![Medical History](GDPR_Anamneza.png)

### 5. Calendar & Scheduling
A visual timeline and appointment management system. Users can easily add, edit, or remove consultations and procedures, providing a clear overview of the daily clinical workflow.

---