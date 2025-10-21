# ToGo Platform Integration Guide

## Overview

ToGo is a unified clinical workforce management platform that consolidates three distinct healthcare workforce solutions while adding AI-powered automation and orchestration capabilities. This document details how the integrated systems work together and the technical integration points.

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

**Integration Points in ToGo**:

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
Med App API → ToGo Integration Layer
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

**Integration Points in ToGo**:

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
Core Schedule API → ToGo Integration Layer
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

**Integration Points in ToGo**:

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
myhealthPD API → ToGo Integration Layer
├── LTI 1.3 (Learning Tools Interoperability)
├── xAPI (Experience API) for learning records
├── RESTful API for course catalog
├── SCORM-compliant content delivery
└── Single Sign-On (SSO) via SAML 2.0
```

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

**Integration Points in ToGo**:

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
Verified Orchestration Platform → ToGo
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

**Integration Points in ToGo**:

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
Hospital EMR System → ToGo Integration Layer
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
- Shift assignments (Core Schedule → ToGo)
- New messages (Med App → ToGo)
- Course enrollments (myhealthPD → ToGo)
- Credential updates (Verified Orchestration → ToGo)
- Patient assignments (EMR → ToGo)

**Batch Sync** (Scheduled API calls):
- Historical timesheet data (Core Schedule)
- Training completion records (myhealthPD)
- Staff directory updates (Med App)
- Credential verification status (Verified Orchestration)

**On-Demand Queries**:
- EMR patient briefings (triggered by shift schedule)
- Real-time license verification (triggered by credential agent)
- Course catalog search (triggered by LMS agent)

---

## API Architecture

### ToGo Integration Layer

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

### ToGo Unified Data Model

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
- Immediate updates to ToGo database
- Conflict resolution via timestamp comparison

**2. Polling Sync** (fallback):
- Scheduled jobs every 5-15 minutes
- Incremental sync based on last_modified timestamps
- Full sync nightly during maintenance window

**3. Master Data Management**:
- Staff records: Med App is source of truth
- Shifts: Core Schedule is source of truth
- Learning: myhealthPD is source of truth
- ToGo maintains read replicas with enrichment (agent actions, preferences)

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
- **Payroll Systems**: ADP, Paychex integration for timesheet export
- **HR Systems**: Workday, BambooHR for employee lifecycle
- **Benefits Platforms**: Health insurance, retirement account sync

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

This integration architecture demonstrates how ToGo unifies disparate healthcare workforce systems into a cohesive platform while adding AI-powered automation that respects clinical workflows and regulatory requirements.
