# Production-Grade MLOps Pipeline on AWS

A fully automated, zero-touch machine learning operations pipeline that orchestrates model training, containerization, deployment, validation, and monitoring on AWS infrastructure.

## Architecture Overview

```
GitHub Repository (Code Changes)
        ↓
GitHub Actions Workflow
  ├─ Unit Tests & Linting
  ├─ Model Training
  ├─ Artifact Storage (S3)
  ├─ Docker Image Build
  ├─ Push to Amazon ECR
  ├─ Deploy to Test EKS
  ├─ Automated Validation
  └─ CloudWatch Monitoring
        ↓
AWS Infrastructure
  ├─ EKS Cluster (Kubernetes)
  ├─ ECR Repository (Container Images)
  ├─ S3 Bucket (Model Artifacts)
  ├─ CloudWatch (Metrics & Logs)
  ├─ SNS (Alerts)
  └─ RDS/DynamoDB (Optional - Model Metadata)
```

## Features

✅ **Continuous Integration/Deployment (CI/CD)**
- Automated workflow triggers on main branch changes
- Manual execution capability
- Comprehensive testing and validation

✅ **Machine Learning Automation**
- Scikit-learn model training pipeline
- Automated feature engineering
- Model versioning and artifact management
- Performance tracking

✅ **Container & Orchestration**
- Optimized multi-stage Docker builds
- Amazon ECR integration
- Kubernetes manifests with Helm charts
- Horizontal Pod Autoscaling (HPA)
- Zero-downtime rolling updates

✅ **Deployment Validation**
- Automated health checks
- Inference request verification
- Response schema validation
- Rollback on failure

✅ **Observability & Monitoring**
- CloudWatch metrics integration
- Custom application metrics
- Latency, throughput, and error rate tracking
- Pre-configured dashboards
- SNS-based alerting

✅ **Infrastructure as Code (IaC)**
- Terraform modules for all AWS resources
- Repeatable, versioned deployments
- Security best practices

✅ **Security**
- GitHub Secrets for credentials
- Least-privilege IAM policies
- Container image scanning
- RBAC for Kubernetes

## Quick Start

### Prerequisites

- AWS Account with appropriate permissions
- GitHub account and repository
- Docker installed locally
- Kubernetes CLI (`kubectl`)
- Helm 3+
- Terraform >= 1.0

### 1. Configure GitHub Secrets

Add these secrets to your repository settings:

```
AWS_ACCOUNT_ID          # Your AWS account ID
AWS_ACCESS_KEY_ID       # IAM user access key
AWS_SECRET_ACCESS_KEY   # IAM user secret key
AWS_REGION              # e.g., us-east-1
ECR_REPOSITORY_NAME     # mlops-model
```

### 2. Deploy AWS Infrastructure

```bash
cd terraform
terraform init
terraform plan
terraform apply -auto-approve
```

### 3. Trigger the Pipeline

Push code to the main branch:

```bash
git add .
git commit -m "Initial MLOps pipeline setup"
git push origin main
```

The workflow will automatically:
1. Run tests and linting
2. Train the model
3. Build and push Docker image to ECR
4. Deploy to EKS
5. Run validation tests
6. Send CloudWatch metrics and alerts

## Project Structure

```
mlops-pipeline/
├── .github/workflows/mlops-pipeline.yml      # CI/CD workflow
├── app/
│   ├── __init__.py
│   ├── main.py                               # FastAPI inference service
│   ├── health.py                             # Health check endpoints
│   └── requirements.txt
├── ml_service/
│   ├── __init__.py
│   ├── train.py                              # Model training script
│   ├── model_utils.py                        # Model utilities
│   ├── config.py                             # Configuration
│   └── requirements.txt
├── docker/
│   └── Dockerfile                            # Production container
├── kubernetes/
│   ├── helm/mlops-model/
│   │   ├── Chart.yaml
│   │   ├── values.yaml
│   │   ├── values-test.yaml
│   │   └── templates/
│   │       ├── deployment.yaml
│   │       ├── service.yaml
│   │       ├── configmap.yaml
│   │       ├── hpa.yaml
│   │       └── ingress.yaml
│   └── manifests/
├── terraform/
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── eks.tf
│   ├── ecr.tf
│   ├── iam.tf
│   ├── cloudwatch.tf
│   └── s3.tf
├── scripts/
│   ├── deploy.sh
│   ├── validate.sh
│   ├── wait_for_service.py
│   └── rollback.sh
├── tests/
│   ├── __init__.py
│   ├── test_api.py
│   ├── test_model.py
│   └── test_inference.py
├── monitoring/
│   ├── dashboards/mlops-dashboard.json
│   └── alarms/alarm-config.tf
└── docs/
    ├── SETUP.md
    ├── DEPLOYMENT.md
    └── MONITORING.md
```

## Pipeline Stages

1. **Test & Lint** (5 min)
   - Unit tests with pytest
   - Code quality with flake8/black
   - Security scanning with bandit

2. **Model Training** (15 min)
   - Load and preprocess data
   - Feature engineering
   - Train scikit-learn model
   - Save artifacts to S3

3. **Build & Push** (10 min)
   - Multi-stage Docker build
   - Image vulnerability scan with Trivy
   - Push to Amazon ECR

4. **Deploy** (5 min)
   - Helm deployment to EKS
   - Rolling update strategy
   - Wait for readiness

5. **Validation** (10 min)
   - Health check endpoint
   - Inference request validation
   - Performance benchmarking
   - Schema verification

6. **Monitoring** (Continuous)
   - CloudWatch metrics
   - Latency/error rate tracking
   - SNS alerts

## Documentation

- [SETUP.md](docs/SETUP.md) - Detailed AWS and local setup
- [DEPLOYMENT.md](docs/DEPLOYMENT.md) - Deployment instructions
- [MONITORING.md](docs/MONITORING.md) - Monitoring guide

## License

MIT License
