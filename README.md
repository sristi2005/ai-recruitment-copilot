# 🤖 AI Recruitment Copilot

An AI-powered recruitment automation workflow built with **n8n** that automates resume screening, candidate evaluation, and recruiter-ready insights using an LLM.

The system accepts a candidate's resume through a form, extracts the resume content, analyzes it against the target role, generates structured evaluation results, stores the resume in Google Drive, and records candidate information in Google Sheets.

---

## 🚀 Overview

Recruiters often spend significant time manually reviewing resumes, identifying relevant skills, comparing candidates with job requirements, and preparing interview questions.

**AI Recruitment Copilot** automates this workflow by combining:

- Resume PDF processing
- LLM-based candidate analysis
- Prompt engineering
- Structured JSON generation
- Google Drive storage
- Google Sheets candidate tracking
- n8n workflow orchestration

The goal is to provide recruiters with a **consistent, structured, and automated first-level screening process**.

---

## ✨ Key Features

### 📄 Automated Resume Intake
- Accepts candidate information and resume PDFs through an n8n form.
- Captures recruiter name, target job role, and resume file.

### 🔍 Resume Processing
- Extracts text from uploaded PDF resumes.
- Passes the extracted content to an LLM for analysis.

### 🧠 AI-Powered Screening
The LLM generates structured candidate insights including:

- Candidate name
- Email
- Phone number
- Technical skills
- Match score
- Recommendation
- Missing skills
- Experience
- Resume summary
- Interview questions
- AI justification

### 📊 Structured Candidate Evaluation
Instead of relying on unstructured LLM responses, the workflow converts the model output into structured JSON and maps the fields into a recruiter-friendly format.

### ☁️ Automated Resume Storage
Uploaded resumes are automatically stored in a dedicated **Google Drive** folder.

### 📑 Candidate Database
Candidate evaluation results are automatically appended to a **Google Sheets** database for centralized tracking.

---

## 🏗️ Workflow Architecture

```text
Candidate
    │
    ▼
┌─────────────────────┐
│  n8n Form Trigger   │
│ Resume + Job Role   │
└──────────┬──────────┘
           │
           ├──────────────────────┐
           │                      │
           ▼                      ▼
┌─────────────────────┐   ┌─────────────────────┐
│  PDF Text Extraction│   │    Google Drive     │
│                     │   │   Resume Storage    │
└──────────┬──────────┘   └──────────┬──────────┘
           │                         │
           ▼                         │
┌─────────────────────┐              │
│    Groq LLM         │              │
│ Candidate Analysis  │              │
└──────────┬──────────┘              │
           │                         │
           ▼                         │
┌─────────────────────┐              │
│ JavaScript          │              │
│ JSON Transformation │              │
└──────────┬──────────┘              │
           │                         │
           └────────────┬────────────┘
                        ▼
              ┌─────────────────────┐
              │   Merge Workflow    │
              └──────────┬──────────┘
                         │
                         ▼
              ┌─────────────────────┐
              │   Google Sheets     │
              │ Candidate Database  │
              └─────────────────────┘
````

---

## 🛠️ Tech Stack

| Technology         | Purpose                                  |
| ------------------ | ---------------------------------------- |
| **n8n**            | Workflow automation and orchestration    |
| **Groq LLM**       | Resume analysis and candidate evaluation |
| **Google Drive**   | Resume storage                           |
| **Google Sheets**  | Candidate database and tracking          |
| **JavaScript**     | Data transformation and JSON processing  |
| **PDF Extraction** | Resume text extraction                   |
| **JSON**           | Structured AI output                     |

---

## 📋 AI Evaluation Output

The workflow generates structured candidate information such as:

```json
{
  "candidate_name": "Candidate Name",
  "email": "candidate@email.com",
  "phone": "+91XXXXXXXXXX",
  "skills": [
    "Python",
    "SQL",
    "Machine Learning",
    "NLP"
  ],
  "match_score": 85,
  "recommendation": "Strong Hire",
  "missing_skills": [],
  "experience": "2 years",
  "resume_summary": "Candidate with experience in...",
  "interview_questions": [
    "Explain your experience with machine learning.",
    "How have you used Python in your projects?"
  ],
  "ai_justification": "The candidate demonstrates..."
}
```

---

## 🔄 Workflow Steps

### 1. Resume Submission

The recruiter submits:

* Recruiter name
* Job role
* Candidate resume

through the n8n form.

### 2. Resume Extraction

The uploaded PDF is processed and its text is extracted for downstream analysis.

### 3. LLM Analysis

The extracted resume content is sent to the Groq LLM with a structured prompt.

The model evaluates the candidate and produces structured recruitment insights.

### 4. Data Transformation

A JavaScript node processes the model response and prepares individual fields for storage.

### 5. Resume Storage

The original resume is uploaded to a dedicated Google Drive folder.

### 6. Data Consolidation

A Merge node combines the AI evaluation data with the Google Drive resume information.

### 7. Candidate Tracking

The final candidate record is appended to Google Sheets.

---

## 🎯 Example Use Case

A recruiter is hiring for an **AI Engineer** position.

Instead of manually reviewing every resume:

```text
Resume Upload
     ↓
PDF Extraction
     ↓
AI Analysis
     ↓
Match Score
     ↓
Missing Skills
     ↓
Recommendation
     ↓
Interview Questions
     ↓
Google Drive + Google Sheets
```

The recruiter receives a structured candidate evaluation that can be reviewed quickly.

---

## 🧠 Prompt Engineering

The LLM prompt is designed to produce consistent and machine-readable output rather than free-form responses.

The workflow requests structured fields for:

* Candidate information
* Skills
* Match score
* Recommendation
* Missing skills
* Experience
* Resume summary
* Interview questions
* AI justification

This makes the LLM output easier to process programmatically and store in downstream systems.

---

## 📊 Candidate Database

The Google Sheets database stores fields such as:

| Field               | Description                              |
| ------------------- | ---------------------------------------- |
| Candidate Name      | Extracted candidate name                 |
| Email               | Candidate email                          |
| Phone               | Candidate contact                        |
| Skills              | Relevant technical skills                |
| Match Score         | AI-generated candidate-job match         |
| Recommendation      | Hiring recommendation                    |
| Missing Skills      | Skills absent from the candidate profile |
| Experience          | Relevant experience                      |
| Interview Questions | Generated technical questions            |
| Resume Link         | Stored Google Drive resume               |
| Resume Summary      | AI-generated summary                     |
| AI Justification    | Reason behind the recommendation         |

---

## ⚙️ Setup

### Prerequisites

* n8n account or self-hosted n8n instance
* Groq API key
* Google account
* Google Drive access
* Google Sheets access

### Steps

1. Import the n8n workflow into your n8n instance.
2. Configure the Groq credentials.
3. Configure Google Drive OAuth credentials.
4. Configure Google Sheets OAuth credentials.
5. Create a Google Drive folder for uploaded resumes.
6. Create a Google Sheet for the candidate database.
7. Map the Google Sheets columns to the workflow output.
8. Test the workflow using the n8n form.
9. Publish the workflow when testing is complete.
