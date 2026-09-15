# jira-service-management-zero-to-hero
Hands-on Jira Service Management Zero-to-Hero project series covering 8 real-world projects from IT Help Desk and ITSM to Assets, CMDB, Incident Response, DevOps integrations, APIs, automation, AI, and Enterprise Service Management.

> **Learn Jira Service Management by building real projects from Zero to Hero.**

---


# 🏗️ The 8 Major Projects

```text
                    JSM ZERO TO HERO
                           |
        +------------------+------------------+
        |                  |                  |
        v                  v                  v
   BEGINNER           INTERMEDIATE         ADVANCED
        |                  |                  |
        v                  v                  v
 Project 1           Project 3           Project 6
 IT Help Desk        Enterprise ITSM     Monitoring
        |                  |              Incident Response
        v                  v                  |
 Project 2           Project 4               v
 Employee Service    Assets + CMDB       Project 7
 Management                               DevOps + APIs
        |                  |
        +------------------+
                 |
                 v
          Project 5
       Knowledge + Self-Service
                 |
                 v
          Project 8
   Enterprise Service Management
```

---

# 🟢 PROJECT 1 — IT Help Desk

## Level: Beginner

This is the starting point of the Zero-to-Hero journey.

We will build a complete internal IT Help Desk for an organization.

The project will introduce the fundamental JSM concepts while building something that looks like a real company Service Desk.

---

## What We Build

### Jira & JSM Setup

* Atlassian account
* Jira Cloud
* Jira Service Management
* Service project
* Project configuration
* Project settings

### Users

* Agents
* Customers
* Users
* Groups
* Roles
* Organizations

### Service Portal

* Customer portal
* Help Center
* Portal configuration
* Portal branding
* Request categories
* Customer experience

### Request Management

Create real-world request types:

* Laptop Issue
* Laptop Request
* Software Installation
* Password Reset
* VPN Issue
* Email Issue
* Wi-Fi Issue
* Access Request
* General IT Support

### Forms

* Forms
* Form fields
* Required fields
* Conditional fields
* Custom fields
* Customer-facing fields

### Workflows

Build a complete request lifecycle:

```text
Open
  ↓
In Progress
  ↓
Waiting for Customer
  ↓
Resolved
  ↓
Closed
```

### Queues

Create queues for:

* New Requests
* Unassigned Requests
* High Priority
* Critical Requests
* Waiting for Customer
* SLA Breached

### Approvals

Implement approval workflows for requests such as:

* Software installation
* Access requests
* Hardware requests

### Notifications

* Customer notifications
* Agent notifications
* Internal communication
* Public comments
* Internal comments

### SLA

Implement basic:

* First Response SLA
* Resolution SLA
* Priority-based SLA

### Automation

Build automations for:

* Auto assignment
* Notifications
* Priority updates
* Status transitions
* Customer communication
* Escalation

### Knowledge Base

Create basic self-service documentation for common IT issues.

---

## 🎯 Final Result

A complete:

> **Company IT Help Desk**

This project teaches the foundation required for everything that follows.

---

# 🟢 PROJECT 2 — Employee Service Management

## Level: Beginner → Intermediate

Now we move beyond IT support.

We will build an **Employee Service Management platform** where employees can request services from different internal teams.

---

## Departments

```text
Enterprise
│
├── IT
├── HR
├── Finance
├── Facilities
└── Security
```

---

## HR Service Requests

Build request types such as:

* Employee Onboarding
* Employee Offboarding
* Leave Request
* Employment Letter
* Payroll Question
* Benefits Request
* Personal Information Update

---

## IT Employee Requests

* Laptop Request
* Software Request
* Access Request
* VPN Access
* Application Access

---

## Facilities Requests

* Office Access
* Desk Request
* Maintenance Request
* Equipment Request

---

## Finance Requests

* Expense Request
* Purchase Request
* Invoice Question

---

## Concepts Covered

* Multiple organizations
* Multiple request types
* Service catalogs
* Forms
* Approvals
* Department-based routing
* Queues
* SLAs
* Notifications
* Automation
* Customer permissions
* Request visibility
* Internal vs external communication

---

## Automation Examples

```text
Employee submits request
        ↓
Identify request type
        ↓
Identify department
        ↓
Assign team
        ↓
Check approval requirement
        ↓
Send notification
        ↓
Track SLA
        ↓
Resolve request
```

---

## 🎯 Final Result

A complete:

> **Enterprise Employee Service Management Portal**

---

# 🟡 PROJECT 3 — Enterprise ITSM Platform

## Level: Intermediate

Now we build a proper IT Service Management platform.

This project focuses heavily on **ITSM practices**.

---

# Incident Management

Build the complete Incident Management lifecycle.

### Concepts

* Incident
* Impact
* Urgency
* Priority
* P1
* P2
* P3
* P4
* Assignment
* Escalation
* Resolution

---

# Major Incident Management

Build a major incident process.

### Concepts

* Major incident
* Incident commander
* Stakeholders
* Communication
* Escalation
* Incident timeline
* Resolution
* Post-incident review

---

# Problem Management

Build Problem Management.

### Concepts

* Incident vs Problem
* Root cause
* Known error
* Workaround
* Investigation
* Problem lifecycle
* Linking incidents to problems

---

# Change Management

Build a Change Management process.

### Change Types

* Standard Change
* Normal Change
* Emergency Change

### Concepts

* Change request
* Risk
* Impact
* Approval
* Implementation
* Validation
* Closure
* Change workflow
* Change calendar concepts

---

# Service Request Management

Build fulfillment processes for:

* Access
* Hardware
* Software
* Accounts
* Applications

---

# ITSM Relationships

Build relationships such as:

```text
Incident
   ↓
Problem
   ↓
Root Cause
   ↓
Change
   ↓
Permanent Fix
```

---

# SLA & Escalation

Build different SLA policies for:

```text
P1 → Critical
P2 → High
P3 → Medium
P4 → Low
```

Implement:

* Response SLA
* Resolution SLA
* Business hours
* SLA pause
* SLA breach
* Escalation

---

## 🎯 Final Result

A realistic:

> **Enterprise ITSM Platform**

---

# 🟡 PROJECT 4 — IT Asset Management & CMDB

## Level: Intermediate

Now we connect Service Management with the infrastructure behind the services.

The goal is to build an **IT Asset and CMDB environment**.

---

# Assets

Create assets for:

* Employees
* Laptops
* Desktops
* Servers
* Applications
* Databases
* Networks
* Cloud Resources
* Software
* Vendors

---

# CMDB

Build:

* Object schemas
* Object types
* Objects
* Attributes
* References
* Relationships
* Dependencies

---

# Infrastructure Relationships

Example:

```text
Business Service
       ↓
Application
       ↓
Application Server
       ↓
Database
       ↓
Cloud Infrastructure
```

---

# Service Mapping

Understand:

* Business services
* Technical services
* Service ownership
* Service dependencies
* Infrastructure relationships

---

# Connect Assets With JSM

Use assets in:

* Requests
* Incidents
* Changes
* Forms
* Automation
* Service management

---

# Real-World Scenario

An employee reports:

> "The Payroll Application is not working."

The Service Desk should be able to understand:

```text
Incident
   ↓
Payroll Application
   ↓
Application Server
   ↓
Database
   ↓
Cloud Infrastructure
```

---

## 🎯 Final Result

A complete:

> **IT Asset Management + CMDB Platform**

---

# 🟡 PROJECT 5 — Knowledge Management & Self-Service Platform

## Level: Intermediate

The goal of this project is to reduce unnecessary tickets by giving customers a powerful self-service experience.

---

# Knowledge Base

Build a knowledge repository for:

* Password Reset
* VPN Troubleshooting
* Email Troubleshooting
* Wi-Fi Troubleshooting
* Laptop Issues
* Software Installation
* MFA Problems
* Access Problems
* Common IT Questions

---

# Self-Service

Implement:

* Help Center
* Knowledge search
* Customer self-service
* Knowledge suggestions
* Request deflection
* Common issue resolution

---

# Knowledge Lifecycle

Build a process for:

```text
Create Article
      ↓
Review
      ↓
Approve
      ↓
Publish
      ↓
Customer Uses Article
      ↓
Feedback
      ↓
Update
```

---

# Service Desk Integration

Connect knowledge with:

* Request types
* Portal
* Incidents
* Customer experience
* Agent workflows

---

# 🎯 Final Result

A:

> **Self-Service + Knowledge Management Platform**

designed to reduce Service Desk workload and improve customer experience.

---

# 🔴 PROJECT 6 — Monitoring → Incident Response Platform

## Level: Advanced

Now we move into modern, event-driven Service Management.

Instead of an engineer manually creating every incident, monitoring systems will generate alerts that flow into JSM.

---

# Architecture

```text
Application
     ↓
Monitoring
     ↓
Alert
     ↓
JSM
     ↓
Incident
     ↓
Priority
     ↓
On-Call Engineer
     ↓
Escalation
     ↓
Resolution
```

---

# Monitoring

Understand:

* Monitoring systems
* Events
* Alerts
* Alert severity
* Alert routing
* Alert grouping
* Alert deduplication

---

# Incident Creation

Build automation for:

```text
Critical Alert
      ↓
Create Incident
      ↓
Set Priority
      ↓
Assign Team
      ↓
Notify On-Call
```

---

# On-Call

Implement concepts around:

* On-call schedules
* Rotations
* Escalation policies
* Notifications
* Incident ownership

---

# Major Incident Automation

Automate:

* Major incident creation
* Priority escalation
* Team notification
* Stakeholder communication
* Incident tracking
* Resolution workflow

---

# Post-Incident Process

Implement:

* Incident review
* Problem creation
* Root cause analysis
* Knowledge article creation
* Follow-up actions

---

## 🎯 Final Result

A:

> **Monitoring → Alert → JSM Incident → On-Call → Resolution Platform**

---

# 🔴 PROJECT 7 — DevOps + JSM Integration Platform

## Level: Advanced

Now we connect Jira Service Management with the DevOps ecosystem.

---

# Architecture

```text
Developer
    ↓
Git Repository
    ↓
CI/CD
    ↓
Deployment
    ↓
Application
    ↓
Monitoring
    ↓
Alert
    ↓
JSM
    ↓
Incident
```

---

# Integrations

Explore integration patterns with:

* Git platforms
* CI/CD platforms
* Monitoring tools
* Cloud platforms
* Collaboration platforms
* External applications

---

# Webhooks

Implement:

* Incoming webhooks
* Outgoing webhooks
* HTTP requests
* JSON payloads
* Event-driven automation

---

# REST API

Use JSM APIs to:

* Create requests
* Read requests
* Update requests
* Add comments
* Assign requests
* Transition requests
* Search requests
* Work with customers
* Work with organizations

---

# API Integration

Build:

```text
External Application
        ↓
      REST API
        ↓
Jira Service Management
        ↓
     Request
        ↓
    Workflow
        ↓
   Automation
```

---

# DevOps Use Cases

Build scenarios such as:

### Deployment Failure

```text
Deployment Failed
       ↓
Automation
       ↓
Create JSM Incident
       ↓
Assign DevOps Team
       ↓
Notify Engineer
       ↓
Resolve
```

### Change Management

```text
Deployment
    ↓
Change Request
    ↓
Approval
    ↓
Deployment
    ↓
Validation
```

---

## 🎯 Final Result

A:

> **DevOps + JSM + Monitoring + API Integration Platform**

---

# 🏆 PROJECT 8 — Enterprise Service Management Platform

## Level: Zero to Hero Final Project

This is the final project.

Everything we learned in the previous projects comes together into one large enterprise implementation.

---

# Enterprise Structure

```text
                         ENTERPRISE
                              |
       +----------------------+----------------------+
       |                      |                      |
       ▼                      ▼                      ▼
      IT                     HR                   Finance
       |                      |                      |
       ▼                      ▼                      ▼
  IT Services          Employee Services       Finance Services
       |                      |                      |
       +----------------------+----------------------+
                              |
                              ▼
                       JSM PLATFORM
                              |
       +----------------------+----------------------+
       |                      |                      |
       ▼                      ▼                      ▼
    Requests              Incidents              Changes
       |                      |                      |
       +----------------------+----------------------+
                              |
                              ▼
                         WORKFLOWS
                              |
       +----------------------+----------------------+
       |                      |                      |
       ▼                      ▼                      ▼
    APPROVALS                SLA               AUTOMATION
       |                      |                      |
       +----------------------+----------------------+
                              |
       +----------------------+----------------------+
       |                      |                      |
       ▼                      ▼                      ▼
    KNOWLEDGE              ASSETS                SERVICES
       |                      |                      |
       +----------------------+----------------------+
                              |
                              ▼
                       MONITORING / ALERTS
                              |
                              ▼
                        DEVOPS / APIs
                              |
                              ▼
                       AI / ROVO CAPABILITIES
                              |
                              ▼
                    REPORTING / DASHBOARDS
```

---

# Enterprise Service Catalog

Build services for:

## IT

* IT Support
* Infrastructure
* Network
* Security
* DevOps

## HR

* Employee Onboarding
* Employee Offboarding
* Benefits
* Payroll
* HR Requests

## Finance

* Expenses
* Purchase Requests
* Invoices
* Finance Support

## Facilities

* Office Access
* Maintenance
* Equipment
* Workplace Services

---

# ITSM

The final project includes:

* Incident Management
* Major Incident Management
* Problem Management
* Change Management
* Service Request Management

---

# Service Portal

Build:

* Help Center
* Service Portal
* Service Catalog
* Request Types
* Forms
* Customer experience

---

# Workflow Engine

Implement:

* Custom statuses
* Transitions
* Conditions
* Validators
* Post-functions
* Approval workflows

---

# SLA

Implement:

* First Response SLA
* Resolution SLA
* Business calendars
* Priority-based SLAs
* SLA pause
* SLA breach
* Escalation

---

# Automation

Build automation for:

* Assignment
* Prioritization
* Escalation
* Approvals
* Notifications
* SLA breaches
* Incident management
* Change management
* Customer communication

---

# Knowledge

Implement:

* Knowledge Base
* Self-Service
* Knowledge Search
* Request Deflection
* Agent Knowledge

---

# Assets / CMDB

Build relationships between:

* Employees
* Applications
* Servers
* Databases
* Networks
* Cloud resources
* Services

---

# Monitoring & Incident Response

Integrate:

```text
Monitoring
    ↓
Alert
    ↓
JSM
    ↓
Incident
    ↓
On-Call
    ↓
Escalation
    ↓
Resolution
```

---

# DevOps

Integrate:

```text
Code
 ↓
CI/CD
 ↓
Deployment
 ↓
Monitoring
 ↓
Incident
 ↓
Change
```

---

# APIs & Webhooks

Implement:

* REST APIs
* API authentication
* JSON
* Webhooks
* HTTP requests
* External integrations
* API-driven request creation
* API-driven automation

---

# AI & Rovo

Explore modern AI-assisted Service Management capabilities, including:

* AI-assisted support
* Knowledge discovery
* Search
* Summarization
* Agent assistance
* Automated assistance
* AI + automation
* AI governance
* Human approval and oversight

---

# Security & Administration

Implement and understand:

* Users
* Groups
* Roles
* Permissions
* Customer access
* Project permissions
* Issue security
* Governance
* Audit
* Least privilege

---

# Reporting & Dashboards

Build dashboards for:

* Request volume
* Incident volume
* SLA performance
* Resolution time
* Response time
* Major incidents
* Change activity
* Agent workload
* Customer satisfaction
* Service performance

---

# 🏆 Final Architecture

The final environment should demonstrate the complete lifecycle:

```text
                         CUSTOMER
                            |
                            ▼
                      HELP CENTER
                            |
                            ▼
                     SERVICE PORTAL
                            |
                            ▼
                        REQUEST
                            |
                            ▼
                       WORKFLOW
                            |
             +--------------+--------------+
             |              |              |
             ▼              ▼              ▼
          APPROVAL          SLA         AUTOMATION
             |              |              |
             +--------------+--------------+
                            |
                            ▼
                       SERVICE TEAM
                            |
          +-----------------+-----------------+
          |                 |                 |
          ▼                 ▼                 ▼
       INCIDENT          PROBLEM           CHANGE
          |                 |                 |
          +-----------------+-----------------+
                            |
                            ▼
                       KNOWLEDGE
                            |
                            ▼
                       ASSETS / CMDB
                            |
                            ▼
                         SERVICES
                            |
                            ▼
                      MONITORING
                            |
                            ▼
                          ALERT
                            |
                            ▼
                       ON-CALL
                            |
                            ▼
                       DEVOPS / API
                            |
                            ▼
                      AUTOMATION
                            |
                            ▼
                    AI / ROVO
                            |
                            ▼
                  REPORTING / DASHBOARD
```

---

# 📊 Project Progression

| Project       | Level           | Primary Focus                  |
| ------------- | --------------- | ------------------------------ |
| **Project 1** | 🟢 Beginner     | IT Help Desk                   |
| **Project 2** | 🟢 Beginner+    | Employee Service Management    |
| **Project 3** | 🟡 Intermediate | Enterprise ITSM                |
| **Project 4** | 🟡 Intermediate | Assets & CMDB                  |
| **Project 5** | 🟡 Intermediate | Knowledge & Self-Service       |
| **Project 6** | 🔴 Advanced     | Monitoring & Incident Response |
| **Project 7** | 🔴 Advanced     | DevOps, APIs & Integrations    |
| **Project 8** | 🏆 Hero         | Enterprise Service Management  |

---

# 📚 Skills Covered

By completing all 8 projects, you will have hands-on exposure to:

### Jira Service Management

* Projects
* Customers
* Agents
* Organizations
* Portals
* Help Centers
* Request Types
* Forms
* Queues
* Workflows
* Approvals
* Notifications
* Email

### ITSM

* Incident Management
* Major Incident Management
* Problem Management
* Change Management
* Service Request Management
* Knowledge Management
* Asset Management
* CMDB

### Service Management

* Service Catalog
* Business Services
* Technical Services
* Service Dependencies
* Service Ownership
* Customer Experience

### SLA

* Response SLA
* Resolution SLA
* Business Hours
* SLA Pause
* SLA Breach
* Escalation

### Automation

* Triggers
* Conditions
* Actions
* Smart Values
* Variables
* Branching
* Scheduled Automation
* Webhooks
* HTTP Requests
* Advanced Automation

### Assets

* Object Schemas
* Object Types
* Objects
* Attributes
* Relationships
* References
* Services
* Dependencies

### Incident Response

* Alerts
* Alert Routing
* Alert Deduplication
* On-Call
* Escalation
* Major Incident Response

### Integrations

* Monitoring
* DevOps
* CI/CD
* Collaboration Tools
* Cloud Platforms
* External Applications
* Webhooks

### Developer

* REST APIs
* HTTP
* JSON
* Authentication
* GET
* POST
* PUT
* DELETE
* API Automation

### AI

* AI-assisted Service Management
* Knowledge Discovery
* Search
* Summarization
* Agent Assistance
* AI + Automation
* AI Governance

### Administration

* Users
* Groups
* Roles
* Permissions
* Security
* Governance
* Audit

### Reporting

* JQL
* Dashboards
* SLA Metrics
* Incident Metrics
* Request Metrics
* Service Metrics
* Customer Metrics

### Enterprise

* IT
* HR
* Finance
* Facilities
* Security
* Enterprise Service Management

---

# 💰 Lab Strategy

The projects follow a **Free-first approach** wherever possible.

Some advanced JSM capabilities may require:

* A Premium trial
* A paid JSM plan
* Additional Atlassian products
* External services or integrations

When a project requires a feature that is not available on the Free plan, the project will clearly identify that requirement.

```text
🟢 FREE
Can be implemented using the available Free-plan capabilities.

🟡 PREMIUM / TRIAL
Requires a higher plan or trial for the hands-on implementation.

🔵 CONCEPT
The concept is explained even if the full implementation
requires an additional product or plan.
```

---

# 📂 Repository Structure

```text
jira-service-management-zero-to-hero/
│
├── README.md
│
├── Project-01-IT-Help-Desk/
│
├── Project-02-Employee-Service-Management/
│
├── Project-03-Enterprise-ITSM/
│
├── Project-04-IT-Asset-CMDB/
│
├── Project-05-Knowledge-Self-Service/
│
├── Project-06-Monitoring-Incident-Response/
│
├── Project-07-DevOps-API-Integration/
│
└── Project-08-Enterprise-Service-Management/
```

---

# 🎓 How To Follow This Series

Each project should follow the same approach:

```text
1. Understand the Business Requirement
              ↓
2. Design the JSM Solution
              ↓
3. Configure the Environment
              ↓
4. Build the Service
              ↓
5. Configure Workflows
              ↓
6. Configure SLAs
              ↓
7. Add Automation
              ↓
8. Add Knowledge / Assets
              ↓
9. Integrate External Systems
              ↓
10. Test Real-World Scenarios
              ↓
11. Troubleshoot
              ↓
12. Apply Best Practices
```

---

# 🚀 Zero-to-Hero Journey

```text
                    START
                      |
                      ▼
             🟢 IT HELP DESK
                      |
                      ▼
          🟢 EMPLOYEE SERVICES
                      |
                      ▼
           🟡 ENTERPRISE ITSM
                      |
                      ▼
            🟡 ASSETS + CMDB
                      |
                      ▼
         🟡 KNOWLEDGE + SELF-SERVICE
                      |
                      ▼
        🔴 MONITORING + INCIDENT RESPONSE
                      |
                      ▼
        🔴 DEVOPS + API + INTEGRATIONS
                      |
                      ▼
       🏆 ENTERPRISE SERVICE MANAGEMENT
                      |
                      ▼
                 JSM HERO 🚀
```

---

# 🏁 Final Goal

This repository is designed to become a **complete portfolio of real-world Jira Service Management implementations**.

The objective is not simply to finish eight projects.

The objective is to understand how JSM is used in the real world:

> **From a simple employee support request to a fully integrated enterprise Service Management platform.**

Build it.

Break it.

Troubleshoot it.

Automate it.

Integrate it.

And become a **Jira Service Management Hero.** 🚀
