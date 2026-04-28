# AGENTS.md

## Workflow requirements

- Flag ambiguous specs for human review rather than interpreting them.
- When you encounter implicit business rules or undocumented edge cases in legacy code, extract them into specification language for human verification.

## Extracting specifications from legacy code

When analyzing COBOL or other legacy code to generate specifications:

- Distinguish business rules from infrastructure, error handling, and technical implementation details.
- Look for references to statutes, regulations, form numbers, or policy documents in comments or naming.
- Pay special attention to conditional logic, boundary conditions, and error handling — these often encode important business rules.
- Capture what the code does, not what you think it should do. Specification review will determine correctness.

Generate specifications that:

- Use plain language a domain expert can verify
- Include all requirements with acceptance criteria
- Document edge cases and boundary conditions
- Reference governing rules where applicable
- Note any ambiguities or areas needing clarification

Flag these for human review:

- Contradictory logic paths
- Undocumented magic numbers or thresholds
- Business rules with no apparent authoritative source
- Dead code that may represent deprecated requirements
- Assumptions you made during analysis

## Project-specific context

### File locations

- Primary specification: `docs/SPECIFICATION.md`
- Test plan: `docs/TESTPLAN.md`
- Legacy COBOL code (analysis only): `src/cobol/`
- Node.js implementation: `src/accounting/`
- Test files reference scenarios from `docs/TESTPLAN.md`

### Domain

- School accounting system for managing student accounts
- Operations: viewing balance, crediting accounts, debiting accounts
- Debits cannot exceed current balance

### Specification format

Specifications in this project use this structure:

~~~markdown
# [Feature/Component Name] Specification

## Purpose
Brief description of what this component does and why it exists.

## Requirements

### Requirement: [Requirement Name]
The system SHALL [behavior description].

#### Acceptance Criteria
- GIVEN [precondition]
- WHEN [action]
- THEN [expected outcome]

#### Edge Cases
- [Edge case description and expected handling]

## References
- [Link to governing statute, regulation, or policy]
~~~