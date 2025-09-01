---
title: "Case Investigation - Unified Runbook" 
type: "runbook"
category: "security_operations"
status: "active"
consolidates: ["prioritize_and_investigate_a_case.md", "investigate_a_case_w_external_tools.md", "case_event_timeline_and_process_analysis.md"]
tags:
  - case_investigation
  - case_prioritization
  - timeline_analysis
  - process_analysis
  - external_tools
---

# Case Investigation - Unified Runbook

## Objective

Comprehensive case investigation framework covering case prioritization, investigation with external tools, and timeline/process analysis. This consolidated runbook provides end-to-end case investigation workflows from initial assessment through detailed forensic analysis.

## Investigation Phases

1. **Case Prioritization** - Risk-based case assessment and priority assignment
2. **Core Investigation** - Comprehensive case analysis with tool integration
3. **Timeline & Process Analysis** - Detailed forensic timeline reconstruction

## Universal Inputs

*   `${CASE_ID}`: Target case for investigation
*   `${INVESTIGATION_PHASE}`: Phase to execute (prioritize, investigate, timeline)
*   `${PRIORITY_FACTORS}`: Factors for prioritization (severity, impact, scope)
*   `${EXTERNAL_TOOLS}`: Additional tools beyond standard MCP stack
*   `${ANALYSIS_DEPTH}`: Investigation depth (standard, deep, forensic)
*   `${TIMELINE_SCOPE}`: Timeline analysis scope (alert_window, extended, comprehensive)

## Universal Tools

*   `secops-soar`: Case and alert management, workflow automation
*   `secops-mcp`: SIEM queries, entity lookup, event correlation
*   `gti-mcp`: Threat intelligence and IOC enrichment
*   External tools as specified in `${EXTERNAL_TOOLS}`
*   **Common Steps**: All enrichment and correlation workflows

## Unified Investigation Framework

### Phase 1: Case Prioritization (`INVESTIGATION_PHASE=prioritize`)

#### Step 1: Case Context Collection
1. **Get Case Details**: Use `secops-soar.get_case_full_details` 
2. **Extract Case Metadata**: Priority, severity, assignee, timestamps
3. **List Associated Alerts**: Get all alerts within case
4. **Identify Key Entities**: Extract users, hosts, IPs, hashes involved

#### Step 2: Risk Assessment Analysis
1. **Severity Analysis**:
   - Alert severity distribution
   - Asset criticality assessment  
   - Data sensitivity evaluation

2. **Impact Scope Assessment**:
   - Number of affected systems
   - User accounts involved
   - Network segments touched
   - Business processes impacted

3. **Time Criticality Analysis**:
   - Alert age and escalation timeline
   - Potential ongoing activity
   - Business operational impact

4. **Threat Intelligence Context**:
   - IOC reputation analysis
   - Known campaign associations
   - Threat actor attribution

#### Step 3: Priority Score Calculation
Generate priority score based on:
- **Severity Weight** (40%): Alert severities and asset criticality
- **Scope Weight** (30%): Breadth of impact across environment  
- **Time Weight** (20%): Age and urgency factors
- **Intelligence Weight** (10%): Threat intelligence context

**Priority Classification**:
- **Critical (90-100)**: Immediate investigation required
- **High (70-89)**: Investigation within 4 hours
- **Medium (50-69)**: Investigation within 24 hours  
- **Low (0-49)**: Investigation within 72 hours

### Phase 2: Core Investigation (`INVESTIGATION_PHASE=investigate`)

#### Step 1: Investigation Planning
1. **Review Prioritization Results** (if available)
2. **Define Investigation Scope** based on `${ANALYSIS_DEPTH}`
3. **Identify Required Tools** including `${EXTERNAL_TOOLS}`
4. **Plan Investigation Timeline**

#### Step 2: Entity Enrichment & Analysis
1. **Comprehensive Entity Enrichment**:
   - Execute `common_steps/enrich_ioc.md` for all key IOCs
   - Perform `common_steps/pivot_on_ioc_gti.md` for high-risk entities
   - Use `common_steps/correlate_ioc_with_alerts_cases.md` for relationship analysis

2. **External Tool Integration**:
   - Execute queries using tools specified in `${EXTERNAL_TOOLS}`
   - Cross-reference findings with internal data
   - Document external tool findings

#### Step 3: Alert & Event Analysis  
1. **Alert Deep Dive**:
   - Analyze each alert within case
   - Extract UDM events using `list_events_by_alert`
   - Identify attack patterns and TTPs

2. **Cross-Alert Correlation**:
   - Identify relationships between alerts
   - Timeline correlation analysis
   - Shared entity analysis

#### Step 4: Advanced SIEM Investigation
1. **Extended SIEM Searches**:
   - Broader time window analysis
   - Related activity discovery
   - Lateral movement detection

2. **Pattern Analysis**:
   - Behavioral pattern identification
   - Anomaly detection
   - Attack progression analysis

### Phase 3: Timeline & Process Analysis (`INVESTIGATION_PHASE=timeline`)

#### Step 1: Comprehensive Event Collection
1. **Gather All Case Events**:
   - Extract events from all alerts in case
   - Collect related SIEM events
   - Include external tool findings

2. **Event Categorization**:
   - Process execution events
   - Network communication events
   - File system activity
   - Authentication events
   - System configuration changes

#### Step 2: Timeline Reconstruction
1. **Chronological Ordering**:
   - Sort all events by timestamp
   - Handle timezone normalization
   - Identify event gaps and overlaps

2. **Timeline Visualization**:
   ```markdown
   ## Event Timeline Analysis
   
   | Timestamp | Event Type | Source | Description | Significance |
   |-----------|------------|--------|-------------|--------------|
   | 2024-01-01 09:15:23 | Process Exec | Host-A | powershell.exe -enc [base64] | Initial compromise |
   | 2024-01-01 09:16:45 | Network Conn | Host-A | Connection to 198.51.100.10:443 | C2 communication |
   ```

#### Step 3: Process Tree Analysis
1. **Process Relationship Mapping**:
   - Parent-child process relationships
   - Process execution chains
   - Privilege escalation sequences

2. **Process Behavior Analysis**:
   - Command line analysis
   - File access patterns
   - Network communications

3. **Attack Path Reconstruction**:
   - Initial access method
   - Persistence establishment
   - Lateral movement paths
   - Data exfiltration routes

### Phase 4: Integrated Analysis & Reporting

#### Comprehensive Case Analysis
1. **Multi-Phase Integration**:
   - Combine prioritization, investigation, and timeline findings
   - Cross-validate findings across analysis types
   - Identify gaps or inconsistencies

2. **Attack Narrative Development**:
   - Construct complete attack story
   - Identify attacker objectives
   - Assess attack sophistication

3. **Impact Assessment**:
   - Determine scope of compromise
   - Assess data exposure risk
   - Calculate business impact

#### Generate Unified Investigation Report

```markdown
# Comprehensive Case Investigation Report - ${CASE_ID}

## Executive Summary
[Key findings and business impact]

## Case Prioritization Results
### Priority Score: [X/100] - [Classification]
### Risk Factors:
- Severity: [Analysis]
- Scope: [Analysis] 
- Time Criticality: [Analysis]
- Threat Intelligence: [Analysis]

## Investigation Overview
- Investigation Depth: ${ANALYSIS_DEPTH}
- External Tools Used: ${EXTERNAL_TOOLS}
- Timeline Scope: ${TIMELINE_SCOPE}

## Key Findings
### High-Confidence Findings
[Confirmed threats and compromises]

### Medium-Confidence Findings
[Potential threats requiring validation]

## Entity Analysis
[Comprehensive entity enrichment results]

## Timeline Analysis
### Complete Event Timeline
[Chronological event sequence]

### Process Tree Analysis
[Process relationships and execution chains]

### Attack Path Reconstruction  
[Step-by-step attack progression]

## External Tool Findings
[Results from non-standard tools]

## Impact Assessment
### Systems Affected
[List of compromised/affected systems]

### Data Exposure Risk
[Assessment of data compromise]

### Business Impact
[Operational and business effects]

## Attack Attribution
### TTPs Identified
[MITRE ATT&CK mapping]

### Threat Intelligence Context
[Campaign/actor attribution if available]

## Recommendations
### Immediate Actions
[Urgent containment and response]

### Investigation Actions
[Additional investigation needs]

### Long-term Actions  
[Strategic improvements]

## Investigation Quality Metrics
- Investigation completion: X%
- Evidence collection: X items
- External tools utilized: X
- Timeline coverage: X hours
- IOCs enriched: X
```

## Investigation Phase Guidelines

### When to Use Prioritization:
- Multiple cases requiring triage
- Resource allocation decisions needed
- SLA compliance requirements
- Risk-based investigation planning

### When to Use Core Investigation:
- High-priority cases requiring deep analysis
- Complex multi-alert cases
- External tool integration needed
- Comprehensive threat assessment required

### When to Use Timeline Analysis:
- Forensic-level investigation needed
- Attack path reconstruction required
- Legal/compliance documentation needed
- Advanced threat analysis required

## Success Metrics

**Investigation Effectiveness:**
- Case resolution time
- Finding accuracy rate
- Evidence quality score
- Stakeholder satisfaction

**Process Efficiency:**
- Time per investigation phase
- Tool utilization effectiveness
- Investigation completeness
- Resource optimization

## Expected Outputs

- **Investigation Report**: Comprehensive case analysis
- **Priority Assessment**: Risk-based case prioritization
- **Timeline Documentation**: Detailed forensic timeline
- **IOC List**: Discovered indicators
- **Process Analysis**: Attack technique documentation
- **Recommendations**: Actionable response guidance

## Usage Examples

### Case Prioritization
```
Execute case_investigation.md with:
- CASE_ID=CASE-2024-001
- INVESTIGATION_PHASE=prioritize
- PRIORITY_FACTORS=severity,scope,time
```

### Comprehensive Investigation
```
Execute case_investigation.md with:  
- CASE_ID=CASE-2024-001
- INVESTIGATION_PHASE=investigate
- ANALYSIS_DEPTH=deep
- EXTERNAL_TOOLS=crowdstrike,carbonblack
```

### Timeline Analysis
```
Execute case_investigation.md with:
- CASE_ID=CASE-2024-001
- INVESTIGATION_PHASE=timeline
- TIMELINE_SCOPE=comprehensive
```

### Complete Investigation
```
Execute all phases sequentially:
1. INVESTIGATION_PHASE=prioritize
2. INVESTIGATION_PHASE=investigate  
3. INVESTIGATION_PHASE=timeline
```