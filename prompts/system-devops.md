# System & DevOps Prompts

Effective prompts for system administration, DevOps automation, infrastructure management, and operational tasks.

## Shell Scripting and Automation

### Shell Script Creation
```
[Additional Information]
- Task: [task description]
- Environment: [Linux/macOS/Windows/cross-platform]
- Shell type: [bash/zsh/powershell/generic]
- Input parameters: [command line arguments expected]
- Output format: [console output, file generation, etc.]

[Directive]
Create a shell script to perform the specified task.

[Output Formatting]
- Script features:
  - Proper error handling and exit codes.
  - Input validation and sanitization.
  - Logging and debugging capabilities.
  - Help/usage documentation.
  - Support for a configuration file if needed.
  - Cross-platform compatibility considerations.
  - Security best practices (no hardcoded secrets).
  - Modularity and reusability.
  - Progress indicators for long-running tasks.
```

### Process Automation
```
[Additional Information]
- Manual process to automate:
[describe the current manual process]
- Process context:
  - Frequency: [how often this needs to run]
  - Dependencies: [systems, files, or services involved]
  - Error conditions: [what can go wrong]
  - Success criteria: [how to verify completion]
  - Notification requirements: [who needs to know when it runs]

[Directive]
Automate this manual process.

[Output Formatting]
- Automation approach:
  - Break down the process into discrete, testable steps.
  - Identify points of failure and implement recovery strategies.
  - Include monitoring and alerting.
  - Design for idempotency (safe to run multiple times).
  - Add configuration management.
  - Include rollback mechanisms.
  - Document prerequisites and setup.
  - Create testing and validation procedures.
```

### Cron Job Configuration
```
[Additional Information]
- Scheduling requirements:
  - Tasks to schedule: [list tasks with timing requirements]
  - Dependencies between tasks.
  - Resource requirements and constraints.
  - Error handling and recovery needs.

[Directive]
Create cron jobs for the specified tasks.

[Output Formatting]
- Cron configuration:
  - Proper scheduling syntax for each task.
  - Environment variable setup.
  - Output redirection and logging.
  - Error notification mechanisms.
  - Resource usage considerations.
  - Backup and recovery procedures.
  - Monitoring and health checks.
  - Documentation and maintenance notes.
```

## Infrastructure as Code

### Terraform Configuration
```
[Role]
You are a DevOps engineer specializing in cloud infrastructure.

[Additional Information]
- Infrastructure requirement: [infrastructure requirement]
- Cloud provider: [AWS/Azure/GCP/multi-cloud]
- Resources needed: [compute, storage, networking, etc.]
- Environment: [dev/staging/prod]
- Compliance requirements: [security, backup, monitoring]
- Scaling requirements: [expected load and growth]

[Directive]
Create a Terraform configuration.

[Output Formatting]
- Terraform design:
  - A modular structure with reusable components.
  - Proper variable definitions and validation.
  - State management and backend configuration.
  - Security best practices (encryption, access controls).
  - Tagging and resource organization.
  - Output definitions for other modules.
  - Documentation and examples.
  - Testing and validation procedures.
```

### Ansible Playbooks
```
[Role]
You are a configuration management specialist.

[Additional Information]
- Task: [configuration management task]
- Target environment:
  - Server types and OS: [Linux distros, Windows, etc.]
  - Inventory structure: [how hosts are organized]
  - Configuration requirements: [software, settings, files]
  - Security requirements: [user access, encryption, etc.]

[Directive]
Create an Ansible playbook.

[Output Formatting]
- Playbook structure:
  - Inventory file organization.
  - Role-based task organization.
  - Variable management (group_vars, host_vars).
  - Template configurations.
  - Handler definitions for service management.
  - Error handling and rollback procedures.
  - Idempotency checks.
  - Testing and validation tasks.
  - Documentation and usage examples.
```

### Docker Configuration
```
[Role]
You are a containerization expert.

[Additional Information]
- Application/Service: [application/service]
- Application details:
  - Technology stack: [languages, frameworks, databases]
  - Runtime requirements: [dependencies, environment variables]
  - Networking needs: [ports, inter-service communication]
  - Data persistence: [volumes, databases, file storage]
  - Scaling requirements: [horizontal scaling, load balancing]

[Directive]
Create a Docker setup for the specified application.

[Output Formatting]
- Docker configuration:
  - Dockerfile with multi-stage builds if appropriate.
  - Docker Compose for multi-service applications.
  - Environment variable management.
  - Volume configurations for data persistence.
  - Network configuration for service communication.
  - Health checks and monitoring.
  - Security considerations (non-root user, minimal base image).
  - Build optimization and image size reduction.
```

## CI/CD Pipeline Configuration

### GitHub Actions Workflow
```
[Additional Information]
- Development workflow: [development workflow]
- Project context:
  - Technology stack: [languages, frameworks, tools]
  - Testing requirements: [unit, integration, e2e tests]
  - Deployment targets: [staging, production environments]
  - Security requirements: [code scanning, dependency checks]
  - Notification needs: [team communication, external systems]

[Directive]
Create a GitHub Actions workflow.

[Output Formatting]
- Workflow configuration:
  - Trigger conditions (push, PR, schedule).
  - Job dependencies and parallel execution.
  - Environment setup and caching.
  - Testing strategy and coverage reporting.
  - Build and artifact management.
  - Deployment automation with approvals.
  - Security scanning and vulnerability management.
  - Notification and reporting mechanisms.
  - Secrets management and environment variables.
```

### Jenkins Pipeline
```
[Additional Information]
- CI/CD process: [CI/CD process]
- Pipeline requirements:
  - Source code management: [Git, SVN, etc.]
  - Build process: [compilation, packaging, testing]
  - Deployment strategy: [blue-green, rolling, canary]
  - Environment management: [dev, staging, prod]
  - Approval processes: [manual gates, automated checks]

[Directive]
Create a Jenkins pipeline.

[Output Formatting]
- Pipeline design:
  - Declarative or scripted pipeline syntax.
  - Stage definitions with proper error handling.
  - Parallel execution where appropriate.
  - Artifact management and promotion.
  - Environment-specific configurations.
  - Rollback and recovery procedures.
  - Monitoring and alerting integration.
  - Documentation and maintenance procedures.
```

## Monitoring and Observability

### Monitoring Setup
```
[Role]
You are a Site Reliability Engineer (SRE).

[Additional Information]
- System/Application to monitor: [system/application]
- Monitoring scope:
  - Infrastructure: [servers, networks, storage]
  - Applications: [performance, errors, user experience]
  - Business metrics: [KPIs, user behavior, revenue impact]
  - Security: [intrusion detection, access monitoring]

[Directive]
Set up a monitoring strategy.

[Output Formatting]
- Monitoring strategy components:
  - Key metrics to track for each area.
  - Recommended monitoring tools and platforms.
  - Alerting thresholds and notification channels.
  - Dashboard design and visualization.
  - Log aggregation and analysis approach.
  - Distributed tracing setup.
  - Health check and uptime monitoring.
  - On-call rotation and incident response plan.
```

### Log Analysis
```
[Role]
You are an operations analyst.

[Additional Information]
- Logs to analyze:
[paste log snippets]
- System context: [describe the system that generated the logs]
- Problem: [describe the issue you are investigating]

[Directive]
Analyze these logs to identify the root cause of the problem.

[Output Formatting]
- Analysis report:
  - Identification of relevant log entries.
  - Correlation of events across different log sources.
  - A timeline of the incident.
  - The root cause analysis.
  - Recommendations for remediation.
  - Suggestions for improving logging to prevent future issues.
```

## Security and Compliance

### Security Hardening
```
[Role]
You are a security engineer.

[Additional Information]
- System to harden: [OS, application, network device]
- Compliance standards: [PCI-DSS, HIPAA, GDPR, etc.]

[Directive]
Create a security hardening plan for the specified system.

[Output Formatting]
- Hardening plan:
  - Minimize the attack surface (e.g., disable unused services).
  - Implement strong access controls and password policies.
  - Configure firewalls and network segmentation.
  - Apply security patches and updates.
  - Set up logging and auditing.
  - Implement file integrity monitoring.
  - Configure intrusion detection/prevention systems.
  - Perform regular vulnerability scanning.
```

### Incident Response Plan
```
[Role]
You are a cybersecurity incident responder.

[Additional Information]
- Organization: [describe the organization]
- Potential incident types: [malware, data breach, DDoS, etc.]

[Directive]
Develop an incident response plan.

[Output Formatting]
- Plan phases:
  - **Preparation:** Tools, training, and documentation.
  - **Identification:** Detecting and verifying an incident.
  - **Containment:** Isolating affected systems to prevent further damage.
  - **Eradication:** Removing the threat from the environment.
  - **Recovery:** Restoring systems to normal operation.
  - **Lessons Learned:** Post-incident analysis to improve future responses.
- Include team roles, communication protocols, and legal considerations.
```

## Cloud Management

### Cost Optimization
```
[Role]
You are a cloud financial operations (FinOps) specialist.

[Additional Information]
- Cloud environment: [AWS/Azure/GCP]
- Services used: [list key services being used]
- Current monthly cost: [provide current spending]

[Directive]
Create a cloud cost optimization strategy.

[Output Formatting]
- Optimization strategy:
  - Identify and terminate unused or idle resources.
  - Right-size instances based on utilization metrics.
  - Implement auto-scaling to match demand.
  - Use reserved instances or savings plans for predictable workloads.
  - Implement storage lifecycle policies.
  - Set up budget alerts and cost monitoring dashboards.
  - Tag resources for cost allocation and accountability.
```

### Disaster Recovery Plan
```
[Role]
You are a business continuity planner.

[Additional Information]
- Application: [describe critical application]
- RTO/RPO: [define Recovery Time Objective and Recovery Point Objective]
- Cloud provider: [AWS/Azure/GCP]

[Directive]
Design a disaster recovery plan.

[Output Formatting]
- Plan components:
  - Backup and restore procedures.
  - Multi-region or multi-AZ deployment strategy.
  - Data replication mechanisms.
  - Automated failover and failback processes.
  - Regular testing and drill procedures.
  - Communication plan for stakeholders during an outage.
  - Documentation of the entire process.
```

## System Administration

### Server Provisioning
```
[Role]
You are a system administrator.

[Additional Information]
- Server purpose: [web server, database server, application server]
- Operating system: [Linux distro, Windows Server version]
- Hardware requirements: [CPU, RAM, storage]
- Software requirements: [list all necessary software]
- Networking configuration: [IP addresses, subnets, firewall rules]

[Directive]
Outline the steps to provision a new server.

[Output Formatting]
- Provisioning checklist:
  - Hardware procurement and setup.
  - OS installation and configuration.
  - Network configuration.
  - User and group management.
  - Security hardening.
  - Software installation and configuration.
  - Monitoring and backup agent installation.
  - Performance testing and validation.
  - Documentation of the server setup.
```

### System Health Check
```
[Role]
You are an IT operations specialist.

[Directive]
Create a daily system health check script.

[Output Formatting]
- A script that checks and reports on:
  - CPU, memory, and disk usage.
  - Running processes and services.
  - Network connectivity and open ports.
  - Recent system and application log errors.
  - Backup status.
  - Server uptime.
- The script should send a summary report via email or to a monitoring system.
```

## Documentation

### Architecture Diagram
```
[Role]
You are a solutions architect.

[Additional Information]
- System description:
[describe the system architecture, components, and data flow]

[Directive]
Create a textual description for a system architecture diagram.

[Output Formatting]
- Use a format compatible with a diagramming tool like Mermaid or PlantUML.
- Include nodes for all components (e.g., web servers, databases, message queues).
- Show data flow and interactions between components.
- Group components into logical units (e.g., VPCs, subnets).
- Differentiate between internal and external services.
```

### Runbook for Outages
```
[Role]
You are a system reliability engineer.

[Additional Information]
- Service: [name of the service]
- Common alert: [describe a common alert for this service]

[Directive]
Create a runbook for handling this alert.

[Output Formatting]
- Runbook structure:
  - **Alert Name:**
  - **Priority:** (e.g., P1, P2, P3)
  - **Description:** What does this alert mean?
  - **Initial Triage Steps:** How to quickly assess the impact.
  - **Troubleshooting Steps:** Detailed commands and procedures to diagnose the issue.
  - **Escalation Path:** Who to contact if the issue cannot be resolved.
  - **Resolution Steps:** How to fix the problem.
  - **Post-Mortem:** Link to post-mortem documentation.
``` 