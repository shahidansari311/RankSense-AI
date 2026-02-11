# RankSense.AI // ENTERPRISE_CORE

**AI-Powered Resume Scoring & Intelligence System**

![RankSense Dashboard](https://via.placeholder.com/800x400.png?text=RankSense+Enterprise+Dashboard)

RankSense is an advanced resume parsing and ranking engine designed for high-volume recruitment. It uses Natural Language Processing (NLP) to extract skills, internships, and projects, and compares them against Job Descriptions (JDs) to provide a tactical "Gap Analysis".

## 🚀 Key Features

-   **Multi-Format Ingestion**: Supports `.pdf` and `.docx` resumes.
-   **NLP Gap Analysis**: Uses **Spacy** to identify matched vs. missing keywords from Job Descriptions.
-   **Weighted Scoring**: 12-factor algorithm (Internships, Projects, Skills, CGPA, etc.).
-   **Enterprise Dashboard**: "Cyberpunk/Enterprise" aesthetic with real-time WebSocket logs.
-   **Persistence**: SQLite database stores all candidate history.
-   **Detail Inspector**: Hover over candidates to see extracted snippets and gap analysis.
-   **CSV Export**: One-click export of ranked candidates.

## 🛠️ Installation & Run

**Prerequisites**: Python 3.9+

1.  **Clone the repository**:
    ```bash
    git clone https://github.com/shashank-tomar0/RankSense-AI.git
    cd RankSense-AI
    ```

2.  **One-Click Setup**:
    Double-click `install_reqs.bat`.
    *(This installs FastAPI, Uvicorn, Spacy, and downloads the NLP model)*.

3.  **Start the System**:
    Double-click `start_ranksense.bat`.
    
    This launches:
    -   **Backend (Brain)**: `http://localhost:8000`
    -   **Frontend (UI)**: `http://localhost:3000`

## 🧠 How It Works (The Backend Pipeline)

When you upload a resume, the backend (`main.py`) executes this **6-Step Pipeline**:

1.  **Ingestion & Async Processing**:
    -   Files are received via FastAPI `BackgroundTasks`.
    -   The server does *not* block; uploads happen in parallel.

2.  **Hybrid Extraction**:
    -   **PDFs**: Uses `pdfplumber` to extract layout-preserved text.
    -   **DOCX**: Uses `python-docx` to parse Word documents.
    -   **Feature Extraction**: Regex and Keyword/Pattern matching identify explicit sections (Education, Skills, Projects, Internships).

3.  **NLP Intelligence (Spacy)**:
    -   The system loads the `en_core_web_sm` NLP model.
    -   If a **Job Description** is provided, it extracts **Noun Chunks** (e.g., "Cloud Infrastructure", "Agile Methodology") to understand *concepts*, not just words.

4.  **Gap Analysis**:
    -   The AI compares Resume Tokens vs. JD Entities.
    -   It classifies keywords into **MATCHED (Green)** and **MISSING (Red)**.

5.  **Weighted Scoring Options**:
    -   It calculates a "Hacker Score" (0-100) based on:
        -   Internships (20%)
        -   Projects (15%)
        -   Skills matches (20%)
        -   Education/CGPA (10%)
        -   JD Relevance (Bonus Points)

6.  **Persistence & Broadcasting**:
    -   Results are saved to `ranksense.db` (SQLite) instantly.
    -   A JSON payload is broadcast via **WebSockets** to the frontend, updating the live dashboard and radar charts immediately.

## 🏗️ Tech Stack

-   **Backend**: Python, FastAPI, Uvicorn, SQLite
-   **AI/NLP**: Spacy, Regex
-   **Frontend**: HTML5, Vanilla JS, Tailwind CSS via CDN, Chart.js
-   **Protocol**: WebSockets (Real-time telemetry)

## 📜 License

MIT License. Built by **Team Xnords**.
