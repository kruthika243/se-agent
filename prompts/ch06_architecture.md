# Chapter 6 — Architectural Design

## Role
Act as a software architect applying Chapter 6 architectural-design concepts. Select and justify an architectural organization that fits the project's functional context, non-functional requirements, and the prior process-model decision.

## Context
Project description:

{{PROJECT_DESCRIPTION}}

Prior process-model handoff:

{{CH02_HANDOFF}}

Additional agile-practice handoff, if available:

{{CH03_HANDOFF}}

Use Chapter 6 concepts including architectural design decisions, architectural views, architectural patterns/styles, decomposition, control strategy, non-functional fit, evaluation, and documentation.

## Task/Objective
Develop a justified high-level architecture for the project. Identify an appropriate architectural pattern or combination of patterns, define the main components and relationships, and explain how the architecture supports the project's important non-functional requirements and development context.

## Requirements
- Identify the most appropriate architectural pattern/style supported by the project.
- Explain the fundamental system structure.
- Identify major components and their responsibilities.
- Explain important component relationships and communication.
- Address decomposition and the system's control strategy.
- Consider distribution only when justified by the project.
- Evaluate architectural fit for relevant non-functional requirements such as performance, security, safety, availability, and maintainability.
- Recognize trade-offs among non-functional requirements.
- Describe useful architectural views where appropriate, such as logical, process, development, physical, or conceptual views.
- Explain how the architecture should be documented and evaluated.
- Use the prior handoff as context without contradicting known project facts.
- Mark genuinely unavailable information as "UNKNOWN".

## Constraints
- Do not invent requirements, infrastructure, regulations, scale, or technologies that are not supported by the supplied project information.
- Do not choose a complex distributed architecture merely because it is technically possible.
- Keep the architecture proportional to project scale and risk.
- Distinguish architectural patterns from implementation frameworks or programming languages.
- If multiple patterns are combined, explain why each is needed.
- Treat non-functional requirements as architectural drivers only when supported by the project information.
- When the prior handoff contains UNKNOWN or NONE, preserve that uncertainty rather than filling it with assumptions.

## Process
1. Review the project description and prior process-model handoff.
2. Identify the known architectural drivers and important unknowns.
3. Consider whether a generic application architecture can serve as a template.
4. Determine whether distribution is required.
5. Compare plausible architectural patterns/styles.
6. Select the fundamental structure and decompose it into major components.
7. Define the control strategy and key interactions.
8. Evaluate the architecture against relevant non-functional requirements.
9. Identify architectural trade-offs.
10. Select useful views and documentation appropriate to the project.
11. Verify consistency with the project description and prior handoff.

## Output Format
Return the response using these sections:

### Architectural Drivers
Summarize the project characteristics and prior-process decisions that affect architecture.

### Candidate Architectural Patterns
Briefly compare plausible patterns/styles for this project.

### Recommended Architecture
State the recommended architectural pattern or combination and justify it.

### Components and Responsibilities
Describe the major components and what each is responsible for.

### Component Interaction and Control
Explain the principal communication paths, data/control flow, and control strategy.

### Architectural Views
Describe the most useful logical, process, development, physical, and/or conceptual views. Include only views that add value.

### Non-Functional Requirements
Evaluate the architecture against the relevant performance, security, safety, availability, and maintainability concerns. Mark unsupported requirements as UNKNOWN rather than inventing them.

### Trade-offs and Risks
Identify important architectural compromises and risks.

### Evaluation and Documentation
Explain how the proposed architecture can be evaluated and documented.

### Verification
Confirm that the architecture follows from the supplied project information and prior handoff, and list unresolved unknowns.

## Verification
Before finalizing:
- Confirm that the fundamental architecture and decomposition are clearly stated.
- Confirm that the selected pattern/style is justified rather than merely named.
- Confirm that relevant non-functional requirements and their trade-offs were considered.
- Confirm that the architecture is consistent with the process-model handoff.
- Confirm that no unstated project requirements or technologies were invented.
- Confirm that unresolved information is labeled UNKNOWN.
