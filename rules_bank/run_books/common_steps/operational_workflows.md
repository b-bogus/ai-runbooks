---
title: "Operational Workflows - Unified Common Steps"
type: "runbook"
category: "security_operations"
status: "active"
consolidates: ["confirm_action.md", "generate_report_file.md", "todo_list_generation.md"]
tags:
  - common_step
  - operational_procedures
  - report_generation
  - task_management
  - confirmation_protocols
  - unified_workflows
---

# Operational Workflows - Unified Common Steps

## Overview

Consolidated operational workflows combining action confirmation, report generation, and task management into a unified, parameter-driven framework. This eliminates redundancy across three separate common steps while providing comprehensive operational support capabilities.

## Supported Workflows

1. **Action Confirmation** - Interactive confirmation for critical operations
2. **Report Generation** - Automated security report creation and formatting
3. **Task Management** - Dynamic todo list generation and progress tracking

## Universal Inputs

*   `${WORKFLOW_TYPE}`: Type of workflow (`confirm`, `report`, `tasks`)
*   `${ACTION_DESCRIPTION}`: Description of action requiring confirmation
*   `${CONFIRMATION_LEVEL}`: Confirmation rigor (`standard`, `elevated`, `critical`)
*   `${REPORT_CONTENT}`: Structured report content and findings
*   `${REPORT_TYPE}`: Report format (`markdown`, `json`, `executive`, `technical`)
*   `${TASK_CONTEXT}`: Context for task generation (runbook execution, investigation phase)
*   `${TASK_COMPLEXITY}`: Task complexity level (`simple`, `moderate`, `complex`)

## Universal Tools

*   **File Operations**: Report writing and task persistence
*   **Interactive Confirmation**: User interaction and decision capture
*   **Template Processing**: Dynamic content generation and formatting

## Unified Workflow Framework

### Phase 1: Workflow Selection & Preparation

Based on `${WORKFLOW_TYPE}`, execute appropriate operational pathway:

#### Action Confirmation (`WORKFLOW_TYPE=confirm`)
**Purpose**: Ensure proper authorization before executing critical operations
**Scope**: Interactive confirmation with risk assessment and documentation
**Duration**: 15-30 seconds (user dependent)
**Output**: Confirmation status and execution authorization

#### Report Generation (`WORKFLOW_TYPE=report`)
**Purpose**: Generate formatted reports from structured findings
**Scope**: Template processing, content formatting, file creation
**Duration**: 5-15 seconds
**Output**: Generated report file with standardized structure

#### Task Management (`WORKFLOW_TYPE=tasks`)
**Purpose**: Generate and track tasks for complex operations
**Scope**: Dynamic task creation, progress tracking, completion management
**Duration**: 10-20 seconds
**Output**: Structured task list with tracking capabilities

### Phase 2: Core Workflow Execution

#### Action Confirmation Workflow

1. **Risk Assessment**:
   ```
   Based on CONFIRMATION_LEVEL:
   - Standard: Simple yes/no confirmation
   - Elevated: Risk explanation + confirmation
   - Critical: Multi-step verification + justification
   ```

2. **Interactive Confirmation**:
   ```
   Standard Level:
   - Display: Action description and impact
   - Request: Simple confirmation (Y/N)
   - Validate: User response
   
   Elevated Level:
   - Display: Detailed risk assessment
   - Request: Confirmation with reasoning
   - Validate: Understanding confirmation
   
   Critical Level:
   - Display: Comprehensive impact analysis
   - Request: Multi-factor confirmation
   - Validate: Executive approval (if required)
   ```

3. **Decision Documentation**:
   ```
   - Record: User decision and timestamp
   - Log: Confirmation level and context
   - Store: Justification and approval chain
   - Audit: Decision trail for compliance
   ```

**Output Structure**:
```json
{
  "confirmation_result": {
    "authorized": true,
    "confirmation_level": "elevated",
    "timestamp": "2024-01-15T10:30:00Z",
    "user": "analyst_id",
    "justification": "Confirmed malicious activity requiring immediate containment"
  },
  "risk_assessment": {
    "impact_level": "high",
    "affected_systems": ["production_db", "web_servers"],
    "business_impact": "moderate_disruption",
    "recovery_time": "2-4_hours"
  }
}
```

#### Report Generation Workflow

1. **Content Processing**:
   ```
   - Parse: REPORT_CONTENT structure and formatting
   - Validate: Required sections and data completeness
   - Enrich: Add metadata, timestamps, and identifiers
   ```

2. **Template Application**:
   ```
   Based on REPORT_TYPE:
   - Markdown: Apply markdown formatting and structure
   - JSON: Generate structured JSON output
   - Executive: Create executive summary format
   - Technical: Generate technical detail format
   ```

3. **File Generation**:
   ```
   - Generate: Unique report filename with timestamp
   - Create: Report file in ./reports/ directory
   - Validate: File creation and content integrity
   - Return: File path and generation confirmation
   ```

**Template Examples**:

**Markdown Template**:
```markdown
# Security Report - ${REPORT_TITLE}

## Metadata
- Report Type: ${REPORT_TYPE}
- Generated: ${TIMESTAMP}
- Analyst: ${ANALYST_ID}
- Case ID: ${CASE_ID}

## Executive Summary
${EXECUTIVE_SUMMARY}

## Detailed Findings
${DETAILED_FINDINGS}

## Recommendations
${RECOMMENDATIONS}

## Workflow Documentation
${MERMAID_DIAGRAM}
```

**Executive Template**:
```markdown
# Executive Brief - ${INCIDENT_TITLE}

**Status**: ${STATUS}
**Impact**: ${BUSINESS_IMPACT}
**Risk Level**: ${RISK_CLASSIFICATION}

## Summary
${EXECUTIVE_SUMMARY}

## Business Impact
${IMPACT_ANALYSIS}

## Immediate Actions Required
${ACTION_ITEMS}

## Timeline
${INCIDENT_TIMELINE}
```

#### Task Management Workflow

1. **Task Analysis & Generation**:
   ```
   Based on TASK_CONTEXT and TASK_COMPLEXITY:
   - Analyze: Current operation phase and requirements
   - Decompose: Complex operations into manageable tasks
   - Prioritize: Tasks by criticality and dependencies
   - Structure: With clear completion criteria
   ```

2. **Dynamic Task Creation**:
   ```
   Simple Complexity:
   - Generate: 3-5 sequential tasks
   - Structure: Linear execution path
   - Tracking: Basic progress indicators
   
   Moderate Complexity:
   - Generate: 5-10 tasks with dependencies
   - Structure: Branching execution paths
   - Tracking: Progress with quality gates
   
   Complex Complexity:
   - Generate: 10+ tasks with complex dependencies
   - Structure: Multi-phase execution
   - Tracking: Advanced progress monitoring
   ```

3. **Progress Tracking Implementation**:
   ```
   - Initialize: Task status tracking structure
   - Define: Completion criteria and validation
   - Implement: Progress update mechanisms
   - Monitor: Task completion and quality
   ```

**Task Structure Examples**:

**Investigation Tasks (Moderate Complexity)**:
```json
{
  "task_framework": {
    "context": "malware_investigation",
    "complexity": "moderate", 
    "total_tasks": 7,
    "estimated_duration": "2-4 hours"
  },
  "task_list": [
    {
      "id": 1,
      "task": "Collect initial malware sample and metadata",
      "status": "pending",
      "dependencies": [],
      "estimated_time": "15 minutes",
      "completion_criteria": "Sample isolated and basic metadata extracted"
    },
    {
      "id": 2,
      "task": "Perform static analysis of malware characteristics",
      "status": "pending", 
      "dependencies": [1],
      "estimated_time": "30 minutes",
      "completion_criteria": "File properties, strings, and imports analyzed"
    }
  ]
}
```

**Threat Hunt Tasks (Complex)**:
```json
{
  "task_framework": {
    "context": "apt_threat_hunt",
    "complexity": "complex",
    "total_tasks": 12,
    "estimated_duration": "6-8 hours"
  },
  "phases": [
    {
      "phase": "preparation",
      "tasks": [1, 2, 3],
      "parallel_execution": true
    },
    {
      "phase": "execution", 
      "tasks": [4, 5, 6, 7, 8, 9],
      "dependencies": ["preparation"],
      "parallel_execution": false
    },
    {
      "phase": "analysis",
      "tasks": [10, 11, 12],
      "dependencies": ["execution"]
    }
  ]
}
```

### Phase 3: Integrated Workflow Orchestration

Common workflow combinations for comprehensive operations:

1. **Confirm → Report** (Authorized Documentation):
   ```
   1. Execute confirmation for critical findings
   2. Upon authorization, generate detailed report
   3. Include confirmation details in report metadata
   ```

2. **Tasks → Report** (Progress Documentation):
   ```
   1. Generate tasks for complex investigation
   2. Track progress through task completion  
   3. Generate final report with task completion summary
   ```

3. **Confirm → Tasks → Report** (Complete Operation Cycle):
   ```
   1. Confirm authorization for complex operation
   2. Generate structured task framework
   3. Execute tasks with progress tracking
   4. Generate comprehensive final report
   ```

## Execution Examples

### Action Confirmation
```bash
Execute operational_workflows.md with:
- WORKFLOW_TYPE="confirm"
- ACTION_DESCRIPTION="Isolate suspected compromised host from network"
- CONFIRMATION_LEVEL="elevated"
```

### Report Generation
```bash
Execute operational_workflows.md with:
- WORKFLOW_TYPE="report"
- REPORT_CONTENT="{structured_findings}"
- REPORT_TYPE="executive"
```

### Task Management
```bash
Execute operational_workflows.md with:
- WORKFLOW_TYPE="tasks"
- TASK_CONTEXT="advanced_threat_investigation"
- TASK_COMPLEXITY="complex"
```

### Integrated Workflow
```bash
# Complete operational cycle
1. WORKFLOW_TYPE="confirm" → Authorize complex investigation
2. WORKFLOW_TYPE="tasks" → Generate investigation framework
3. [Execute tasks with progress tracking]
4. WORKFLOW_TYPE="report" → Generate final documentation
```

## Integration with Parent Runbooks

This consolidated workflow integrates with:
- **All Investigation Runbooks**: Confirmation and task management
- **All Hunting Runbooks**: Task generation and progress tracking
- **All Reporting Workflows**: Report generation and formatting
- **Incident Response Plans**: Confirmation protocols and documentation

## Performance Optimization

**Template Caching**: Report templates cached for rapid generation
**Async Processing**: File operations executed asynchronously
**Smart Defaults**: Intelligent parameter defaulting based on context
**Resource Management**: Efficient file handling and cleanup

## Quality Assurance

**Input Validation**: All content validated for completeness and format
**Template Integrity**: Report template validation and error handling
**Audit Compliance**: All confirmations and decisions logged
**File Verification**: Generated files validated for integrity

---

*This unified workflow eliminates redundancy across three separate common steps while providing comprehensive operational support through intelligent parameter-driven execution and integrated workflow orchestration.*