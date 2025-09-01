---
title: "IOC Investigation - Unified Runbook"
type: "runbook"
category: "security_operations"
status: "active"
consolidates: ["basic_ioc_enrichment.md", "deep_dive_ioc_analysis.md", "investigate_a_gti_collection_id.md"]
tags:
  - ioc_enrichment
  - ioc_analysis
  - threat_intelligence
  - investigation
  - gti_collection
  - deep_dive
---

# IOC Investigation - Unified Runbook

## Objective

Comprehensive IOC investigation workflow supporting basic enrichment, deep-dive analysis, and GTI collection investigation. This consolidated runbook scales from Tier 1 basic enrichment to advanced threat intelligence analysis.

## Investigation Levels

1. **Basic Enrichment** - Initial IOC context gathering (Tier 1)
2. **Deep Dive Analysis** - Comprehensive IOC investigation (Tier 2/3)
3. **GTI Collection Investigation** - Advanced threat intelligence research

## Universal Inputs

*   `${IOC_VALUE}`: The IOC value to investigate
*   `${IOC_TYPE}`: Type of IOC (IP, Domain, Hash, URL, etc.)
*   `${INVESTIGATION_LEVEL}`: Level of investigation (basic, deep, gti_collection)
*   `${GTI_COLLECTION_ID}`: Required for GTI collection investigations
*   `${CASE_ID}`: Optional case ID for documentation
*   `${SIEM_SEARCH_HOURS}`: Lookback period (default: 96 hours)

## Universal Tools

*   `secops-mcp`: SIEM queries, entity lookup, IOC matching
*   `gti-mcp`: All GTI reporting and collection tools
*   `secops-soar`: Case management and documentation
*   **Common Steps**: `enrich_ioc.md`, `pivot_on_ioc_gti.md`, `correlate_ioc_with_alerts_cases.md`

## Unified Workflow

### Phase 1: Investigation Level Determination

Based on `${INVESTIGATION_LEVEL}`:

#### Basic Enrichment (`INVESTIGATION_LEVEL=basic`)
**Purpose**: Quick context for initial triage decisions
**Target Users**: Tier 1 SOC Analysts
**Scope**: Fundamental enrichment using GTI and SIEM lookups

#### Deep Dive Analysis (`INVESTIGATION_LEVEL=deep`)  
**Purpose**: Comprehensive threat analysis and attribution
**Target Users**: Tier 2/3 Analysts, Threat Hunters
**Scope**: Extended investigation with pivoting and campaign analysis

#### GTI Collection Investigation (`INVESTIGATION_LEVEL=gti_collection`)
**Purpose**: Research specific GTI threat collections
**Target Users**: CTI Researchers, Advanced Analysts
**Scope**: Collection-based threat intelligence analysis

### Phase 2: Core Investigation Workflow

#### Step 1: Initial IOC Validation & Context
1. **Validate IOC Format** - Ensure IOC value matches expected type
2. **Get Case Context** (if `${CASE_ID}` provided)
3. **Initialize Investigation Structure** 

#### Step 2: Primary Enrichment

**For All Investigation Levels:**
1. **Execute** `common_steps/enrich_ioc.md` with:
   - `IOC_VALUE=${IOC_VALUE}`
   - `IOC_TYPE=${IOC_TYPE}`
2. **Store Results**: GTI findings, SIEM context, IOC matches

**Basic Level - Stop Here**
- Document findings
- Generate basic enrichment report
- Provide triage recommendation

#### Step 3: Extended Analysis (Deep Dive & GTI Collection)

**Deep Dive Analysis:**
1. **Advanced GTI Pivoting**:
   - Execute `common_steps/pivot_on_ioc_gti.md`
   - Investigate related IOCs and campaigns
   - Analyze threat actor attribution

2. **Historical SIEM Analysis**:
   - Extended lookback searches (30-90 days)
   - Pattern analysis across time
   - Related host and user activity

3. **Cross-Reference Analysis**:
   - Execute `common_steps/correlate_ioc_with_alerts_cases.md`
   - Find related cases and campaigns
   - Assess organizational exposure

**GTI Collection Investigation:**
1. **Collection Analysis**:
   - Use `gti-mcp.get_collection_report` for `${GTI_COLLECTION_ID}`
   - Analyze collection metadata and associated IOCs
   - Research threat actor/campaign context

2. **Collection IOC Enumeration**:
   - Extract all IOCs from collection
   - Prioritize by confidence and recency
   - Cross-reference with organizational data

3. **Campaign Attribution**:
   - Research associated threat actors
   - Analyze TTPs and infrastructure
   - Assess relevance to organization

#### Step 4: Impact Assessment

**Basic Level**: Simple risk classification
**Deep Dive**: Comprehensive impact analysis including:
- Affected systems and users
- Potential data exposure
- Business process impact
- Containment requirements

**GTI Collection**: Organizational relevance assessment:
- Collection applicability to environment
- Threat actor targeting alignment
- Infrastructure overlap analysis

#### Step 5: Documentation & Reporting

**Generate Comprehensive Report** with investigation level-appropriate detail:

```markdown
# IOC Investigation Report - ${IOC_VALUE}

## Executive Summary
[Investigation level and key findings]

## IOC Details
- Value: ${IOC_VALUE}
- Type: ${IOC_TYPE}
- Investigation Level: ${INVESTIGATION_LEVEL}

## Primary Enrichment
[GTI and SIEM findings from common_steps/enrich_ioc.md]

## [Level-Specific Analysis]
[Extended analysis based on investigation level]

## Key Findings
[Critical discoveries and insights]

## Risk Assessment
[Risk classification and justification]

## Recommendations
[Next steps and containment actions]

## Investigation Timeline
[Chronological analysis of IOC activity]

## Related Indicators
[Connected IOCs and infrastructure]
```

### Phase 3: Follow-up Actions

#### Basic Level:
- Update case comments
- Provide triage recommendation
- Escalate if high-risk indicators found

#### Deep Dive Level:
- Create detailed threat profile
- Recommend detection rules
- Coordinate containment actions
- Brief stakeholders on findings

#### GTI Collection Level:
- Publish threat intelligence report
- Update organizational threat model
- Recommend hunting activities
- Share findings with threat community

## Investigation Level Guidelines

### When to Use Basic Enrichment:
- Initial alert triage
- Low-priority investigations
- Resource-constrained environments
- Quick IOC validation needed

### When to Use Deep Dive:
- High-priority incidents
- Suspected advanced threats
- Campaign attribution needed
- Organizational exposure assessment required

### When to Use GTI Collection:
- Threat intelligence research
- Campaign-specific investigations
- Strategic threat analysis
- Proactive hunting preparation

## Completion Criteria

**Universal:**
- IOC thoroughly analyzed at appropriate level
- Findings documented with evidence
- Risk assessment completed
- Report generated with recommendations

**Level-Specific:**
- **Basic**: Triage decision made, escalation path clear
- **Deep**: Comprehensive threat profile created, containment plan developed  
- **GTI Collection**: Threat collection fully researched, organizational relevance assessed

## Expected Outputs

- **Investigation Report**: Level-appropriate markdown report in ./reports/
- **Risk Classification**: Clear risk assessment with justification
- **Recommendations**: Actionable next steps
- **Evidence Package**: Supporting data and analysis
- **System Updates**: Case comments and documentation
- **Escalation Info**: Clear guidance for further investigation if needed

## Usage Examples

### Basic IOC Enrichment
```
Execute ioc_investigation.md with:
- IOC_VALUE=192.168.1.100
- IOC_TYPE="IP Address"  
- INVESTIGATION_LEVEL=basic
- CASE_ID=CHR-2024-001
```

### Deep Dive Analysis
```
Execute ioc_investigation.md with:
- IOC_VALUE=evil-domain.com
- IOC_TYPE="Domain"
- INVESTIGATION_LEVEL=deep
- SIEM_SEARCH_HOURS=720
```

### GTI Collection Investigation
```
Execute ioc_investigation.md with:
- GTI_COLLECTION_ID=22-00012345
- INVESTIGATION_LEVEL=gti_collection
- IOC_VALUE=[extracted from collection]
```