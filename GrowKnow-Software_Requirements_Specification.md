# GrowKnow - Software Requirements Specification 

## Table of contents
- [Table of contents](#table-of-contents)
- [Introduction](#1-introduction)
    - [Purpose](#11-purpose)
    - [Scope](#12-scope)
    - [Definitions, Acronyms and Abbreviations](#13-definitions-acronyms-and-abbreviations)
    - [References](#14-references)
    - [Overview](#15-overview)
- [Overall Description](#2-overall-description)
    - [Vision](#21-vision)
    - [Use Case Diagram](#22-use-case-diagram)
	- [Technology Stack](#23-technology-stack)
- [Specific Requirements](#3-specific-requirements)
    - [Functionality](#31-functionality)
    - [Usability](#32-usability)
    - [Reliability](#33-reliability)
    - [Performance](#34-performance)
    - [Supportability](#35-supportability)
    - [Design Constraints](#36-design-constraints)
    - [Online User Documentation and Help System Requirements](#37-on-line-user-documentation-and-help-system-requirements)
    - [Purchased Components](#purchased-components)
    - [Interfaces](#39-interfaces)
    - [Licensing Requirements](#310-licensing-requirements)
    - [Legal, Copyright And Other Notices](#311-legal-copyright-and-other-notices)
    - [Applicable Standards](#312-applicable-standards)
- [Supporting Information](#4-supporting-information)

## 1. Introduction

### 1.1 Purpose
This Software Requirements Specification (SRS) describes all specifications for the application "GrowKnow". It includes an overview of the project and its vision, detailed information about the planned features, and the boundary conditions of the development process.


### 1.2 Scope
The project is going to be realized as a web-based platform that consolidates current AI developments, organizes tools, and provides structured learning paths for IT professionals.

Actors of this platform can be Visitors, Registered Users, Admins, or the Automation Orchestrator (n8n). 
  
Planned Subsystems are: 

* AI News Feed & Newsletter:
At the core, an automated feed consolidates vetted AI sources. Articles are deduplicated, summarized, and tagged with metadata (source, date, relevance, use case). They are published on the platform and distributed through a weekly newsletter.

* AI Tool Directory:
A curated repository of AI tools, categorized by tasks (generate, analyze, automate, build, secure). Each tool includes metadata such as domains, alternatives, integration effort, and example workflows. Users can filter by goal, budget, and maturity.

* Role-Based Learning Roadmaps:
Roadmaps for roles like Data Engineer, ML Engineer, DevOps, or Security Engineer. Each roadmap includes ordered learning objectives, resources, and practice tasks.

* Account & Feedback System:
Registered users can subscribe to newsletters, suggest new tools/sources, and provide corrections.

* Administration & Data Pipelines:
Admins manage content review, user roles, and automation pipelines for ingestion, embeddings, and fact-checking. Automations (via n8n) handle crawling, newsletter generation, and triggers.

### 1.3 Definitions, Acronyms and Abbreviations
| Abbrevation | Explanation                            |
| ----------- | -------------------------------------- |
| SRS         | Software Requirements Specification    |
| UC          | Use Case                               |
| n/a         | not applicable                         |
| tbd         | to be determined                       |
| UCD         | overall Use Case Diagram               |
| FAQ         | Frequently asked Questions             |

### 1.4 References

| Title                                                                 |    Date    | Publishing organization |
| --------------------------------------------------------------------- | :--------: | ----------------------- |
| [GrowKnow Blog – Project Vision](#)                                   | 2025-09-25 | GrowKnow Team           |
| [GrowKnow Blog – Team & Technology](#)                                | 2025-09-26 | GrowKnow Team           |
| [GitHub Repository](https://github.com/bermar24/GrowKnow)             | 2025-10-01 | GrowKnow Team           |


### 1.5 Overview
The following chapter provides an overview of this project with vision and Overall Use Case Diagram. The third chapter (Requirements Specification) delivers more details about the specific requirements in terms of functionality, usability and design parameters. Finally there is a chapter with supporting information. 
    
## 2. Overall Description

### 2.1 Vision
We aim to build a central hub for AI professionals. The platform consolidates AI news, organizes tools by utility, and offers structured learning roadmaps. The goals are:
* Provide orientation without noise.
* Support faster and more confident technology decisions.
* Enable measurable progress in AI/IT learning paths.

The system will be delivered iteratively:
1. MVP (by December): News feed, newsletter, tool search & filtering, and initial roadmaps.
2. Next phase: Expansion of the tool directory and roadmap coverage.
3. Later: More advanced feedback loops, contributor system, and extended automation.

### 2.2 Use Case Diagram

![OUCD](./UseCaseDiagramCP.png)

- Green: Planned till end of december
- Yellow: Planned till end of june

### 2.3 Technology Stack
The technology we use is:

Frontend:

* React

Backend:

* Node.js (API services)
* Supabase (Postgres-based DB with authentication)

Automation:

* n8n (workflow automation for crawling, newsletter runs, fact-checking)

Search & Data Processing:

* OpenSearch / Elasticsearch

Project Management:

* GitHub
* Rational Unified Process (RUP) iteration planning - YouTrack

Deployment & DevOps:

* CI/CD pipelines (planned)
* Containerized environments (Docker/Kubernetes considered)

Testing:

* Jest / Cypress (frontend & API)
* Manual + automated test cases for newsletter generation and search filters

## 3. Specific Requirements

### 3.1 Functionality
This section explains the different use cases shown in the Use Case Diagram and their functionality.

Until December (MVP) we plan to implement:
- 3.1.1 Browse AI News
- 3.1.2 Subscribe to Newsletter
- 3.1.3 Receive Weekly Newsletter
- 3.1.4 Search & Filter Tools
- 3.1.5 Explore Learning Roadmaps

For later releases we plan to implement:
- 3.1.6 Suggest New Tools/Sources
- 3.1.7 Provide Feedback / Corrections
- 3.1.8 Admin Panel
- 3.1.9 Manage Database & Pipelines
- 3.1.10 Manage Users & Roles
- 3.1.11 Trigger Newsletter Run (via n8n)
- 3.1.12 Review/Edit/Publish Articles
- 3.1.1 Browse AI News

Visitors can read and navigate through the latest AI news, which are automatically collected, summarized, and tagged.

#### 3.1.2 Subscribe to Newsletter
Registered users can subscribe to receive the weekly newsletter.

#### 3.1.3 Receive Weekly Newsletter
Subscribers receive a curated newsletter summarizing the most relevant AI updates with source transparency.

#### 3.1.4 Search & Filter Tools
Visitors and registered users can search and filter through the AI tool directory using categories, domains, and budget.

#### 3.1.5 Explore Learning Roadmaps
Users can navigate role-based roadmaps (e.g., Data Engineer, ML Engineer) with structured paths and linked resources.

#### 3.1.6 Suggest New Tools/Sources
Registered users can propose new tools or sources to be added to the directory.

#### 3.1.7 Provide Feedback / Corrections
Registered users can suggest corrections or improvements to existing content.

#### 3.1.8 Admin Panel
Admins access a dashboard for managing users, roles, and platform-wide settings.

#### 3.1.9 Manage Database & Pipelines
Admins ensure the consistency and quality of stored news, tools, and roadmaps while managing automation pipelines.

#### 3.1.10 Manage Users & Roles
Admins manage user accounts and assign or revoke roles.

#### 3.1.11 Trigger Newsletter Run
The automation orchestrator (n8n) can initiate newsletter generation and delivery.

#### 3.1.12 Review/Edit/Publish Articles
Admins review automatically ingested articles before publishing them.

### 3.2 Usability
We aim to design the GrowKnow platform with a clean, intuitive, and responsive interface. The user experience should feel natural, requiring no special training.

#### 3.2.1 No Training Time Needed
Users should be able to navigate the platform easily, discover tools, and subscribe without needing documentation.

#### 3.2.2 Familiar Feeling
By using standard UI/UX patterns, GrowKnow feels familiar to users accustomed to modern platforms, reducing friction in adoption.

### 3.3 Reliability

#### 3.3.1 Availability
The server shall be available 95% of the time. This also means we have to figure out the "rush hours" of our app because the downtime of the server is only tolerable when as few as possible players want to use the app.

#### 3.3.2 Defect Rate
Our goal is that we have no loss of any data. This is important so that the game sessions can carry on, even after a downtime of the server.

### 3.4 Perfomance

#### 3.4.1 Capacity
The system should scale to handle thousands of concurrent visitors, with newsletter delivery supporting large mailing lists.

#### 3.4.2 Storage 
Stored data (tools, articles, feedback) should be optimized for efficiency without sacrificing accessibility.

#### 3.4.3 Response time
Pages and search queries should load within 1–2 seconds under normal load.

### 3.5 Supportability

#### 3.5.1 Coding Standards
We will follow industry best practices and clean code principles for both backend (Node.js, Express) and frontend (React).

#### 3.5.2 Testing Strategy
The system will use automated testing for core functionalities (user registration, newsletter, search). Unit, integration, and pipeline tests will ensure reliability.

### 3.6 Design Constraints
* Modular architecture (frontend, backend, automation orchestrator).
* RESTful APIs for data exchange.
* Tech stack: React, Node.js, PostgreSQL, n8n for automation.
* Hosted on scalable cloud infrastructure (e.g., Vercel, AWS).

### 3.7 On-line User Documentation and Help System Requirements
GrowKnow will provide a “Help” section with FAQs, tutorials, and contact forms. Most features are designed to be self-explanatory.

### 3.8 Purchased Components
We don't have any purchased components yet. If there will be purchased components in the future we will list them here.

### 3.9 Interfaces

#### 3.9.1 User Interfaces
The User interfaces that will be implented are:
- Dashboard: Lists AI news and tools with filters.
- Roadmap Page: Displays curated learning roadmaps.
- Newsletter: Subscription form and archive.
- Admin Panel: Content, users, and pipeline management.
- Profile Page: User account management.

#### 3.9.2 Hardware Interfaces
(n/a)

#### 3.9.3 Software Interfaces
- Browser-based frontend.
- RESTful APIs for backend.
- Automation workflows via n8n.

#### 3.9.4 Communication Interfaces
HTTP/HTTPS protocols for all interactions. 

### 3.10 Licensing Requirements
All open-source components used will comply with MIT, Apache, or similar permissive licenses.

### 3.11 Legal, Copyright, and Other Notices
The GrowKnow logo and brand are reserved for this project. We disclaim responsibility for third-party content accuracy.

### 3.12 Applicable Standards
The development will follow the common clean code standards and naming conventions. Also we will create a definition of d which will be added here as soon as its complete.

## 4. Supporting Information
For any further information you can contact the Common Playground Team or check our [GrowKnow Blog](https://knowgrow7.wordpress.com/). 
The Team Members are:
- Joaquin Berriel
- Emin
- Roic

<!-- Picture-Link definitions: -->
[OUCD]: https://github.com/IB-KA/CommonPlayground/blob/master/UseCaseDiagramCP.png "Overall Use Case Diagram"
