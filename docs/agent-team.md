# Agent team

Summary of the custom agents for Mona's Project Pulse dashboard.

- Orchestrator — Claude Opus 4.7 (copilot)
  - Responsibility: Coordinates the Planner, Coder, and Designer; breaks work into phases, assigns explicit file scopes, runs tasks in parallel or sequentially as appropriate, and verifies integrated results.
  - Definition: .github/agents/orchestrator.agent.md

- Planner — Claude Opus 4.7 (copilot)
  - Responsibility: Researches the codebase and dependencies, identifies edge cases and risks, and produces an ordered implementation plan with file assignments and validation criteria.
  - Definition: .github/agents/planner.agent.md

- Coder — GPT-5.5 (copilot)
  - Responsibility: Implements code and runnable app support (tests, config, deterministic .vscode/launch.json for Project Pulse), follows repo patterns, and validates changes within assigned file scope.
  - Definition: .github/agents/coder.agent.md

- Designer — Gemini 3.1 Pro (copilot)
  - Responsibility: Produces UI/UX, accessibility, and visual design for the dashboard (project cards, status badges, responsive layout, CSS hooks like .dashboard and .project-card).
  - Definition: .github/agents/designer.agent.md

Note: This work will be orchestrated interactively using the GitHub Copilot CLI running in a Codespace; the Orchestrator agent delegates tasks to the specialist agents above and reports progress and blockers back through the CLI.
