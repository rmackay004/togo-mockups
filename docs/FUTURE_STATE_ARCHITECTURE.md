# Togo Health - Future State Modern Architecture

**Version**: 1.0
**Audience**: Technical stakeholders, integration partners (Verified Orchestration), investors
**Purpose**: High-level architectural overview of the production-ready Togo Health platform

---

## Executive Summary

Togo Health will be built as a **cloud-native, microservices-based platform** using modern web technologies and AI orchestration frameworks. The architecture prioritizes:

- **Scalability**: Handle 100,000+ clinicians across 500+ healthcare facilities
- **Reliability**: 99.9% uptime SLA with multi-region failover
- **Security**: HIPAA-compliant, SOC 2 Type II certified infrastructure
- **Extensibility**: Plugin architecture for new integrations (EMR, HR systems, etc.)
- **Developer Experience**: API-first design with comprehensive SDK support

**Core Technology Pillars**:
1. **Frontend**: React 18+ with TypeScript, Next.js for SSR/SSG
2. **Backend**: Node.js microservices with GraphQL Federation
3. **AI Layer**: Python-based agent orchestration with LangChain/LangGraph
4. **Integration**: Go-based integration services for high-performance external API calls
5. **Infrastructure**: Kubernetes on AWS with Terraform IaC

---

## Architecture Overview

### High-Level System Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                          CLIENT LAYER                                    │
├─────────────────────────────────────────────────────────────────────────┤
│  Web App (React/Next.js)  │  Mobile (React Native)  │  API Clients      │
└────────────────┬────────────────────────┬────────────────────┬──────────┘
                 │                        │                    │
                 └────────────────────────┼────────────────────┘
                                          │
                              ┌───────────▼───────────┐
                              │   CloudFront (CDN)    │
                              │   + WAF + DDoS        │
                              └───────────┬───────────┘
                                          │
┌─────────────────────────────────────────┼─────────────────────────────────┐
│                          API GATEWAY LAYER                                 │
├─────────────────────────────────────────┼─────────────────────────────────┤
│                    ┌────────────────────▼─────────────────────┐            │
│                    │  Kong API Gateway / AWS API Gateway      │            │
│                    │  - Authentication (JWT validation)       │            │
│                    │  - Rate limiting & throttling            │            │
│                    │  - Request routing & load balancing      │            │
│                    │  - Observability (logging, metrics)      │            │
│                    └────────────────────┬─────────────────────┘            │
└─────────────────────────────────────────┼─────────────────────────────────┘
                                          │
┌─────────────────────────────────────────┼─────────────────────────────────┐
│                      APPLICATION LAYER (Microservices)                     │
├─────────────────────────────────────────┼─────────────────────────────────┤
│                                         │                                  │
│  ┌──────────────────┐  ┌───────────────▼──────┐  ┌────────────────────┐  │
│  │   GraphQL API    │  │   REST API Services  │  │   WebSocket API    │  │
│  │   Federation     │  │   (Node.js/Express)  │  │   (Real-time)      │  │
│  │   (Apollo)       │  └──────────────────────┘  └────────────────────┘  │
│  └────────┬─────────┘                                                     │
│           │                                                               │
│  ┌────────▼─────────────────────────────────────────────────────────┐    │
│  │              CORE MICROSERVICES (Node.js + TypeScript)           │    │
│  ├──────────────────────────────────────────────────────────────────┤    │
│  │  • User Service (auth, profiles, preferences)                    │    │
│  │  • Staff Service (directory, roles, permissions)                 │    │
│  │  • Shift Service (scheduling, rostering, time tracking)          │    │
│  │  • Learning Service (courses, CPD, competencies)                 │    │
│  │  • Credential Service (licenses, certifications, verification)   │    │
│  │  • Communication Service (messages, notifications, announcements)│    │
│  │  • Compliance Service (regulatory tracking, audit logs)          │    │
│  │  • Analytics Service (reporting, dashboards, insights)           │    │
│  └──────────────────────────────────────────────────────────────────┘    │
│                                                                           │
│  ┌──────────────────────────────────────────────────────────────────┐    │
│  │         AI AGENT ORCHESTRATION LAYER (Python)                    │    │
│  ├──────────────────────────────────────────────────────────────────┤    │
│  │  Framework: LangChain + LangGraph + Temporal.io                  │    │
│  │                                                                   │    │
│  │  • Agent Orchestrator (workflow coordination)                    │    │
│  │  • Timesheet Agent (autonomous)                                  │    │
│  │  • Credential Agent (human-in-the-loop)                          │    │
│  │  • Shift Swap Agent (human-in-the-loop)                          │    │
│  │  • LMS Recommendation Agent (human-in-the-loop)                  │    │
│  │  • EMR Briefing Agent (human-on-the-loop)                        │    │
│  │  • Rostering Optimization Agent (human-on-the-loop)              │    │
│  │  • Compliance Monitoring Agent (human-on-the-loop)               │    │
│  │  • Notification Agent (autonomous)                               │    │
│  │  • Documentation Agent (autonomous)                              │    │
│  │  • Onboarding Agent (human-in-the-loop)                          │    │
│  │  • Email Categorization Agent (autonomous)                       │    │
│  │  • Emergency Coverage Agent (human-on-the-loop)                  │    │
│  │  • Analytics Agent (autonomous)                                  │    │
│  │  • Wellbeing Monitor Agent (human-in-the-loop)                   │    │
│  │  • Leave Management Agent (human-in-the-loop)                    │    │
│  │                                                                   │    │
│  │  LLM: Claude 3.5 Sonnet (Anthropic) via AWS Bedrock              │    │
│  │  Vector DB: Pinecone for semantic search & embeddings            │    │
│  └──────────────────────────────────────────────────────────────────┘    │
│                                                                           │
│  ┌──────────────────────────────────────────────────────────────────┐    │
│  │         INTEGRATION SERVICES (Go for performance)                │    │
│  ├──────────────────────────────────────────────────────────────────┤    │
│  │  • Med App Integration Service                                   │    │
│  │  • Core Schedule Integration Service                             │    │
│  │  • myhealthPD Integration Service                                │    │
│  │  • Time Filer Integration Service                                │    │
│  │  • My Digital Passport Integration Service                       │    │
│  │  • Verified Orchestration Integration Service                    │    │
│  │  • EMR Integration Service (Epic, Cerner, FHIR)                  │    │
│  │  • Payroll Integration Service                                   │    │
│  │                                                                   │    │
│  │  Pattern: Adapter pattern for each external system               │    │
│  │  Communication: gRPC for inter-service, REST for external APIs   │    │
│  └──────────────────────────────────────────────────────────────────┘    │
└───────────────────────────────────────────────────────────────────────────┘
                                          │
┌─────────────────────────────────────────┼─────────────────────────────────┐
│                          DATA LAYER                                        │
├─────────────────────────────────────────┼─────────────────────────────────┤
│                                         │                                  │
│  ┌──────────────────┐  ┌───────────────▼──────┐  ┌────────────────────┐  │
│  │   PostgreSQL     │  │   MongoDB (Document  │  │   Redis (Cache)    │  │
│  │   (Relational)   │  │   Store for Agents)  │  │   ElastiCache      │  │
│  │   Aurora RDS     │  │   DocumentDB         │  │                    │  │
│  └──────────────────┘  └──────────────────────┘  └────────────────────┘  │
│                                                                           │
│  ┌──────────────────┐  ┌──────────────────────┐  ┌────────────────────┐  │
│  │   Elasticsearch  │  │   S3 (Object Store)  │  │   Pinecone         │  │
│  │   (Search)       │  │   Documents, Assets  │  │   (Vector DB)      │  │
│  └──────────────────┘  └──────────────────────┘  └────────────────────┘  │
│                                                                           │
│  ┌──────────────────────────────────────────────────────────────────┐    │
│  │   Event Streaming: Apache Kafka / AWS Kinesis                    │    │
│  │   - Real-time shift updates                                      │    │
│  │   - Agent activity events                                        │    │
│  │   - Audit logs and compliance events                             │    │
│  └──────────────────────────────────────────────────────────────────┘    │
└───────────────────────────────────────────────────────────────────────────┘
                                          │
┌─────────────────────────────────────────┼─────────────────────────────────┐
│                   INFRASTRUCTURE & PLATFORM LAYER                          │
├─────────────────────────────────────────┼─────────────────────────────────┤
│                                         │                                  │
│  ┌──────────────────────────────────────▼──────────────────────────────┐  │
│  │   Kubernetes (EKS) - Container Orchestration                        │  │
│  │   - Auto-scaling (HPA, VPA)                                         │  │
│  │   - Service mesh (Istio for mTLS, traffic management)              │  │
│  │   - Helm charts for deployment                                     │  │
│  └─────────────────────────────────────────────────────────────────────┘  │
│                                                                           │
│  ┌──────────────────────────────────────────────────────────────────┐    │
│  │   Observability Stack                                            │    │
│  │   - Prometheus + Grafana (metrics)                               │    │
│  │   - ELK Stack (Elasticsearch, Logstash, Kibana) for logs         │    │
│  │   - Jaeger for distributed tracing                               │    │
│  │   - Datadog for APM and monitoring                               │    │
│  └──────────────────────────────────────────────────────────────────┘    │
│                                                                           │
│  ┌──────────────────────────────────────────────────────────────────┐    │
│  │   CI/CD Pipeline                                                 │    │
│  │   - GitHub Actions for CI                                        │    │
│  │   - ArgoCD for GitOps-based CD                                   │    │
│  │   - Container Registry: AWS ECR                                  │    │
│  │   - Infrastructure as Code: Terraform + AWS CDK                  │    │
│  └──────────────────────────────────────────────────────────────────┘    │
│                                                                           │
│  ┌──────────────────────────────────────────────────────────────────┐    │
│  │   Security & Compliance                                          │    │
│  │   - AWS WAF (Web Application Firewall)                           │    │
│  │   - AWS Shield (DDoS protection)                                 │    │
│  │   - Secrets Manager (AWS Secrets Manager / HashiCorp Vault)      │    │
│  │   - Encryption: KMS for data at rest, TLS 1.3 for transit        │    │
│  │   - HIPAA compliance controls                                    │    │
│  │   - SOC 2 Type II audit automation                               │    │
│  └──────────────────────────────────────────────────────────────────┘    │
└───────────────────────────────────────────────────────────────────────────┘
```

---

## Frontend Architecture

### Technology Stack

**Core Framework**: React 18 with TypeScript
**Meta-Framework**: Next.js 14+ (App Router)
**State Management**: Zustand + React Query (TanStack Query)
**Styling**: Tailwind CSS + shadcn/ui component library
**Forms**: React Hook Form + Zod validation
**Charts & Visualizations**: Recharts + D3.js
**Real-time**: Socket.io client for WebSocket connections
**Mobile**: React Native with Expo (iOS/Android)

### Frontend Architecture Pattern

**Micro-Frontend Architecture** using Module Federation:
- **Clinician App**: Dashboard, shifts, learning, credentials
- **Admin App**: Workforce management, compliance, analytics
- **Shared Components**: Design system, authentication, common utilities

```
togo-health-frontend/
├── apps/
│   ├── clinician-portal/          # Next.js app for clinicians
│   │   ├── app/                   # Next.js 14 App Router
│   │   │   ├── (dashboard)/       # Dashboard routes
│   │   │   ├── (shifts)/          # Shift management routes
│   │   │   ├── (learning)/        # Learning routes
│   │   │   ├── (profile)/         # Profile & credentials routes
│   │   │   └── api/               # API routes (BFF pattern)
│   │   ├── components/            # Page-specific components
│   │   ├── hooks/                 # Custom React hooks
│   │   └── lib/                   # Utilities
│   │
│   ├── admin-portal/              # Next.js app for administrators
│   │   ├── app/
│   │   │   ├── (workforce)/       # Staff management
│   │   │   ├── (rostering)/       # Schedule optimization
│   │   │   ├── (compliance)/      # Compliance monitoring
│   │   │   ├── (analytics)/       # Reporting & analytics
│   │   │   └── api/
│   │   └── ...
│   │
│   └── mobile-app/                # React Native app
│       ├── src/
│       │   ├── screens/
│       │   ├── navigation/
│       │   ├── components/
│       │   └── hooks/
│       └── app.json
│
├── packages/
│   ├── ui/                        # Shared UI component library
│   │   ├── components/            # shadcn/ui + custom components
│   │   │   ├── Button/
│   │   │   ├── Card/
│   │   │   ├── AgentActivityFeed/
│   │   │   ├── ShiftCalendar/
│   │   │   └── ...
│   │   ├── hooks/
│   │   └── styles/
│   │
│   ├── api-client/                # TypeScript SDK for API
│   │   ├── graphql/               # GraphQL client (Apollo)
│   │   ├── rest/                  # REST client (Axios)
│   │   ├── types/                 # Generated TypeScript types
│   │   └── hooks/                 # React Query hooks
│   │
│   ├── auth/                      # Authentication utilities
│   │   ├── providers/
│   │   ├── hooks/
│   │   └── verified-orchestration/ # VO SSO integration
│   │
│   └── shared/                    # Shared utilities
│       ├── types/
│       ├── utils/
│       └── constants/
│
├── turbo.json                     # Turborepo configuration
├── package.json
└── tsconfig.json
```

### Key Frontend Features

**1. Real-Time Updates**
- WebSocket connection for live shift updates, agent notifications
- Optimistic UI updates with React Query mutations
- Server-Sent Events (SSE) for agent activity feed

**2. Offline Support**
- Service Workers for offline functionality
- IndexedDB for local data caching
- Background sync for form submissions

**3. Performance Optimization**
- Code splitting and lazy loading
- Image optimization (Next.js Image component)
- Edge caching via CloudFront
- React Server Components for reduced bundle size

**4. Accessibility**
- WCAG 2.1 AA compliance
- Keyboard navigation
- Screen reader support
- ARIA labels and landmarks

**5. Responsive Design**
- Mobile-first approach
- Breakpoints: mobile (320px+), tablet (768px+), desktop (1024px+), wide (1440px+)
- Progressive Web App (PWA) support

---

## Backend Architecture

### Technology Stack

**Core Runtime**: Node.js 20 LTS with TypeScript
**API Framework**: Express.js + Apollo Server (GraphQL)
**ORM**: Prisma (PostgreSQL) + Mongoose (MongoDB)
**Message Queue**: AWS SQS + SNS for async tasks
**Workflow Engine**: Temporal.io for durable workflows
**Authentication**: Passport.js + JWT + Verified Orchestration SSO
**Testing**: Jest + Supertest + Playwright

### Microservices Architecture

Each microservice follows **Domain-Driven Design (DDD)** principles:

```
togo-health-backend/
├── services/
│   ├── user-service/
│   │   ├── src/
│   │   │   ├── domain/              # Domain models and business logic
│   │   │   │   ├── entities/
│   │   │   │   ├── value-objects/
│   │   │   │   └── repositories/
│   │   │   ├── application/         # Use cases and application services
│   │   │   │   ├── commands/
│   │   │   │   ├── queries/
│   │   │   │   └── handlers/
│   │   │   ├── infrastructure/      # External dependencies
│   │   │   │   ├── database/
│   │   │   │   ├── cache/
│   │   │   │   └── messaging/
│   │   │   ├── interfaces/          # API controllers
│   │   │   │   ├── http/            # REST/GraphQL endpoints
│   │   │   │   ├── grpc/            # gRPC services
│   │   │   │   └── events/          # Event handlers
│   │   │   └── index.ts
│   │   ├── prisma/                  # Database schema
│   │   ├── tests/
│   │   ├── Dockerfile
│   │   └── package.json
│   │
│   ├── staff-service/
│   ├── shift-service/
│   ├── learning-service/
│   ├── credential-service/
│   ├── communication-service/
│   ├── compliance-service/
│   └── analytics-service/
│
├── graphql-gateway/                 # Apollo Federation Gateway
│   ├── src/
│   │   ├── schemas/                 # Federated schema composition
│   │   ├── resolvers/
│   │   ├── datasources/
│   │   └── index.ts
│   └── package.json
│
├── shared/
│   ├── types/                       # Shared TypeScript types
│   ├── utils/                       # Common utilities
│   ├── middleware/                  # Shared Express middleware
│   └── events/                      # Event schemas
│
└── infrastructure/
    ├── database/
    │   └── migrations/
    ├── kubernetes/                  # K8s manifests
    └── terraform/                   # IaC for AWS resources
```

### API Layer Design

**GraphQL Federation** for unified API:
- Each microservice exposes its own GraphQL schema
- Apollo Gateway composes schemas into single graph
- Clients query unified API, gateway routes to appropriate services

**Example Schema (Staff Service)**:
```graphql
type Staff @key(fields: "id") {
  id: ID!
  firstName: String!
  lastName: String!
  email: String!
  role: StaffRole!
  department: Department!
  credentials: [Credential!]!
  shifts: [Shift!]!
  learningRecords: [LearningRecord!]!
  digitalPassport: DigitalPassport
}

extend type Query {
  staff(id: ID!): Staff
  allStaff(filter: StaffFilter, pagination: Pagination): StaffConnection!
}

extend type Mutation {
  updateStaffProfile(input: UpdateStaffInput!): Staff!
  assignShift(staffId: ID!, shiftId: ID!): Shift!
}

extend type Subscription {
  staffUpdated(staffId: ID!): Staff!
}
```

**REST API** for simple CRUD operations and external integrations:
- RESTful endpoints following OpenAPI 3.0 spec
- Versioned API (v1, v2) for backward compatibility
- Pagination, filtering, sorting support
- HATEOAS links for resource discoverability

### Authentication & Authorization

**Multi-Layered Security**:

1. **API Gateway Level**:
   - JWT validation (RS256 signing)
   - Rate limiting by IP and user
   - Request/response logging

2. **Service Level**:
   - Role-Based Access Control (RBAC)
   - Attribute-Based Access Control (ABAC) for patient data
   - Scope validation (OAuth 2.0 scopes)

3. **Data Level**:
   - Row-Level Security (RLS) in PostgreSQL
   - Field-level permissions in GraphQL
   - Audit logging for all data access

**Integration with Verified Orchestration**:
```typescript
// Verified Orchestration SSO flow
class VerifiedOrchestrationAuthProvider {
  async authenticate(code: string): Promise<User> {
    // Exchange authorization code for tokens
    const tokens = await this.exchangeCode(code);

    // Verify ID token with VO public key
    const claims = await this.verifyIdToken(tokens.id_token);

    // Fetch user profile from VO
    const voProfile = await this.fetchUserProfile(tokens.access_token);

    // Create or update user in Togo Health database
    const user = await this.upsertUser(voProfile);

    // Generate Togo Health JWT
    const jwt = this.generateJWT(user);

    return { user, jwt };
  }

  async verifyCredential(credentialId: string): Promise<CredentialStatus> {
    // Query VO API for real-time credential verification
    return await this.voClient.verifyCredential(credentialId);
  }
}
```

### Data Access Patterns

**Repository Pattern** for database abstraction:
```typescript
// Domain Repository Interface
interface IStaffRepository {
  findById(id: string): Promise<Staff | null>;
  findByEmail(email: string): Promise<Staff | null>;
  create(staff: CreateStaffDTO): Promise<Staff>;
  update(id: string, data: UpdateStaffDTO): Promise<Staff>;
  delete(id: string): Promise<void>;
}

// Implementation using Prisma
class PrismaStaffRepository implements IStaffRepository {
  constructor(private prisma: PrismaClient) {}

  async findById(id: string): Promise<Staff | null> {
    const staffData = await this.prisma.staff.findUnique({
      where: { id },
      include: {
        credentials: true,
        shifts: true,
        learningRecords: true,
      },
    });

    return staffData ? this.toDomain(staffData) : null;
  }

  private toDomain(data: PrismaStaff): Staff {
    // Map database model to domain entity
    return new Staff({
      id: data.id,
      firstName: data.firstName,
      lastName: data.lastName,
      // ... map other fields
    });
  }
}
```

**Caching Strategy**:
- **L1 Cache**: In-memory cache (Node.js Map) for request-scoped data
- **L2 Cache**: Redis for cross-request, cross-service caching
- **Cache-aside pattern**: Check cache → miss → fetch from DB → populate cache
- **TTL policies**: Short-lived (5min) for frequently changing data, long-lived (1hr+) for static data
- **Cache invalidation**: Event-driven invalidation on mutations

**Event Sourcing for Audit Trail**:
```typescript
// Event schema for compliance
interface StaffCredentialUpdatedEvent {
  eventId: string;
  eventType: 'StaffCredentialUpdated';
  aggregateId: string; // staffId
  timestamp: Date;
  userId: string; // who made the change
  data: {
    credentialId: string;
    previousExpiryDate: Date;
    newExpiryDate: Date;
    updatedBy: 'agent' | 'user';
  };
  metadata: {
    ipAddress: string;
    userAgent: string;
  };
}

// Store all events in append-only log
await eventStore.append(event);

// Query audit trail
const history = await eventStore.getEvents({ aggregateId: staffId });
```

---

## AI Agent Orchestration Layer

### Technology Stack

**Runtime**: Python 3.11+
**Framework**: LangChain + LangGraph for agent workflows
**Workflow Engine**: Temporal.io for durable execution
**LLM**: Claude 3.5 Sonnet via AWS Bedrock (Anthropic)
**Vector Database**: Pinecone for embeddings and semantic search
**Message Queue**: RabbitMQ for agent-to-agent communication
**Monitoring**: LangSmith for LLM observability

### Agent Architecture

**Multi-Agent System** with specialized agents:

```python
# Agent architecture using LangGraph
from langgraph.graph import StateGraph, END
from langchain_anthropic import ChatAnthropic

# Define agent state
class AgentState(TypedDict):
    input: str
    context: dict
    workflow_type: Literal["autonomous", "human_in_loop", "human_on_loop"]
    approval_status: Optional[str]
    execution_result: Optional[dict]
    error: Optional[str]

# Orchestrator graph
class AgentOrchestrator:
    def __init__(self):
        self.llm = ChatAnthropic(model="claude-3-5-sonnet-20241022")
        self.graph = self.build_graph()

    def build_graph(self) -> StateGraph:
        workflow = StateGraph(AgentState)

        # Add nodes
        workflow.add_node("classify_task", self.classify_task)
        workflow.add_node("route_to_agent", self.route_to_agent)
        workflow.add_node("execute_autonomous", self.execute_autonomous)
        workflow.add_node("request_approval", self.request_approval)
        workflow.add_node("execute_with_approval", self.execute_with_approval)
        workflow.add_node("notify_human", self.notify_human)
        workflow.add_node("log_audit", self.log_audit)

        # Add edges
        workflow.set_entry_point("classify_task")
        workflow.add_conditional_edges(
            "route_to_agent",
            self.determine_workflow_type,
            {
                "autonomous": "execute_autonomous",
                "human_in_loop": "request_approval",
                "human_on_loop": "notify_human",
            }
        )
        workflow.add_edge("execute_autonomous", "log_audit")
        workflow.add_edge("request_approval", "execute_with_approval")
        workflow.add_edge("execute_with_approval", "log_audit")
        workflow.add_edge("notify_human", "execute_autonomous")
        workflow.add_edge("log_audit", END)

        return workflow.compile()

    async def classify_task(self, state: AgentState) -> AgentState:
        # Use LLM to classify incoming task
        response = await self.llm.ainvoke([
            ("system", "Classify this healthcare workforce task and determine which agent should handle it."),
            ("user", state["input"])
        ])

        state["context"] = response.task_classification
        return state

    async def execute_autonomous(self, state: AgentState) -> AgentState:
        # Execute task immediately without human approval
        agent = self.get_agent(state["context"]["agent_type"])
        result = await agent.execute(state["input"])
        state["execution_result"] = result
        return state

# Specialized agent example: Timesheet Agent
class TimesheetAgent:
    def __init__(self):
        self.llm = ChatAnthropic(model="claude-3-5-sonnet-20241022")
        self.tools = [
            self.fetch_shift_data,
            self.calculate_hours,
            self.apply_award_rates,
            self.submit_to_time_filer
        ]

    async def execute(self, shift_data: dict) -> dict:
        """
        Autonomous workflow:
        1. Fetch completed shifts from Core Schedule
        2. Calculate total hours
        3. Apply award interpretation from Time Filer
        4. Submit timesheet
        5. Notify clinician
        """
        # Create agent chain
        agent = create_react_agent(self.llm, self.tools)

        result = await agent.ainvoke({
            "input": f"Process timesheet for week ending {shift_data['week_ending']}",
            "shifts": shift_data["shifts"]
        })

        return result

# Human-in-the-Loop example: Credential Agent
class CredentialAgent:
    async def execute(self, credential_renewal: dict) -> dict:
        """
        Human-in-the-Loop workflow:
        1. Detect expiring credential
        2. Pre-fill renewal application
        3. Wait for clinician approval
        4. Submit approved application
        5. Update credential records
        """
        # Step 1-2: Prepare recommendation
        recommendation = await self.prepare_renewal(credential_renewal)

        # Step 3: Request approval (blocks until human responds)
        approval = await self.request_approval(
            user_id=credential_renewal["staff_id"],
            recommendation=recommendation,
            timeout_hours=48
        )

        if approval.status == "approved":
            # Step 4-5: Execute approved action
            result = await self.submit_renewal(recommendation, approval.modifications)
            return result
        else:
            return {"status": "rejected", "reason": approval.reason}

# Human-on-the-Loop example: EMR Briefing Agent
class EMRBriefingAgent:
    async def execute(self, shift_assignment: dict) -> dict:
        """
        Human-on-the-Loop workflow:
        1. Fetch patient assignments from EMR (Epic/Cerner)
        2. Generate pre-shift briefing
        3. Deliver briefing to clinician
        4. Allow clinician to override/request more detail
        """
        # Step 1-2: Fetch and generate briefing (executes immediately)
        patients = await self.fetch_patient_assignments(shift_assignment)
        briefing = await self.generate_briefing(patients)

        # Step 3: Deliver to clinician (non-blocking)
        await self.deliver_briefing(
            user_id=shift_assignment["staff_id"],
            briefing=briefing,
            allow_override=True
        )

        # Step 4: Monitor for override requests
        await self.monitor_for_overrides(shift_assignment["staff_id"], briefing_id)

        return {"status": "delivered", "briefing_id": briefing.id}
```

### Temporal.io for Durable Workflows

**Why Temporal?**
- Workflows survive process crashes and restarts
- Built-in retry logic with exponential backoff
- Long-running workflows (hours, days, weeks)
- Activity timeouts and compensation logic
- Workflow versioning for zero-downtime updates

**Example Workflow**:
```python
from temporalio import workflow, activity
from datetime import timedelta

@workflow.defn
class CredentialRenewalWorkflow:
    @workflow.run
    async def run(self, credential_id: str) -> str:
        # Step 1: Check credential expiry (60 days before)
        credential = await workflow.execute_activity(
            fetch_credential,
            credential_id,
            start_to_close_timeout=timedelta(seconds=30),
        )

        if not credential.is_expiring_soon():
            return "not_expiring"

        # Step 2: Pre-fill renewal application
        application = await workflow.execute_activity(
            prefill_renewal_application,
            credential,
            start_to_close_timeout=timedelta(minutes=5),
        )

        # Step 3: Wait for human approval (up to 14 days)
        approval = await workflow.wait_condition(
            lambda: self.approval_received,
            timeout=timedelta(days=14)
        )

        if not approval:
            # Timeout: send escalation
            await workflow.execute_activity(
                send_escalation_notification,
                credential.staff_id,
            )
            return "approval_timeout"

        # Step 4: Submit renewal
        result = await workflow.execute_activity(
            submit_renewal,
            application,
            start_to_close_timeout=timedelta(minutes=10),
        )

        # Step 5: Update records
        await workflow.execute_activity(
            update_credential_record,
            credential_id,
            result.new_expiry_date,
        )

        return "renewal_completed"

    @workflow.signal
    def approve_renewal(self, approval_data: dict):
        self.approval_received = approval_data
```

### LLM Integration via AWS Bedrock

**Why AWS Bedrock?**
- Managed Claude 3.5 Sonnet access (no API key management)
- HIPAA-eligible with BAA
- Lower latency (AWS network)
- Built-in content moderation
- Usage tracking and billing integration

```python
import boto3
from langchain_aws import ChatBedrock

class BedrockLLMProvider:
    def __init__(self):
        self.client = boto3.client('bedrock-runtime', region_name='us-west-2')
        self.model = ChatBedrock(
            model_id="anthropic.claude-3-5-sonnet-20241022-v2:0",
            client=self.client,
            model_kwargs={
                "max_tokens": 4096,
                "temperature": 0.0,  # Deterministic for healthcare
                "top_p": 1.0,
            }
        )

    async def generate_shift_briefing(self, patient_data: list) -> str:
        """Generate pre-shift patient briefing"""
        prompt = f"""You are a clinical AI assistant preparing a pre-shift briefing for a nurse.

Patient Census:
{json.dumps(patient_data, indent=2)}

Generate a concise briefing that includes:
1. Patient count and acuity overview
2. Key alerts and critical information
3. Medication schedules requiring attention
4. Recent changes to patient conditions

Format as bullet points. Be clear and actionable."""

        response = await self.model.ainvoke(prompt)
        return response.content
```

### Vector Database for Semantic Search

**Pinecone Integration**:
```python
from pinecone import Pinecone
from langchain_openai import OpenAIEmbeddings

class KnowledgeGraphSearch:
    def __init__(self):
        self.pc = Pinecone(api_key=os.getenv("PINECONE_API_KEY"))
        self.index = self.pc.Index("togo-health-knowledge")
        self.embeddings = OpenAIEmbeddings()

    async def find_similar_credentials(self, query: str, top_k: int = 5):
        """Find similar credentials using semantic search"""
        # Generate embedding for query
        query_embedding = await self.embeddings.aembed_query(query)

        # Search Pinecone
        results = self.index.query(
            vector=query_embedding,
            top_k=top_k,
            include_metadata=True,
            namespace="credentials"
        )

        return results.matches

    async def recommend_courses(self, clinical_cases: list) -> list:
        """Recommend learning courses based on recent clinical work"""
        # Embed recent clinical case descriptions
        case_text = " ".join([case["description"] for case in clinical_cases])
        case_embedding = await self.embeddings.aembed_query(case_text)

        # Find similar courses
        results = self.index.query(
            vector=case_embedding,
            top_k=10,
            include_metadata=True,
            namespace="learning_courses"
        )

        return [match.metadata for match in results.matches]
```

---

## Integration Layer

### Technology Stack

**Runtime**: Go 1.21+
**Framework**: Gin (HTTP), gRPC-Go
**HTTP Client**: Resty
**Message Broker**: RabbitMQ
**Circuit Breaker**: hystrix-go
**Observability**: OpenTelemetry

### Integration Services Architecture

**Adapter Pattern** for each external system:

```
integration-services/
├── med-app-adapter/
│   ├── internal/
│   │   ├── handler/         # HTTP/gRPC handlers
│   │   ├── service/         # Business logic
│   │   ├── client/          # Med App API client
│   │   ├── mapper/          # Data transformation
│   │   └── repository/      # Database operations
│   ├── pkg/
│   │   └── medapp/          # Shared Med App types
│   ├── cmd/
│   │   └── server/
│   │       └── main.go
│   └── go.mod
│
├── core-schedule-adapter/
├── myhealthpd-adapter/
├── time-filer-adapter/
├── digital-passport-adapter/
├── verified-orchestration-adapter/
├── emr-adapter/                # Epic, Cerner, FHIR
└── shared/
    ├── auth/                   # OAuth 2.0 client
    ├── retry/                  # Retry logic
    ├── circuit/                # Circuit breaker
    └── telemetry/              # Observability
```

**Example Integration Service (Time Filer Adapter)**:

```go
package main

import (
    "context"
    "fmt"
    "time"

    "github.com/gin-gonic/gin"
    "github.com/afex/hystrix-go/hystrix"
)

// TimeFilerClient handles API communication with Time Filer
type TimeFilerClient struct {
    baseURL    string
    apiKey     string
    httpClient *resty.Client
}

// SubmitTimesheet submits a timesheet to Time Filer with circuit breaker
func (c *TimeFilerClient) SubmitTimesheet(ctx context.Context, timesheet *Timesheet) (*TimesheetResponse, error) {
    output := make(chan *TimesheetResponse, 1)
    errors := hystrix.Go("submit_timesheet", func() error {
        // Main execution path
        resp, err := c.httpClient.R().
            SetContext(ctx).
            SetHeader("Authorization", fmt.Sprintf("Bearer %s", c.apiKey)).
            SetBody(timesheet).
            SetResult(&TimesheetResponse{}).
            Post(c.baseURL + "/api/v1/timesheets")

        if err != nil {
            return err
        }

        if resp.IsError() {
            return fmt.Errorf("time filer API error: %d", resp.StatusCode())
        }

        output <- resp.Result().(*TimesheetResponse)
        return nil
    }, func(err error) error {
        // Fallback: queue for retry
        return c.queueForRetry(timesheet)
    })

    select {
    case result := <-output:
        return result, nil
    case err := <-errors:
        return nil, err
    case <-ctx.Done():
        return nil, ctx.Err()
    }
}

// gRPC service for inter-service communication
type TimeFilerService struct {
    timefiler.UnimplementedTimeFilerServiceServer
    client *TimeFilerClient
}

func (s *TimeFilerService) SubmitTimesheet(ctx context.Context, req *timefiler.SubmitTimesheetRequest) (*timefiler.SubmitTimesheetResponse, error) {
    // Map gRPC request to Time Filer API format
    timesheet := s.mapToTimeFilerFormat(req)

    // Submit with retry logic
    result, err := s.client.SubmitTimesheet(ctx, timesheet)
    if err != nil {
        return nil, status.Errorf(codes.Internal, "failed to submit timesheet: %v", err)
    }

    // Map response back to gRPC
    return &timefiler.SubmitTimesheetResponse{
        TimesheetId: result.ID,
        Status:      result.Status,
        SubmittedAt: timestamppb.New(result.SubmittedAt),
    }, nil
}
```

**Integration with My Digital Passport**:

```go
// DigitalPassportClient integrates with My Digital Passport API
type DigitalPassportClient struct {
    baseURL    string
    oauthClient *oauth2.Client
}

// FetchPassport retrieves a clinician's digital passport
func (c *DigitalPassportClient) FetchPassport(ctx context.Context, clinicianID string, scope []string) (*DigitalPassport, error) {
    // 1. Check if clinician has granted access to Togo Health
    permission, err := c.checkSharingPermission(ctx, clinicianID)
    if err != nil {
        return nil, err
    }

    if !permission.Granted {
        return nil, ErrPermissionNotGranted
    }

    // 2. Fetch passport data with scoped access
    passport := &DigitalPassport{}
    resp, err := c.httpClient.R().
        SetContext(ctx).
        SetAuthToken(c.accessToken).
        SetQueryParam("scope", strings.Join(scope, ",")).
        SetResult(passport).
        Get(fmt.Sprintf("%s/api/v2/passports/%s", c.baseURL, clinicianID))

    if err != nil {
        return nil, err
    }

    // 3. Verify blockchain-backed credentials
    for i, cred := range passport.Credentials {
        verified, err := c.verifyCredentialOnChain(cred.VerificationHash)
        if err != nil {
            log.Printf("failed to verify credential %s: %v", cred.ID, err)
        }
        passport.Credentials[i].BlockchainVerified = verified
    }

    return passport, nil
}

// SyncPassportData syncs Digital Passport data to Togo Health database
func (c *DigitalPassportClient) SyncPassportData(ctx context.Context, passport *DigitalPassport) error {
    // Use Temporal workflow for reliable sync
    workflowOptions := client.StartWorkflowOptions{
        ID:        fmt.Sprintf("sync-passport-%s", passport.ClinicianID),
        TaskQueue: "digital-passport-sync",
    }

    we, err := c.temporalClient.ExecuteWorkflow(
        ctx,
        workflowOptions,
        "SyncDigitalPassportWorkflow",
        passport,
    )

    if err != nil {
        return err
    }

    // Wait for sync to complete (or timeout after 5 minutes)
    ctx, cancel := context.WithTimeout(ctx, 5*time.Minute)
    defer cancel()

    var result SyncResult
    err = we.Get(ctx, &result)
    return err
}
```

**Integration with Verified Orchestration**:

```go
// VerifiedOrchestrationClient handles SSO and credential verification
type VerifiedOrchestrationClient struct {
    baseURL      string
    clientID     string
    clientSecret string
    oidcProvider *oidc.Provider
}

// AuthenticateUser handles OIDC authentication flow
func (c *VerifiedOrchestrationClient) AuthenticateUser(ctx context.Context, authCode string) (*User, error) {
    // Exchange authorization code for tokens
    oauth2Config := c.oidcProvider.OAuth2Config()
    token, err := oauth2Config.Exchange(ctx, authCode)
    if err != nil {
        return nil, fmt.Errorf("failed to exchange code: %w", err)
    }

    // Verify ID token
    idToken, err := c.oidcProvider.Verifier(&oidc.Config{ClientID: c.clientID}).Verify(ctx, token.Extra("id_token").(string))
    if err != nil {
        return nil, fmt.Errorf("failed to verify ID token: %w", err)
    }

    // Extract claims
    var claims struct {
        Email             string `json:"email"`
        EmailVerified     bool   `json:"email_verified"`
        GivenName         string `json:"given_name"`
        FamilyName        string `json:"family_name"`
        CredentialSubject string `json:"credential_subject"`
    }
    if err := idToken.Claims(&claims); err != nil {
        return nil, err
    }

    // Fetch full user profile from VO API
    userProfile, err := c.fetchUserProfile(ctx, token.AccessToken)
    if err != nil {
        return nil, err
    }

    return &User{
        VOSubject:     claims.CredentialSubject,
        Email:         claims.Email,
        FirstName:     claims.GivenName,
        LastName:      claims.FamilyName,
        Credentials:   userProfile.Credentials,
        BiometricAuth: userProfile.BiometricEnabled,
    }, nil
}

// VerifyCredential checks credential status in real-time
func (c *VerifiedOrchestrationClient) VerifyCredential(ctx context.Context, credentialID string) (*CredentialStatus, error) {
    status := &CredentialStatus{}

    resp, err := c.httpClient.R().
        SetContext(ctx).
        SetAuthToken(c.getServiceToken()).
        SetResult(status).
        Get(fmt.Sprintf("%s/api/v2/credentials/%s/verify", c.baseURL, credentialID))

    if err != nil {
        return nil, err
    }

    if resp.IsError() {
        return nil, fmt.Errorf("verification failed: %d", resp.StatusCode())
    }

    return status, nil
}
```

### Message Queue for Async Integration

**RabbitMQ for event-driven integration**:

```go
// Event publisher
type EventPublisher struct {
    conn    *amqp.Connection
    channel *amqp.Channel
}

func (p *EventPublisher) PublishCredentialUpdated(ctx context.Context, event *CredentialUpdatedEvent) error {
    body, err := json.Marshal(event)
    if err != nil {
        return err
    }

    return p.channel.PublishWithContext(
        ctx,
        "togo.events",              // exchange
        "credential.updated",        // routing key
        false,                       // mandatory
        false,                       // immediate
        amqp.Publishing{
            ContentType:  "application/json",
            Body:         body,
            DeliveryMode: amqp.Persistent,
            Timestamp:    time.Now(),
        },
    )
}

// Event consumer
type CredentialEventConsumer struct {
    channel      *amqp.Channel
    agentService *AgentOrchestrator
}

func (c *CredentialEventConsumer) Start(ctx context.Context) error {
    msgs, err := c.channel.Consume(
        "credential-events-queue",
        "credential-consumer",
        false, // auto-ack
        false, // exclusive
        false, // no-local
        false, // no-wait
        nil,   // args
    )
    if err != nil {
        return err
    }

    for {
        select {
        case msg := <-msgs:
            if err := c.handleMessage(msg); err != nil {
                log.Printf("failed to handle message: %v", err)
                msg.Nack(false, true) // requeue
            } else {
                msg.Ack(false)
            }
        case <-ctx.Done():
            return ctx.Err()
        }
    }
}

func (c *CredentialEventConsumer) handleMessage(msg amqp.Delivery) error {
    var event CredentialUpdatedEvent
    if err := json.Unmarshal(msg.Body, &event); err != nil {
        return err
    }

    // Trigger Credential Agent workflow
    return c.agentService.TriggerCredentialCheck(event.StaffID, event.CredentialID)
}
```

---

## Infrastructure & DevOps

### Container Orchestration (Kubernetes)

**EKS Architecture**:

```yaml
# Kubernetes namespace structure
apiVersion: v1
kind: Namespace
metadata:
  name: togo-production
  labels:
    environment: production
    compliance: hipaa

---
# Example deployment: Staff Service
apiVersion: apps/v1
kind: Deployment
metadata:
  name: staff-service
  namespace: togo-production
spec:
  replicas: 3
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0
  selector:
    matchLabels:
      app: staff-service
  template:
    metadata:
      labels:
        app: staff-service
        version: v1.2.0
    spec:
      serviceAccountName: staff-service-sa
      containers:
      - name: staff-service
        image: 123456789.dkr.ecr.us-west-2.amazonaws.com/togo/staff-service:v1.2.0
        ports:
        - containerPort: 3000
          name: http
        - containerPort: 9090
          name: metrics
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef:
              name: db-credentials
              key: connection-string
        - name: VERIFIED_ORCHESTRATION_CLIENT_ID
          valueFrom:
            secretKeyRef:
              name: vo-credentials
              key: client-id
        resources:
          requests:
            cpu: 200m
            memory: 512Mi
          limits:
            cpu: 1000m
            memory: 1Gi
        livenessProbe:
          httpGet:
            path: /health
            port: 3000
          initialDelaySeconds: 30
          periodSeconds: 10
        readinessProbe:
          httpGet:
            path: /ready
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 5

---
# Horizontal Pod Autoscaler
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: staff-service-hpa
  namespace: togo-production
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: staff-service
  minReplicas: 3
  maxReplicas: 20
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 80

---
# Service mesh (Istio) for mTLS
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: staff-service
  namespace: togo-production
spec:
  hosts:
  - staff-service
  http:
  - match:
    - headers:
        x-api-version:
          exact: v1
    route:
    - destination:
        host: staff-service
        subset: v1
  - route:
    - destination:
        host: staff-service
        subset: v2
```

### CI/CD Pipeline

**GitHub Actions → ArgoCD GitOps**:

```yaml
# .github/workflows/ci-cd.yml
name: CI/CD Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'

      - name: Install dependencies
        run: npm ci

      - name: Run linting
        run: npm run lint

      - name: Run unit tests
        run: npm run test:unit

      - name: Run integration tests
        run: npm run test:integration

      - name: Upload coverage
        uses: codecov/codecov-action@v3

  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Run Trivy vulnerability scanner
        uses: aquasecurity/trivy-action@master
        with:
          scan-type: 'fs'
          scan-ref: '.'
          format: 'sarif'
          output: 'trivy-results.sarif'

      - name: Upload to GitHub Security
        uses: github/codeql-action/upload-sarif@v2
        with:
          sarif_file: 'trivy-results.sarif'

  build-and-push:
    needs: [test, security-scan]
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    steps:
      - uses: actions/checkout@v4

      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-west-2

      - name: Login to Amazon ECR
        id: login-ecr
        uses: aws-actions/amazon-ecr-login@v2

      - name: Build, tag, and push image
        env:
          ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
          ECR_REPOSITORY: togo/staff-service
          IMAGE_TAG: ${{ github.sha }}
        run: |
          docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
          docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
          docker tag $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG $ECR_REGISTRY/$ECR_REPOSITORY:latest
          docker push $ECR_REGISTRY/$ECR_REPOSITORY:latest

      - name: Update GitOps repo
        run: |
          git clone https://github.com/togo-health/gitops.git
          cd gitops
          yq eval '.spec.template.spec.containers[0].image = "${{ steps.login-ecr.outputs.registry }}/togo/staff-service:${{ github.sha }}"' -i overlays/production/staff-service-deployment.yaml
          git commit -am "Update staff-service to ${{ github.sha }}"
          git push
```

**ArgoCD Application**:

```yaml
# ArgoCD application definition
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: togo-production
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/togo-health/gitops.git
    targetRevision: main
    path: overlays/production
  destination:
    server: https://kubernetes.default.svc
    namespace: togo-production
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
    - CreateNamespace=true
    retry:
      limit: 5
      backoff:
        duration: 5s
        factor: 2
        maxDuration: 3m
```

### Infrastructure as Code (Terraform)

```hcl
# terraform/main.tf
terraform {
  required_version = ">= 1.5"

  backend "s3" {
    bucket         = "togo-health-terraform-state"
    key            = "production/terraform.tfstate"
    region         = "us-west-2"
    encrypt        = true
    dynamodb_table = "terraform-state-lock"
  }

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
    kubernetes = {
      source  = "hashicorp/kubernetes"
      version = "~> 2.23"
    }
  }
}

# VPC and Networking
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "~> 5.0"

  name = "togo-production-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["us-west-2a", "us-west-2b", "us-west-2c"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  public_subnets  = ["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]

  enable_nat_gateway   = true
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Environment = "production"
    Project     = "togo-health"
    Compliance  = "hipaa"
  }
}

# EKS Cluster
module "eks" {
  source  = "terraform-aws-modules/eks/aws"
  version = "~> 19.0"

  cluster_name    = "togo-production-eks"
  cluster_version = "1.28"

  vpc_id     = module.vpc.vpc_id
  subnet_ids = module.vpc.private_subnets

  cluster_endpoint_public_access = true

  eks_managed_node_groups = {
    general = {
      min_size     = 3
      max_size     = 10
      desired_size = 5

      instance_types = ["m5.xlarge"]
      capacity_type  = "ON_DEMAND"

      labels = {
        role = "general"
      }

      taints = []
    }

    agents = {
      min_size     = 2
      max_size     = 20
      desired_size = 5

      instance_types = ["c5.2xlarge"]  # CPU-optimized for AI agents
      capacity_type  = "SPOT"

      labels = {
        role = "ai-agents"
      }

      taints = [{
        key    = "workload"
        value  = "ai-agents"
        effect = "NoSchedule"
      }]
    }
  }

  tags = {
    Environment = "production"
    Project     = "togo-health"
  }
}

# RDS Aurora PostgreSQL
module "aurora" {
  source  = "terraform-aws-modules/rds-aurora/aws"
  version = "~> 8.0"

  name           = "togo-production-db"
  engine         = "aurora-postgresql"
  engine_version = "15.3"

  vpc_id  = module.vpc.vpc_id
  subnets = module.vpc.private_subnets

  instances = {
    writer = {
      instance_class      = "db.r6g.xlarge"
      publicly_accessible = false
    }
    reader_1 = {
      instance_class      = "db.r6g.xlarge"
      publicly_accessible = false
    }
  }

  storage_encrypted   = true
  apply_immediately   = false
  monitoring_interval = 60

  enabled_cloudwatch_logs_exports = ["postgresql"]

  backup_retention_period = 30
  preferred_backup_window = "03:00-04:00"

  tags = {
    Environment = "production"
    Compliance  = "hipaa"
  }
}

# ElastiCache Redis
resource "aws_elasticache_replication_group" "redis" {
  replication_group_id       = "togo-production-redis"
  replication_group_description = "Redis cluster for Togo Health"

  engine               = "redis"
  engine_version       = "7.0"
  node_type            = "cache.r6g.large"
  num_cache_clusters   = 3

  subnet_group_name    = aws_elasticache_subnet_group.redis.name
  security_group_ids   = [aws_security_group.redis.id]

  at_rest_encryption_enabled = true
  transit_encryption_enabled = true
  auth_token_enabled         = true

  automatic_failover_enabled = true
  multi_az_enabled           = true

  snapshot_retention_limit = 7
  snapshot_window          = "03:00-05:00"

  tags = {
    Environment = "production"
  }
}

# S3 for document storage
resource "aws_s3_bucket" "documents" {
  bucket = "togo-production-documents"

  tags = {
    Environment = "production"
    Compliance  = "hipaa"
  }
}

resource "aws_s3_bucket_versioning" "documents" {
  bucket = aws_s3_bucket.documents.id

  versioning_configuration {
    status = "Enabled"
  }
}

resource "aws_s3_bucket_server_side_encryption_configuration" "documents" {
  bucket = aws_s3_bucket.documents.id

  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm     = "aws:kms"
      kms_master_key_id = aws_kms_key.s3.arn
    }
  }
}
```

### Observability Stack

**Prometheus + Grafana for metrics**:

```yaml
# Prometheus configuration
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'kubernetes-pods'
    kubernetes_sd_configs:
    - role: pod
    relabel_configs:
    - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
      action: keep
      regex: true
    - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
      action: replace
      target_label: __metrics_path__
      regex: (.+)
    - source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
      action: replace
      regex: ([^:]+)(?::\d+)?;(\d+)
      replacement: $1:$2
      target_label: __address__

  - job_name: 'agent-metrics'
    static_configs:
    - targets: ['agent-orchestrator:9090']

  - job_name: 'nodejs-services'
    kubernetes_sd_configs:
    - role: pod
      namespaces:
        names:
        - togo-production
    relabel_configs:
    - source_labels: [__meta_kubernetes_pod_label_app]
      regex: '.*-service'
      action: keep
```

**Grafana Dashboard for AI Agents**:

```json
{
  "dashboard": {
    "title": "Togo Health - AI Agent Monitoring",
    "panels": [
      {
        "title": "Agent Execution Rate",
        "targets": [
          {
            "expr": "rate(agent_executions_total[5m])",
            "legendFormat": "{{agent_type}}"
          }
        ]
      },
      {
        "title": "Agent Success Rate",
        "targets": [
          {
            "expr": "rate(agent_executions_total{status=\"success\"}[5m]) / rate(agent_executions_total[5m]) * 100",
            "legendFormat": "{{agent_type}}"
          }
        ]
      },
      {
        "title": "LLM Token Usage",
        "targets": [
          {
            "expr": "sum(llm_tokens_used_total) by (model)",
            "legendFormat": "{{model}}"
          }
        ]
      },
      {
        "title": "Human-in-Loop Approval Time",
        "targets": [
          {
            "expr": "histogram_quantile(0.95, rate(agent_approval_duration_seconds_bucket[5m]))",
            "legendFormat": "p95"
          }
        ]
      }
    ]
  }
}
```

**ELK Stack for centralized logging**:

```yaml
# Filebeat configuration for log collection
filebeat.inputs:
- type: container
  paths:
    - /var/log/containers/*.log
  processors:
  - add_kubernetes_metadata:
      host: ${NODE_NAME}
      matchers:
      - logs_path:
          logs_path: "/var/log/containers/"

output.elasticsearch:
  hosts: ["elasticsearch:9200"]
  indices:
    - index: "togo-production-logs-%{+yyyy.MM.dd}"
      when.contains:
        kubernetes.namespace: "togo-production"

# Logstash pipeline for log enrichment
input {
  beats {
    port => 5044
  }
}

filter {
  if [kubernetes][namespace] == "togo-production" {
    json {
      source => "message"
    }

    # Extract trace ID for distributed tracing
    grok {
      match => { "message" => "trace_id=%{UUID:trace_id}" }
    }

    # Classify log severity
    if [level] == "error" or [level] == "fatal" {
      mutate {
        add_field => { "severity" => "high" }
      }
    }
  }
}

output {
  elasticsearch {
    hosts => ["elasticsearch:9200"]
    index => "togo-production-logs-%{+yyyy.MM.dd}"
  }
}
```

**Jaeger for distributed tracing**:

```go
// OpenTelemetry instrumentation
import (
    "go.opentelemetry.io/otel"
    "go.opentelemetry.io/otel/exporters/jaeger"
    "go.opentelemetry.io/otel/sdk/trace"
)

func initTracer() (*trace.TracerProvider, error) {
    exporter, err := jaeger.New(jaeger.WithCollectorEndpoint(
        jaeger.WithEndpoint("http://jaeger-collector:14268/api/traces"),
    ))
    if err != nil {
        return nil, err
    }

    tp := trace.NewTracerProvider(
        trace.WithBatcher(exporter),
        trace.WithResource(resource.NewWithAttributes(
            semconv.SchemaURL,
            semconv.ServiceName("staff-service"),
            semconv.ServiceVersion("1.2.0"),
        )),
    )

    otel.SetTracerProvider(tp)
    return tp, nil
}

// Example traced handler
func handleRequest(c *gin.Context) {
    ctx := c.Request.Context()
    tracer := otel.Tracer("staff-service")

    ctx, span := tracer.Start(ctx, "handleStaffRequest")
    defer span.End()

    // Add attributes
    span.SetAttributes(
        attribute.String("staff_id", staffID),
        attribute.String("request_type", "update_profile"),
    )

    // Call downstream service (trace propagates automatically)
    result, err := credentialService.FetchCredentials(ctx, staffID)
    if err != nil {
        span.RecordError(err)
        span.SetStatus(codes.Error, err.Error())
        return
    }

    c.JSON(200, result)
}
```

---

## Security & Compliance

### HIPAA Compliance Architecture

**PHI Encryption**:
- **At Rest**: AES-256 encryption via AWS KMS
- **In Transit**: TLS 1.3 for all external communications, mTLS (mutual TLS) for inter-service
- **Application Level**: Field-level encryption for highly sensitive data (SSN, patient IDs)

**Access Controls**:
```yaml
# Example RBAC policy (Open Policy Agent)
package togo.authorization

default allow = false

# Clinicians can only view their own data
allow {
    input.user.role == "clinician"
    input.resource.type == "profile"
    input.resource.owner_id == input.user.id
}

# Admins can view all staff in their hospital
allow {
    input.user.role == "admin"
    input.resource.type == "staff"
    input.resource.hospital_id == input.user.hospital_id
}

# AI agents can only access data within approved scope
allow {
    input.user.role == "agent"
    input.resource.type in input.user.allowed_resources
    input.action in ["read", "update"]
    not input.resource.requires_human_approval
}
```

**Audit Logging**:
```typescript
// Audit log schema
interface AuditLog {
  eventId: string;
  timestamp: Date;
  eventType: 'access' | 'modify' | 'delete' | 'export';
  userId: string;
  userRole: 'clinician' | 'admin' | 'agent';
  resourceType: string;
  resourceId: string;
  action: string;
  ipAddress: string;
  userAgent: string;
  result: 'success' | 'failure';
  errorMessage?: string;
  phi_accessed: boolean;

  // HIPAA required fields
  reasonForAccess?: string;
  emergencyAccess: boolean;
}

// Every PHI access is logged
async function logPhiAccess(context: RequestContext, resource: Resource) {
  await auditLogger.log({
    eventType: 'access',
    userId: context.user.id,
    userRole: context.user.role,
    resourceType: resource.type,
    resourceId: resource.id,
    ipAddress: context.ip,
    phi_accessed: true,
    reasonForAccess: context.reason,
    emergencyAccess: context.emergencyOverride || false,
  });
}
```

**Data Retention & Deletion**:
- PHI retained for 6 years (HIPAA requirement)
- Automated deletion workflows via Temporal
- Soft delete with audit trail, hard delete after retention period
- Right to erasure (GDPR) with exceptions for legal/compliance requirements

### SOC 2 Type II Controls

**Change Management**:
- All code changes require PR review + approval
- Automated security scans (Snyk, Trivy) block insecure deployments
- Production deployments require two-person approval
- Rollback procedures documented and tested quarterly

**Incident Response**:
```yaml
# PagerDuty integration for critical alerts
apiVersion: v1
kind: ConfigMap
metadata:
  name: alertmanager-config
data:
  config.yml: |
    route:
      receiver: 'pagerduty-critical'
      group_by: ['alertname', 'cluster', 'service']
      routes:
      - match:
          severity: critical
        receiver: 'pagerduty-critical'
        continue: true
      - match:
          severity: warning
        receiver: 'slack-alerts'

    receivers:
    - name: 'pagerduty-critical'
      pagerduty_configs:
      - service_key: '<PAGERDUTY_KEY>'
        severity: 'critical'
        description: '{{ .GroupLabels.alertname }}'

    - name: 'slack-alerts'
      slack_configs:
      - api_url: '<SLACK_WEBHOOK>'
        channel: '#togo-alerts'
        title: 'Alert: {{ .GroupLabels.alertname }}'
```

**Disaster Recovery**:
- **RTO (Recovery Time Objective)**: 4 hours
- **RPO (Recovery Point Objective)**: 15 minutes
- Multi-region active-passive setup
- Daily automated backups to S3 with cross-region replication
- Quarterly DR drills with runbook validation

---

## Performance & Scalability

### Load Testing Strategy

**K6 Load Testing**:

```javascript
// k6 load test script
import http from 'k6/http';
import { check, sleep } from 'k6';

export const options = {
  stages: [
    { duration: '2m', target: 100 },   // Ramp up to 100 users
    { duration: '5m', target: 100 },   // Stay at 100 users
    { duration: '2m', target: 200 },   // Ramp up to 200 users
    { duration: '5m', target: 200 },   // Stay at 200 users
    { duration: '2m', target: 0 },     // Ramp down
  ],
  thresholds: {
    http_req_duration: ['p(95)<500'],  // 95% of requests < 500ms
    http_req_failed: ['rate<0.01'],    // Error rate < 1%
  },
};

export default function() {
  const baseUrl = 'https://api.togohealth.com';

  // Login
  let loginRes = http.post(`${baseUrl}/auth/login`, JSON.stringify({
    email: 'test@example.com',
    password: 'password',
  }), {
    headers: { 'Content-Type': 'application/json' },
  });

  check(loginRes, {
    'login successful': (r) => r.status === 200,
  });

  const token = loginRes.json('token');

  // Fetch dashboard data
  let dashboardRes = http.get(`${baseUrl}/graphql`, {
    headers: {
      'Authorization': `Bearer ${token}`,
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      query: `
        query Dashboard {
          me {
            upcomingShifts {
              id
              startTime
              location
            }
            credentials {
              id
              expiryDate
              status
            }
            agentActivities(limit: 10) {
              id
              agentType
              status
            }
          }
        }
      `
    }),
  });

  check(dashboardRes, {
    'dashboard loaded': (r) => r.status === 200,
    'has shifts': (r) => r.json('data.me.upcomingShifts').length > 0,
  });

  sleep(1);
}
```

### Caching Strategy

**Multi-Layer Caching**:

```typescript
// L1: In-memory cache (Node.js)
class MemoryCache {
  private cache = new Map<string, { value: any, expiry: number }>();

  get(key: string): any | null {
    const item = this.cache.get(key);
    if (!item) return null;
    if (Date.now() > item.expiry) {
      this.cache.delete(key);
      return null;
    }
    return item.value;
  }

  set(key: string, value: any, ttlSeconds: number = 60) {
    this.cache.set(key, {
      value,
      expiry: Date.now() + (ttlSeconds * 1000),
    });
  }
}

// L2: Redis distributed cache
class RedisCache {
  constructor(private redis: Redis) {}

  async get<T>(key: string): Promise<T | null> {
    const value = await this.redis.get(key);
    return value ? JSON.parse(value) : null;
  }

  async set(key: string, value: any, ttlSeconds: number = 300) {
    await this.redis.setex(key, ttlSeconds, JSON.stringify(value));
  }

  async invalidate(pattern: string) {
    const keys = await this.redis.keys(pattern);
    if (keys.length > 0) {
      await this.redis.del(...keys);
    }
  }
}

// Cache-aside pattern implementation
class StaffRepository {
  constructor(
    private db: PrismaClient,
    private l1Cache: MemoryCache,
    private l2Cache: RedisCache
  ) {}

  async findById(id: string): Promise<Staff | null> {
    const cacheKey = `staff:${id}`;

    // Check L1 cache
    let staff = this.l1Cache.get(cacheKey);
    if (staff) {
      return staff;
    }

    // Check L2 cache (Redis)
    staff = await this.l2Cache.get<Staff>(cacheKey);
    if (staff) {
      this.l1Cache.set(cacheKey, staff, 60); // 1 min in L1
      return staff;
    }

    // Fetch from database
    staff = await this.db.staff.findUnique({
      where: { id },
      include: { credentials: true, shifts: true },
    });

    if (staff) {
      this.l1Cache.set(cacheKey, staff, 60);
      this.l2Cache.set(cacheKey, staff, 300); // 5 min in L2
    }

    return staff;
  }

  async update(id: string, data: UpdateStaffDTO): Promise<Staff> {
    const staff = await this.db.staff.update({
      where: { id },
      data,
    });

    // Invalidate caches
    const cacheKey = `staff:${id}`;
    this.l1Cache.set(cacheKey, staff, 60);
    await this.l2Cache.set(cacheKey, staff, 300);

    // Invalidate related caches
    await this.l2Cache.invalidate(`staff:${id}:*`);

    return staff;
  }
}
```

### Database Optimization

**Read Replicas**:
```typescript
// Prisma read replica configuration
const primaryDb = new PrismaClient({
  datasources: {
    db: {
      url: process.env.DATABASE_PRIMARY_URL,
    },
  },
});

const replicaDb = new PrismaClient({
  datasources: {
    db: {
      url: process.env.DATABASE_REPLICA_URL,
    },
  },
});

// Route reads to replica, writes to primary
class DatabaseRouter {
  async read<T>(query: () => Promise<T>): Promise<T> {
    return replicaDb.$transaction(query);
  }

  async write<T>(query: () => Promise<T>): Promise<T> {
    return primaryDb.$transaction(query);
  }
}
```

**Connection Pooling**:
```typescript
// PgBouncer configuration
[databases]
togohealth = host=aurora-cluster.us-west-2.rds.amazonaws.com port=5432 dbname=togohealth

[pgbouncer]
pool_mode = transaction
max_client_conn = 1000
default_pool_size = 25
reserve_pool_size = 10
reserve_pool_timeout = 3
max_db_connections = 100
```

---

## Cost Optimization

### AWS Cost Estimates (Monthly)

**Compute (EKS)**:
- 5x m5.xlarge nodes (general): $730
- 5x c5.2xlarge nodes (AI agents, SPOT): $340
- Total: ~$1,070/month

**Database**:
- Aurora PostgreSQL (2x db.r6g.xlarge): $875
- ElastiCache Redis (3x cache.r6g.large): $580
- Total: ~$1,455/month

**Storage**:
- S3 (documents, backups): $200
- EBS volumes: $150
- Total: ~$350/month

**Data Transfer**:
- CloudFront CDN: $300
- Inter-region transfer: $100
- Total: ~$400/month

**AI/LLM**:
- AWS Bedrock (Claude 3.5 Sonnet):
  - Input tokens: 10M tokens/day × $3/1M = $900/month
  - Output tokens: 2M tokens/day × $15/1M = $900/month
  - Total: ~$1,800/month

**Observability**:
- Datadog APM: $500
- CloudWatch: $200
- Total: ~$700/month

**TOTAL ESTIMATED**: ~$5,775/month for 100,000 clinicians (~$0.058 per clinician/month)

### Cost Optimization Strategies

1. **Use Spot Instances**: 50-70% savings on AI agent workloads
2. **Right-size resources**: Auto-scaling based on actual usage
3. **Reserved Instances**: 1-year RI for predictable workloads (40% savings)
4. **S3 Lifecycle Policies**: Move old documents to Glacier ($0.004/GB vs $0.023/GB)
5. **CloudFront caching**: Reduce origin requests by 80%
6. **LLM caching**: Cache frequent agent prompts to reduce token usage

---

## Technology Stack Summary

### Frontend
| Component | Technology | Rationale |
|-----------|-----------|-----------|
| Framework | React 18 + TypeScript | Industry standard, strong typing, large ecosystem |
| Meta-Framework | Next.js 14 (App Router) | SSR/SSG, excellent performance, Vercel deployment |
| State Management | Zustand + React Query | Lightweight, server state caching, optimistic updates |
| Styling | Tailwind CSS + shadcn/ui | Rapid development, consistent design, accessibility |
| Mobile | React Native (Expo) | Code sharing with web, native performance |
| Build Tool | Turborepo | Monorepo support, fast builds, caching |

### Backend
| Component | Technology | Rationale |
|-----------|-----------|-----------|
| Runtime | Node.js 20 LTS + TypeScript | JavaScript everywhere, strong typing, async/await |
| API Framework | Express + Apollo Server | Mature, flexible, GraphQL Federation support |
| ORM | Prisma | Type-safe, migrations, excellent DX |
| Workflow Engine | Temporal.io | Durable workflows, retry logic, long-running tasks |
| Authentication | Passport.js + JWT + VO SSO | Flexible, OAuth 2.0/OIDC support |
| Testing | Jest + Supertest + Playwright | Unit, integration, E2E testing |

### AI Layer
| Component | Technology | Rationale |
|-----------|-----------|-----------|
| Framework | LangChain + LangGraph | Agent orchestration, chain-of-thought reasoning |
| LLM | Claude 3.5 Sonnet (AWS Bedrock) | Best-in-class reasoning, HIPAA-compliant, Bedrock managed |
| Vector DB | Pinecone | Managed, fast semantic search, easy integration |
| Monitoring | LangSmith | LLM observability, prompt debugging |

### Integration
| Component | Technology | Rationale |
|-----------|-----------|-----------|
| Runtime | Go 1.21+ | High performance, concurrency, low memory |
| Framework | Gin (HTTP), gRPC-Go | Fast, type-safe inter-service communication |
| Circuit Breaker | hystrix-go | Fault tolerance, graceful degradation |
| Message Queue | RabbitMQ | Reliable, mature, dead-letter queues |

### Data
| Component | Technology | Rationale |
|-----------|-----------|-----------|
| Relational DB | PostgreSQL (Aurora) | ACID compliance, JSON support, mature |
| Document Store | MongoDB (DocumentDB) | Flexible schema for agent logs, EMR data |
| Cache | Redis (ElastiCache) | In-memory speed, pub/sub for real-time |
| Search | Elasticsearch | Full-text search, staff directory, logs |
| Object Storage | AWS S3 | Scalable, durable, HIPAA-compliant |
| Event Stream | Apache Kafka / AWS Kinesis | Real-time events, audit logs, replays |

### Infrastructure
| Component | Technology | Rationale |
|-----------|-----------|-----------|
| Container Orchestration | Kubernetes (EKS) | Industry standard, auto-scaling, self-healing |
| Service Mesh | Istio | mTLS, traffic management, observability |
| IaC | Terraform + AWS CDK | Declarative, version controlled, multi-cloud |
| CI/CD | GitHub Actions + ArgoCD | GitOps, automated deployments, rollbacks |
| Monitoring | Prometheus + Grafana | Open-source, flexible, alerting |
| Logging | ELK Stack | Centralized logs, full-text search, visualizations |
| Tracing | Jaeger (OpenTelemetry) | Distributed tracing, performance debugging |
| APM | Datadog | Unified monitoring, dashboards, alerts |

---

## Verified Orchestration Integration Highlights

### SSO & Authentication
- **OIDC/SAML 2.0 integration** for seamless login
- **Biometric authentication** support (Face ID, Touch ID, hardware tokens)
- **MFA step-up** for sensitive agent actions (e.g., approve credential changes)
- **Session management** with JWT tokens signed by VO

### Credential Verification
- **Real-time license validation** via VO API
- **Blockchain-backed verification** for credential integrity
- **Automated background checks** status updates
- **Cross-organizational identity federation** for staff mobility

### Security & Compliance
- **HIPAA-compliant identity infrastructure**
- **Audit trails** for all authentication events
- **Privacy-preserving attribute sharing** (selective disclosure)
- **Trusted credential portability** across Togo Health customer hospitals

### Technical Integration Points
```typescript
// Example: VO SSO integration in frontend
import { VerifiedOrchestrationProvider } from '@togo/auth';

function App() {
  return (
    <VerifiedOrchestrationProvider
      clientId={process.env.VO_CLIENT_ID}
      redirectUri={process.env.VO_REDIRECT_URI}
      scope="openid profile email credentials"
    >
      <AppContent />
    </VerifiedOrchestrationProvider>
  );
}

// Backend: Verify VO ID token
import { verifyIdToken } from '@togo/verified-orchestration-sdk';

async function authenticateUser(idToken: string) {
  const claims = await verifyIdToken(idToken, {
    issuer: 'https://auth.verified-orchestration.com',
    audience: process.env.VO_CLIENT_ID,
  });

  // Fetch full credential profile
  const credentials = await voClient.getCredentials(claims.sub);

  // Create/update user in Togo Health
  const user = await upsertUser({
    voSubject: claims.sub,
    email: claims.email,
    credentials,
  });

  return user;
}
```

---

## Deployment Timeline (12-18 Months)

### Phase 1: Foundation (Months 1-4)
- **Infrastructure setup**: AWS account, VPC, EKS cluster, databases
- **Core services**: User, Staff, Authentication (VO integration)
- **Frontend shell**: Next.js app with VO SSO login
- **Integration adapters**: Med App, Core Schedule (read-only)
- **Deliverable**: Authenticated users can view staff directory and shifts

### Phase 2: Core Agents (Months 5-8)
- **AI infrastructure**: Temporal workflows, Bedrock integration, Pinecone
- **Agents**: Timesheet (autonomous), Credential (HITL), Notification (autonomous)
- **Orchestrator**: LangGraph-based agent coordination
- **Time Filer integration**: Bidirectional sync for timesheets
- **Deliverable**: Working timesheet auto-submission, credential monitoring

### Phase 3: Advanced Features (Months 9-12)
- **EMR integration**: Epic certification, FHIR API, EMR Briefing Agent
- **LMS Recommendation Agent**: Course suggestions based on clinical work
- **Digital Passport integration**: Sync clinician-owned knowledge graphs
- **Mobile app**: React Native iOS/Android launch
- **Deliverable**: Full clinician dashboard with AI agents, mobile access

### Phase 4: Scale & Optimization (Months 13-18)
- **Multi-hospital orchestration**: Cross-facility staff sharing
- **Advanced analytics**: Predictive staffing, workforce insights
- **Wellbeing monitoring**: Burnout detection, intervention suggestions
- **Enterprise features**: White-labeling, custom integrations, SSO
- **Deliverable**: Production-ready platform for 10+ hospitals, 10,000+ clinicians

---

## Conclusion

This modern architecture positions Togo Health as a **cloud-native, AI-first healthcare workforce platform** that:

1. **Scales effortlessly** from 1,000 to 100,000+ clinicians
2. **Integrates deeply** with Verified Orchestration for trusted identity and credential verification
3. **Automates intelligently** via 15 specialized AI agents powered by Claude 3.5 Sonnet
4. **Empowers clinicians** with data ownership through My Digital Passport integration
5. **Ensures compliance** with HIPAA, SOC 2, and healthcare regulatory requirements
6. **Delivers measurable ROI**: 12.5 hours/month saved per clinician, 28% burnout reduction

The technology stack balances **cutting-edge AI capabilities** (LangChain, Claude 3.5) with **proven enterprise infrastructure** (Kubernetes, PostgreSQL, Terraform), ensuring both innovation and stability for healthcare customers.

**For Verified Orchestration**: This architecture showcases deep integration opportunities beyond SSO—including real-time credential verification, cross-organizational identity federation, and blockchain-backed credential integrity. As Togo Health scales across hospital networks, VO becomes the foundational trust layer enabling seamless, secure clinician mobility.
