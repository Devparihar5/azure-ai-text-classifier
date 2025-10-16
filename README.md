# Custom Text Classification with Azure AI Language

A Python application that uses Azure AI Language service to classify text documents into predefined categories.

## Features

- Batch text classification using Azure AI Language
- Processes multiple text files from a directory
- Returns classification results with confidence scores

## Setup

1. Clone the repository
2. Create a virtual environment:
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # On Windows: .venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
4. Configure environment variables in `.env`:
   ```
   AI_SERVICE_ENDPOINT=your_azure_endpoint
   AI_SERVICE_KEY=your_azure_key
   PROJECT=your_project_name
   DEPLOYMENT=your_deployment_name
   ```

## Usage

1. Place text files in the `articles/` directory
2. Run the application:
   ```bash
   python app.py
   ```

## Complete Workflow Process

### Model Training and Deployment Pipeline

```mermaid
flowchart TD
    A[Start] --> B[Provision Azure Resources]
    B --> C[Create Storage Account]
    C --> D[Upload Training Data]
    D --> E[Create Language Studio Project]
    E --> F[Label Training Data]
    F --> G[Configure Data Split]
    G --> H[Train Model]
    H --> I{Model Performance OK?}
    I -->|No| J[Adjust Labels/Add Data]
    J --> F
    I -->|Yes| K[Deploy Model]
    K --> L[Test Deployment]
    L --> M[Production Ready]
    M --> N[End]
```

### Data Labeling Process

```mermaid
flowchart LR
    A[Raw Text Files] --> B[Review Content]
    B --> C{Determine Category}
    C -->|Sports| D[Label as Sports]
    C -->|Entertainment| E[Label as Entertainment]
    C -->|News| F[Label as News]
    C -->|Classifieds| G[Label as Classifieds]
    D --> H[Assign to Training/Test Set]
    E --> H
    F --> H
    G --> H
    H --> I[Save Labels]
    I --> J{More Files?}
    J -->|Yes| A
    J -->|No| K[Complete Dataset]
```

### Model Evaluation Workflow

```mermaid
flowchart TD
    A[Trained Model] --> B[Run Test Set]
    B --> C[Calculate Metrics]
    C --> D[Precision Score]
    C --> E[Recall Score]
    C --> F[F1 Score]
    C --> G[Overall Accuracy]
    D --> H{Performance Acceptable?}
    E --> H
    F --> H
    G --> H
    H -->|No| I[Retrain with More Data]
    H -->|Yes| J[Deploy to Production]
    I --> K[Add Training Examples]
    K --> L[Relabel Data]
    L --> M[Retrain Model]
    M --> B
    J --> N[Monitor Performance]
```

### Application Testing Process

```mermaid
flowchart TD
    A[Deploy Model] --> B[Configure Environment]
    B --> C[Set API Credentials]
    C --> D[Prepare Test Files]
    D --> E[Run Classification]
    E --> F[Check Results]
    F --> G{Results Accurate?}
    G -->|No| H[Debug Configuration]
    G -->|Yes| I[Validate Confidence Scores]
    H --> C
    I --> J{Confidence > Threshold?}
    J -->|No| K[Review Model Training]
    J -->|Yes| L[Production Ready]
    K --> M[Improve Training Data]
    M --> N[Retrain Model]
    N --> A
```

## Sample Results

When running with the provided test files:

```
test2.txt was classified as 'Sports' with confidence score 0.33.
test1.txt was classified as 'Entertainment' with confidence score 0.33.
```

## Requirements

- Python 3.7+
- Azure AI Language service resource
- Trained custom classification model

## References

- [Azure AI Text Analytics SDK](https://pypi.org/project/azure-ai-textanalytics/)
- [Microsoft Learn AI Language Repository](https://github.com/microsoftlearning/mslearn-ai-language)

## File Structure

```
├── app.py              # Main application
├── requirements.txt    # Dependencies
├── .env               # Environment variables
└── articles/          # Text files to classify
    ├── test1.txt
    └── test2.txt
```
