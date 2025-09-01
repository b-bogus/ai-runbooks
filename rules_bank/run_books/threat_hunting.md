---
title: "Threat Hunting - Unified Runbook"
type: "runbook"
category: "security_operations"
status: "active"
consolidates: ["advanced_threat_hunting.md", "apt_threat_hunt.md", "ioc_threat_hunt.md", "proactive_threat_hunting_based_on_gti_campaign_or_actor.md"]
tags:
  - threat_hunting
  - proactive_hunting
  - apt_hunting
  - ioc_hunting
  - campaign_hunting
  - hypothesis_driven
---

# Threat Hunting - Unified Runbook

## Objective

Comprehensive threat hunting framework supporting hypothesis-driven hunting, IOC-based hunting, APT-specific hunts, and campaign/actor-based proactive hunting. This consolidated runbook provides structured approaches for all threat hunting methodologies.

## Hunt Types Supported

1. **Hypothesis-Driven Hunting** - Advanced threat hunting based on assumptions
2. **IOC-Based Hunting** - Hunt for specific indicators of compromise  
3. **APT-Specific Hunting** - Target specific advanced persistent threat actors
4. **Campaign/Actor Hunting** - Proactive hunting based on GTI campaigns or actors

## Universal Inputs

*   `${HUNT_TYPE}`: Type of hunt (hypothesis, ioc, apt, campaign_actor)
*   `${HUNT_TARGET}`: Specific target (hypothesis, IOCs, APT name, GTI collection)
*   `${HUNT_SCOPE}`: Scope (endpoints, network, cloud, identity, all)
*   `${HUNT_TIMEFRAME}`: Time window for analysis (hours, days, weeks)
*   `${HUNT_CASE_ID}`: SOAR case for documentation
*   `${CONFIDENCE_THRESHOLD}`: Minimum confidence level for findings

## Universal Tools

*   `secops-mcp`: SIEM queries, event correlation, entity lookup
*   `gti-mcp`: Threat intelligence integration and collection analysis
*   `secops-soar`: Case management and documentation
*   **Common Steps**: `enrich_ioc.md`, `pivot_on_ioc_gti.md`, `correlate_ioc_with_alerts_cases.md`

## Unified Hunt Framework

### Phase 1: Hunt Planning & Preparation

#### Step 1: Hunt Type Determination
Based on `${HUNT_TYPE}`, initialize appropriate hunting methodology:

**Hypothesis-Driven (`HUNT_TYPE=hypothesis`)**:
- **Input**: `${HUNT_TARGET}` = hypothesis statement
- **Focus**: Test specific assumptions about threat presence
- **Approach**: Systematic evidence collection and validation

**IOC-Based (`HUNT_TYPE=ioc`)**:
- **Input**: `${HUNT_TARGET}` = list of IOCs
- **Focus**: Search for specific indicators across environment
- **Approach**: Comprehensive IOC matching and correlation

**APT-Specific (`HUNT_TYPE=apt`)**:
- **Input**: `${HUNT_TARGET}` = APT group name/identifier
- **Focus**: Hunt for APT-specific TTPs and infrastructure
- **Approach**: TTP-based behavioral hunting

**Campaign/Actor (`HUNT_TYPE=campaign_actor`)**:
- **Input**: `${HUNT_TARGET}` = GTI collection ID or actor name
- **Focus**: Proactive hunting based on current threat intelligence
- **Approach**: Intelligence-driven hunting with GTI integration

#### Step 2: Hunt Scoping & Resource Planning
1. **Define Hunt Boundaries** based on `${HUNT_SCOPE}`
2. **Establish Timeline** using `${HUNT_TIMEFRAME}`
3. **Set Success Criteria** and confidence thresholds
4. **Allocate Resources** and assign hunting team

### Phase 2: Hunt Execution (Type-Specific)

#### Hypothesis-Driven Hunting Workflow

1. **Hypothesis Refinement**:
   - Break down hypothesis into testable components
   - Define observable indicators that would support/refute hypothesis
   - Prioritize search strategies

2. **Evidence Collection**:
   - Design targeted SIEM queries for hypothesis validation
   - Search across multiple data sources (logs, network, endpoints)
   - Document all search attempts and results

3. **Hypothesis Testing**:
   - Analyze collected evidence against hypothesis
   - Identify supporting and contradicting evidence
   - Refine hypothesis based on findings

#### IOC-Based Hunting Workflow

1. **IOC Preparation**:
   - Validate and normalize IOC list
   - Categorize IOCs by type and confidence
   - Prioritize high-confidence indicators

2. **Comprehensive IOC Search**:
   - Execute `common_steps/enrich_ioc.md` for each IOC
   - Search historical SIEM data for IOC matches
   - Cross-reference with existing alerts and cases

3. **IOC Correlation Analysis**:
   - Execute `common_steps/correlate_ioc_with_alerts_cases.md`
   - Identify patterns and clusters in IOC activity
   - Analyze temporal relationships between IOCs

#### APT-Specific Hunting Workflow

1. **APT Profile Research**:
   - Research known TTPs for target APT group
   - Identify signature behaviors and tools
   - Map APT tactics to MITRE ATT&CK framework

2. **TTP-Based Hunting**:
   - Design queries targeting APT-specific techniques
   - Search for behavioral indicators across kill chain
   - Focus on persistence, lateral movement, and exfiltration patterns

3. **Infrastructure Hunting**:
   - Hunt for known APT infrastructure
   - Search for similar infrastructure patterns
   - Analyze C2 communication patterns

#### Campaign/Actor Hunting Workflow

1. **GTI Intelligence Gathering**:
   - If GTI collection provided, use `gti-mcp.get_collection_report`
   - Extract IOCs, TTPs, and infrastructure from intelligence
   - Analyze threat actor attribution and capabilities

2. **Proactive IOC Hunting**:
   - Execute `common_steps/pivot_on_ioc_gti.md` for campaign IOCs
   - Search for campaign-specific indicators
   - Identify potential organizational exposure

3. **Campaign Pattern Analysis**:
   - Analyze campaign timeline and evolution
   - Search for similar attack patterns in environment
   - Assess organizational risk from campaign

### Phase 3: Analysis & Correlation

#### Universal Analysis Steps (All Hunt Types)

1. **Finding Validation**:
   - Verify all potential positive findings
   - Eliminate false positives through analysis
   - Assess confidence level for each finding

2. **Entity Enrichment**:
   - Enrich all suspicious entities found during hunt
   - Perform deep analysis on high-confidence findings
   - Document entity relationships and timelines

3. **Impact Assessment**:
   - Assess scope of potential compromise
   - Identify affected systems and data
   - Evaluate business impact

4. **Threat Classification**:
   - Classify findings by threat severity
   - Assign confidence scores to detections
   - Prioritize response actions

### Phase 4: Documentation & Reporting

#### Generate Comprehensive Hunt Report

```markdown
# Threat Hunt Report - ${HUNT_TYPE} 

## Executive Summary
[Hunt results and key findings]

## Hunt Overview
- Hunt Type: ${HUNT_TYPE}
- Target: ${HUNT_TARGET}  
- Scope: ${HUNT_SCOPE}
- Timeframe: ${HUNT_TIMEFRAME}
- Case ID: ${HUNT_CASE_ID}

## Hunt Hypothesis/Objective
[Specific hunting goal and approach]

## Methodology
[Detailed hunting process and techniques used]

## Key Findings
### High-Confidence Findings
[Confirmed threats and indicators]

### Medium-Confidence Findings  
[Potential threats requiring investigation]

### Negative Findings
[Areas searched with no threats found]

## IOCs Discovered
[New indicators identified during hunt]

## Timeline Analysis
[Temporal analysis of discovered activity]

## Impact Assessment
[Organizational impact and exposure]

## Recommendations
### Immediate Actions
[Urgent response requirements]

### Long-term Actions  
[Strategic improvements and hunting opportunities]

## Hunt Metrics
- Data sources searched: X
- Queries executed: X  
- Findings generated: X
- False positives: X
- Time invested: X hours

## Lessons Learned
[Hunt process improvements and insights]

## Follow-up Actions
[Required next steps and responsible parties]
```

### Phase 5: Hunt Conclusion & Follow-up

1. **Threat Validation**:
   - Validate all high-confidence findings
   - Escalate confirmed threats to incident response
   - Document threat intelligence for future hunts

2. **Hunt Metrics Collection**:
   - Record hunt effectiveness metrics
   - Analyze search coverage and gaps
   - Document lessons learned

3. **Follow-up Planning**:
   - Plan follow-up hunts based on findings
   - Recommend detection rule creation
   - Schedule regular hunting cycles

## Hunt Type Guidelines

### When to Use Hypothesis-Driven Hunting:
- Testing specific threat assumptions
- Following up on partial indicators
- Researching new attack techniques
- Investigating suspicious network patterns

### When to Use IOC-Based Hunting:
- Following threat intelligence reports
- Hunting for specific malware families
- Validating detection rule gaps
- Post-incident hunting activities

### When to Use APT-Specific Hunting:  
- Suspected advanced threat presence
- Industry-targeted threat actors
- Post-breach assessment activities
- Strategic threat landscape analysis

### When to Use Campaign/Actor Hunting:
- New threat intelligence releases
- Industry threat advisories
- Proactive defense posture
- Threat landscape monitoring

## Success Metrics

**Hunt Effectiveness:**
- Threat detection rate
- False positive ratio
- Coverage percentage
- Time to detection

**Organizational Impact:**
- Incidents prevented
- Risk reduction achieved  
- Security posture improvement
- Detection capability enhancement

## Expected Outputs

- **Hunt Report**: Comprehensive markdown report in ./reports/
- **IOC List**: Discovered indicators for threat intelligence
- **Detection Rules**: Recommended rules based on findings  
- **Incident Cases**: Escalated threats requiring response
- **Hunt Metrics**: Performance and effectiveness data
- **Lessons Learned**: Process improvements and insights

## Usage Examples

### Hypothesis-Driven Hunt
```
Execute threat_hunting.md with:
- HUNT_TYPE=hypothesis
- HUNT_TARGET="Lateral movement via WMI on weekends"
- HUNT_SCOPE=endpoints
- HUNT_TIMEFRAME=30d
```

### IOC-Based Hunt  
```
Execute threat_hunting.md with:
- HUNT_TYPE=ioc
- HUNT_TARGET=[list of campaign IOCs]
- HUNT_SCOPE=all
- HUNT_TIMEFRAME=90d
```

### APT Hunt
```
Execute threat_hunting.md with:
- HUNT_TYPE=apt
- HUNT_TARGET="APT29"
- HUNT_SCOPE=network,endpoints
- HUNT_TIMEFRAME=6months
```

### Campaign Hunt
```
Execute threat_hunting.md with:  
- HUNT_TYPE=campaign_actor
- HUNT_TARGET="GTI-COLLECTION-12345"
- HUNT_SCOPE=all
- HUNT_TIMEFRAME=60d
```