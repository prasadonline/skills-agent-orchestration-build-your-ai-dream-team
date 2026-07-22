# Agent team

For Project Pulse, I will use a four-agent custom team orchestrated with GitHub Copilot CLI in a Codespace.

- Agent: Orchestrator
- Model: Claude Opus 4.7 (copilot)
- Responsibility: Coordinate the project end to end, request planning first, sequence phases, delegate file-scoped work, and validate final integration.
- Agent file: .github/agents/orchestrator.agent.md

- Agent: Planner
- Model: Claude Opus 4.7 (copilot)
- Responsibility: Analyze requirements and repository context, identify dependencies and edge cases, and produce a practical implementation plan with parallel and sequential steps.
- Agent file: .github/agents/planner.agent.md

- Agent: Coder
- Model: GPT-5.5 (copilot)
- Responsibility: Implement dashboard functionality, fix logic issues, and deliver deterministic, testable code following repository patterns.
- Agent file: .github/agents/coder.agent.md

- Agent: Designer
- Model: Gemini 3.1 Pro (copilot)
- Responsibility: Define and implement Project Pulse UI/UX quality, including hierarchy, accessibility, responsive behavior, and polished visual styling.
- Agent file: .github/agents/designer.agent.md

How the team will work together to build Project Pulse:

1. Orchestrator asks Planner for a complete build plan with file ownership, dependencies, validation checks, and risks.
2. Orchestrator breaks the plan into phases and assigns non-overlapping tasks to Coder and Designer where parallel work is safe.
3. Coder builds and updates implementation files while Designer refines dashboard experience and styling in scoped files.
4. Orchestrator sequences any overlapping work, verifies integration across app behavior and UI, and reports completion with remaining risks.
