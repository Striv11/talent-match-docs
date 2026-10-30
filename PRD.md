# Product Requirements Document (PRD)

## 1) Problem statement
Candidates and companies both suffer from fragmented recruiting systems.

Candidates:
- lose time to application spam
- rely on weak job discovery mechanisms
- do not get timely context on role fit or compensation
- rarely get direct introductions to hiring managers

Companies:
- get too many noisy inbound applications
- spend hours on unqualified sourcing
- miss hidden talent outside traditional channels
- waste time with poor early screening

## 2) Product goal
Build a two-sided recruiting platform for India that helps:
- candidates discover relevant jobs via an AI career agent
- companies discover strong candidates via an AI hiring agent
- both sides communicate through direct, consent-based introductions

## 3) Core product concepts
### Jack
Jack is the candidate-side AI career agent.

Responsibilities:
- profile candidate career story
- infer skills, interests, and intent
- search for and rank opportunities
- recommend jobs and intros
- coach for interview and negotiation

### Jill
Jill is the company-side AI hiring agent.

Responsibilities:
- parse job requirements
- infer the people profile required
- source matching candidates from internal and external pools
- provide ranked shortlist
- learn from recruiter feedback
- facilitate direct candidate introduction

## 4) User roles
- Candidate
- Company admin
- Hiring manager
- Recruiter / talent operator
- Team collaborator

## 5) Functional requirements

### 5.1 Candidate onboarding
- Candidate can sign up with email or social login
- Candidate can create an initial profile
- Candidate completes guided conversation collecting:
  - work experience
  - skills
  - roles of interest
  - salary expectation
  - preferred cities
  - remote/hybrid/onsite preference
  - notice period
  - career goals
- System stores structured profile and derived summary

### 5.2 Candidate opportunity discovery
- System fetches relevant jobs from multiple sources
- Matches are scored by fit and relevance
- Candidate sees recommended jobs and intro opportunities
- Candidate can accept, pass, or ask for more signals
- System keeps learning from user actions

### 5.3 Candidate intro workflow
- If candidate is a strong match, the platform can generate a direct intro
- Company and candidate consent must be present before intro is sent
- Candidate can accept or decline intro
- System logs all intro events

### 5.4 Candidate career support
- job tracking dashboard
- mock interviews
- role-fit explanations
- salary benchmark guidance
- negotiation support

### 5.5 Company onboarding
- Company can create account
- Company can invite team members
- Company creates a role brief
- Company can define: title, seniority, compensation, location, must-haves, stage
- System generates a suggested candidate profile from the brief

### 5.6 Company candidate discovery
- Jill surfaces ranked talent based on role fit
- System can search across active candidate pool, passive network, and curated talent feeds
- Company can view candidate cards with fit reasons
- Company can reject, shortlist, or request more matches

### 5.7 Company intro workflow
- Company can send intro request
- Candidate consent is required
- Candidate can accept/decline
- Both sides can message or schedule a call

### 5.8 Feedback loop
- Recruiter feedback updates candidate ranking,
- role fit scoring improves over time
- system stores hidden feedback signals for model tuning

### 5.9 Pipeline management
- role has candidate stages: new, shortlisted, intro sent, contacted, interview, hired, rejected
- recruiter notes are stored per candidate per role
- candidate status is visible in a dashboard

### 5.10 ATS integration
- integrate with ATS / recruiting tools as a later phase
- support sync for candidate status and hiring events

## 6) Non-functional requirements
- secure handling of candidate data
- consent-based introductions
- privacy controls for every profile
- role-based access for company team members
- reliable notifications
- low-latency match generation for the top candidates
- observability and score logging
- moderation and abuse controls

## 7) Acceptance criteria
### Candidate MVP acceptance
- candidate can create a profile and specify preferences
- candidate sees ranked jobs/opportunities within 1–10 minutes of setup
- candidate can accept or reject job suggestions
- candidate can receive direct intro to company

### Company MVP acceptance
- company can create a role with detail
- company sees top-ranked candidate matches
- company can shortlist, reject, or request more matches
- company can track candidate pipeline
- system can generate intro with consent controls

## 8) Edge cases
- candidate is not actively looking but wants to be considered
- company only wants high-signal candidates
- candidate declines intro
- role is deeply niche and no good matches currently exist
- candidate has multiple work-experience phases that require interpretation
- compensation mismatch or notice period mismatch

## 9) Success metrics
- candidate activation rate
- role creation to shortlist time
- intro acceptance rate
- candidate response rate
- recruiter time saved
- hire conversion rate
- candidate retention on platform
- quality of hire and role fit accuracy

## 10) Risks and mitigations
### Risk: poor matching quality
Mitigation: human feedback loops, transparent reasons, manual override

### Risk: candidate distrust
Mitigation: clear consent, privacy controls, opt-out, communication transparency

### Risk: spammy outbound experience
Mitigation: role-based matching and quality thresholds before intro sends

### Risk: low employer adoption
Mitigation: success-fee pricing, founder-led sales, strong pilot program

## 11) Launch version
The first launch should be limited to:
- startup tech hirers
- 1–2 cities initially
- 1–2 role families initially
- manual review support in the loop

## 12) Long-term vision
Expand beyond India to other verticals and geographies once the trust layer, AI ranking layer, and network effect are proven.
