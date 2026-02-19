# AWS Strategy and Infrastructure Review

## Overview
This document outlines the current AWS infrastructure usage within the AWS Toolkit for VS Code repository and provides recommendations for future development and optimization.

## Current AWS Infrastructure
- **CI/CD**: The project currently uses AWS CodeBuild for its CI/CD pipeline, including linting, unit tests, and integration tests.
- **Build Artifacts**: ECR is used to store the Docker images required for the build environment.
- **Telemetry**: User telemetry is handled via AWS Cognito, which manages identities for reporting metrics and feedback.
- **Service Integration**: As a core AWS tool, the repository integrates deeply with nearly all AWS services via generated and official SDKs.

## Evaluation
### Pros
- **Dogfooding**: Using AWS for development demonstrates the capabilities of the platform.
- **Security & Compliance**: Built-in integration with AWS security tools ensures the project meets corporate standards.
- **Performance**: High-speed access to AWS services during build and test phases.

### Cons
- **Visibility**: CodeBuild results are less visible to the open-source community compared to GitHub Actions.
- **Overhead**: For non-core services like documentation hosting, AWS infrastructure can be more complex to manage than simpler alternatives.

## Recommendations

### 1. Hybrid CI/CD Model
While retaining CodeBuild for official releases and sensitive tests, consider moving public-facing CI/CD (linting, basic unit tests) to **GitHub Actions**. This improves visibility for external contributors and integrates better with the GitHub UI.

### 2. Documentation Hosting on Render
The project's documentation (currently in the `docs/` folder) should be transformed into a hosted static site using a framework like Docusaurus. **Render** is recommended for this purpose due to its simplicity, automatic SSL, and global CDN, providing a superior experience for users over raw markdown files.

### 3. Beta Distribution Portal
The current beta distribution mechanism (checks a hardcoded URL) could be modernized using a simple web service on **Render**. This would allow for easier management of beta releases and better tracking of downloads and usage.

### 4. Telemetry Evolution
Continue using **AWS Cognito** for telemetry to maintain data security and consistency with the AWS ecosystem. However, consider a backend aggregator (hosted on AWS or Render) to pre-process data and reduce the direct dependency of the client on multiple AWS APIs.

## Conclusion
The AWS Toolkit for VS Code should remain "AWS-first" to maintain its product identity. However, adopting modern platforms like **Render** and **GitHub Actions** for supporting services and community engagement will improve developer agility and user satisfaction.
