# cicd-pipeline-architectures
GitLab & AWS CodePipeline implementations for TechNova Inc. 10+ projects, 30% faster releases, 25% fewer errors, supporting 15 engineers.

## Overview
This repository contains CI/CD pipeline architectures and configuration files used across multiple projects. The implementations support automated testing, building, and deployment workflows.

## Technologies
- **GitLab CI/CD**: Automated pipelines using `.gitlab-ci.yml`
- **AWS CodePipeline**: Cloud-native CI/CD with AWS services
- **Docker**: Containerized builds and deployments
- **Kubernetes**: Container orchestration and deployment
- **Infrastructure as Code**: Automated infrastructure provisioning

## Pipeline Features
- Automated testing and quality gates
- Multi-stage deployments (dev, staging, production)
- Rollback capabilities
- Integrated security scanning
- Performance monitoring

## Results
- **10+ projects** successfully migrated to automated CI/CD
- **30% faster** release cycles
- **25% fewer** deployment errors
- Supporting **15 engineers** across multiple teams

## Kubernetes Deployment Architecture

The `k8s/` directory contains Kubernetes manifests for containerized application deployment:

### Files Structure
```
k8s/
├── deployment.yaml    # Application deployment configuration
├── service.yaml       # Service for cluster access
└── ingress.yaml       # Ingress configuration (placeholder)
```

### Deployment Configuration
The `deployment.yaml` file defines:
- **Replicas**: 3 pods for high availability
- **Container**: nginx:latest (example application)
- **Resources**: 
  - CPU limits: 500m, requests: 250m
  - Memory limits: 512Mi, requests: 256Mi
- **Port**: Container port 80

### Service Configuration
The `service.yaml` provides:
- **Type**: ClusterIP (internal cluster access)
- **Port**: 80 (HTTP)
- **Selector**: Routes traffic to pods with label `app: myapp`

### Ingress Configuration
The `ingress.yaml` is a placeholder for external access configuration:
- Configure your ingress controller settings
- Define host-based routing rules
- Set up TLS/SSL certificates if needed

## Deployment Process

### Prerequisites
- Kubernetes cluster (1.19+)
- kubectl configured with cluster access
- (Optional) Ingress controller installed

### Manual Deployment
1. Apply the Kubernetes manifests:
   ```bash
   kubectl apply -f k8s/deployment.yaml
   kubectl apply -f k8s/service.yaml
   kubectl apply -f k8s/ingress.yaml  # After configuration
   ```

2. Verify deployment:
   ```bash
   kubectl get deployments
   kubectl get pods
   kubectl get services
   ```

3. Check application logs:
   ```bash
   kubectl logs -l app=myapp
   ```

### CI/CD Integration
The `.gitlab-ci.yml` file automates the deployment process:
- **Build Stage**: Creates Docker images
- **Test Stage**: Runs automated tests
- **Deploy Stage**: Applies Kubernetes manifests to target cluster

#### GitLab CI/CD Pipeline Stages
1. **Build**: Compile and containerize application
2. **Test**: Execute unit, integration, and security tests
3. **Deploy to Dev**: Automatic deployment to development environment
4. **Deploy to Staging**: Manual approval for staging deployment
5. **Deploy to Production**: Manual approval for production deployment

### Environment Variables
Configure these variables in your CI/CD settings:
- `KUBE_CONFIG`: Kubernetes cluster configuration
- `DOCKER_REGISTRY`: Container registry URL
- `NAMESPACE`: Target Kubernetes namespace

## Files
- `.gitlab-ci.yml`: GitLab CI/CD pipeline configuration
- `aws-codepipeline.json`: AWS CodePipeline infrastructure definition
- `k8s/`: Kubernetes deployment manifests
  - `deployment.yaml`: Application deployment specification
  - `service.yaml`: Service configuration
  - `ingress.yaml`: Ingress rules (placeholder)
- Additional pipeline configurations for specific project types

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/aliu2298/cicd-pipeline-architectures.git
   cd cicd-pipeline-architectures
   ```

2. Review and customize the Kubernetes manifests in the `k8s/` directory

3. Update the `.gitlab-ci.yml` file with your project-specific settings

4. Deploy to your Kubernetes cluster using kubectl or through the CI/CD pipeline

## Support
For questions or issues, please open an issue in this repository.
