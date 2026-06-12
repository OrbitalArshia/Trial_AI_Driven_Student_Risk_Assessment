# Student Risk Assessment AI System

An AI-powered educational analytics system that transforms qualitative student and teacher feedback into actionable risk assessments using keyword analysis and machine learning.

---

## Overview

The **Student Risk Assessment AI System** is designed to help educators identify students who may require additional academic, behavioral, or emotional support. The project combines two separate AI components:

1. **Assessment Score Aggregator** – Converts written feedback from students and teachers into numerical category scores using keyword-based analysis.
2. **Student Risk AI Model** – Uses a Decision Tree Classifier to predict overall student risk levels based on assessment data and generate human-readable explanations.

By integrating multiple perspectives into a unified framework, this system aims to support early intervention and informed decision-making in educational environments.

---

## Features

### Assessment Score Aggregator

* Connects directly to **Google Sheets**.
* Processes both **student self-assessments** and **teacher assessments**.
* Uses **keyword matching** to convert qualitative feedback into numerical scores.
* Evaluates students across **seven assessment categories**.
* Combines assessment sources using **configurable weighted averages**.
* Automatically exports aggregated results to a **new Google Sheet**.
* Includes basic error handling for data loading and parsing.

### Student Risk AI

* Loads training and assessment data directly from **Google Sheets**.
* Uses a **Decision Tree Classifier** to predict student risk levels.
* Categorizes students into **High**, **Medium**, or **Low Risk** groups.
* Provides **feature importance analysis** to increase model transparency.
* Generates **human-readable reasoning** for each prediction.
* Exports final reports to a newly created **Google Sheet**.

---

## Project Workflow

```text
Student Feedback ──┐
                   │
                   ▼
          Assessment Score
             Aggregator
                   │
Teacher Feedback ──┘
                   │
                   ▼
      Weighted Category Scores
                   │
                   ▼
         Student Risk AI Model
                   │
                   ▼
    Risk Prediction + Reasoning
                   │
                   ▼
       Final Google Sheet Report
```

---

## Assessment Categories

The system evaluates students using seven key categories:

1. Behavior
2. Academic Performance
3. Attendance Issues
4. Physical Indicators
5. Emotional Distress
6. Academic Diligence
7. Rule-Boundary Behavior

Each category receives a score ranging from **1 to 5**, where higher scores generally indicate more positive outcomes.

---

## Assessment Score Aggregator

### Description

Educational assessments often involve multiple perspectives. This component streamlines the process of combining qualitative feedback from different stakeholders into quantifiable scores.

Using keyword-based natural language processing techniques, the system identifies positive and negative indicators within textual feedback and assigns numerical scores across predefined categories.

### Weighted Aggregation

The final score for each category is calculated using configurable weights.

**Example weighting:**

* Student Assessment: **35%**
* Teacher Assessment: **65%**

This allows educators to prioritize professional observations while still incorporating student perspectives.

---

## Student Risk AI

### Description

The Student Risk AI model uses machine learning to identify students who may benefit from additional support.

The model is trained using historical assessment data and predicts risk levels for new students based on their aggregated category scores.

### Risk Levels

| Risk Level | Description                                            |
| ---------- | ------------------------------------------------------ |
| High       | Immediate intervention may be beneficial.              |
| Medium     | Continued monitoring and targeted support recommended. |
| Low        | No significant concerns identified at this time.       |

---

## Technologies Used

* Python
* Google Colab
* Google Sheets API
* gspread
* oauth2client
* pandas
* scikit-learn
* Decision Tree Classifier

---

## Setup

### 1. Open in Google Colab

Upload the notebook files to Google Colab.

---

### 2. Install Dependencies

Run the following command:

```bash
!pip install gspread oauth2client pandas scikit-learn
```

---

### 3. Authenticate Google Account

The notebooks require permission to access Google Sheets.

```python
from google.colab import auth
from google.auth import default
import gspread

auth.authenticate_user()
creds, project = default()
gc = gspread.authorize(creds)
```

After running this cell, a pop-up window will appear requesting access to your Google Drive.

---

## Google Sheet Structure

The Assessment Score Aggregator expects two input sheets:

* Student Feedback Sheet
* Teacher Feedback Sheet

Both sheets should follow the same structure.

### Example

| Student ID | Behavior            | Academic Performance | Attendance Issues |
| ---------- | ------------------- | -------------------- | ----------------- |
| S001       | respectful, engaged | grades improving     | on time           |
| S002       | disruptive          | failing              | skipping class    |

---

## Keyword Configuration

The system relies on customizable keyword dictionaries.

```python
CATEGORIES = [
    "Behavior",
    "Academic Performance",
    "Attendance Issues",
    "Physical Indicators",
    "Emotional Distress",
    "Academic Diligence",
    "Rule-Boundary Behavior"
]

KEYWORDS = {
    "Behavior": {
        "negative": [
            "disruptive",
            "rude"
        ],
        "positive": [
            "respectful",
            "calmer"
        ]
    }

    # Additional categories omitted for brevity
}
```

Educators can expand or modify these keywords to align with local terminology and assessment practices.

---

## Usage

### Step 1: Aggregate Assessment Scores

The Assessment Score Aggregator will:

* Load student feedback.
* Load teacher feedback.
* Analyze responses using keyword matching.
* Generate category scores.
* Calculate weighted averages.
* Export the results to a new Google Sheet.

---

### Step 2: Run the Student Risk AI

The Student Risk AI will:

* Load training data.
* Load aggregated assessment scores.
* Train the Decision Tree Classifier.
* Predict risk levels.
* Generate reasoning statements.
* Export the final report to Google Sheets.

---

## Output

### Aggregated Assessment Sheet

| Student ID | Behavior | Academic Performance | Attendance Issues |
| ---------- | -------- | -------------------- | ----------------- |
| S001       | 4.3      | 4.7                  | 4.8               |
| S002       | 2.1      | 2.4                  | 1.9               |

---

### Student Risk Report

| Student ID | Predicted Risk | Reasoning                                                           |
| ---------- | -------------- | ------------------------------------------------------------------- |
| S001       | Low            | Strong academic performance and consistent attendance.              |
| S002       | High           | Significant attendance concerns and declining academic performance. |

---

## Future Improvements

Potential enhancements include:

* Advanced natural language processing using transformer-based models.
* Longitudinal analysis across multiple grading periods.
* Interactive dashboards for counselors and administrators.
* Automated intervention recommendations.
* Integration with additional educational data sources.

---

## Disclaimer

This tool is intended to **support educational professionals**, not replace professional judgment. Predictions should always be reviewed alongside contextual information and existing school support processes.

---

## License

This project is intended for educational and research purposes. Please review and add an appropriate open-source license before public distribution.
