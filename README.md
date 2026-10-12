TEST PLAN — VOTING APPLICATION DEVOPS CAPSTONE
Document ID: TP-VA-001
Version: 1.0
Status: In Progress
Test Environment: Ubuntu 24.04 on WSL2
Application: Docker Compose-based Voting Application
Test Approach: Manual testing, followed by automated CI and Kubernetes testing
1. Introduction
This test plan defines the approach for testing the voting application as part of the DevOps capstone project. The application consists of five core services: Vote, Redis, Worker, PostgreSQL and Result.
The plan covers application functionality, service integration, container operations, recovery, container image security and, in later stages, CI/CD automation and Kubernetes deployment.
The tester will independently analyse the application, identify testing requirements, design test cases, execute tests, report defects and document the results. The plan will be reviewed and updated as the project progresses.
2. Test Objectives
The objectives of testing are to:
Verify that the application can be built and started using Docker Compose.
Confirm that the voting interface accepts votes.
Verify that submitted votes are processed and reflected on the results page.
Check that the core services interact as expected.
Identify and document functional defects and operational failures.
Verify recovery after service interruptions and retest previously working functionality.
Assess container images for known vulnerabilities using Trivy.
Verify that the CI pipeline enforces the agreed security gate before publishing images.
Verify application deployment and recovery using Terraform-managed Kubernetes infrastructure and Helm.
Produce test evidence and a final report identifying passed tests, failed tests, unresolved defects and remaining risks.
3. Scope of Testing
3.1 In Scope
Docker Compose configuration validation.
Application image builds.
Startup and availability of the five core services.
Voting page accessibility and option selection.
Vote submission and results updates.
Integration between Vote, Redis, Worker, PostgreSQL and Result.
Basic recovery and regression testing.
Container image vulnerability scanning with Trivy.
CI workflow behaviour, including test execution, security checks and SHA-tagged image publishing.
Kubernetes deployment and service accessibility.
Helm release verification and rollback.
3.2 Out of Scope
Full penetration testing.
Formal load and stress testing.
Production-scale availability testing.
Comprehensive performance benchmarking.
Testing unrelated features of the original application.
Production infrastructure readiness certification.
These activities may be added later if required by the project.
4. Test Strategy and Approach
Testing will be performed in stages, beginning with local manual testing and progressing to automated and deployment testing.
Test level
Approach
Purpose
Configuration testing
Manual validation
Confirm that Docker Compose configuration is valid
Smoke testing
Manual and automated
Confirm that the application starts and core functions are available
Functional testing
Manual, followed by automation where practical
Verify voting and results behaviour
Integration testing
Manual and automated where practical
Verify communication between application services
Recovery testing
Manual
Check application behaviour after service interruption
Regression testing
Repeat relevant tests after changes
Confirm that existing functionality still works
Security testing
Trivy scans and CI gate checks
Identify known vulnerabilities and enforce the agreed policy
Deployment testing
Kubernetes and Helm verification
Confirm deployment, application access and rollback

Test execution method
For each test case, the tester will record:
Test case ID and title.
Preconditions.
Test steps.
Test data.
Expected result.
Actual result.
Pass, fail or blocked status.
Evidence and defect reference, where applicable.
5. Test Environment
Component
Configuration
Operating system
Ubuntu 24.04 on WSL2
Container platform
Docker
Local orchestration
Docker Compose
Voting service
Python / Flask
Results service
Node.js
Worker
.NET
Message queue
Redis
Database
PostgreSQL
Voting interface
http://localhost:8080
Results interface
http://localhost:8081
Vulnerability scanner
Trivy v0.75.0
CI platform
GitHub Actions
Container registry
GitHub Container Registry (GHCR)
Infrastructure provisioning
Terraform
Kubernetes deployment
Helm

The local environment will be used for initial functional testing. The CI and Kubernetes environments will be tested when their configurations are implemented.
6. Test Data
Test data will be limited to non-production data generated for the capstone.
Planned test data includes:
Valid voting selections supported by the application.
Individual test votes for verifying result updates.
Repeated voting attempts to observe application behaviour.
Application image versions and Git commit SHA tags.
Vulnerability scan results and image metadata.
Controlled deployment changes for testing Helm rollback.
The tester will avoid using real personal data or production credentials. Database persistence and duplicate-vote behaviour will be tested without deleting existing data unnecessarily.
7. Entry Criteria
Testing may begin when:
The application source code is available.
Docker and Docker Compose are installed and running.
The Compose configuration can be loaded.
Required images can be built or obtained.
Required services and ports are available.
Test cases and expected results have been documented.
For CI testing, the workflow and repository permissions must be configured. For Kubernetes testing, the cluster, required access credentials and deployment configuration must be available.
8. Exit Criteria
A test stage may be considered complete when:
All planned tests for that stage have been executed or explicitly marked as blocked.
Results and supporting evidence have been recorded.
Failed tests have associated defect records.
Critical outstanding issues have been identified and assessed.
Retesting has been completed for fixes within the stage.
A test summary has been prepared.
The security stage cannot be declared successful until the required Trivy security gate has passed or an explicitly approved exception has been documented. The current vote image has unresolved HIGH findings, so security approval has not yet been achieved.
9. Test Deliverables
The testing activities will produce:
Test plan.
Manual test cases and execution records.
Bug reports and troubleshooting log.
Test execution summary.
Trivy scan reports and vulnerability assessment.
CI workflow execution evidence.
Kubernetes deployment and Helm rollback test results.
Final test report with outstanding risks and recommendations.
10. Roles and Responsibilities
Tester
The tester is responsible for analysing the application, preparing the test plan, designing and executing test cases, documenting defects, performing retesting, collecting evidence and preparing test reports.
DevOps Engineer / Project Owner
The project owner is responsible for maintaining the application, implementing configuration and pipeline changes, addressing defects and security findings, and providing the infrastructure required for testing.
In this capstone, these responsibilities may be performed by the same person. Test planning and execution should still be documented separately from implementation and remediation.
11. Risks and Mitigation
Risk
Potential impact
Mitigation
Unexpected container shutdown
Interrupts testing
Record evidence, recover services carefully and investigate the cause
Duplicate database-key errors
May affect vote processing
Preserve data and investigate the worker/database interaction
HIGH or CRITICAL vulnerabilities
Security gate blocks publishing
Investigate findings and apply verified fixes
Inconsistent vulnerability metadata
May lead to incorrect conclusions
Compare Trivy findings with the image inventory and package metadata
Unsupported base images
Increased security and maintenance risk
Review compatibility and plan supported image upgrades
CI workflow errors
Prevents automated checks
Validate YAML and test workflow behaviour before relying on it
Kubernetes configuration errors
Deployment failure
Validate manifests, Helm templates and service connectivity
Loss of persistent data
Invalidates testing evidence
Avoid destructive volume operations and preserve test data

12. Defect Management
All defects will be recorded with a unique ID, title, description, reproduction steps, expected result, actual result, severity, priority, evidence, status and retest outcome.
Defects will be prioritised according to their impact on core functionality, data integrity, security and deployment reliability.
A recovered issue will not automatically be considered fully resolved if its root cause remains unknown. The record must distinguish between recovery, verified resolution and outstanding investigation.
13. Test Schedule
Testing will follow the project implementation sequence:
Complete local Docker Compose functional testing.
Investigate unresolved operational issues.
Complete container security assessment.
Implement and validate GitHub Actions CI.
Provision Kubernetes infrastructure using Terraform.
Deploy the application using Helm.
Test release rollback.
Complete regression testing and final reporting.
The schedule will be updated according to test results and the resolution of blocking issues.
14. Test Approval and Sign-Off
The test plan will be reviewed and updated by the tester as the project progresses.
Final sign-off will be based on documented evidence that the required functional, security, automation and deployment tests have been completed. Outstanding defects and risks will be listed explicitly rather than treated as passed.
Current status: Local functional smoke tests have passed. Container security remediation, CI validation and Kubernetes deployment testing remain in progress.

