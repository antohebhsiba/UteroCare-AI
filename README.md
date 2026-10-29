# UteroCare AI — Clinical-Grade Women's Uterine Health Platform

UteroCare AI is a full-stack, production-grade women's uterine health evaluation, cycle tracking, and clinical consultation preparation application. Grounded in the **FIGO PALM-COEIN classification system**, ACOG clinical practice bulletins, and RCOG guidelines, the platform bridges the gap between chronic pelvic symptoms and medical diagnosis.

---

## Architecture & System Overview

- **Frontend**: React 19, TypeScript, Vite, Tailwind CSS, React Router v7, Lucide Icons, Framer Motion.
- **Backend**: Node.js, Express, TypeScript, Zod schema validation, Better-SQLite3 with WAL mode and foreign key cascading.
- **Security & Auth**: Salted password hashing with Bcrypt, HTTP-only secure session cookies, multi-user isolation, private disk file storage outside web roots, and brute-force rate limiting.
- **Clinical Engine**: Deterministic FIGO PALM-COEIN evaluation engine with acute red-flag emergency triage, structured evidence tracking, missing info detection, and tailored doctor consultation questions.

---

## Project Structure

```
├── data/
│   └── uterocare.db              # Persistent SQLite database file
├── uploads/                      # Private document storage (outside public directory)
├── prisma/
│   └── schema.prisma             # Documented Prisma schema
├── server/
│   ├── app.ts                    # Express app configuration & middleware
│   ├── database/
│   │   └── db.ts                 # SQLite database connection, DDL, and migrations
│   ├── middleware/
│   │   └── auth.ts               # HTTP-only cookie and Bearer session verification
│   ├── routes/
│   │   ├── auth.routes.ts        # Register, Login, Logout, Session restore, Account deletion
│   │   ├── assessments.routes.ts # Assessment lifecycle CRUD & active listing
│   │   ├── symptoms.routes.ts    # Progressive symptom saving & red-flag detection
│   │   ├── documents.routes.ts   # Private file upload, streaming, and deletion
│   │   ├── analysis.routes.ts    # Clinical rule engine execution and report generation
│   │   ├── cycle.routes.ts       # Menstrual tracking & cycle interval analytics
│   │   └── conditions.routes.ts  # FIGO educational conditions encyclopaedia
│   ├── security/
│   │   └── auth.ts               # Password hashing & unique assessment ID generation
│   ├── services/
│   │   ├── assessmentEngine.ts   # Clinical decision rules & emergency triage
│   │   └── documentService.ts    # Safe upload management & PDF text parsing
│   └── tests/
│       └── server.test.ts        # Automated Vitest test suite (17 passed tests)
├── src/
│   ├── components/
│   │   ├── UI/                   # Button, Card, Badge, EmergencyModal
│   │   ├── Navbar.tsx            # Responsive navigation & user controls
│   │   ├── Footer.tsx            # Clinical disclaimer & navigation links
│   │   ├── ProtectedRoute.tsx    # Auth guard with loading skeletons
│   │   └── UterusIllustration.tsx# 3D-inspired SVG uterine anatomy visual
│   ├── context/
│   │   ├── AuthContext.tsx       # Global session restoration & user state
│   │   └── AssessmentContext.tsx # Central assessment lifecycle manager
│   ├── pages/
│   │   ├── Home.tsx              # Landing with 3D illustration & clinical overview
│   │   ├── Register.tsx          # Account registration with password strength indicators
│   │   ├── Login.tsx             # Database authentication with demo pre-fill
│   │   ├── GuidedAssessment.tsx  # 8-step questionnaire with auto-saving
│   │   ├── ActiveAssessments.tsx # Saved assessments registry (resume, report, delete)
│   │   ├── UploadScans.tsx       # Private scan/PDF upload & text extractor
│   │   ├── AIWorkspace.tsx       # Symptom & record synthesis review
│   │   ├── AssessmentResults.tsx # Comprehensive clinical findings & printable report
│   │   ├── AssessmentHistory.tsx # Longitudinal assessment history & filtering
│   │   ├── CycleTracker.tsx      # Menstrual calendar, flow, pain, and analytics
│   │   ├── HealthLibrary.tsx     # Searchable FIGO conditions guide
│   │   ├── DoctorPrep.tsx        # Consultation preparation packet & checklist
│   │   ├── AccountSettings.tsx   # Profile management, JSON export & account deletion
│   │   ├── PrivacySecurity.tsx   # Security, encryption & data sovereignty details
│   │   └── NotFound.tsx          # 404 error page
│   ├── services/
│   │   └── api.ts                # Central typed client with credentials include
│   ├── types/
│   │   └── index.ts              # TypeScript domain types
│   ├── App.tsx                   # Central router for all 15 pages
│   ├── main.tsx                  # React entry point
│   └── index.css                 # Theme tokens & editorial typography
├── server.ts                     # Full-stack server entry point (port 3000)
├── vite.config.ts
└── package.json
