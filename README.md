# n8n Multi-Label Gmail to Google Sheets & Drive Automation

## Overview
This workflow automates the processing of incoming emails under monitored Gmail labels.
Every 30 minutes, the workflow checks Gmail for new messages matching the configured label, extracts important email metadata, detects attachments, archives those attachments into a structured Google Drive hierarchy, records one row per email in Google Sheets, and marks successfully processed Gmail messages as read

## Workflow
![n8n Workflow](n8n_workflow.png)

## Diagram Flowchart

```mermaid
graph TD;
    A[Schedule Trigger<br/>Every 30 Minutes] --> B[Gmail<br/>Get Labeled Emails];
    B --> C[Extract Sender Info];

    C --> D[Add Row to Sheet];
    D --> E[Mark as Read];

    C --> F{Has Attachments?};
    F -->|Yes| G[Loop Emails];
    G --> H[Current Email];
    H --> I[Find Label Folder];
    I --> J{Label Folder Missing?};

    J -->|Yes| K[Create Label Folder];
    K --> L[Find Date Folder];
    J -->|No| L;

    L --> M{Date Folder Missing?};
    M -->|Yes| N[Create Date Folder];
    N --> O[Find Sender Folder];
    M -->|No| O;

    O --> P{Sender Folder Missing?};
    P -->|Yes| Q[Create Sender Folder];
    Q --> R[Split Attachments];
    P -->|No| R;

    R --> S[Upload Attachment];
    S --> G;

    F -->|No| E;
```
## Features
- Gmail label-based email processing
- Email metadata extraction
- Automatic attachment archiving
- Structured Google Drive folders
- Google Sheets logging
- Duplicate folder prevention
- Scheduled processing

## Archive Structure

```text
<label>/<date>/<sender>/
```

### Example

```text
Receipts/
└── 2026-09-07/
    └── Sender Name/
        └── receipt.pdf
```

## Tech Stack

- n8n
- Google Authentication
- Google Drive
- Google Sheets
- JavaScript

### Tools

[![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)](https://n8n.io/)
[![Google](https://img.shields.io/badge/Google-4285F4?style=for-the-badge&logo=google&logoColor=white)](https://www.google.com/)
[![Google Drive](https://img.shields.io/badge/Google%20Drive-4285F4?style=for-the-badge&logo=googledrive&logoColor=white)](https://drive.google.com/)
[![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)](https://sheets.google.com/)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
