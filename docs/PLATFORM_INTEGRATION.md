# Togo Health Platform Integration Guide

## Overview

Togo Health is a unified clinical workforce management platform that consolidates three distinct healthcare workforce solutions while adding AI-powered automation and orchestration capabilities. This document details how the integrated systems work together and the technical integration points.

---

## Company Integrations

### 1. Med App - Onboarding & Communications

**Core Functionality**:
- New hire onboarding workflows
- Credential collection and verification
- Policy acknowledgment tracking
- Staff directory and profiles
- Internal messaging and announcements
- Document distribution

**Integration Points in Togo Health**:

**Clinician Dashboard**:
- **Messages Widget**: Displays Med App communications inbox
  - Unread count badge
  - Message preview with sender and timestamp
  - Direct link to full message thread
- **Credentials Section**: Shows Med App credential status
  - License expiration tracking
  - Certification status
  - Required document uploads
  - Automated renewal reminders

**Admin Dashboard**:
- **Staff Management**: Med App profiles integrated
  - Complete staff directory
  - Credential compliance overview
  - Onboarding status tracking
- **Communications Hub**: Broadcast capabilities
  - Facility-wide announcements
  - Department-specific messages
  - Emergency notifications

**AI Agent Integration**:
- **Credential Verification Agent**: Pulls data from Med App profiles
- **Notification Agent**: Routes Med App messages to appropriate channels
- **Onboarding Agent**: Automates new hire checklist completion

**Technical Integration**:
```
Med App API → Togo Health Integration Layer
├── RESTful API (JSON)
├── Webhook notifications for real-time updates
├── OAuth 2.0 authentication
└── Bidirectional sync for staff profiles
```

---

### 2. Core Schedule - Rostering & Shift Management

**Core Functionality**:
- Shift scheduling and rostering
- Availability management
- Shift swap and coverage requests
- Time tracking and timesheets
- Schedule templates
- Overtime calculation

**Integration Points in Togo Health**:

**Clinician Dashboard**:
- **Upcoming Shifts Widget**: Core Schedule data display
  - Next shift countdown
  - Shift details (location, role, time)
  - Shift swap options
  - Calendar view of upcoming schedule
- **Timesheet Section**: Automated time tracking
  - Hours worked per pay period
  - Overtime alerts
  - Auto-submission via Timesheet Agent

**Admin Dashboard**:
- **Workforce Overview**: Real-time staffing data
  - Current shift coverage
  - Open shifts requiring fill
  - Upcoming staffing needs
  - Skills gap analysis
- **Schedule Optimization**: AI-enhanced rostering
  - Optimal shift assignments
  - Coverage predictions
  - Staff utilization metrics

**AI Agent Integration**:
- **Timesheet Agent**: Auto-submits based on Core Schedule shift data
- **Schedule Optimization Agent**: Fills open shifts from Core Schedule
- **Shift Swap Agent**: Facilitates swaps within Core Schedule system
- **Rostering Agent**: Creates optimal schedules considering preferences, skills, compliance

**Technical Integration**:
```
Core Schedule API → Togo Health Integration Layer
├── RESTful API (JSON)
├── Real-time shift updates via WebSocket
├── iCal feed for calendar integrations
├── Batch sync for historical data
└── FHIR-compatible for healthcare standards
```

---

### 3. myhealthPD - CPD & Learning Management

**Core Functionality**:
- Continuing Professional Development (CPD) tracking
- Learning Management System (LMS)
- Course catalog and enrollment
- Compliance training
- Competency assessments
- Learning pathway recommendations
- CE credit tracking

**Integration Points in Togo Health**:

**Clinician Dashboard**:
- **Learning Progress Widget**: myhealthPD course data
  - Active courses and completion percentage
  - Upcoming due dates
  - Recent achievements and certificates
  - Recommended courses
- **AI-Powered LMS Recommendations**: Personalized learning
  - Courses matched to recent clinical cases
  - Skills development based on career goals
  - Compliance training alerts
  - Peer learning suggestions

**Admin Dashboard**:
- **Training Compliance**: Organization-wide tracking
  - Staff competency status
  - Required training completion rates
  - Certification expiration tracking
  - Skills inventory

**AI Agent Integration**:
- **LMS Recommendation Agent**: Analyzes EMR cases and suggests relevant courses
  - "You treated 3 diabetic patients this week. Recommended: Advanced Diabetes Management (2.5 CE)"
  - Context-aware learning based on actual clinical work
  - Proactive identification of knowledge gaps
- **Compliance Agent**: Monitors myhealthPD completion requirements
- **LMS Enrollment Agent**: Auto-enrolls in required courses

**Technical Integration**:
```
myhealthPD API → Togo Health Integration Layer
├── LTI 1.3 (Learning Tools Interoperability)
├── xAPI (Experience API) for learning records
├── RESTful API for course catalog
├── SCORM-compliant content delivery
└── Single Sign-On (SSO) via SAML 2.0
```

---

### 4. Time Filer - Payroll & Award Compliance

**Core Functionality**:
- Timesheet management and approval
- Award interpretation and compliance
- Leave and absence tracking
- Roster planning integration
- Payroll system integration
- Award-specific rate calculations
- Public holiday and penalty rate management
- Leave entitlements and accruals

**Integration Points in Togo Health**:

**Clinician Dashboard**:
- **Timesheet Auto-Submit**: Automated payroll processing
  - AI agents submit timesheets directly to Time Filer
  - Award compliance verified automatically
  - Hours tracked from Core Schedule shifts
  - Leave accruals calculated in real-time
- **Payslip Access**: View payment details
  - Award rates breakdown
  - Overtime and penalty rates
  - Leave balance and accruals
  - Superannuation contributions

**Admin Dashboard**:
- **Payroll Integration Banner**: 247 staff timesheets automated
  - Award rates auto-applied
  - Leave entitlements calculated
  - Payroll export ready
- **Workforce Cost Management**: Real-time payroll insights
  - Labor costs by department
  - Award compliance status
  - Overtime tracking and alerts
  - Budget variance reporting

**AI Agent Integration**:
- **Timesheet Agent**: Auto-submits timesheets to Time Filer
  - Syncs shift data from Core Schedule
  - Applies correct award rates based on role and shift type
  - Calculates leave accruals (annual leave, sick leave, etc.)
  - Submits weekly timesheets with award compliance verified
  - Example: "Automatically submitted your timesheet for week ending Oct 13 with 38.5 hours to Time Filer. Award rates applied, leave accrual calculated."
- **Compliance Agent**: Monitors award compliance
  - Verifies correct penalty rates applied
  - Alerts to rostering that may breach award conditions
  - Tracks maximum hours and minimum breaks
- **Leave Management Agent**: Coordinates leave requests
  - Integrates leave approvals with Time Filer
  - Updates leave balances automatically
  - Ensures rostering considers leave availability

**Business Benefits**:
- **90% reduction** in payroll corrections
- **2-5 hours saved** per pay cycle on timesheet processing
- **Guaranteed award compliance** with automated rate calculations
- **Real-time visibility** into labor costs and budget tracking
- **Elimination** of manual timesheet entry errors

**Technical Integration**:
```
Time Filer Platform → Togo Health Integration Layer
├── RESTful API (JSON)
├── Automated timesheet submission (Core Schedule → Time Filer)
├── Award interpretation engine integration
├── Payroll system connectors (API-based)
├── Real-time leave balance updates
└── Webhook notifications for payroll events
```

**Award Compliance Features**:
- **Automated Award Interpretation**:
  - Healthcare industry awards (Nurses Award, Health Professionals Award, etc.)
  - State-specific variations and allowances
  - Public holiday loading calculations
  - Overtime and penalty rate thresholds
- **Leave Entitlements**:
  - Annual leave accrual tracking
  - Personal/sick leave balances
  - Long service leave calculations
  - Parental leave entitlements
- **Payroll Export**:
  - Direct integration with major payroll providers
  - Formatted exports for manual processing
  - Detailed audit trails for payroll verification

**Data Flow Example**:
```
1. Clinician completes shift (tracked in Core Schedule)
2. Timesheet Agent syncs shift data to Time Filer
3. Time Filer applies appropriate award rates
4. Leave accruals calculated automatically
5. Payroll export generated for approved timesheets
6. Clinician receives notification: "Timesheet submitted, payroll processing initiated"
```

---

### 5. My Digital Passport - Unified Knowledge Graph

**Core Functionality**:
- Clinician-owned professional knowledge graph
- Unified data repository (learning, CPD, credentials, shifts, connections, rosters, hospitals, onboarding, training)
- Shareable professional profiles
- Data portability across healthcare organizations
- Automatic verification and credential validation
- Industry body data sharing

**Integration Points in Togo Health**:

**Clinician Dashboard**:
- **Digital Passport Widget**: Complete professional data overview
  - 42 credentials tracked
  - 156 CPD hours aggregated
  - 5 hospitals serviced
  - 2,847 shifts completed
  - Knowledge graph components: Learning & CPD, Credentials & Licenses, Shift History, Hospital Networks, Professional Connections, Training Records
- **Data Ownership Messaging**:
  - "You own your data: Share your passport with employers, industry bodies, or keep it private."
  - "Portable across all healthcare organizations using Togo Health."
- **Manage Passport Button**: Control sharing permissions and data visibility

**Admin Dashboard**:
- **Digital Passport Integration Overview**:
  - 228/247 staff passports shared (92% adoption rate)
  - 3,248 total credentials tracked across organization
  - 18.5h average admin time saved per staff member
- **Data Portability Benefits**:
  - Onboarding reduced from 14 days to 2 days for new hires with existing passports
  - Automatic verification eliminates manual credential checking
  - Staff can move between facilities without re-verification

**AI Agent Integration**:
- **Credential Agent**: Syncs with Digital Passport for license tracking
- **Onboarding Agent**: Imports existing passport data for new hires
- **Compliance Agent**: Monitors Digital Passport for expiring credentials
- **LMS Agent**: Recommends courses based on passport learning history

**Business Benefits**:
- **Reduced onboarding time**: From 14 days to 2 days (86% faster)
- **Eliminated duplicate data entry**: Staff enter credentials once, use everywhere
- **Increased staff satisfaction**: Clinicians own and control their professional data
- **Network effects**: More hospitals using Digital Passport = more valuable for clinicians
- **Competitive advantage**: Attract staff who value data portability

**Technical Integration**:
```
My Digital Passport Platform → Togo Health Integration Layer
├── RESTful API (JSON) for knowledge graph queries
├── OAuth 2.0 for secure data sharing authorization
├── GraphQL for flexible data retrieval
├── Webhook notifications for credential updates
├── Blockchain-backed verification ledger
└── Privacy-preserving selective attribute disclosure
```

**Data Schema Example**:
```json
{
  "passportId": "mdp_abc123",
  "clinicianId": "sarah.chen@example.com",
  "sharingPermissions": {
    "stMarysHospital": {
      "granted": true,
      "scope": ["credentials", "learning", "shifts"],
      "expiresAt": "2026-10-17T00:00:00Z"
    }
  },
  "knowledgeGraph": {
    "credentials": [
      {
        "type": "RN_LICENSE",
        "issuingBody": "NSW Nursing Board",
        "licenseNumber": "NUR12345",
        "issueDate": "2018-03-15",
        "expiryDate": "2026-03-15",
        "verified": true,
        "verifiedAt": "2025-10-10T09:23:12Z"
      }
    ],
    "learning": {
      "cpdHours": 156,
      "courses": [
        {
          "name": "Advanced Wound Care",
          "provider": "myhealthPD",
          "completedDate": "2025-08-12",
          "ceCredits": 2.5
        }
      ]
    },
    "shifts": {
      "totalCompleted": 2847,
      "hospitals": ["St. Mary's", "City General", "Regional Medical Center", "Metro Health", "Community Hospital"],
      "specialties": ["Emergency Medicine", "ICU", "Med-Surg"]
    }
  }
}
```

**Privacy & Security**:
- Clinician-controlled sharing permissions (granular consent)
- Time-limited access grants (e.g., employment duration only)
- Selective attribute disclosure (share only what's needed)
- Audit trail of all data access
- GDPR and HIPAA compliant
- Right to data portability and deletion

**Use Cases**:
1. **New Hospital Onboarding**: Clinician shares existing Digital Passport → Hospital verifies credentials automatically → Onboarding time reduced from 14 days to 2 days
2. **Credential Renewal**: Digital Passport tracks expiration → Alerts sent 60 days before expiry → Auto-books renewal courses via myhealthPD
3. **Professional Portfolio**: Clinician applies to new position → Shares Digital Passport with prospective employer → Complete work history, credentials, and learning visible instantly
4. **Industry Body Reporting**: Annual CPD requirements → Digital Passport exports certified CPD summary → Submit to nursing board with one click

---

## Verified Orchestration Partnership

**Purpose**: Secure identity and credential verification infrastructure

**Core Functionality**:
- Multi-factor authentication (MFA)
- Biometric verification
- Cross-organizational identity federation
- Real-time credential verification
- Blockchain-based credential ledger
- Regulatory database integration

**Integration Points in Togo Health**:

**Authentication & Authorization**:
- **Login**: Verified Orchestration SSO
  - Passwordless authentication options
  - Biometric support (Face ID, Touch ID, Windows Hello)
  - Hardware token support (YubiKey)
- **Agent Approvals**: High-assurance verification
  - Sensitive actions require MFA step-up
  - Biometric confirmation for critical decisions
  - Audit trail of all authentication events

**Credential Verification**:
- **Real-Time License Validation**:
  - Connects to state nursing boards
  - Verifies medical licenses with regulatory authorities
  - Checks certification status with issuing bodies
- **Automated Compliance Checks**:
  - Background check status
  - Drug screening results
  - Immunization records

**Identity Federation**:
- **Cross-Hospital Staff Sharing**:
  - Verified credentials portable across facilities
  - Trusted identity assertions
  - Privacy-preserving attribute sharing

**AI Agent Integration**:
- **Credential Agent**: Uses Verified Orchestration for license verification
- **Compliance Agent**: Real-time regulatory database queries
- **Onboarding Agent**: Automated background check status updates

**Technical Integration**:
```
Verified Orchestration Platform → Togo Health
├── OpenID Connect (OIDC) for authentication
├── SAML 2.0 for enterprise SSO
├── WebAuthn for passwordless/biometric
├── FIDO2 for hardware tokens
├── REST API for credential verification
└── Blockchain ledger queries (read-only)
```

---

## EMR (Electronic Medical Record) Integration

**Purpose**: Provide clinicians with patient context before shifts

**Supported EMR Systems**:
- Epic (primary)
- Cerner
- Meditech
- Allscripts

**Integration Points in Togo Health**:

**Clinician Dashboard - AI-Powered EMR Briefing**:
- **Pre-Shift Patient Overview**:
  ```
  "You're scheduled for ICU tomorrow (3p-11p). Your assignment includes:
  - 3 critical patients
  - 2 post-surgical (Day 1 recovery)
  - 1 long-term ventilator patient

  Key alerts:
  - Bed 12: New admission, recent MI, requires close monitoring
  - Bed 7: Complex medication schedule, see care plan"
  ```

**Real-Time EMR Sync**:
- **EMR Briefing Agent**: Pulls assignment data
  - Patient census for assigned unit
  - Acuity levels and care requirements
  - Recent changes to patient conditions
  - Medication schedules
  - Isolation precautions

**AI Agent Integration**:
- **EMR Briefing Agent** (Human-on-the-Loop):
  - Automatically pulls data when shift is scheduled
  - Summarizes complex patient information
  - Highlights critical alerts and changes
  - Presents briefing 4 hours before shift start
  - Clinician can request more details on specific patients

**Privacy & Compliance**:
- HIPAA-compliant data handling
- Role-based access control (RBAC)
- Only assigned patients visible
- Automatic data purge after shift ends
- Audit logging of all EMR access

**Technical Integration**:
```
Hospital EMR System → Togo Health Integration Layer
├── FHIR R4 API (Fast Healthcare Interoperability Resources)
├── HL7 v2 messages for real-time ADT (Admit/Discharge/Transfer)
├── CDA (Clinical Document Architecture) for care summaries
├── SMART on FHIR for app launch context
└── Encrypted data transport (TLS 1.3)
```

**Example FHIR Query**:
```json
GET /Patient?_has:Encounter:patient:location=ICU-2A
GET /MedicationRequest?patient={patientId}&status=active
GET /Observation?patient={patientId}&category=vital-signs&date=ge2025-10-21
```

---

## Data Flow Architecture

### Agent Orchestration Flow

```
User Action / Scheduled Event
         ↓
    Orchestrator Agent
         ↓
    ├─→ Specialized Agent 1 (Autonomous)
    │        ↓
    │   [Executes immediately]
    │        ↓
    │   Audit Log + User Notification
    │
    ├─→ Specialized Agent 2 (Human-in-the-Loop)
    │        ↓
    │   [Prepares recommendation]
    │        ↓
    │   User Approval UI
    │        ↓
    │   [Executes if approved]
    │        ↓
    │   Audit Log + Confirmation
    │
    └─→ Specialized Agent 3 (Human-on-the-Loop)
             ↓
        [Executes immediately]
             ↓
        Monitoring Dashboard + Alert
             ↓
        User can override
             ↓
        Audit Log
```

### Integration Data Sync

**Real-Time Events** (WebSocket/Webhook):
- Shift assignments (Core Schedule → Togo Health)
- New messages (Med App → Togo Health)
- Course enrollments (myhealthPD → Togo Health)
- Timesheet submissions (Togo Health → Time Filer)
- Payroll processing events (Time Filer → Togo Health)
- Credential updates (Verified Orchestration → Togo Health)
- Patient assignments (EMR → Togo Health)

**Batch Sync** (Scheduled API calls):
- Historical timesheet data (Core Schedule, Time Filer)
- Leave balance updates (Time Filer)
- Training completion records (myhealthPD)
- Staff directory updates (Med App)
- Credential verification status (Verified Orchestration)

**On-Demand Queries**:
- EMR patient briefings (triggered by shift schedule)
- Real-time license verification (triggered by credential agent)
- Course catalog search (triggered by LMS agent)

---

## API Architecture

### Togo Health Integration Layer

**Design Pattern**: API Gateway with microservices

```
External Systems → API Gateway → Microservices
                        ↓
                   Rate Limiting
                   Authentication
                   Request Routing
                   Response Caching
                        ↓
    ├─→ Med App Service
    ├─→ Core Schedule Service
    ├─→ myhealthPD Service
    ├─→ Time Filer Service
    ├─→ Verified Orchestration Service
    ├─→ EMR Integration Service
    └─→ Agent Orchestration Service
```

### Security Layers

**1. Authentication**:
- OAuth 2.0 client credentials for system-to-system
- JWT tokens for user sessions
- API keys for webhook endpoints

**2. Authorization**:
- Role-based access control (RBAC)
- Attribute-based access control (ABAC) for patient data
- Scope-limited tokens

**3. Encryption**:
- TLS 1.3 for data in transit
- AES-256 for data at rest
- Field-level encryption for PII/PHI

**4. Audit & Compliance**:
- All API calls logged with user context
- HIPAA audit trail maintained
- Retention policies enforced
- Regular compliance reports

---

## Database Architecture

### Togo Health Unified Data Model

**Primary Database**: PostgreSQL (relational data)
**Cache Layer**: Redis (session data, rate limiting)
**Document Store**: MongoDB (unstructured agent logs, EMR briefings)
**Search Index**: Elasticsearch (staff directory, message search)

**Core Tables**:
```sql
-- Staff unified from Med App
CREATE TABLE staff (
  id UUID PRIMARY KEY,
  med_app_id VARCHAR(255),
  verified_orchestration_id VARCHAR(255),
  first_name VARCHAR(255),
  last_name VARCHAR(255),
  email VARCHAR(255),
  role VARCHAR(100),
  department VARCHAR(100),
  hire_date DATE,
  status VARCHAR(50)
);

-- Shifts from Core Schedule
CREATE TABLE shifts (
  id UUID PRIMARY KEY,
  core_schedule_id VARCHAR(255),
  staff_id UUID REFERENCES staff(id),
  facility_id UUID,
  start_time TIMESTAMP,
  end_time TIMESTAMP,
  role VARCHAR(100),
  status VARCHAR(50)
);

-- Learning records from myhealthPD
CREATE TABLE learning_records (
  id UUID PRIMARY KEY,
  staff_id UUID REFERENCES staff(id),
  myhealthpd_course_id VARCHAR(255),
  course_name VARCHAR(500),
  enrollment_date DATE,
  completion_date DATE,
  progress_percent INTEGER,
  ce_credits DECIMAL(4,2)
);

-- Timesheet records synced to Time Filer
CREATE TABLE timesheets (
  id UUID PRIMARY KEY,
  staff_id UUID REFERENCES staff(id),
  time_filer_id VARCHAR(255),
  week_ending DATE,
  total_hours DECIMAL(5,2),
  award_type VARCHAR(100),
  status VARCHAR(50), -- submitted, approved, processed
  submitted_at TIMESTAMP,
  submitted_by VARCHAR(50), -- agent or user
  award_compliance_verified BOOLEAN
);

-- Leave balances from Time Filer
CREATE TABLE leave_balances (
  id UUID PRIMARY KEY,
  staff_id UUID REFERENCES staff(id),
  leave_type VARCHAR(50), -- annual, sick, long_service
  balance_hours DECIMAL(6,2),
  accrual_rate DECIMAL(4,2),
  last_updated TIMESTAMP
);

-- Agent activity logs
CREATE TABLE agent_activities (
  id UUID PRIMARY KEY,
  agent_type VARCHAR(100),
  workflow_type VARCHAR(50), -- autonomous, hitl, hotl
  staff_id UUID REFERENCES staff(id),
  action_description TEXT,
  status VARCHAR(50),
  created_at TIMESTAMP,
  completed_at TIMESTAMP,
  requires_approval BOOLEAN,
  approved_at TIMESTAMP,
  approved_by UUID
);
```

### Data Synchronization Strategy

**1. Event-Driven Sync** (preferred):
- Webhook listeners for Med App, Core Schedule, myhealthPD
- Immediate updates to Togo Health database
- Conflict resolution via timestamp comparison

**2. Polling Sync** (fallback):
- Scheduled jobs every 5-15 minutes
- Incremental sync based on last_modified timestamps
- Full sync nightly during maintenance window

**3. Master Data Management**:
- Staff records: Med App is source of truth
- Shifts: Core Schedule is source of truth
- Learning: myhealthPD is source of truth
- Timesheets & Payroll: Time Filer is source of truth
- Togo Health maintains read replicas with enrichment (agent actions, preferences)

---

## Deployment Architecture

### Cloud Infrastructure

**Hosting**: AWS (Amazon Web Services)
**Regions**: Multi-region for high availability

```
CloudFront (CDN) → ALB (Load Balancer) → ECS (Containers)
                                              ↓
                                         ├─→ Web App (React)
                                         ├─→ API Gateway (Node.js)
                                         ├─→ Agent Services (Python)
                                         └─→ Integration Services (Go)
                                              ↓
                                         RDS (PostgreSQL)
                                         ElastiCache (Redis)
                                         DocumentDB (MongoDB)
                                         Elasticsearch
```

### Scalability

**Horizontal Scaling**:
- Web app: Auto-scaling based on CPU/memory
- API services: Auto-scaling based on request rate
- Agent workers: Queue-based scaling (SQS)

**Database Scaling**:
- Read replicas for query load distribution
- Connection pooling (PgBouncer)
- Caching layer (Redis) for frequently accessed data

---

## Future Integration Roadmap

### Phase 2 Integrations
- **HR Systems**: Workday, BambooHR for employee lifecycle management
- **Benefits Platforms**: Health insurance, retirement account sync
- **Performance Management**: 360 reviews, goal tracking integration

### Phase 3 Integrations
- **Telemedicine**: Integration for virtual shift coverage
- **Supply Chain**: Ensure materials available for scheduled procedures
- **Patient Engagement**: Notify patients of assigned care team

### Advanced AI Capabilities
- **Multi-hospital orchestration**: Coordinate temporary assignments across hospital networks
- **Predictive staffing**: Forecast needs based on historical patterns, seasonal trends, local events
- **Natural language interface**: Voice and chat-based agent interactions
- **Reinforcement learning**: Agents improve from outcome feedback

---

## Developer Resources

### API Documentation
- Swagger/OpenAPI specs for all endpoints
- Postman collections for testing
- SDK libraries (JavaScript, Python, Ruby)

### Sandbox Environment
- Test accounts for Med App, Core Schedule, myhealthPD
- Sample data for development
- Webhook testing tools

### Support
- Developer portal: https://developers.togohealth.com (future)
- API status page: https://status.togohealth.com (future)
- Integration support: integrations@togohealth.com (future)

---

## Compliance & Certification

**Healthcare Standards**:
- HIPAA compliant infrastructure and processes
- HITECH Act requirements met
- SOC 2 Type II certified
- FHIR R4 compliant

**Security Certifications**:
- ISO 27001 (Information Security Management)
- ISO 27017 (Cloud Security)
- PCI DSS (for payment processing)

**Accessibility**:
- WCAG 2.1 AA compliance
- Section 508 compliant
- ARIA landmarks and labels

---

This integration architecture demonstrates how Togo Health unifies disparate healthcare workforce systems into a cohesive platform while adding AI-powered automation that respects clinical workflows and regulatory requirements.
