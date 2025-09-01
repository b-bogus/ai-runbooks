---
title: "IOC Analysis Workflows - Unified Common Steps"
type: "runbook"
category: "security_operations"
status: "active"
consolidates: ["enrich_ioc.md", "pivot_on_ioc_gti.md", "correlate_ioc_with_alerts_cases.md"]
tags:
  - common_step
  - ioc_enrichment
  - threat_intelligence
  - correlation_analysis
  - unified_workflows
---

# IOC Analysis Workflows - Unified Common Steps

## Overview

Consolidated IOC analysis workflows combining enrichment, GTI pivoting, and correlation analysis into a unified, parameter-driven framework. This eliminates redundancy across three separate common steps while providing enhanced analytical capabilities.

## Supported Workflows

1. **Basic Enrichment** - Standard GTI + SIEM IOC lookup
2. **Advanced Pivoting** - GTI relationship exploration and expansion
3. **Correlation Analysis** - Cross-reference with organizational alerts and cases

## Universal Inputs

*   `${IOC_VALUE}`: The IOC value to analyze
*   `${IOC_TYPE}`: Type of IOC (IP, Domain, Hash, URL, etc.)
*   `${ANALYSIS_TYPE}`: Workflow type (`enrich`, `pivot`, `correlate`)
*   `${PIVOT_DEPTH}`: For pivoting - depth of relationship exploration (1-3)
*   `${CORRELATION_SCOPE}`: For correlation - scope of case search (`recent`, `extended`, `comprehensive`)
*   `${LOOKBACK_DAYS}`: Historical search window (default: 30)

## Universal Tools

*   `gti-mcp`: All GTI reporting and relationship tools
*   `secops-mcp`: SIEM entity lookup and IOC matching
*   `secops-soar`: Case correlation and alert analysis

## Unified Workflow Framework

### Phase 1: Workflow Selection & Preparation

Based on `${ANALYSIS_TYPE}`, execute appropriate analytical pathway:

#### Basic Enrichment (`ANALYSIS_TYPE=enrich`)
**Purpose**: Standard IOC context gathering for decision support
**Scope**: GTI reputation + SIEM entity data + recent IOC matches
**Duration**: 30-60 seconds
**Output**: Structured enrichment summary

#### Advanced Pivoting (`ANALYSIS_TYPE=pivot`)  
**Purpose**: Discover related IOCs and threat infrastructure
**Scope**: GTI relationship exploration + campaign analysis
**Duration**: 2-5 minutes
**Output**: Related entity collection with relationship mapping

#### Correlation Analysis (`ANALYSIS_TYPE=correlate`)
**Purpose**: Cross-reference IOC with organizational security events
**Scope**: Historical case search + alert correlation + pattern analysis
**Duration**: 1-3 minutes
**Output**: Organizational exposure assessment

### Phase 2: Core Analysis Execution

#### Enrichment Workflow

1. **GTI Primary Analysis**:
   ```
   Based on IOC_TYPE, execute:
   - IP Address: gti-mcp.get_ip_address_report(ip=IOC_VALUE)
   - Domain: gti-mcp.get_domain_report(domain=IOC_VALUE)
   - File Hash: gti-mcp.get_file_report(hash=IOC_VALUE)
   - URL: gti-mcp.get_url_report(url=IOC_VALUE)
   ```

2. **SIEM Entity Context**:
   ```
   - Execute: secops-mcp.lookup_entity(entity_value=IOC_VALUE)
   - Extract: First seen, last seen, event count, related systems
   ```

3. **Recent IOC Matches**:
   ```
   - Execute: secops-mcp.get_ioc_matches(ioc=IOC_VALUE)
   - Analyze: Match frequency, affected systems, event patterns
   ```

**Output Structure**:
```json
{
  "gti_analysis": {
    "reputation_score": "X/100",
    "threat_types": ["malware", "c2"],
    "first_submission": "YYYY-MM-DD",
    "community_score": "X/100"
  },
  "siem_context": {
    "first_seen": "YYYY-MM-DD HH:MM",
    "last_seen": "YYYY-MM-DD HH:MM", 
    "event_count": N,
    "affected_systems": ["host1", "host2"]
  },
  "ioc_matches": {
    "match_count": N,
    "recent_matches": "last_7_days",
    "match_types": ["dns", "http", "file"]
  }
}
```

#### Pivoting Workflow

1. **Relationship Discovery**:
   ```
   Based on IOC_TYPE and PIVOT_DEPTH:
   - Level 1: Direct relationships (same campaign/family)
   - Level 2: Extended relationships (related infrastructure)
   - Level 3: Comprehensive mapping (full campaign network)
   ```

2. **Related Entity Extraction**:
   ```
   - Execute: gti-mcp.get_entities_related_to_a_[type](entity=IOC_VALUE)
   - Categories: communicating_files, contacted_domains, contacted_ips
   - Filter: By confidence score and recency
   ```

3. **Campaign Attribution**:
   ```
   - Analyze: Common threat actor indicators
   - Map: Infrastructure overlap patterns
   - Assess: Campaign timeline and evolution
   ```

**Output Structure**:
```json
{
  "direct_relationships": {
    "related_domains": ["domain1.com", "domain2.com"],
    "related_ips": ["1.1.1.1", "2.2.2.2"],
    "related_files": ["hash1", "hash2"]
  },
  "campaign_context": {
    "threat_actor": "APT-X",
    "campaign_name": "Operation-Y", 
    "infrastructure_overlap": "high",
    "timeline_span": "2024-01 to 2024-06"
  },
  "confidence_assessment": {
    "relationship_confidence": "high",
    "attribution_confidence": "medium",
    "infrastructure_confidence": "high"
  }
}
```

#### Correlation Workflow

1. **Historical Case Search**:
   ```
   Based on CORRELATION_SCOPE:
   - Recent: 30 days of case data
   - Extended: 90 days of case data  
   - Comprehensive: 365 days of case data
   ```

2. **Alert Pattern Analysis**:
   ```
   - Execute: secops-soar.list_cases() with entity filters
   - Filter: Cases containing IOC_VALUE or related entities
   - Analyze: Frequency patterns and organizational impact
   ```

3. **Cross-Reference Analysis**:
   ```
   - Map: IOC appearance across multiple cases
   - Identify: Recurring attack patterns
   - Assess: Organizational exposure and risk
   ```

**Output Structure**:
```json
{
  "case_correlations": {
    "total_related_cases": N,
    "case_ids": ["CASE-001", "CASE-002"],
    "first_occurrence": "YYYY-MM-DD",
    "most_recent": "YYYY-MM-DD"
  },
  "pattern_analysis": {
    "attack_patterns": ["lateral_movement", "data_exfil"],
    "affected_systems_count": N,
    "organizational_scope": "department_X"
  },
  "risk_assessment": {
    "exposure_level": "medium",
    "recurrence_risk": "high",
    "business_impact": "moderate"
  }
}
```

### Phase 3: Integrated Analysis (Multi-Workflow)

For complex investigations, workflows can be chained:

1. **Enrich → Pivot** (Common Pattern):
   - Start with basic enrichment
   - If high-risk IOC found, execute pivoting
   - Combine results for comprehensive threat profile

2. **Enrich → Correlate** (Organizational Assessment):
   - Start with basic enrichment  
   - Execute correlation to assess organizational exposure
   - Combine for risk-based prioritization

3. **Full Analysis Chain** (Comprehensive Investigation):
   - Execute: Enrich → Pivot → Correlate
   - Integrate: All findings into master analysis
   - Generate: Complete threat and exposure assessment

## Execution Examples

### Basic IOC Enrichment
```bash
Execute ioc_analysis_workflows.md with:
- IOC_VALUE="192.168.1.100"
- IOC_TYPE="IP Address"
- ANALYSIS_TYPE="enrich"
```

### Advanced GTI Pivoting
```bash
Execute ioc_analysis_workflows.md with:
- IOC_VALUE="evil-domain.com" 
- IOC_TYPE="Domain"
- ANALYSIS_TYPE="pivot"
- PIVOT_DEPTH=2
```

### Organizational Correlation
```bash
Execute ioc_analysis_workflows.md with:
- IOC_VALUE="malware-hash"
- IOC_TYPE="File Hash"
- ANALYSIS_TYPE="correlate"
- CORRELATION_SCOPE="comprehensive" 
- LOOKBACK_DAYS=90
```

### Chained Analysis
```bash
# Execute sequentially for complete analysis
1. ANALYSIS_TYPE="enrich"
2. ANALYSIS_TYPE="pivot" (if high-risk)
3. ANALYSIS_TYPE="correlate" (for exposure assessment)
```

## Integration with Parent Runbooks

This consolidated workflow integrates seamlessly with:
- `ioc_investigation.md` - All investigation levels
- `threat_hunting.md` - IOC-based hunting workflows  
- `case_investigation.md` - Evidence collection phases
- `generate_security_reports.md` - Report enrichment sections

## Performance Optimization

**Caching Strategy**: Results cached within session for repeated IOC analysis
**Parallel Execution**: Independent GTI/SIEM calls executed concurrently
**Smart Filtering**: Results filtered by relevance and confidence scores
**Resource Management**: API call optimization based on analysis type

## Quality Assurance

**Input Validation**: IOC format validation before analysis
**Result Verification**: Cross-validation between GTI and SIEM data
**Confidence Scoring**: All findings include confidence assessments
**Error Handling**: Graceful degradation when tools unavailable

---

*This unified workflow eliminates redundancy across three separate common steps while providing enhanced analytical capabilities through intelligent parameter-driven execution and integrated analysis options.*