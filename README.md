# CareerCraft Pro

CareerCraft Pro is a Streamlit-based AI career assistant that combines interview practice, CV analysis, resume rewriting, cover letter generation, LinkedIn profile writing, and progress tracking in one app.

The project is built as a single-file Streamlit application: [interview_agent.py](/Users/abid/Downloads/CareerCraft/interview_agent.py).

See live preview at https://career-craft-pro.streamlit.app

## What It Does

CareerCraft Pro helps a user prepare for job applications end to end:

- Practice mock interviews with AI-generated questions and instant feedback
- Analyse a CV against a target role and job description
- Rewrite a CV for stronger ATS and recruiter performance
- Edit and export the rewritten CV
- Generate tailored cover letters using CV and job-description context
- Create a LinkedIn About section
- Track interview history and basic performance analytics

## Main Features

### 1. Interview Coach

- Multiple interview modes:
  - Full Interview
  - Behavioural
  - Technical
  - Situational
  - Speed Round
  - Stress Test
- Difficulty levels for junior to executive candidates
- Resume-aware interview question generation
- Instant scoring and STAR-based answer feedback
- Rewritten answer suggestions
- Follow-up coaching prompts
- Session save and history export

### 2. CV Analyser

- Works independently without starting an interview session
- Upload CV in `PDF`, `TXT`, or `DOCX`
- Paste a job description or provide a job URL
- Match score out of 100
- Section-by-section scoring:
  - Work Experience
  - Skills & Keywords
  - Education & Credentials
  - CV Format & ATS
  - Achievements & Impact
- Keyword gap detection
- ATS and grammar observations
- Actionable quick wins

### 3. CV Rewrite

- AI-powered rewrite based on the uploaded CV and target role
- Multiple rewrite tones
- Inline editing after generation
- Download options:
  - `.txt`
  - `.doc`
  - `.docx`

### 4. Cover Letter Generator

- Reuses `position`, `company`, and `job description` from the CV Analyser when available
- Also supports fully manual entry
- Uses CV context when available for better personalization
- Multiple letter styles
- Inline editing and grammar-check support
- Download options:
  - `.txt`
  - `.doc`
  - `.docx`

### 5. LinkedIn About Generator

- Generates a recruiter-focused LinkedIn About section
- Can use uploaded CV or rewritten CV context
- Supports manual career-goal input
- Editable before export
- Download options:
  - `.txt`
  - `.doc`

### 6. Analytics and History

- Saves interview sessions locally
- Tracks average score, best score, score distribution, and trends
- Exports history as CSV

## Tech Stack

- Python
- Streamlit
- Groq API
- PyPDF2
- python-docx
- requests
- beautifulsoup4

## Project Structure

This repository is currently very simple:

```text
CareerCraft/
├── interview_agent.py
└── README.md
```

The app also creates a local history file at runtime:

```text
careercraft_history.json
```

## Installation

### 1. Clone or download the project

```bash
git clone <your-repo-url>
cd CareerCraft
```

If you already have the folder locally, just open the project directory.

### 2. Create and activate a virtual environment

macOS/Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Windows:

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install streamlit groq PyPDF2 python-docx requests beautifulsoup4
```

## Running the App

Start the Streamlit app with:

```bash
streamlit run interview_agent.py
```

Then open the local Streamlit URL shown in your terminal, usually:

```text
http://localhost:8501
```

## How To Use

### Interview Practice

1. Enter the target role in the sidebar.
2. Choose industry, interview mode, difficulty, and question count.
3. Optionally upload a CV.
4. Click `Start Interview Session`.
5. Answer questions in chat and review AI scoring and rewritten answers.

### CV Analysis

1. Open the `CV Analyser` tab.
2. Upload a CV.
3. Enter the target role and your name.
4. Paste the job description or enter a job URL.
5. Click `Run Analysis`.
6. Optionally click `Rewrite CV`, `Grammar Audit`, `LinkedIn Summary`, or `Cover Letter`.

### Cover Letter

1. Open the `Cover Letter` tab.
2. If you already used the CV Analyser, the app pre-fills the role, company, and job description context.
3. Optionally adjust the position, company, CV, or job description manually.
4. Choose a style.
5. Click `Generate Letter`.
6. Edit and download the result.

### LinkedIn About

1. Open the `LinkedIn` tab.
2. Upload a CV or rely on the CV already loaded in the app.
3. Enter your name and target goal.
4. Add optional achievements.
5. Click `Generate LinkedIn About`.
6. Edit and export the final result.

## Supported Input Formats

### CV Uploads

- `.pdf`
- `.txt`
- `.docx`

### Job Description Input

- Pasted text
- URL scraping using `requests` and `beautifulsoup4`

## Generated Output Formats

### CV

- `.txt`
- `.doc`
- `.docx`

### Cover Letter

- `.txt`
- `.doc`
- `.docx`

### LinkedIn About

- `.txt`
- `.doc`

## Configuration Notes

Inside the app, the following configuration values are currently defined in code:

- `HISTORY_FILE = "careercraft_history.json"`
- `GROQ_MODEL = "llama-3.3-70b-versatile"`

## Important Security Note

The current code contains a Groq API key directly inside [interview_agent.py](/Users/abid/Downloads/CareerCraft/interview_agent.py). This is not safe for production or public repositories.

Recommended improvement:

1. Remove the hardcoded API key from the source file.
2. Store it in an environment variable instead.
3. Load it with something like:

```python
import os
GROQ_API_KEY = os.getenv("GROQ_API_KEY", "")
```

Then run the app like this:

macOS/Linux:

```bash
export GROQ_API_KEY="your_api_key_here"
streamlit run interview_agent.py
```

Windows PowerShell:

```powershell
$env:GROQ_API_KEY="your_api_key_here"
streamlit run interview_agent.py
```

## Known Limitations

- The app is currently implemented in one large Python file, which makes maintenance harder as features grow.
- API failures are surfaced in the UI but do not yet have robust retry handling.
- URL scraping depends on the structure of the target job page and may fail on dynamic sites.
- The app stores history locally in JSON rather than using a database.
- There is no automated test suite yet.

## Recommended Next Improvements

- Move secrets to environment variables
- Split the app into modules:
  - prompts
  - utilities
  - exporters
  - UI sections
- Add a `requirements.txt`
- Add automated tests for parsing and export helpers
- Add stronger validation for CV and job-description inputs
- Add richer company research and application tracking features

## Troubleshooting

### `ModuleNotFoundError`

Install the missing packages:

```bash
pip install streamlit groq PyPDF2 python-docx requests beautifulsoup4
```

### `DOCX` features are not working

Make sure `python-docx` is installed:

```bash
pip install python-docx
```

### URL scraping is not working

Make sure these packages are installed:

```bash
pip install requests beautifulsoup4
```

Also note that some job sites block scraping or render content dynamically.

### PDF CV text looks incomplete

Some PDFs extract poorly depending on how they were generated. If possible, use `.docx` or `.txt` for better text extraction.

## Future README Additions You May Want

If by "including a;;" you meant extra sections, good candidates would be:

- screenshots
- architecture overview
- deployment guide
- contribution guide
- license
- changelog

## License

No license file is currently included in this project. If you plan to publish it, add a license such as MIT, Apache-2.0, or a proprietary internal-use license.
