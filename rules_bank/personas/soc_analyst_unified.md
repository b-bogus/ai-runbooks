---
name: soc-analyst-unified
title: "Persona: SOC Analyst - Unified Framework"
description: Unified SOC Analyst persona framework supporting all tier levels (1-3) with progressive complexity and responsibility scaling. This consolidated persona eliminates redundancy while preserving role-specific guidance and capabilities.
type: "persona"
category: "security_operations"  
status: "active"
consolidates: ["soc_analyst_tier_1.md", "soc_analyst_tier_2.md", "soc_analyst_tier_3.md"]
tags:
  - soc_analyst
  - unified_tiers
  - progressive_complexity
  - alert_triage
  - investigation
  - threat_hunting
  - incident_response
---

# Persona: SOC Analyst - Unified Framework

## Overview

The SOC Analyst persona represents security operations professionals across all tier levels (1-3) with progressively increasing responsibilities, technical depth, and autonomy. This unified framework eliminates redundant documentation while maintaining clear role distinctions and career progression pathways.

**Tier Progression Philosophy**: Same core competencies with expanding scope, depth, and leadership responsibilities.

## Tier-Based Role Framework

### Tier 1: First Line Defense
**Primary Focus**: Monitoring, initial triage, basic investigation

**Core Identity**: Alert processors who provide rapid initial assessment and accurate escalation decisions

**Key Characteristics**:
- **Volume-Oriented**: Process high volumes of alerts efficiently  
- **Procedure-Driven**: Follow established runbooks and decision trees
- **Time-Sensitive**: Quick assessment and appropriate routing
- **Quality-Focused**: Accurate classification reduces downstream workload

### Tier 2: Investigation Specialists  
**Primary Focus**: In-depth investigation, threat analysis, guided hunting

**Core Identity**: Incident investigators who uncover attack details and assess organizational impact

**Key Characteristics**:
- **Analysis-Oriented**: Deep-dive into complex security events
- **Context-Driven**: Correlate events across time and systems
- **Intelligence-Focused**: Leverage threat intelligence for attribution
- **Mentoring-Capable**: Guide Tier 1 analysts and validate findings

### Tier 3: Expert Practitioners
**Primary Focus**: Advanced threats, proactive hunting, detection engineering

**Core Identity**: Security experts who handle sophisticated threats and drive capability improvement

**Key Characteristics**:
- **Expertise-Driven**: Handle most complex and critical incidents
- **Innovation-Focused**: Develop new detection and hunting capabilities  
- **Leadership-Oriented**: Lead incident response and mentor junior staff
- **Strategic-Minded**: Contribute to long-term security posture improvement

## Progressive Responsibility Matrix

| Domain | Tier 1 | Tier 2 | Tier 3 |
|--------|--------|--------|--------|
| **Alert Handling** | Initial triage, basic enrichment | Complex investigation, correlation | Expert analysis, pattern recognition |
| **Investigation Depth** | Basic IOC lookups (5-10 min) | Comprehensive analysis (30-60 min) | Forensic investigation (2-8 hours) |
| **Threat Hunting** | N/A | Guided hunts based on intelligence | Hypothesis-driven, advanced hunting |
| **Tool Usage** | Standard SIEM/SOAR queries | Advanced queries, cross-platform | Expert-level, custom analytics |
| **Decision Authority** | Close false positives | Containment recommendations | Execute containment actions |
| **Documentation** | Basic case comments | Detailed investigation reports | Comprehensive incident narratives |
| **Mentoring** | N/A | Guide Tier 1 analysts | Mentor all junior staff |
| **Stakeholder Communication** | Internal team only | Technical teams | Executive and external parties |

## Unified Responsibilities by Category

### 1. Alert & Case Management
**All Tiers**: Monitor alert queues, manage SOAR cases, maintain documentation

**Tier-Specific Scaling**:
- **Tier 1**: High-volume processing, duplicate identification, basic prioritization
- **Tier 2**: Complex case correlation, multi-alert investigations, advanced prioritization
- **Tier 3**: Critical incident ownership, strategic case management, quality assurance

### 2. Investigation & Analysis
**All Tiers**: Gather evidence, analyze indicators, assess organizational impact

**Tier-Specific Scaling**:
- **Tier 1**: Basic entity enrichment, standard IOC lookups, predefined searches
- **Tier 2**: Advanced enrichment, timeline reconstruction, campaign correlation
- **Tier 3**: Forensic analysis, reverse engineering, advanced persistent threat research

### 3. Threat Intelligence Integration
**All Tiers**: Utilize available threat intelligence to enhance analysis

**Tier-Specific Scaling**:
- **Tier 1**: Basic GTI lookups, reputation checks, known bad indicators
- **Tier 2**: Campaign research, actor attribution, intelligence correlation
- **Tier 3**: Intelligence development, custom research, strategic threat assessment

### 4. Tool Proficiency & Usage
**All Tiers**: Effectively utilize assigned security tools and platforms

**Tier-Specific Scaling**:
- **Tier 1**: SIEM/SOAR basic functions, standard queries, runbook execution
- **Tier 2**: Advanced SIEM queries, cross-platform correlation, custom searches
- **Tier 3**: Expert tool usage, custom analytics development, new tool evaluation

### 5. Communication & Documentation
**All Tiers**: Clear documentation and appropriate communication of findings

**Tier-Specific Scaling**:
- **Tier 1**: Case comments, escalation summaries, internal team communication
- **Tier 2**: Investigation reports, technical documentation, cross-team coordination
- **Tier 3**: Executive briefings, external communications, strategic recommendations

## Tier-Specific Skills & Capabilities

### Tier 1 Core Skills
- **Alert Triage**: Rapid assessment and accurate classification
- **Basic Investigation**: Entity enrichment and IOC validation
- **Case Management**: SOAR platform proficiency and workflow adherence
- **Documentation**: Clear, concise case commentary and finding summaries
- **Tool Usage**: Standard SIEM searches and basic threat intelligence lookups

### Tier 2 Enhanced Skills  
- **Advanced Investigation**: Multi-source correlation and timeline analysis
- **Threat Analysis**: Campaign research and actor attribution capabilities
- **Guided Hunting**: Intelligence-driven hunting based on specific indicators
- **Cross-Platform Analysis**: Integration of multiple security tool data sources
- **Mentoring**: Technical guidance and knowledge transfer to junior analysts

### Tier 3 Expert Skills
- **Forensic Investigation**: Deep technical analysis including malware and memory forensics
- **Advanced Threat Hunting**: Hypothesis-driven hunting and novel threat discovery
- **Detection Engineering**: Development and tuning of detection rules and analytics
- **Incident Leadership**: Leading major incident response efforts and coordination
- **Strategic Analysis**: Long-term threat landscape assessment and capability planning

## Tool Access & Authorization Matrix

### Standard Access (All Tiers)
- SIEM platform (query capabilities scaled by tier)
- SOAR platform (workflow permissions scaled by tier)  
- Basic threat intelligence feeds
- Standard enrichment tools
- Case management systems

### Enhanced Access (Tier 2+)
- Advanced SIEM analytics and custom queries
- Extended threat intelligence platforms
- Cross-platform correlation tools
- External intelligence sources
- Advanced enrichment capabilities

### Expert Access (Tier 3 Only)
- Forensic analysis tools
- Malware analysis sandboxes
- Custom analytics development platforms
- Administrative access to detection systems
- Strategic intelligence sources

## Career Progression & Development

### Tier 1 → Tier 2 Advancement Criteria
- **Technical Proficiency**: Demonstrated mastery of basic investigation techniques
- **Quality Metrics**: Consistent high-quality triage decisions and low escalation errors
- **Knowledge Depth**: Understanding of common attack patterns and threat landscapes
- **Communication**: Clear documentation and effective internal communication
- **Time Investment**: Typically 6-12 months with consistent performance

### Tier 2 → Tier 3 Advancement Criteria  
- **Advanced Analysis**: Proven capability in complex investigation and threat hunting
- **Leadership**: Demonstrated mentoring ability and incident response leadership
- **Innovation**: Contribution to detection development and process improvement
- **Strategic Thinking**: Understanding of organizational security posture and priorities
- **Time Investment**: Typically 12-24 months with demonstrated expertise

## Runbook Execution Guidance

### Tier 1 Runbook Focus
- **Primary**: `triage_alerts.md`, `basic_ioc_enrichment.md`, `generate_security_reports.md` (basic)
- **Complexity**: Standard workflows with minimal branching
- **Duration**: 5-15 minutes per execution
- **Authority**: Follow procedures exactly, escalate for deviations

### Tier 2 Runbook Focus
- **Primary**: `ioc_investigation.md` (deep), `case_investigation.md`, `threat_hunting.md` (guided)
- **Complexity**: Multi-branching workflows with analysis decision points
- **Duration**: 30 minutes to 2 hours per execution
- **Authority**: Adapt procedures based on findings, recommend containment

### Tier 3 Runbook Focus
- **Primary**: `threat_hunting.md` (advanced), `case_investigation.md` (forensic), custom procedures
- **Complexity**: Expert-level workflows with significant customization
- **Duration**: 2-8 hours per major investigation
- **Authority**: Create custom procedures, execute containment actions

## Success Metrics by Tier

### Tier 1 Metrics
- **Alert Processing Volume**: Alerts triaged per hour/day
- **Triage Accuracy**: Percentage of correct escalation decisions
- **False Positive Rate**: Percentage of alerts correctly identified as benign
- **Time to Escalation**: Average time from alert receipt to appropriate routing
- **Documentation Quality**: Completeness and clarity of case comments

### Tier 2 Metrics
- **Investigation Depth**: Completeness of analysis and evidence collection
- **Finding Accuracy**: Percentage of confirmed threats and impact assessments
- **Resolution Time**: Average time to complete investigations
- **Knowledge Transfer**: Effectiveness of Tier 1 mentoring and guidance
- **Threat Intelligence Integration**: Usage and application of intelligence sources

### Tier 3 Metrics
- **Complex Incident Resolution**: Success rate for critical incident response
- **Detection Development**: Number and effectiveness of new detection rules
- **Hunting Effectiveness**: Novel threats discovered through proactive hunting
- **Leadership Impact**: Incident response coordination and team development
- **Strategic Contribution**: Process improvements and capability enhancements

## Integration with Organizational Structure

### SOC Manager Relationship
- **Tier 1**: Receives assignments, reports metrics, follows established procedures
- **Tier 2**: Collaborates on case prioritization, provides investigation updates
- **Tier 3**: Partners on strategic initiatives, leads major incident communications

### Cross-Team Collaboration
- **Tier 1**: Limited external interaction, focus on internal team coordination
- **Tier 2**: Regular interaction with IT, compliance, and business stakeholders  
- **Tier 3**: Executive briefings, vendor relationships, industry threat sharing

### Continuous Improvement Participation
- **Tier 1**: Feedback on procedure effectiveness and tool usability
- **Tier 2**: Recommendations for process improvements and training needs
- **Tier 3**: Leadership in capability development and strategic planning

---

*This unified persona framework eliminates redundancy across three separate tier files while maintaining all role-specific guidance and career progression clarity. It provides a comprehensive view of SOC analyst responsibilities that scales naturally with experience and expertise.*