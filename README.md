# n8n Multi-Label Gmail to Google Sheets & Drive Automation

## Overview
This workflow automates the processing of incoming emails under monitored Gmail labels.
Every 30 minutes, the workflow checks Gmail for new messages matching the configured label, extracts important email metadata, detects attachments, archives those attachments into a structured Google Drive hierarchy, records one row per email in Google Sheets, and marks successfully processed Gmail messages as read

## Workflow

![n8n Multi-Label Gmail Automation Workflow](n8n_automation_workflow.png)

## Diagram Flowchart

```mermaid
graph TD;
    A[Schedule Trigger<br/>Every 30 Minutes] --> B[Gmail<br/>Get Messages];
    B --> C[Extract Email Information];
    C --> D{Has Attachments?};
    D -->|Yes| E[Loop Through Emails];
    E --> F[Resolve Google Drive Folders];
    F --> G[Upload Attachment];
    G --> H[Log to Google Sheets];
    H --> I[Mark Gmail Message as Read];
    D -->|No| I;
```
