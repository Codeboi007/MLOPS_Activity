I need you to analyze and explain an existing machine learning project so I can write my college assignment report myself. Do not write the report for me.

The project is **Customer Churn Prediction Using a Machine Learning Workflow**, developed in a Kaggle notebook for Activity 1 of Data Engineering & MLOps (BAD714C).

Dataset: https://www.kaggle.com/datasets/blastchar/telco-customer-churn

I will provide the actual Kaggle notebook, its execution outputs, and the generated `model_metrics.csv` and other result files where available.

Your task is to act as a technical analyst and give me a comprehensive **report-writing reference document containing the factual details, explanations, results, and technical information I need to write the report myself**.

## 1. Analyze the implementation

Inspect the provided notebook and files. Explain exactly what the project implements, including:

- Problem statement and business objective.
- Dataset source, structure, target variable, and relevant features.
- Data validation and cleaning procedures.
- Exploratory data analysis and what each graph is intended to show.
- Feature engineering, categorical encoding, numerical scaling, and missing-value handling.
- Train/test split and reproducibility settings.
- Logistic Regression and Random Forest training procedures.
- Evaluation metrics and what each measures.
- Model-selection logic and the F1-score quality gate.
- Smoke tests and their purpose.
- Model serialization, metadata, reloading, and prediction verification.

For each stage, provide the actual implementation details from the notebook, not generic descriptions of how such a project could work.

## 2. Extract the actual results

Inspect the execution outputs and result files. Provide:

- Dataset dimensions before and after cleaning.
- Missing-value and duplicate counts.
- Churn distribution and churn rate.
- Important EDA findings supported by the actual graphs or data.
- A comparison table of Logistic Regression and Random Forest using the actual accuracy, precision, recall, F1-score, and ROC-AUC values.
- The selected model and whether it passed the configured quality gate.
- Confusion matrix values and relevant interpretation.
- ROC curve interpretation.
- Example prediction outputs and model reload test status.
- Names of all generated artifacts and their purposes.

Never invent a value. If a result is unavailable, explicitly tell me which notebook cell or file I need to inspect or rerun to obtain it.

## 3. Explain the MLOps aspects accurately

Explain how the current implementation demonstrates:
- Data validation.
- Reproducible training.
- Model evaluation and acceptance criteria.
- Automated smoke testing.
- Model artifact management.
- Metadata-based model version identification.

Then clearly separate what has **not** yet been implemented:
- Git-based source-code version control.
- GitHub Actions continuous integration.
- Automated retraining.
- Production deployment.
- Production monitoring.
- MLflow experiment tracking.

For these missing components, explain briefly what they would involve and whether they are necessary to describe the current implementation or should instead be listed as future improvements.

Do not falsely claim that running a Kaggle notebook alone implements full CI/CD.

## 4. Give me report-writing material, not a report

Organize your response into these sections:

A. Project overview and problem definition.

B. Dataset and data preprocessing details.

C. EDA graph-by-graph explanation and actual findings.

D. Feature engineering and train/test methodology.

E. Model training and comparison, including actual metrics.

F. Evaluation graphs and their interpretation.

G. MLOps pipeline stages and the purpose of each stage.

H. Reproducibility, testing, saved model, and metadata.

I. Limitations, missing MLOps components, and future improvements.

J. A technical glossary of important terms I should understand.

K. A checklist mapping each Activity 1 requirement to the actual project component that satisfies it.

For each section, provide:
1. The factual information I should include.
2. Relevant technical explanations in simple but accurate language.
3. Specific numbers, filenames, graph names, and implementation details wherever available.
4. Suggested points I should discuss in my own words.
5. Any gaps or limitations I must acknowledge.

Do not produce a polished academic report, abstract, ready-to-submit paragraphs, or a complete report with chapters. Instead, provide detailed, organized research notes and technical explanations that I can use to write the report independently.

Base claims about the implementation on the uploaded files and execution outputs. Clearly distinguish verified results from assumptions or general technical explanations.