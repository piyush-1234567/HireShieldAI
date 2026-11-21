Here's your `SYSTEM_ARCHITECTURE.md` for HireShield AI.

# HireShield AI – System Architecture

## 1. Architecture Overview

HireShield AI follows a modular client-server architecture. The React frontend communicates with a FastAPI backend, which coordinates rule-based detection, machine learning classification, URL analysis, and risk assessment.

MongoDB stores user accounts, analysis history, and community reports.

## 2. High-Level Architecture

```
flowchart TD
    A[User] --> B[React Frontend]
    B --> C[FastAPI Backend]

    C --> D[Input Validation]
    D --> E[Analysis Coordinator]

    E --> F[Rule-Based Detection]
    E --> G[ML Classification]
    E --> H[URL Analysis]

    F --> I[Risk Assessment Engine]
    G --> I
    H --> I

    I --> J[Explanation Generator]
    J --> K[Analysis Result]

    K --> C
    C --> B

    C <--> L[(MongoDB)]
```

## 3. Component Responsibilities

### 3.1 Frontend – React.js and Tailwind CSS

Responsibilities:

- Provide the user interface.
- Accept job descriptions and recruitment messages.
- Accept recruitment URLs in a later phase.
- Send analysis requests to FastAPI.
- Display risk scores and warning signs.
- Display safety recommendations.
- Provide analysis history in a later phase.

### 3.2 Backend – FastAPI

Responsibilities:

- Receive frontend requests.
- Validate submitted information.
- Coordinate the detection pipeline.
- Invoke the rule-based detection engine.
- Invoke the ML classification model.
- Invoke URL analysis when applicable.
- Combine detection results.
- Generate the final analysis response.
- Communicate with MongoDB.

### 3.3 Rule-Based Detection Engine

Responsibilities:

- Detect registration fee requests.
- Identify suspicious salary promises.
- Detect urgency and pressure tactics.
- Identify requests for sensitive personal information.
- Generate structured warning indicators.

### 3.4 Machine Learning Engine

Responsibilities:

- Preprocess recruitment text.
- Extract relevant text features.
- Classify recruitment content.
- Return a prediction and confidence score.
- Support model evaluation and improvement.

Initial implementation: Scikit-learn baseline classifier.

### 3.5 URL Analysis Engine

Responsibilities:

- Extract domain information.
- Examine domain characteristics.
- Retrieve available reputation information.
- Identify suspicious website signals.

This module will be introduced after the initial text-analysis MVP.

### 3.6 Risk Assessment Engine

Responsibilities:

- Combine rule-based detection results.
- Incorporate ML predictions.
- Incorporate URL intelligence when available.
- Calculate a normalized risk score between 0 and 100.
- Determine the corresponding risk category.

Proposed risk categories:

| Score  | Category    |
| ------ | ----------- |
| 0–30   | Low Risk    |
| 31–60  | Medium Risk |
| 61–100 | High Risk   |

These thresholds are initial design choices and will require evaluation.

### 3.7 Explanation Generator

Responsibilities:

- Explain why an opportunity was flagged.
- List detected suspicious indicators.
- Provide evidence from the submitted content.
- Generate relevant safety recommendations.

### 3.8 Database – MongoDB

Planned collections:

| Collection | Purpose                                      |
| ---------- | -------------------------------------------- |
| users      | Store user account information               |
| analyses   | Store submitted content and analysis results |
| reports    | Store community-submitted scam reports       |

## 4. Application Data Flow

The application follows this sequence:

1. User submits a recruitment message or job description.
2. React sends the content to the FastAPI backend.
3. FastAPI validates the input.
4. The analysis coordinator starts the detection pipeline.
5. The rule engine identifies predefined suspicious patterns.
6. The ML model classifies the submitted content.
7. The risk assessment engine combines the available signals.
8. The explanation generator prepares warning signs and recommendations.
9. FastAPI returns the structured analysis result.
10. React displays the result to the user.

## 5. Frontend and Backend Communication

The frontend and backend communicate through REST APIs using JSON.

Example request:

```
{
  "content": "Congratulations! You have been selected. Pay a registration fee of Rs. 2000.",
  "input_type": "job_description"
}
```

Example response:

```
{
  "risk_score": 82,
  "risk_level": "high",
  "detected_signals": [
    {
      "indicator": "Registration fee requested",
      "severity": "high",
      "evidence": "Pay a registration fee of Rs. 2000."
    }
  ],
  "recommendations": [
    "Do not pay registration fees.",
    "Verify the company through its official website."
  ]
}
```

The values above are illustrative examples, not actual model predictions.

## 6. Proposed API Endpoints

| Method | Endpoint              | Purpose                      |
| ------ | --------------------- | ---------------------------- |
| GET    | /                     | Health check                 |
| POST   | /api/v1/analyze       | Analyse recruitment content  |
| GET    | /api/v1/analyses      | Retrieve analysis history    |
| GET    | /api/v1/analyses/{id} | Retrieve a specific analysis |
| POST   | /api/v1/auth/register | Register a user              |
| POST   | /api/v1/auth/login    | Authenticate a user          |

Authentication and history endpoints will be implemented in later phases.

## 7. Initial MVP Architecture

For the first working version, we will implement only:

- React frontend.
- FastAPI backend.
- Input validation.
- Rule-based detection engine.
- Baseline ML classifier.
- Risk assessment engine.
- Explanation generator.

MongoDB integration and URL intelligence can follow once the core analysis pipeline works.

## 8. Design Principles

- Modular architecture.
- Separation of concerns.
- Explainable risk assessments.
- Secure input handling.
- Independent detection components.
- Extensibility for future intelligence sources.

## 9. Current Development Status

| Component              | Status    |
| ---------------------- | --------- |
| README.md              | Completed |
| PROJECT_PLAN.md        | Completed |
| SYSTEM_ARCHITECTURE.md | Completed |
| Database Design        | Pending   |
| API Design             | Pending   |
| Frontend Development   | Pending   |
| Backend Development    | Pending   |
| ML Integration         | Pending   |

**Next:** Create `DATABASE_DESIGN.md` to define the MongoDB collections, fields, relationships, and data types.