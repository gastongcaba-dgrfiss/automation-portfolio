# Automated Operational Monitoring & Alerting

**Workflow Automation · Scheduled Monitoring · Google Sheets · Operational Alerts**

> Turning manual case tracking into a continuously running operational monitoring system.

---

## Overview

Our team manages operational processes that move through multiple departments before reaching final approval.

Each process needs to be monitored to understand:

- Where it currently is
- When it entered a department
- How long it has remained there
- Whether it has moved since the previous review
- Whether a delay requires attention
- Whether a final resolution has been issued

Historically, this information was checked manually.

Someone on the team had to find time during the workday to open each case individually, review its history, calculate elapsed time, update a tracking spreadsheet and notify management when something required attention.

I automated this monitoring process.

Today, the system performs **four scheduled reviews per day**, updates the operational dashboards automatically, calculates elapsed time, sends status summaries and generates alerts when relevant events occur.

---

## The Problem

The original monitoring process depended entirely on human availability.

There was no dedicated person responsible only for monitoring.

The task was performed by someone who also had other operational responsibilities.

A typical review required:

1. Opening the tracking dashboard
2. Identifying every active case
3. Copying the case identifier
4. Accessing the government case-management system
5. Searching for the case
6. Opening its history
7. Identifying its current department
8. Checking the date of its latest movement
9. Returning to the tracking dashboard
10. Updating the corresponding information
11. Calculating how long the case had remained in its current stage
12. Identifying potential delays
13. Informing management when intervention might be necessary
14. Detecting whether a final resolution had been issued

One dashboard contains approximately **18 active cases**.

Two operational dashboards are currently monitored using this approach.

A single manual review could take approximately **30 minutes per dashboard**, depending on the number of movements and updates required.

---

## The Real Constraint: Human Availability

The main problem was not only the amount of time required.

Monitoring competed with every other task happening during the workday.

A review might happen in the morning.

It might happen closer to midday.

On a busy day, it might happen only once.

If the person usually responsible for the task was unavailable, the review could be delayed.

This meant that monitoring frequency depended on human capacity rather than operational need.

---

## The Solution

I designed an automated monitoring workflow that performs the repetitive tracking process independently.

Instead of requiring someone to manually inspect every case, the system periodically reviews the active portfolio and updates the operational dashboards.

The automation:

- Reviews active cases
- Identifies their current location
- Detects new movements
- Records relevant dates
- Calculates elapsed time in each stage
- Updates the tracking dashboard
- Identifies potential delays
- Sends scheduled status summaries
- Alerts the team when a final resolution appears

---

## How It Works

```text
        Active Cases
      (~18 per dashboard)
               │
               ▼
      Scheduled Automation
               │
               ▼
     Case Management System
               │
               ▼
        Retrieve History
               │
               ▼
       Detect Current Stage
               │
               ▼
       Detect New Movement
               │
               ▼
        Calculate Elapsed
          Time in Stage
               │
               ▼
       Update Dashboard
               │
        ┌──────┴──────┐
        ▼             ▼
   Status Summary   Event Detection
        │             │
        ▼             ▼
    Email Report    Resolution Alert
        │
        └──────┬──────┘
               ▼
      Management Visibility
```

---

## From Manual Checking to Scheduled Monitoring

### Before

Monitoring depended on someone finding time to perform it.

A typical pattern was:

`Person available → Open cases → Review histories → Update dashboard → Calculate delays → Notify management`

Reviews could happen once or twice per day depending on workload.

### After

Monitoring follows a scheduled operational rhythm:

`Early morning → Midday → Mid-afternoon → Late afternoon`

The system performs approximately **4 automated checks per day**.

The first review can be completed before the team arrives at the office.

Monitoring continues even when the person who previously performed the task is unavailable.

---

## Automated Time Tracking

The dashboard includes elapsed-time monitoring.

Instead of requiring someone to manually calculate how long a case has remained within a particular department, the system maintains the count automatically.

This makes it easier to identify cases that may require follow-up.

The workflow therefore does more than report:

> **Where is the case?**

It also provides:

> **Who currently has it, and for how long?**

This gives management better information for deciding when operational intervention may be necessary.

---

## Event-Driven Alerts

Some changes require more than a dashboard update.

When a final resolution is detected, the system automatically generates an email notification.

This changes the information flow.

### Before

`Person checks system → Finds resolution → Tells management`

### After

`Resolution appears → Automation detects it → Alert is sent`

The team no longer needs to continuously search for the event.

The event comes to the team.

---

## Scheduled Management Reports

In addition to updating the dashboards, the system generates email summaries describing the status of active cases.

These reports provide visibility into:

- Current stage
- Responsible department
- Time spent in that stage
- Relevant movements
- Cases requiring attention

This gives management a recurring operational overview without requiring direct access to every individual case.

---

## Impact

| Metric | Manual Monitoring | Automated Monitoring |
| --- | --- | --- |
| Active dashboards | 2 | 2 |
| Active cases | ~36 total | ~36 total |
| Review frequency | 1–2 times/day when possible | 4 scheduled checks/day |
| Availability dependency | High | Low |
| Case history review | Manual | Automated |
| Dashboard updates | Manual | Automated |
| Elapsed-time tracking | Manual | Automated |
| Status reporting | Manual/ad hoc | Scheduled |
| Resolution detection | Found during manual review | Automatic alert |
| Monitoring outside office activity | No | Yes |

### 2×–4× monitoring frequency

A workflow that previously depended on one or two manual reviews per day can now be executed four times per day consistently.

More importantly, monitoring no longer depends on someone remembering to perform the task or having enough time available.

---

## Operational Impact

The value of the automation is not primarily the number of minutes saved.

The larger improvement is **operational continuity**.

The workflow moved from:

> **Human-dependent checking**

to:

> **Systematic monitoring with human attention triggered when needed**

This reduces the risk of important changes going unnoticed and allows the team to focus on cases that actually require judgment or intervention.

---

## My Role

I identified the monitoring problem after working directly with the manual tracking process.

The challenge was not simply that reviewing cases was repetitive.

The process depended on someone interrupting other work, checking every case individually and remembering which situations required escalation.

I mapped the monitoring logic and translated it into an automated workflow.

This included:

- Identifying the information required from each case
- Mapping relevant status and movement data
- Automating scheduled reviews
- Designing elapsed-time calculations
- Automating dashboard updates
- Defining conditions for operational alerts
- Creating management summaries
- Iteratively refining the monitoring rules

The result changed the role of the team from **actively searching for changes** to **responding when the system identifies something relevant**.

---

## Design Principle

This project represents an important principle in how I think about operations automation:

> **People should not have to repeatedly check whether something happened. Systems can monitor; people can decide what to do next.**

---
## Tech Stack & Architecture

`Python` · `Playwright` · `Google Apps Script` · `Google Sheets` · `Google Triggers` · `Environment Variables` · `Browser Automation`

The monitoring system combines different technologies according to the role each one performs.

### Python + Playwright

Python handles the browser automation layer.

Using Playwright, the workflow accesses the government case-management system, navigates the required interfaces, searches for active cases and retrieves the information needed for monitoring.

Playwright Inspector was also used during development to understand and validate the navigation flow before translating it into automated browser interactions.

### Secure Authentication

Authentication credentials are kept outside the source code using environment variables (`.env`).

This prevents production credentials from being hard-coded into the automation logic.

### Google Apps Script

Google Apps Script handles part of the workflow orchestration and connects the monitoring process with the operational dashboards.

It is also used for automation logic around spreadsheet updates, calculations, notifications and reporting.

### Google Sheets

Google Sheets functions as the operational interface used by the team.

The dashboard contains the active portfolio and displays information such as:

- Current stage
- Responsible department
- Movement dates
- Time spent in each stage
- Relevant status changes
- Resolution status

### Scheduled Triggers

Google triggers are used to execute scheduled parts of the workflow throughout the day.

This allows monitoring to occur consistently without requiring someone to manually start each review.

---

## System Architecture

```text
             SCHEDULED TRIGGER
                    │
                    ▼
          WORKFLOW ORCHESTRATION
          Google Apps Script
                    │
                    ▼
          PYTHON AUTOMATION
                    │
              Playwright
                    │
                    ▼
        CASE MANAGEMENT SYSTEM
                    │
           Secure authentication
                via .env
                    │
                    ▼
            Browser navigation
                    │
                    ▼
           Case history retrieval
                    │
                    ▼
           Status interpretation
                    │
                    ▼
          GOOGLE SHEETS DASHBOARD
                    │
        ┌───────────┼───────────┐
        ▼           ▼           ▼
     Update      Elapsed      Change
     status       time       detection
        │           │           │
        └───────────┼───────────┘
                    ▼
             NOTIFICATION LAYER
                    │
           ┌────────┴────────┐
           ▼                 ▼
     Status reports     Resolution alerts
           │                 │
           └────────┬────────┘
                    ▼
             HUMAN DECISION
```

The architecture intentionally separates repetitive system monitoring from human decision-making.

The automation collects, updates and monitors operational information.

People remain responsible for deciding when and how to intervene.

---

## Privacy & Confidentiality

This case study describes the monitoring architecture and operational logic without exposing real case identifiers, internal documents, personal information or confidential organizational data.

All public portfolio materials use sanitized descriptions and representations.

---

## What I Would Improve Next

Future iterations could include:

- Centralized execution logs
- Monitoring-health alerts
- Historical performance analytics
- Average time by operational stage
- Bottleneck detection across departments
- Escalation thresholds based on historical behavior
- A dedicated monitoring interface
- Additional exception handling for system availability

---

[← Back to Portfolio](../README.md)
