# AI-Powered Healthcare Appointment & Patient Reminder System

## Project Overview

The AI-Powered Healthcare Appointment & Patient Reminder System is a workflow automation project developed using n8n. This system automates the healthcare appointment booking process by collecting patient details through a form, storing data automatically in Google Sheets, and sending confirmation emails to patients.

The project helps hospitals, clinics, and healthcare centers reduce manual work, improve patient communication, and manage appointments efficiently.

---

# Problem Statement

Hospitals and clinics often manage appointments manually, which leads to:

* Missed appointments
* Increased administrative workload
* Delayed patient communication
* Human errors in patient records
* Inefficient appointment management

Manual healthcare workflows consume time and reduce operational efficiency.

---

# Objective

To build an AI-powered healthcare workflow automation system using n8n that:

* Automates patient appointment booking
* Stores patient information automatically
* Sends automated confirmation emails
* Reduces manual healthcare administrative work
* Improves healthcare workflow efficiency

---

# Features

* Healthcare appointment booking form
* Automated patient data collection
* Google Sheets database integration
* Automated confirmation email system
* Real-time workflow automation
* Cloud deployment using Render
* GitHub integration

---

# Technologies Used

| Technology    | Purpose              |
| ------------- | -------------------- |
| n8n           | Workflow automation  |
| Google Sheets | Patient database     |
| Gmail API     | Email notifications  |
| Render        | Cloud deployment     |
| GitHub        | Version control      |
| Docker        | Container deployment |

---


# System Workflow

┌──────────────────────────────────────────────────────────┐
│                    Healthcare Appointment System         │
└──────────────────────────────────────────────────────────┘

        Patient Submits Appointment Form
        
                           │
                           ▼
┌──────────────────────────────────────────────────────────┐
│ 1. Form Submission Trigger                               │
│    - Collect patient details                             │
│    - Name, Email, Phone, Symptoms, Date                  │
└──────────────────────────────────────────────────────────┘

                           │
                           ▼
┌──────────────────────────────────────────────────────────┐
│ 2. Google Sheets Database                                │
│    - Store patient records                               │
│    - Maintain appointment history                        │
└──────────────────────────────────────────────────────────┘

                           │
                           ▼
┌──────────────────────────────────────────────────────────┐
│ 3. Data Processing (Edit Fields Node)                    │
│    - Clean and structure input data                      │
│    - Prepare AI prompt                                   │
└──────────────────────────────────────────────────────────┘

                           │
                           ▼
┌──────────────────────────────────────────────────────────┐
│ 4. AI Decision Engine                                    │
│    OpenAI Chat Model + Basic LLM Chain                   │
│    - Analyze symptoms                                    │
│    - Determine approval/rejection                        │
└──────────────────────────────────────────────────────────┘

                           │
                           ▼
┌──────────────────────────────────────────────────────────┐
│ 5. Decision Validation (IF Node)                         │
│    Check AI response                                     │
└───────────────────────┬──────────────────────────────────

                        │
          ┌─────────────┴─────────────┐
          │                           │
          ▼                           ▼

┌──────────────────────┐   ┌──────────────────────┐
│ 6A. Approved Flow    │   │ 6B. Rejected Flow    │
└──────────┬───────────┘   └──────────┬───────────┘
           │                          │
           ▼                          ▼

┌──────────────────────┐   ┌──────────────────────┐
│ Gmail Notification   │   │ Gmail Notification   │
│ Approval Email Sent  │   │ Rejection Email Sent │
└──────────┬───────────┘   └──────────────────────┘
           │
           ▼
┌──────────────────────────────────────────────────────────┐
│ 7. Google Calendar Integration                           │
│    - Create appointment event                            │
│    - Add patient details                                 │
│    - Schedule meeting automatically                      │
└──────────────────────────────────────────────────────────┘

                           │
                           ▼
┌──────────────────────────────────────────────────────────┐
│                 Appointment Successfully Managed         │
└──────────────────────────────────────────────────────────┘

---

# Architecture Diagram

                    ┌─────────────────────┐
                    │  Patient Form       │
                    │ (Form Submission)   │
                    └─────────┬───────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │ Google Sheets       │
                    │ Store Patient Data  │
                    └─────────┬───────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │ Edit Fields         │
                    │ Prepare AI Prompt   │
                    └─────────┬───────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │ OpenAI Chat Model   │
                    │ AI Decision Engine  │
                    └─────────┬───────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │ Basic LLM Chain     │
                    │ Analyze Symptoms    │
                    └─────────┬───────────┘
                              │
                              ▼
                    ┌─────────────────────┐
                    │ IF Condition        │
                    │ Approved/Rejection  │
                    └──────┬───────┬──────┘
                           │       │
                    TRUE   │       │ FALSE
                           │       │
                           ▼       ▼

              ┌─────────────────┐   ┌─────────────────┐
              │ Gmail Node      │   │ Gmail Node      │
              │ Approval Email  │   │ Rejection Email │
              └────────┬────────┘   └─────────────────┘
                       │
                       ▼
              ┌─────────────────┐
              │ Google Calendar │
              │ Create Event    │
              └─────────────────┘

---

# Project Setup

## Step 1: Clone Repository

```bash
git clone https://github.com/gdimpulchandrika-rgb/healthcare-automation-system.git
```

---

## Step 2: Open Project Folder

```bash
cd healthcare-automation-system
```

---

# Running n8n Locally

## Install n8n

```bash
npm install n8n -g
```

## Start n8n

```bash
n8n start
```

---

# Workflow Configuration

## Form Trigger

The system uses an n8n Form Trigger node to collect patient information.

### Form Fields

* Patient Name
* Email
* Doctor Name
* Appointment Date
* Symptoms

---

## Google Sheets Integration

Patient data is automatically stored in Google Sheets.

### Columns Used

| Name | Email | Appointment Date | Doctor | Symptoms |

---

## Gmail Integration

The system sends automatic confirmation emails to patients.

### Example Email

```text
Hello Patient,

Your appointment has been confirmed successfully.

Patient Name: 
Doctor: 
Appointment Date: 
Symptoms: 

Thank you,
Healthcare Team
```

---

# Deployment on Render

## Dockerfile

```dockerfile
FROM n8nio/n8n

EXPOSE 5678

CMD ["n8n"]
```

---

## Environment Variables

| Key                 | Value   |
| ------------------- | ------- |
| N8N_HOST            | 0.0.0.0 |
| N8N_PORT            | 5678    |
| N8N_PROTOCOL        | https   |
| N8N_RUNNERS_ENABLED | false   |

---

## Deployment Steps

1. Push project to GitHub
2. Create Render Web Service
3. Connect GitHub repository
4. Add environment variables
5. Deploy application
6. Import n8n workflow
7. Reconnect Gmail and Google Sheets credentials

---

# Real-World Use Case

This system can be used in:

* Hospitals
* Clinics
* Diagnostic centers
* Telemedicine platforms
* Healthcare startups

The automation system improves appointment management and reduces manual administrative workload.

---

# Benefits of the Project

* Saves healthcare staff time
* Reduces manual work
* Improves patient communication
* Stores patient records automatically
* Reduces appointment errors
* Enhances workflow efficiency

---

# Future Enhancements

Future improvements that can be added:

* AI health recommendations
* WhatsApp appointment reminders
* SMS notifications
* Doctor dashboard
* Appointment scheduling system
* AI symptom analysis
* Medical report summarizer
* Chatbot integration

---

# Project Outcome

Successfully developed and deployed a healthcare workflow automation system that:

* Automates patient appointment booking
* Stores patient information in real-time
* Sends automated email confirmations
* Demonstrates workflow automation using n8n

---

# Resume Description

Developed and deployed an AI-powered healthcare appointment automation system using n8n, Google Sheets, Gmail API, Docker, and Render. The system automates patient appointment booking, stores patient records, and sends automated confirmation emails to improve healthcare workflow efficiency.

---

# Skills Demonstrated

* Workflow Automation
* API Integration
* Healthcare Automation
* Google Sheets Integration
* Gmail Automation
* Cloud Deployment
* Docker
* GitHub
* No-Code/Low-Code Development

---

# GitHub Repository

Repository Link:

[https://github.com/gdimpulchandrika-rgb/healthcare-automation-system](https://github.com/gdimpulchandrika-rgb/healthcare-automation-system)

---

# Author

Dimpul Chandrika

---

# Conclusion

The AI-Powered Healthcare Appointment & Patient Reminder System demonstrates how workflow automation can improve healthcare management by reducing manual administrative work and improving patient communication.

This project provides a real-world healthcare automation solution using modern no-code automation tools.

- AI health tips
- WhatsApp reminders
- Appointment scheduling
- Doctor dashboard
