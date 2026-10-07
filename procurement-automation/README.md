# Procurement Document Automation

**Python · Playwright · Browser Automation · Process Automation**

> Automating a high-volume procurement workflow involving multiple bidders, documentation requirements and 500+ files per process.

---

## Overview

A government procurement process required our team to retrieve, classify and organize hundreds of documents submitted by multiple bidders through a multi-step procurement portal.

During the first process, two people spent approximately two hours manually navigating the platform, opening each bidder, reviewing documentation requirements, downloading files, creating folder structures and organizing the resulting documents.

With multiple procurement processes expected over the following months, repeating the same workflow manually would consume significant operational capacity.

Instead of scaling the manual work, I designed and built a browser automation workflow to execute the process autonomously.

---

## The Problem

Each procurement process can involve approximately **8–12 bidders**.

Each bidder has multiple documentation requirements, and each requirement may contain several individual files.

The manual workflow required:

1. Opening the procurement platform
2. Searching for the procurement process
3. Navigating to the bid-opening section
4. Identifying every bidder
5. Opening each bidder individually
6. Identifying its documentation requirements
7. Opening each requirement
8. Downloading every associated file
9. Determining how each document should be classified
10. Creating the corresponding folder structure
11. Detecting duplicate or previously downloaded files
12. Organizing the final documentation

A single procurement process can involve **500+ files**.

The first complete process required approximately **two hours of work involving two people**.

The repetitive nature of the workflow made it a strong candidate for automation.

---

## The Solution

I built a Python-based browser automation workflow using **Playwright**.

The operator provides only:

- Procurement process ID
- Group
- Destination folder

The automation then executes the operational workflow.

```text
Process ID + Group + Destination
                │
                ▼
        Python Automation
                │
                ▼
       Procurement Portal
                │
                ▼
          Secure Login
       (.env credentials)
                │
                ▼
          Find Process
                │
                ▼
       Bid Opening Section
                │
                ▼
        Discover Bidders
                │
                ▼
     Identify Requirements
                │
                ▼
       Retrieve Documents
                │
                ▼
       Classify Documents
                │
                ▼
       Duplicate Detection
                │
                ▼
      Build Folder Structure
                │
                ▼
        Retry Failed Items
                │
                ▼
          Final Output
