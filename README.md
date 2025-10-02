# end-to-end-ML-Ops-production-pipeline-
This repository contains an end-to-end Machine Learning project demonstrating best practices for building, training, and managing models in a production-ready MLOps environment. We use a standard regression task (predicting house prices) and leverage MLflow for comprehensive experiment tracking and model lifecycle management.

✨ Key Features & MLOps Tools
This project focuses on the reproducibility and traceability of the Machine Learning lifecycle:

Experiment Tracking (MLflow): Every model training run is automatically logged, capturing parameters, performance metrics (MAE, RMSE), and the resulting model artifact.

Model Registry (MLflow): The best performing models are registered in the MLflow Model Registry, allowing for versioning and stage transitions (Staging, Production, Archived).

Reproducible Pipeline: All data processing, feature engineering, and training steps are codified in Python scripts, ensuring the pipeline can be run consistently.

Model Training: Uses a simple Scikit-learn model for regression.

🛠️ Project Setup and Local Run
1. Prerequisites
You'll need Python 3.8+ installed on your system.

2. Environment Setup
Clone the repository and create a virtual environment:

git clone [https://github.com/your-username/mlops-project.git](https://github.com/shreyakanade/end-to-end-ML-Ops-production-pipeline-)
cd mlops-project
python -m venv venv
source venv/bin/activate  # On Linux/macOS
# .\venv\Scripts\activate # On Windows

3. Install Dependencies
Install all required Python packages, including MLflow and Scikit-learn:

pip install -r requirements.txt

4. Running the MLflow Tracking Server
To view and manage your experiments, start the MLflow UI locally. This command saves your experiment data locally in the ./mlruns folder.

mlflow ui

Once started, open your web browser and navigate to https://www.google.com/search?q=http://127.0.0.1:5000 to see the MLflow dashboard.

🚀 Running the Training Pipeline
The core training logic is contained in src/train.py. This script handles data loading, preprocessing, model training, and critically, logging all results to the active MLflow server.

Run the training script with example hyperparameters:

# Example 1: Train a model with n_estimators=100 and max_depth=5
python src/train.py --n_estimators 100 --max_depth 5

# Example 2: Train a model with different parameters
python src/train.py --n_estimators 200 --max_depth 8

After running these commands, refresh the MLflow UI. You will see two separate runs logged under the HousePricePrediction experiment, allowing you to compare metrics and parameters side-by-side.

Using the MLflow Model Registry
After evaluating your runs in the MLflow UI, you can register the best model:

Find the Run ID of the best performing model in the MLflow UI.

Navigate to the Artifacts section of that run.

Click the registered model artifact  and select "Register Model".

Register it under a descriptive name 

This makes the model available for deployment in different stages (Staging, Production).

📂 Project Structure
mlops-project/
├── data/
│   └── housing_data.csv          # Raw dataset
├── mlruns/                       # MLflow tracking data (ignore in git)
├── models/                       # Stored model artifacts (if not using remote registry)
├── src/
│   ├── __init__.py
│   └── train.py                  # Main script: loads data, trains model, logs to MLflow
├── requirements.txt              # Project dependencies
└── README.md                     # This file

📝 Next Steps (Future MLOps Enhancements)
This project can be extended with full MLOps automation:

Containerization: Add a Dockerfile for the training environment to ensure complete portability.

CI/CD: Integrate a tool like GitHub Actions or Airflow to automatically trigger training upon data or code changes.

Deployment: Implement a FastAPI service to serve the registered model and containerize it.

Monitoring: Add Evidently AI or a similar tool to monitor the deployed model for data and concept drift.
