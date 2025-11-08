# CV Analyzer - Intelligent Recruitment System

A web application that analyzes CVs against job descriptions using string matching algorithms (Brute Force, Rabin-Karp, KMP).

## Features

- ✅ Upload multiple CV files (PDF/DOCX/TXT)
- ✅ Select job descriptions with mandatory and optional skills
- ✅ Choose between different string matching algorithms
- ✅ **NEW: Case sensitivity toggle**
- ✅ **NEW: Whole-word matching toggle** (avoids partial matches like "Sequel" for "SQL")
- ✅ View detailed analysis results with match scores
- ✅ Compare algorithm performance metrics
- ✅ CV size bucketing (Small/Medium/Large)
- ✅ Rabin-Karp collision tracking

## Setup

### Prerequisites

- Python 3.7+
- pip

### Installation

1. Navigate to the backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

Or using the virtual environment:
```bash
# On Windows
venv\Scripts\activate

# Install dependencies (if not already installed)
pip install flask flask-cors PyPDF2 python-docx
```

3. Run the server:
```bash
python app.py
```

4. Open your browser and navigate to:
```
http://localhost:5000
```

## Usage

1. **Select a Job Description**: Choose from Data Scientist, Web Developer, or Software Tester
2. **Upload CV Files**: Click the upload area and select PDF, DOCX, or TXT files
3. **Choose Algorithm**: Select which string matching algorithm(s) to use
4. **Set Matching Options** (optional):
   - **Case Sensitive**: Match exact capitalization
   - **Whole Word Only**: Avoid partial matches (e.g., "SQL" won't match "Sequel")
5. **Start Analysis**: Click the "Start Analysis" button
6. **View Results**: See candidate rankings, match scores, and algorithm performance metrics

### Matching Options Explained

- **Case Sensitive OFF** (default): "python" matches "Python", "PYYYYE", etc.
- **Case Sensitive ON**: "python" only matches "python"
- **Whole Word OFF** (default): "SQL" matches "Sequel", "Transact-SQL", etc.
- **Whole Word ON**: "SQL" only matches "SQL" as a complete word

## API Endpoints

- `GET /`: Serve the frontend application
- `POST /api/upload`: Upload CV files
- `GET /api/job-descriptions`: Get available job descriptions
- `POST /api/analyze`: Analyze CVs against job description
- `GET /api/health`: Health check endpoint

## Project Structure

```
ALGO_APP/
├── backend/
│   ├── app.py              # Flask backend server
│   ├── algorithms.py        # String matching algorithms
│   ├── cv_processor.py     # CV text extraction
│   ├── requirements.txt    # Python dependencies
│   └── uploads/            # Uploaded CV files (created automatically)
├── frontend/
│   └── index.html          # React frontend
└── README.md
```

## Technologies

- **Backend**: Flask (Python)
- **Frontend**: React (loaded via CDN), TailwindCSS
- **Algorithms**: Brute Force, Rabin-Karp, KMP
- **File Processing**: PyPDF2, python-docx

## How It Works

1. CV files are uploaded and saved to the `uploads` folder
2. The backend extracts text from PDF/DOCX files
3. Selected string matching algorithms search for keywords in the CV text
4. Performance metrics (execution time, comparisons) are tracked for each algorithm
5. Candidates are scored and ranked based on matched skills
6. Results are displayed with visualizations and detailed breakdowns

## Troubleshooting

**Port already in use**: Change the port in `app.py` (line 252):
```python
app.run(debug=True, host='0.0.0.0', port=5000)
```

**Files not uploading**: Check that the `uploads` folder exists in the backend directory

**Analysis not starting**: 
- Open browser console (F12) to check for errors
- Verify the backend server is running
- Ensure CV files are valid PDF or DOCX format

