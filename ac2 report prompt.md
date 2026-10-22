# Research Brief for Activity 2 — Data Engineering & MLOps (BAD714C)

Act as a technical research assistant specializing in MLOps. I am preparing a self-study report for Activity 2 of my undergraduate Data Engineering & MLOps assignment.

**My chosen tool is MLflow.**

I do not want you to write the final report for me. I want you to research the topic thoroughly and give me detailed, accurate, well-organized technical information, explanations, examples, diagrams, and sources that I can use to write the report myself.

## 1. Assignment requirements

My assignment instructs me to select an open-source MLOps tool, such as MLflow, Kubeflow or TFX, and study how it supports:

- CI/CD pipelines.
- Model testing and validation.
- Deployment strategies.

The report must cover:

1. Tool overview and core components.
2. CI/CD support.
3. One deployment strategy explained in context.
4. Advantages and challenges of using the tool in a real project.

Focus exclusively on MLflow. Do not switch to another tool.

## 2. Research sources

Use the following official documentation as primary sources. Consult the latest documentation available and supplement it with other trustworthy technical sources where necessary.

**MLflow official documentation**

- MLflow Tracking: https://mlflow.org/docs/latest/ml/tracking/
- Tracking Server: https://mlflow.org/docs/latest/tracking/server/
- MLflow Models: https://mlflow.org/docs/latest/ml/model/
- Model Registry: https://mlflow.org/docs/latest/ml/model-registry/
- Model Registry workflows: https://mlflow.org/docs/latest/ml/model-registry/workflow/
- Model Evaluation: https://mlflow.org/docs/latest/ml/evaluation
- Model Serving and Deployment: https://mlflow.org/docs/latest/ml/deployment/
- Local Model Serving: https://mlflow.org/docs/latest/ml/deployment/deploy-model-locally
- Model Dependencies: https://mlflow.org/docs/latest/ml/model/dependencies/
- Model Signatures: https://mlflow.org/docs/latest/ml/model/signatures/

**CI/CD sources**

- GitHub Actions documentation: https://docs.github.com/en/actions
- Building and testing Python projects using GitHub Actions: https://docs.github.com/en/actions/tutorials/build-and-test-code/python

**Deployment strategy source**

- Microsoft Azure Well-Architected guidance on blue-green deployment: https://learn.microsoft.com/en-us/azure/well-architected/mission-critical/mission-critical-deployment-testing
- AWS blue-green deployment methodology: https://docs.aws.amazon.com/whitepapers/latest/blue-green-deployments/introduction.html

Use these as starting points, not as the only permitted sources. Cite technical claims and identify the source of each important fact. Do not invent citations or references.

## 3. Section A — MLflow overview and core components

Research and explain:

- What MLflow is and what problems it addresses.
- Why experiment tracking and model lifecycle management matter.
- The role of MLflow in the machine learning lifecycle.
- Its principal components and their relationships.
- How it works with common machine learning libraries such as scikit-learn, TensorFlow and PyTorch.
- Its local development and team-oriented deployment options.
- Its principal advantages and limitations.

Explain these components individually:

**A. MLflow Tracking**
Explain experiments, runs, parameters, metrics, tags, code-version information, logged models and artifacts. Give examples such as comparing Logistic Regression and Random Forest models.

**B. MLflow Models**
Explain the standard model packaging format, supported model flavors, dependency information, input signatures and how models can be used by downstream tools.

**C. MLflow Model Registry**
Explain registered models, model versions, lineage, tags, metadata, aliases and controlled promotion of models.

Use current terminology. In particular, verify the current status of traditional model stages such as `Staging` and `Production`, and explain the modern model-alias approach, such as assigning a `champion` alias to the intended production version.

**D. Model Evaluation**
Explain how MLflow can calculate or record evaluation metrics, generate diagnostic plots and validate candidate models against configured thresholds. Clarify which operations MLflow performs and which rules must be defined by the developer.

**E. Model Serving and Deployment**
Explain how an MLflow model can be served locally or deployed using supported deployment targets. Describe the prediction endpoint, REST requests, dependency handling, and the distinction between model serving and the infrastructure that hosts the service.

Also explain the roles of the tracking server, backend metadata store and artifact store. Clarify that these serve different purposes and may be configured separately.

Provide a component table with these columns:

Component | Purpose | Main information or artifacts handled | Role in a customer churn project

## 4. Section B — CI/CD pipeline support

Explain CI/CD carefully in the context of machine learning.

Define:

- Continuous Integration (CI).
- Continuous Delivery.
- Continuous Deployment.
- How these differ from ordinary model training.

Then explain how MLflow can be integrated into a CI/CD pipeline. Do not claim that MLflow automatically supplies a complete CI/CD system.

Use GitHub Actions as the example orchestration tool.

Describe a realistic workflow:

1. A developer pushes code or opens a pull request.
2. GitHub Actions installs dependencies and runs automated tests.
3. Data validation and preprocessing checks are executed.
4. The training workflow trains or evaluates a candidate model when appropriate.
5. Evaluation metrics are logged to MLflow.
6. The candidate is checked against acceptance criteria.
7. A failed test or quality check stops the release.
8. A passing candidate can be registered or marked for promotion, according to the workflow's approval rules.
9. A separate deployment job deploys the approved version.

Explain the division of responsibility:

- GitHub Actions runs the automated workflow.
- Test code performs the required software and data checks.
- MLflow records experiments and manages model artifacts and registered versions.
- A deployment mechanism serves the model and manages traffic.

Discuss the benefits of this arrangement, the limitations of MLflow in this context, and practical implementation challenges such as credentials, dependencies, data availability, artifact storage and permissions.

Give a Mermaid flowchart of the proposed CI/CD process, including a clear failure path and a successful release path.

Include an illustrative GitHub Actions workflow outline only if useful. Label it as an example design, not as a workflow that has actually been executed.

## 5. Section C — Model testing and validation

Distinguish the following concepts:

1. Software unit and integration testing.
2. Data validation.
3. Model evaluation.
4. Model acceptance or quality-gate validation.
5. Testing the packaged model and its inference environment.
6. Production monitoring after deployment.

Explain how MLflow relates to each and which responsibilities require additional code or tools.

Use a customer churn classification example to illustrate:

- Precision, recall, F1-score and ROC-AUC.
- Why accuracy alone may not be sufficient for imbalanced data.
- Comparing a new model against a baseline or current approved model.
- Configuring metric thresholds and stopping promotion when a candidate fails.
- Logging evaluation plots and metrics in MLflow.
- Recording model lineage and metadata.
- Testing model inputs and dependencies before deployment.

Explain `mlflow.models.evaluate()` and the relevant metric-threshold validation functionality using the current official API documentation. Verify current names and usage rather than relying on outdated code snippets.

Give a compact table:

Validation stage | What is checked | How MLflow contributes | What additional implementation is needed

Do not suggest that MLflow automatically guarantees a model is fair, safe, accurate or production-ready merely because it has been evaluated.

## 6. Section D — Deployment strategy: Blue-green deployment

Use blue-green deployment as the single deployment strategy examined in depth.

Explain:

- What blue-green deployment means.
- Why two separate environments are used.
- The roles of the blue and green environments.
- How the new model is tested before receiving production traffic.
- How traffic is switched to the new version.
- How rollback works if the new model fails.
- Benefits, risks, costs and operational requirements.

Use this concrete scenario:

A telecom company uses a deployed customer churn prediction model to identify customers likely to leave. The current model is version 1. A newly trained and evaluated model is version 2.

Develop the scenario through these stages:

1. Version 1 continues serving live requests in the blue environment.
2. Version 2 is packaged and registered in MLflow.
3. Version 2 is deployed to the separate green environment.
4. Green is tested for prediction correctness, latency, error rates and expected model behaviour.
5. After validation and approval, the traffic-management system redirects traffic to green.
6. Operational metrics are monitored after the switch.
7. If serious issues arise, traffic is redirected to blue and version 1 remains available for rollback.
8. Once the new deployment is stable, the previous environment can be retired according to the rollback-retention policy.

Explain exactly where MLflow participates: experiment tracking, evaluation, model packaging, registry and model serving. Explain separately which infrastructure or external deployment tooling implements the two environments, health checks and traffic routing.

Provide a Mermaid flowchart showing both successful deployment and rollback paths.

Explain the advantages of blue-green deployment, including controlled releases and rapid rollback, and its limitations, including duplicated infrastructure cost, environment consistency, traffic-routing complexity and the need to validate the new environment.

Do not imply that MLflow alone creates and controls the entire blue-green deployment setup.

## 7. Section E — Advantages and challenges in a real project

Research and explain both benefits and limitations.

Cover advantages such as:

- Better experiment tracking and model comparison.
- Improved traceability and model lineage.
- Model packaging and dependency management.
- Easier collaboration through shared tracking infrastructure.
- Model version management.
- Integration with other machine learning tools.
- Support for repeatable model evaluation and deployment workflows.

Cover challenges such as:

- Tracking server and backend configuration.
- Artifact storage choices, storage costs and permissions.
- Managing credentials and access control.
- Dependency conflicts and reproducibility across environments.
- Integrating external testing, CI/CD and deployment tools.
- Keeping data and model versions traceable together.
- Production monitoring and drift detection requiring additional capabilities or integrations.
- Operational complexity when running shared or distributed infrastructure.

Distinguish intrinsic limitations from problems that depend on how MLflow is configured. Support important claims with sources.

## 8. Section F — Applied case study

Use a single running example: a telecom customer churn classifier.

Assume the system trains Logistic Regression and Random Forest models on historical customer data. The team compares their precision, recall, F1-score and ROC-AUC, records experiments in MLflow, validates a candidate against predefined thresholds, registers the selected candidate and deploys it using a blue-green release process.

Use hypothetical values only when illustrating a clearly labelled example. Never present hypothetical metrics or results as actual experimental findings.

For this example, explain what would be logged during an MLflow run:

- Model type and hyperparameters.
- Dataset or dataset-version information.
- Evaluation metrics.
- Relevant plots and other artifacts.
- Model package, dependency files and input signature.
- Run identifier and model-version information.
- Validation status.

Explain how these records help the team reproduce experiments, compare models, audit a release and roll back when necessary.

## 9. Required output from you

I need **report-writing research material, not a completed academic report**.

Organize your answer as:

1. A concise technical summary of MLflow.
2. A core-components reference table.
3. Detailed notes for the overview and architecture section.
4. Detailed notes for CI/CD, including the GitHub Actions and MLflow division of responsibilities.
5. Detailed notes for model testing, evaluation and validation.
6. A blue-green deployment explanation using the customer churn example.
7. Advantages and challenges.
8. Mermaid diagrams for the CI/CD workflow and blue-green deployment.
9. A technical glossary.
10. A checklist mapping every assignment requirement to the material I should include.
11. A list of references with titles, organizations and direct URLs.

For each report section, provide:
- Facts and technical explanations I should include.
- A step-by-step explanation of how the system works.
- Practical examples using the churn project.
- Relevant terminology.
- Source links supporting the facts.
- A short list of discussion points I should explain in my own words.

Do not write a polished report with an abstract, complete chapters and ready-to-submit prose. Instead, provide extensive technical notes and explanations that I can use to write my own report.

## 10. Research quality requirements

- Prioritize current official MLflow documentation and other authoritative technical sources.
- Verify current MLflow terminology, APIs and deprecated features.
- Cite claims close to the relevant explanation.
- Do not fabricate sources, quotations, metrics, implementation results or case-study outcomes.
- Clearly separate documented MLflow functionality, an illustrative architecture, and hypothetical example values.
- Distinguish MLflow's native capabilities from those supplied by GitHub Actions, CI test code, traffic-management systems and deployment infrastructure.
- Explain concepts in accessible but technically precise language suitable for a BE Artificial Intelligence and Data Science student.
- Where official documentation does not establish a feature or guarantee, state that limitation explicitly.

The final output should be detailed enough that I can use it as the primary technical reference while independently preparing my Activity 2 assignment report.