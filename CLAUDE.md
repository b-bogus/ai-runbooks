# LLM Agent Instructions

This file provides comprehensive guidance for AI assistants (Claude, Gemini, ChatGPT, etc.) working with this security operations repository. It serves as the primary orientation document for understanding the project structure, capabilities, and specialized workflows.

## Project Overview

This is a security operations (SOC) runbook and persona system designed to guide LLM agents through standardized security workflows. The repository contains documentation, procedural guides, and configuration scripts for AI-assisted security operations.

## Repository Structure

- `rules_bank/` - Master directory containing all documentation, personas, and runbooks
  - `personas/` - Security role definitions (SOC Analysts, Threat Hunters, Incident Responders, etc.)
  - `run_books/` - Step-by-step procedural guides for security tasks
    - `common_steps/` - Reusable procedure components
    - `irps/` - Incident Response Plans for major incidents
    - `guidelines/` - Best practices and documentation guides
- `reports/` - Generated security reports and examples

## Configuration Scripts

### Setting Active Persona
```bash
python set_persona_rules.py <persona_name>
# Example: python set_persona_rules.py tier1_soc_analyst
```
Currently supported personas: `tier1_soc_analyst`, `threat_hunter`

### Linking Common Steps
```bash
python symlink_common_steps.py
```
Run this after changing personas to ensure common steps remain accessible.

## Key Concepts & Capabilities

### Core Components
- **Runbooks**: Tactical, step-by-step procedures for specific security tasks (alert triage, IOC enrichment, threat hunting)
- **IRPs**: End-to-end incident response plans for major incidents following PICERL lifecycle  
- **Personas**: Predefined security roles with specific responsibilities, skills, tool access, and specialized slash commands
- **MCP Integration**: Model Context Protocol tools for Chronicle SIEM, SOAR, Google Threat Intelligence, and Security Command Center

### Advanced Features
- **Slash Commands**: Specialized commands for security workflows (primarily supported in Claude)
- **Dynamic Configuration**: Persona-based context switching and tool access management
- **Report Generation**: Automated security report creation with standardized templates
- **Threat Intelligence**: Active integration with Google Threat Intelligence and security feeds
- **Multi-Platform SIEM**: Chronicle, SOAR case management, and cloud security integration

## Working with the Codebase

1. All content lives in `rules_bank/` - this is the primary working directory
2. The project uses MCP (Model Context Protocol) tools for integration with Google Cloud security services
3. Runbook actions map to specific agent tools (see `rules_bank/agent_tool_mapping.md`)

## Essential Context Sources for LLMs

This repository includes multiple layers of context to help AI assistants understand domain-specific security terminology, workflows, and relationships:

### Primary Context Files (Check These First!)
- **`LLMS-THESAURUS.md`** - Controlled vocabulary with security terminology definitions, hierarchical relationships (BT/NT/RT), and scope notes. **CRITICAL for understanding security concepts and terminology consistency.**
- **`LLMS-SITEMAP.md`** - Structural navigation providing directory overviews, content organization maps, priority markers, and cross-references. **ESSENTIAL for understanding content relationships and navigation.**
- **`agent_tool_mapping.md`** - Maps runbook actions to specific MCP tools and security platforms
- **`personas/`** - Role-specific context including responsibilities, skills, tools, and specialized slash commands

**Note on IA File Precedence:** When multiple LLMS-* files exist, prioritize the one closest to your working directory. The rules_bank/LLMS-* files take precedence for security operations, while local directory LLMS-* files provide the most specific context.

### Information Architecture Files (When Present)
- **`CONTENT_AUDIT_[date].md`** - Quality assessments and improvement recommendations
- **`CONTENT_INVENTORY_[date].md`** - Comprehensive catalogs of all content assets
- **`CONTENT_RELATIONSHIPS_[date].md`** - Dependency and relationship analysis between documents
- **`DOCUMENT_CLUSTERING_[date].md`** - Automated topic grouping and similarity analysis  
- **`TAXONOMY_[date].md`** - Hierarchical classification systems for content organization

### Specialized Enhancement Files
- **`SuperClaude_Framework/`** - Advanced command framework with specialized security slash commands
- **`reporting_templates.md`** - Standardized formats for security report generation
- **`./reports/`** - Real-world examples of generated security reports and investigations

### Usage Guidelines
**ALWAYS check for these essential files in directories:**
- **LLMS-THESAURUS.md** - For domain vocabulary and terminology consistency
- **LLMS-SITEMAP.md** - For structural navigation and content relationships

These files provide critical context that standard directory listings cannot convey. The specialized terminology and controlled vocabulary from LLMS-THESAURUS.md combined with the structural relationships from LLMS-SITEMAP.md are essential for maintaining consistency and accuracy in security operations.

## Code Style

When writing Python scripts:
- Follow Google Python Style Guide
- Use `pyink` for formatting
- Use `isort` for import sorting
- Line length: 88 characters
- Indentation: 2 or 4 spaces (be consistent within files)

## Report Generation

When executing security runbooks that generate reports (triage, investigations, hunts, etc.):

- **ALWAYS write reports to the `./reports/` directory**
- Use standardized naming convention: `<report_type>_<identifier>_<timestamp>.md`
- Examples:
  - `./reports/alert_triage_report_2194_20250504_1807.md`
  - `./reports/rule_triage_report_ru_99d1f620_20250720_0215.md`
  - `./reports/ioc_enrichment_report_scarfponcho.com_20250503_1856.md`
- Follow the reporting templates in `rules_bank/reporting_templates.md`
- Include proper metadata, findings, and recommendations in all reports

## Available Tools & Integrations

### MCP (Model Context Protocol) Tools
The repository integrates with multiple security platforms through MCP tools:

- **`secops-mcp`** - Chronicle SIEM integration (alerts, events, rules, threat intelligence)
- **`secops-soar`** - SOAR platform integration (case management, alerts, entities, workflows)
- **`gti`** - Google Threat Intelligence (threat analysis, IOC enrichment, malware research)
- **`scc-mcp`** - Security Command Center (cloud security posture, vulnerability management)

### Slash Commands (Claude-Specific)
Specialized security commands available in Claude for advanced workflows:
- **`/security:investigate`** - Comprehensive incident investigation and analysis
- **`/security:hunt`** - Proactive threat hunting and pattern detection
- **`/security:analyze`** - Deep analysis of rules, IOCs, and security events
- **`/security:enrich`** - Threat intelligence enrichment and contextualization
- **`/security:correlate`** - Multi-source correlation and pattern matching
- **`/security:detect`** - Detection rule creation and optimization

### Information Architecture Commands (Claude-Specific)
Content organization and analysis capabilities:
- **`/thesaurus`** - Generate controlled vocabulary and terminology maps
- **`/content-audit`** - Comprehensive content quality assessment
- **`/sitemap`** - Create structural navigation and content maps
- **`/taxonomy`** - Develop hierarchical classification systems

## Important Notes & Best Practices

### Repository Guidelines
- This is primarily a documentation repository - no build, test, or lint commands exist
- All content is stored directly in `rules_bank/` for simple, direct access
- Designed for AI-assisted security operations and incident response workflows

### Security Operations Focus
- Specialized for defensive security operations and incident response
- Integrates with enterprise security platforms (Chronicle, SOAR, GTI, SCC)
- Follows industry-standard frameworks (MITRE ATT&CK, NIST, SANS)
- Designed for real-world SOC analyst and security engineer workflows

### Context Optimization
- **Read LLMS-THESAURUS.md files first** for domain vocabulary understanding
- Check persona files for role-specific context and available tools
- Reference agent_tool_mapping.md for MCP tool capabilities
- Use reporting templates for consistent output formatting
