# System Architecture and Technical Blueprint

## 1) High-level architecture
The platform is a two-sided AI recruiting system with three major layers:

1. User and workflow layer
   - candidate app
   - company dashboard
   - recruiter tooling
   - admin tools

2. Matching and intelligence layer
   - candidate profiling
   - role parsing
   - ranking engine
   - AI recommendations
   - intro generation

3. Data and integration layer
   - user database
   - candidate and company data
   - role and matching data
   - ATS and notification adapters
   - job feed connectors

## 2) Recommended stack
### Frontend
- Next.js for web app
- TypeScript
- Tailwind CSS
- React Query / TanStack Query

### Backend
- Python FastAPI for APIs and AI orchestration
- PostgreSQL for transactional data
- Redis for queues and caching
- Celery or BullMQ for async tasks

### Search and ranking
- Elasticsearch or OpenSearch for candidate-role search and filters
- PostgreSQL + pgvector for embeddings and vector search
- optional Pinecone / Weaviate for more advanced retrieval

### Storage
- AWS S3 or equivalent for resumes, media, and attachments

### AI layer
- LLM API for structured extraction and summarization
- embeddings for semantic feature matching
- ranking service for fit score generation

### Messaging and notifications
- Email service
- SMS service
- WhatsApp or messaging workflows
- Slack integration for company workflows

### Auth and security
- Clerk, Auth.js, or custom auth
- role-based access controls
- secure secret management

## 3) Core services
### Candidate profile service
- parse candidate inputs
- extract experience and skills
- generate structured profile JSON
- maintain career summary and preferences

### Role brief service
- parse company job description
- create structured job brief
- infer required skills, experience, salary, etc.

### Matching service
- compute candidate-role fit scores
- rank candidates for each role
- produce explainable reasons
- learn from recruiter action data

### Intro service
- validate consent
- generate intro content
- coordinate candidate/company communication
- log intro state transitions

### Pipeline service
- maintain candidate status per role
- support stage transitions
- sync with ATS when configured

### Notification service
- send candidate updates, intro requests, interview invites, and employer alerts

## 4) Data model
### Users
- id
- email
- name
- role_type
- created_at
- updated_at

### Candidates
- id
- user_id
- current_title
- experience_summary
- location
- remote_preference
- notice_period
- expected_ctc
- created_at

### Companies
- id
- name
- company_stage
- industry
- size
- created_at

### Roles
- id
- company_id
- title
- description
- seniority
- location
- compensation_band
- work_mode
- status
- created_at

### CandidateProfile
- id
- candidate_id
- skills_json
- career_summary
- role_preferences_json
- salary_preferences_json
- geographic_preferences_json
- ai_profile_snapshot

### Matches
- id
- candidate_id
- role_id
- score
- reason_summary
- status
- created_at

### Intros
- id
- candidate_id
- role_id
- company_id
- intro_status
- consent_status
- sent_at
- accepted_at
- declined_at

### Feedback
- id
- candidate_id
- role_id
- feedback_type
- detail
- created_at

### ATSIntegration
- id
- company_id
- provider
- status
- config_json

## 5) Core API modules
### Candidate APIs
- POST /api/candidates/onboard
- POST /api/candidates/profile/update
- GET /api/candidates/matches
- POST /api/candidates/accept-intro
- POST /api/candidates/decline-intro

### Company APIs
- POST /api/companies/roles
- GET /api/companies/roles/:id/matches
- POST /api/companies/roles/:id/shortlist
- POST /api/companies/intro/send
- GET /api/companies/pipeline

### Matching APIs
- POST /api/matching/profile
- POST /api/matching/role
- POST /api/matching/rank
- GET /api/matching/reasons/:match_id

### Notification APIs
- POST /api/notifications/send
- GET /api/notifications

## 6) AI workflow details
### Candidate intelligence pipeline
1. Extract structured data from résumé / profile form
2. Generate text summary and role preferences
3. Store embedding of candidate profile
4. Search for matching roles and opportunities
5. Rank by fit score and generate reasons
6. Return candidate-facing recommendations

### Company intelligence pipeline
1. Parse role brief
2. Generate expected candidate persona
3. Retrieve candidate embeddings and metadata
4. Filter by hard criteria
5. Rank by fit score
6. Deliver shortlist with reasons
7. Learn from recruiter feedback and update ranking

## 7) Security and trust requirements
- only approved candidate data is shared to company
- direct intro requires explicit consent
- company team members require role-based permissions
- candidate can control visibility to specific companies
- profile data should support deletion requests
- all sensitive actions logged for audit

## 8) Launch constraints
Start with:
- limited candidate pool
- structured role library
- manual review support
- smaller geographic launch area
- reduced risk of poor-quality mass intro events

## 9) Performance expectations
- top K matches returned within a few seconds for role and candidate searches
- push notifications sent within 1–5 minutes of matching trigger
- pipeline updates available immediately in dashboard
- ingestion and ranking jobs handled asynchronously

## 10) Future extensibility
- multi-city and multi-language support
- more external hiring sources
- deeper AI interviewing and preparation modules
- campus and referral network features
- enterprise recruiting suites
- recruiter copilot workflows

## 11) Suggested MVP implementation order
1. auth + profile system
2. role creation + candidate matching
3. shortlist + intro approval flow
4. notes and pipeline tracking
5. notifications and email
6. ATS and Slack integration
7. ranking improvements and feedback learning

## 12) Recommended stack summary
- Next.js + TypeScript + Tailwind
- FastAPI + PostgreSQL + Redis
- Elasticsearch + pgvector
- S3 for assets
- AWS or GCP hosting
- LLM-based extraction and ranking
- success-fee billing logic in backend
