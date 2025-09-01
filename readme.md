# AI Runbooks for Security Operations

This repository provides security operations runbooks and role-based guides for AI-assisted cybersecurity workflows.

## Overview

Built by and for enterprise security teams, this project standardizes incident response procedures and threat analysis workflows for AI-assisted cybersecurity. It equips LLMs with specialized context and cognitive tools to perform complex security investigations with the same rigor and consistency as experienced analysts.

## Key Components

### Personas
Security role definitions including:
- SOC Analysts (Tier 1-3)
- Threat Hunters
- Incident Responders
- CTI Researchers
- Security Engineers
- And more...

### Runbooks
Step-by-step procedural guides for:
- Alert triage
- IOC enrichment and investigation
- Threat hunting
- Incident response
- Case management
- And many more security operations tasks

### Incident Response Plans (IRPs)
Comprehensive end-to-end strategies for:
- Malware incidents
- Phishing attacks
- Ransomware
- Compromised accounts

## Repository Structure

### Quick Overview
```
ai_runbooks/
├── rules_bank/                    # All content - personas, runbooks, documentation
│   ├── personas/                  # Security role definitions  
│   ├── run_books/                 # Procedural guides for security tasks
│   │   ├── common_steps/         # Reusable procedure components
│   │   ├── irps/                 # Incident Response Plans
│   │   └── guidelines/           # Best practices and documentation
│   └── [other documentation]     # Configuration and reference files
├── reports/                      # Generated security reports
├── mcp-security/                 # MCP server implementations
└── [configuration files]         # Various setup and config scripts
```

### Complete Directory Structure & File Analysis

#### 🎯 **Core SOC Automation Content** *(Most Important)*

**`rules_bank/` (54 files)** - The heart of SOC automation
- **Personas** (11 files): AI role definitions for different SOC positions
  - `soc_analyst_unified.md` - Unified Tier 1-3 SOC analyst framework
  - `threat_hunter.md` - Proactive threat hunting specialist
  - `incident_responder.md` - Incident response coordination
  - `detection_engineer.md` - Detection rule development
  - `cti_researcher.md` - Cyber threat intelligence analysis
  - Plus executive roles (CISO, compliance, security engineer)

- **Main Runbooks** (22 files): Core SOC operational procedures
  - `generate_security_reports.md` - Unified reporting (alert, case, detection, UEBA)
  - `ioc_investigation.md` - Progressive IOC analysis (basic → deep → GTI)
  - `threat_hunting.md` - Comprehensive hunting (hypothesis, IOC, APT, campaign)
  - `case_investigation.md` - Complete case analysis (prioritize → investigate → timeline)
  - `triage_alerts.md` - Initial alert assessment and routing
  - Plus specialized workflows for malware, endpoints, cloud, detection engineering

- **Common Steps** (3 files): Intelligent workflow modules
  - `ioc_analysis_workflows.md` - IOC enrichment, pivoting, correlation
  - `case_management_workflows.md` - SOAR case lifecycle management  
  - `operational_workflows.md` - Confirmation, reporting, task management

- **Incident Response Plans** (4 files): Major incident playbooks
  - `ransomware_response.md` - Ransomware incident response
  - `malware_incident_response.md` - Malware outbreak response
  - `phishing_response.md` - Phishing attack response
  - `compromised_user_account_response.md` - Account compromise response

- **Guidelines** (4 files): SOC best practices and standards
  - `report_writing.md` - SOC report standardization
  - `soc_analyst_workflows.md` - SOC analyst process guidance
  - `runbook_guidelines.md` - Operational procedure standards
  - `threat_intel_workflows.md` - Threat intelligence procedures

**`reports/` (37+ files)** - Real SOC automation outputs
- Generated security reports from actual runbook executions
- Examples: Alert triage, hunt reports, IOC enrichment, case investigations
- Demonstrates actual AI-generated SOC documentation

#### 🔧 **Configuration & Integration Files**

**Root Configuration**:
- `configure-mcp.sh` - MCP server setup for SIEM/SOAR/GTI integration
- `CLAUDE.md` - Claude Code AI configuration (core automation setup)
- `LLMS.md` - Multi-LLM agent instructions
- `CHANGELOG.md` - Complete optimization and change history

**Hidden Directories**:
- `.claude/` - Claude Code settings and local configuration
- `.github/workflows/` - Automated quality assurance for SOC runbooks
- `.env.example` - Template for MCP server environment variables

#### 📚 **Supporting Documentation**

- `SUPERCLAUDE_INTEGRATION_SUMMARY.md` - Advanced slash command framework
- `SuperClaude_Framework/` - Git submodule for enhanced automation
- `mcp-security/` - Placeholder for custom MCP server development

#### 🏢 **Administrative Files**

- Standard repository files: LICENSE, CODE_OF_CONDUCT.md, CONTRIBUTING
- Git system files and version control metadata

### SOC Automation Relevance

**🔴 CRITICAL (High Relevance)**: ~100+ files
- All of `rules_bank/` - Complete SOC operational framework  
- All of `reports/` - Actual automation outputs
- Configuration files - SIEM/SOAR/GTI integration setup

**🟡 SUPPORTING (Medium Relevance)**: ~10 files  
- GitHub workflows - Quality assurance automation
- Multi-LLM support - Platform flexibility

**⚪ ADMINISTRATIVE (Low Relevance)**: ~20 files
- Legal, community, and repository management files

**Total: 54 core SOC procedures + 37+ example reports + configuration = Complete AI-assisted SOC automation framework**

## Usage

1. **For Security Teams**: Use this repository to standardize and document your security operations procedures for AI-assisted workflows.

2. **For Developers**: All content is stored in the `rules_bank/` directory for direct access and editing.

3. **For AI Assistants**: The `rules_bank` directory contains all personas, runbooks, and documentation needed for security operations.

## Integration

This project is designed to work with:
- Chronicle SIEM
- SOAR platforms
- Google Threat Intelligence (GTI)
- Security Command Center (SCC)
- Various MCP (Model Context Protocol) tools

## Contributing

See `CONTRIBUTING` file for guidelines on contributing to this project.

## License

This project is licensed under the Apache License 2.0 - see the `LICENSE` file for details.

---

## Quick Start

1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd ai-runbooks
   ```

2. All content is available in the `rules_bank/` directory for immediate use by AI assistants.

### Configuration

- `configure-mcp.sh`: Configure MCP (Model Context Protocol) tools for enhanced security platform integration

## Example Runbook Invocation Prompts

Use these realistic prompts to invoke various security runbooks. All examples use real data extracted from the `reports/` directory:

### Alert Triage
```
Please execute the alert triage runbook for SOAR case 2194.
```
The case involves repeated authentication failures for user F.K. on host A.S.L from IP 10.1.0.4. Check for duplicate cases and perform initial entity enrichment.

### IOC Enrichment
```
Run the basic IOC enrichment runbook for the suspicious domain scarfponcho.com.
```
Threat intelligence analysis and SIEM correlation for a domain which was flagged in our environment.

```
Execute IOC enrichment for the file hash de96a6e69944335375dc1ac238336066889d9ffc7d73628ef4fe1b1b160ab32c found on host WINS-D19.
```
This was associated with PowerShell obfuscation activity by user LISAWALKER.

### Case Investigation
```
Perform a comprehensive case investigation for SOAR case 3480.
```
 This is a critical priority case involving PowerShell attacks on WINS-D19, potential data exfiltration via BigQuery, and GCP exploitation attempts. Focus on the 17 associated alerts.

### Detection Rule Analysis
```
Analyze detection rule ru_99d1f620-3fe2-41d5-918e-0e1bd2402065 (ursnif_malware_dns).
```
 I need rule validation, tuning recommendations, and analysis of recent detections for this high-severity rule.

### Threat Hunting
```
Execute the IOC threat hunt runbook for IP addresses 46.8.9.205, 46.8.9.206, and 46.8.9.207.
```
These IPs are associated with the malicious domain scarfponcho.com and need comprehensive SIEM analysis.

```
Run the advanced threat hunting runbook focusing on lateral movement techniques (PSExec, WMI) around host WINS-D19.
```
This follows the PowerShell attack activity discovered in case 3480.

### Malware Triage
```
Perform malware triage for the sample with hash de96a6e69944335375dc1ac238336066889d9ffc7d73628ef4fe1b1b160ab32c.
```
This was involved in the PowerShell obfuscation incident on WINS-D19.

### Suspicious Login Analysis
```
Execute the suspicious login triage runbook for authentication events involving user F.K. on host A.S.L from source IP 10.1.0.4.
```
This is related to case 2194 with multiple failed followed by successful logins.

### Incident Response
```
Initiate the compromised user account IRP for user LISAWALKER'
```
Evidence includes PowerShell execution with obfuscation techniques on host WINS-D19 and potential privilege escalation attempts.

### Cloud Security Analysis
```
Run the cloud vulnerability triage runbook for the BigQuery exfiltration alerts in case 3480.
```
Focus on the DLP context and Google Drive data movement patterns detected by SCC.


### Endpoint Isolation
```
Execute the basic endpoint triage and isolation runbook for host WINS-D19.
```
This system was compromised in case 3480 with PowerShell attacks and potential malware execution.

### Deep Dive Analysis
```
Perform a deep dive IOC analysis on domain scarfponcho.com using GTI collections.
```
Include malware family associations, campaign attribution, and infrastructure analysis.


### Summary
These examples demonstrate how to invoke runbooks with specific, actionable intelligence that mirrors real security operations scenarios.