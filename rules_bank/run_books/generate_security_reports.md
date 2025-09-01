---
title: "Generate Security Reports - Unified Runbook"
type: "runbook"
category: "security_operations"
status: "active"
consolidates: ["alert_report.md", "case_report.md", "detection_report.md", "ueba_report.md"]
tags:
  - reporting
  - documentation
  - alert_investigation
  - case_management
  - detection_engineering
  - ueba_analysis
---

# Generate Security Reports - Unified Runbook

## Objective

Generate standardized reports for various security entities and investigations including alerts, cases, detection rules, and UEBA findings. This consolidated runbook covers all report generation workflows in one comprehensive procedure.

## Report Types Supported

1. **Alert Reports** - Investigation summary for security alerts
2. **Case Reports** - Comprehensive case investigation documentation  
3. **Detection Reports** - Analysis and validation of detection rules
4. **UEBA Reports** - User and Entity Behavior Analysis findings

## Universal Inputs

*   `${REPORT_TYPE}`: Type of report to generate (alert, case, detection, ueba)
*   `${PRIMARY_IDENTIFIER}`: Main ID (CASE_ID, ALERT_ID, RULE_ID, USER_ID)
*   `${REPORT_FILENAME_SUFFIX}`: Optional suffix for report filename
*   `${REPORT_AUDIENCE}`: Target audience (technical, executive, compliance)

## Universal Tools

*   `secops-soar`: Case and alert management
*   `secops-mcp`: SIEM queries and entity lookup
*   `gti-mcp`: Google Threat Intelligence integration
*   **Action:** Generate report file

## Consolidated Workflow

### Phase 1: Report Type Selection & Input Validation

1. **Determine Report Type** based on `${REPORT_TYPE}`:
   - **alert**: Generate alert investigation summary
   - **case**: Generate comprehensive case report
   - **detection**: Generate detection rule analysis
   - **ueba**: Generate UEBA analysis report

2. **Validate Required Inputs** for each report type
3. **Initialize Report Context** with metadata

### Phase 2: Data Collection (Type-Specific)

#### For Alert Reports (`REPORT_TYPE=alert`)
- **Input Requirements**: `${CASE_ID}`, `${ALERT_GROUP_IDENTIFIERS}` or `${ALERT_IDS}`
- **Data Collection**:
  1. Get case details using `secops-soar.get_case_full_details`
  2. Identify target alerts and extract key entities
  3. Gather alert events via `list_events_by_alert`
  4. Perform entity enrichment (SIEM + GTI)
  5. Optional: Search related SIEM activity

#### For Case Reports (`REPORT_TYPE=case`)
- **Input Requirements**: `${CASE_ID}`
- **Data Collection**:
  1. Get comprehensive case details
  2. List all alerts in case
  3. Extract all entities across alerts
  4. Perform deep entity enrichment
  5. Timeline analysis of events
  6. Risk assessment and impact analysis

#### For Detection Reports (`REPORT_TYPE=detection`)
- **Input Requirements**: `${RULE_ID}` or `${RULE_NAME}`
- **Data Collection**:
  1. Get detection rule details
  2. Analyze recent rule performance
  3. Review triggered alerts and false positives
  4. Assess rule effectiveness metrics
  5. Identify tuning opportunities

#### For UEBA Reports (`REPORT_TYPE=ueba`)
- **Input Requirements**: `${USER_ID}` or `${ENTITY_ID}`
- **Data Collection**:
  1. Get user/entity behavior baseline
  2. Identify anomalous activities
  3. Analyze risk indicators
  4. Review related security events
  5. Assess behavioral patterns

### Phase 3: Universal Report Generation

1. **Format Report Content** with standardized structure:
   - **Metadata**: Runbook used, timestamp, identifiers
   - **Executive Summary**: High-level findings
   - **Detailed Analysis**: Type-specific analysis
   - **Key Findings**: Critical discoveries
   - **Recommendations**: Next steps and actions
   - **Workflow Diagram**: Mermaid sequence diagram

2. **Generate Report File**:
   - Construct filename: `./reports/${REPORT_TYPE}_report_${PRIMARY_IDENTIFIER}_${TIMESTAMP}.md`
   - Write formatted markdown content

3. **Update Source System** (optional):
   - Post summary to SOAR case
   - Update detection rule notes
   - Log analysis completion

## Report Templates by Type

### Alert Report Structure
```markdown
# Alert Investigation Report - ${CASE_ID}

## Executive Summary
Brief overview of alert investigation findings

## Case Summary
Case details, priority, status

## Alert(s) Summary
Target alerts with IDs, names, timestamps, severities

## Key Entities Involved
List of entities with descriptions

## Enrichment Summary
SIEM and GTI findings for each entity

## Event Summary
Key triggering events with timestamps

## Initial Assessment
Assessment classification and rationale

## Recommendations
Next steps for handling
```

### Case Report Structure
```markdown
# Case Investigation Report - ${CASE_ID}

## Executive Summary
Case overview and key findings

## Case Details
Comprehensive case information

## Timeline Analysis
Chronological event sequence

## Entity Analysis
All involved entities with enrichment

## Impact Assessment
Business and security impact

## Investigation Findings
Detailed analysis results

## Recommendations
Response and mitigation actions
```

### Detection Report Structure
```markdown
# Detection Rule Analysis - ${RULE_ID}

## Executive Summary
Rule performance and effectiveness summary

## Rule Details
Configuration and logic analysis

## Performance Metrics
Alert generation and false positive rates

## Effectiveness Assessment
Coverage and detection capability

## Tuning Recommendations
Suggested improvements and optimizations

## Validation Results
Testing and validation outcomes
```

### UEBA Report Structure
```markdown
# UEBA Analysis Report - ${USER_ID}

## Executive Summary
Behavioral analysis summary

## Baseline Analysis
Normal behavior patterns

## Anomaly Detection
Unusual activities identified

## Risk Assessment
Risk scoring and justification

## Behavioral Patterns
Trends and patterns analysis

## Recommendations
Monitoring and response actions
```

## Completion Criteria

- Report generated in correct format for specified type
- All required data collection completed
- Standardized structure maintained
- File saved to ./reports/ directory
- Source system updated (if applicable)
- Workflow documented with Mermaid diagram

## Expected Outputs

- **Report File**: Standardized markdown report in ./reports/
- **System Updates**: Comments/notes in source systems
- **Audit Trail**: Complete workflow documentation
- **Next Steps**: Clear recommendations for follow-up actions

## Usage Examples

### Generate Alert Report
```
Execute generate_security_reports.md with:
- REPORT_TYPE=alert
- PRIMARY_IDENTIFIER=CHR-2024-001
- ALERT_GROUP_IDENTIFIERS=group_123
```

### Generate Case Report  
```
Execute generate_security_reports.md with:
- REPORT_TYPE=case
- PRIMARY_IDENTIFIER=CASE-2024-456
- REPORT_AUDIENCE=executive
```

### Generate Detection Report
```
Execute generate_security_reports.md with:
- REPORT_TYPE=detection
- PRIMARY_IDENTIFIER=rule_malware_detection_v2
- REPORT_FILENAME_SUFFIX=quarterly_review
```

### Generate UEBA Report
```
Execute generate_security_reports.md with:
- REPORT_TYPE=ueba
- PRIMARY_IDENTIFIER=john.doe
- REPORT_AUDIENCE=technical
```