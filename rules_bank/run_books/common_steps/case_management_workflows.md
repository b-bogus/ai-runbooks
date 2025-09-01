---
title: "Case Management Workflows - Unified Common Steps"
type: "runbook"
category: "security_operations"
status: "active"
consolidates: ["check_duplicate_cases.md", "find_relevant_soar_case.md", "document_in_soar.md", "close_soar_artifact.md"]
tags:
  - common_step
  - case_management
  - soar_operations
  - duplicate_detection
  - documentation
  - unified_workflows
---

# Case Management Workflows - Unified Common Steps

## Overview

Consolidated case management workflows combining duplicate detection, case discovery, documentation, and closure operations into a unified, parameter-driven framework. This eliminates redundancy across four separate common steps while providing comprehensive case lifecycle management.

## Supported Workflows

1. **Duplicate Detection** - Identify similar or duplicate cases
2. **Case Discovery** - Find relevant cases based on search criteria
3. **Documentation** - Add comments and updates to SOAR cases
4. **Case Closure** - Close cases and artifacts with proper categorization

## Universal Inputs

*   `${WORKFLOW_TYPE}`: Type of workflow (`duplicate`, `discovery`, `document`, `close`)
*   `${CASE_ID}`: Target case ID (required for document/close workflows)
*   `${SEARCH_TERMS}`: Search criteria for duplicate/discovery workflows
*   `${CASE_STATUS_FILTER}`: Status filter for searches (`Opened`, `Closed`, `All`)
*   `${SIMILARITY_THRESHOLD}`: Duplicate detection sensitivity (0.1-1.0)
*   `${DOCUMENTATION_CONTENT}`: Comment or documentation content
*   `${CLOSURE_REASON}`: Reason for closure (e.g., `NOT_MALICIOUS`, `RESOLVED`)
*   `${ROOT_CAUSE}`: Root cause classification for closed cases

## Universal Tools

*   `secops-soar`: Complete SOAR platform integration
   - Case management and search capabilities
   - Documentation and commenting functions
   - Artifact and case closure operations

## Unified Workflow Framework

### Phase 1: Workflow Selection & Preparation

Based on `${WORKFLOW_TYPE}`, execute appropriate case management pathway:

#### Duplicate Detection (`WORKFLOW_TYPE=duplicate`)
**Purpose**: Identify similar cases to prevent duplicate work
**Scope**: Similarity analysis based on entities, timeline, and context
**Duration**: 30-90 seconds
**Output**: List of similar cases with confidence scores

#### Case Discovery (`WORKFLOW_TYPE=discovery`)
**Purpose**: Find relevant cases based on specific search criteria
**Scope**: Multi-field search across case metadata and content
**Duration**: 30-60 seconds  
**Output**: Filtered case list with relevance ranking

#### Documentation (`WORKFLOW_TYPE=document`)
**Purpose**: Add structured comments and updates to cases
**Scope**: Comment addition with metadata and timestamp
**Duration**: 5-10 seconds
**Output**: Documentation confirmation and case update

#### Case Closure (`WORKFLOW_TYPE=close`)
**Purpose**: Close cases and artifacts with proper categorization
**Scope**: Status update, reason/cause assignment, final documentation
**Duration**: 10-15 seconds
**Output**: Closure confirmation with audit trail

### Phase 2: Core Workflow Execution

#### Duplicate Detection Workflow

1. **Case Context Analysis**:
   ```
   - Extract: Current case entities, timeline, alert types
   - Normalize: Entity formats for comparison
   - Generate: Search signature for similarity matching
   ```

2. **Similarity Search Execution**:
   ```
   - Execute: secops-soar.siemplify_get_similar_cases(case_id=CASE_ID)
   - Apply: SIMILARITY_THRESHOLD filtering
   - Rank: Results by confidence and recency
   ```

3. **Duplicate Assessment**:
   ```
   - Compare: Entity overlap percentage
   - Analyze: Timeline proximity (within 24-48 hours)
   - Evaluate: Alert type and severity alignment
   - Score: Overall similarity confidence
   ```

**Output Structure**:
```json
{
  "similar_cases": [
    {
      "case_id": "CASE-001",
      "similarity_score": 0.85,
      "entity_overlap": 0.90,
      "timeline_proximity": "2_hours",
      "recommendation": "likely_duplicate"
    }
  ],
  "analysis_summary": {
    "total_candidates": 5,
    "high_confidence_matches": 2,
    "recommended_action": "review_for_closure"
  }
}
```

#### Case Discovery Workflow

1. **Search Query Construction**:
   ```
   Based on SEARCH_TERMS and CASE_STATUS_FILTER:
   - Entity-based: Search for specific IOCs, users, hosts
   - Keyword-based: Search case titles and descriptions
   - Timeline-based: Search within date ranges
   - Combined: Multi-criteria search with ranking
   ```

2. **Advanced Search Execution**:
   ```
   - Execute: secops-soar.list_cases() with filters
   - Apply: Entity filters, status filters, date ranges
   - Rank: Results by relevance and recency
   ```

3. **Relevance Assessment**:
   ```
   - Score: Entity match percentage
   - Weight: Case priority and severity
   - Filter: Remove low-relevance results
   - Organize: By confidence and business impact
   ```

**Output Structure**:
```json
{
  "discovered_cases": [
    {
      "case_id": "CASE-123", 
      "case_name": "Suspicious Login Investigation",
      "relevance_score": 0.92,
      "entity_matches": ["192.168.1.100", "john.doe"],
      "case_priority": "High",
      "last_updated": "2024-01-15T10:30:00Z"
    }
  ],
  "search_summary": {
    "total_results": 15,
    "high_relevance": 3,
    "medium_relevance": 7,
    "search_criteria": "IP address and user analysis"
  }
}
```

#### Documentation Workflow

1. **Content Preparation**:
   ```
   - Validate: DOCUMENTATION_CONTENT format and length
   - Enrich: Add timestamp and analyst metadata
   - Structure: Format for SOAR platform requirements
   ```

2. **Documentation Execution**:
   ```
   - Execute: secops-soar.post_case_comment(
       case_id=CASE_ID,
       comment=DOCUMENTATION_CONTENT
     )
   - Verify: Comment addition successful
   - Log: Documentation action in audit trail
   ```

3. **Quality Verification**:
   ```
   - Confirm: Comment visible in case timeline
   - Validate: Formatting and content integrity
   - Update: Case modification timestamp
   ```

**Output Structure**:
```json
{
  "documentation_result": {
    "status": "success",
    "comment_id": "COMMENT-456",
    "case_id": "CASE-123",
    "timestamp": "2024-01-15T14:25:00Z",
    "analyst": "current_user"
  },
  "case_update": {
    "last_modified": "2024-01-15T14:25:00Z",
    "comment_count": 8,
    "case_status": "In Progress"
  }
}
```

#### Case Closure Workflow

1. **Pre-Closure Validation**:
   ```
   - Verify: Case is in appropriate state for closure
   - Validate: CLOSURE_REASON and ROOT_CAUSE are valid
   - Check: Required documentation is complete
   ```

2. **Closure Execution**:
   ```
   For Cases:
   - Execute: secops-soar.siemplify_close_case(
       case_id=CASE_ID,
       reason=CLOSURE_REASON,
       root_cause=ROOT_CAUSE,
       comment=final_comment
     )
     
   For Alerts:
   - Execute: secops-soar.siemplify_close_alert(
       case_id=CASE_ID,
       alert_id=ALERT_ID,
       reason=CLOSURE_REASON,
       root_cause=ROOT_CAUSE
     )
   ```

3. **Closure Verification**:
   ```
   - Confirm: Status updated to "Closed"
   - Verify: Reason and root cause recorded
   - Validate: Final documentation added
   - Log: Closure action in audit trail
   ```

**Output Structure**:
```json
{
  "closure_result": {
    "status": "success",
    "case_id": "CASE-123",
    "closure_reason": "NOT_MALICIOUS",
    "root_cause": "False Positive",
    "closed_timestamp": "2024-01-15T16:45:00Z",
    "closed_by": "current_analyst"
  },
  "audit_trail": {
    "action": "case_closed",
    "previous_status": "In Progress", 
    "new_status": "Closed",
    "documentation_added": true
  }
}
```

### Phase 3: Integrated Workflow Chains

Common workflow combinations for efficient case management:

1. **Duplicate Check → Close** (Efficient Triage):
   ```
   1. Execute duplicate detection
   2. If high-confidence duplicate found
   3. Execute documentation (duplicate reason)
   4. Execute closure with NOT_MALICIOUS/Duplicate
   ```

2. **Discovery → Document** (Context Building):
   ```
   1. Execute case discovery for related cases
   2. Analyze findings for investigation context
   3. Execute documentation with related case insights
   ```

3. **Document → Close** (Investigation Completion):
   ```
   1. Execute documentation with final findings
   2. Execute closure with appropriate categorization
   ```

## Execution Examples

### Duplicate Detection
```bash
Execute case_management_workflows.md with:
- WORKFLOW_TYPE="duplicate"
- CASE_ID="CASE-2024-001"
- SIMILARITY_THRESHOLD=0.80
```

### Case Discovery
```bash
Execute case_management_workflows.md with:
- WORKFLOW_TYPE="discovery"
- SEARCH_TERMS=["192.168.1.100", "suspicious_login"]
- CASE_STATUS_FILTER="Opened"
```

### Documentation
```bash
Execute case_management_workflows.md with:
- WORKFLOW_TYPE="document"
- CASE_ID="CASE-2024-001"
- DOCUMENTATION_CONTENT="Completed IOC enrichment analysis. No malicious indicators found."
```

### Case Closure
```bash
Execute case_management_workflows.md with:
- WORKFLOW_TYPE="close"
- CASE_ID="CASE-2024-001"
- CLOSURE_REASON="NOT_MALICIOUS"
- ROOT_CAUSE="False Positive"
```

### Chained Workflow (Duplicate Triage)
```bash
# Efficient duplicate handling
1. WORKFLOW_TYPE="duplicate" → Check for similar cases
2. WORKFLOW_TYPE="document" → Document duplicate reasoning  
3. WORKFLOW_TYPE="close" → Close as duplicate
```

## Integration with Parent Runbooks

This consolidated workflow integrates with:
- `triage_alerts.md` - Duplicate checking and case closure
- `case_investigation.md` - Case discovery and documentation
- `generate_security_reports.md` - Case correlation analysis
- All investigation runbooks - Documentation and closure operations

## Performance Optimization

**Caching Strategy**: Search results cached within session
**Parallel Operations**: Independent SOAR calls executed concurrently  
**Smart Filtering**: Results filtered by relevance thresholds
**Batch Operations**: Multiple comments/closures batched where possible

## Quality Assurance

**Input Validation**: All parameters validated before execution
**Permission Checking**: Verify analyst permissions for operations
**Audit Logging**: All actions logged with timestamp and user
**Error Handling**: Graceful failure with clear error messages

---

*This unified workflow eliminates redundancy across four separate common steps while providing comprehensive case lifecycle management through intelligent parameter-driven execution and integrated workflow chains.*