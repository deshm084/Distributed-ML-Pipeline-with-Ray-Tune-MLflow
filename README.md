Distributed ML Pipeline with Ray Tune & MLflow
📖 Overview
This project implements an end-to-end MLOps workflow for training a Random Forest Regressor on the Diabetes dataset. Unlike standard scripts that train models sequentially, this pipeline leverages Ray Tune for parallel distributed hyperparameter optimization and MLflow for robust experiment tracking and model versioning.

The goal is to demonstrate how to scale model training from a single script to a distributed cluster environment while maintaining full reproducibility.

🏗 Architecture
The pipeline follows a "Train-Tune-Register-Serve" pattern:

Code snippet

graph LR
    A[Data Source] --> B{Ray Tune Cluster};
    B -->|Worker 1| C[Train Config A];
    B -->|Worker 2| C[Train Config B];
    C -->|Log Metrics| D[MLflow Tracking Server];
    D -->|Select Best| E[Model Registry];
    E -->|Load via URI| F[Inference Engine];
🛠 Tech Stack
Orchestration: Ray Tune (Distributed Hyperparameter Optimization)

Tracking & Registry: MLflow

Modeling: Scikit-Learn (Random Forest)

Environment: Python 3.10+

⚡ Key Features
Parallel Execution: Utilizes Ray to parallelize training trials across available CPU cores, reducing total tuning time.

Experiment Tracking: Automatically logs parameters (n_estimators, max_depth) and metrics (RMSE) for every trial to MLflow.

Artifact Management: Solves common "Path Hell" issues by using MLflow's runs:/ URI scheme for portable model loading.

Automated Promotion: Automatically selects the best trial based on validation error and promotes it to the production registry.

🚀 How to Run
1. Prerequisites
Bash

pip install ray[default] mlflow scikit-learn pandas
2. Execute Pipeline
Run the main script to initialize the Ray cluster and start tuning:

Bash

python main.py
3. View Dashboard
To visualize the parallel training sessions:

Bash

# Ray Dashboard
tensorboard --logdir ~/ray_results

# MLflow UI
mlflow ui
📊 Results Snapshot
Baseline RMSE: ~55.0

Optimized RMSE: ~47.5 (15% Improvement)

Tuning Efficiency: 10 trials completed in parallel, fully saturating logical cores.

👨‍💻 Author
Sanskruti Machine Learning Engineer | MLOps Enthusiast
