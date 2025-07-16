---
title: "Group Cases v2 - Enhanced Workflow (Placeholder)"
type: "runbook"
category: "security_operations"
status: "placeholder"
supersedes: "group_cases.md"
version: "2.0"
tags:
  - case_management
  - case_grouping
  - workflow_automation
  - enhanced_grouping
  - version_2
---

# Runbook: Group Cases v2 - Enhanced Workflow (Placeholder)

## Status Note

**This is a placeholder for an enhanced version of the Group Cases workflow.** 

**Current Active Version**: Use `group_cases.md` for operational workflows.  
**Future Enhancement**: This v2 will provide improved grouping algorithms, enhanced automation, and streamlined reporting.

## Objective

To provide an enhanced workflow for analyzing recent SOAR cases with improved grouping logic, automated prioritization algorithms, and advanced entity correlation capabilities that extend beyond the current `group_cases.md` implementation.

## Scope

*(Define what is included/excluded, e.g., Focuses on analyzing existing case data and alerts. May involve basic enrichment but not deep investigation of each case.)*

## Inputs

*   *(Optional) `${NUMBER_OF_CASES}`: Number of recent cases to analyze (e.g., 5, 10).*
*   *(Optional) `${TIME_FRAME_HOURS}`: Lookback period for cases.*
*   *(Optional) `${GROUPING_CRITERIA}`: Specific criteria for grouping (e.g., shared hostname, alert type, CVE).*

## Tools

*   `secops-soar`: `list_cases`, `get_case_full_details`, `list_alerts_by_case`, `get_entities_by_alert_group_identifiers`
*   `secops-mcp`: `lookup_entity`
*   `gti-mcp`: (Relevant enrichment tools)
*   **Action:** Generate report file (e.g., using `write_to_file`)

## Workflow Steps & Diagram

1.  **List Cases:** Retrieve recent cases using `list_cases`.
2.  **Gather Case Details:** For each case, get details using `get_case_full_details` and `list_alerts_by_case`. Extract key entities.
3.  **Group Cases:** Analyze entities and alert details across cases to identify logical groups based on `${GROUPING_CRITERIA}` or observed similarities.
4.  **Prioritize Groups:** Assess the priority of each group based on alert severity, entity criticality, or potential impact.
5.  **Enrich Key Entities (Optional):** Perform basic enrichment on key shared entities within high-priority groups using `lookup_entity` and GTI tools.
6.  **Generate Summary Report:** Create a report summarizing the case groups, prioritization rationale, and key findings using the "Generate report file" action.

```mermaid
sequenceDiagram
    participant Analyst/User
    participant Cline as Cline (MCP Client)
    participant SOAR as secops-soar
    participant SIEM as secops-mcp
    participant GTI as gti-mcp

    Analyst/User->>Cline: Start Group Cases v2 Workflow\nInput: NUMBER_OF_CASES, ...

    %% Step 1: List Cases
    Cline->>SOAR: list_cases(limit=NUMBER_OF_CASES)
    SOAR-->>Cline: List of Cases (C1, C2...)

    %% Step 2: Gather Details
    loop For each Case Ci
        Cline->>SOAR: get_case_full_details(case_id=Ci)
        SOAR-->>Cline: Details for Ci
        Cline->>SOAR: list_alerts_by_case(case_id=Ci)
        SOAR-->>Cline: Alerts for Ci
        Note over Cline: Extract Key Entities for Ci
    end

    %% Step 3 & 4: Group & Prioritize
    Note over Cline: Analyze entities/alerts across cases, form groups (G1, G2...), prioritize groups

    %% Step 5: Enrich (Optional)
    opt Enrich High Priority Groups
        loop For each High Priority Group Gp
            Note over Cline: Identify key shared entities (Ep1, Ep2...)
            loop For each Entity Epi
                Cline->>SIEM: lookup_entity(entity_value=Epi)
                SIEM-->>Cline: SIEM Summary
                Cline->>GTI: get_..._report(ioc=Epi)
                GTI-->>Cline: GTI Enrichment
            end
        end
    end

    %% Step 6: Generate Report
    Note over Cline: Synthesize findings into report content
    Cline->>Cline: Generate report file (path="./reports/case_grouping_report...", content=ReportMarkdown)
    Note over Cline: Report file created

    Cline->>Analyst/User: Conclude runbook (result="Case grouping analysis complete. Report generated.")

```

## Completion Criteria

*(Define how successful completion is determined, e.g., Cases analyzed, groups identified and prioritized, summary report generated.)*
