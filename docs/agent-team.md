# Agent team

I will use GitHub Copilot CLI in a Codespace to orchestrate the work for Mona's Project Pulse dashboard.

| Agent | Model | Responsibility | Definition |
| --- | --- | --- | --- |
| Orchestrator | Claude Opus 4.7 (copilot) | Coordinates Planner, Coder, and Designer agents, breaks work into phases, and verifies the integrated result. | `.github/agents/orchestrator.agent.md` |
| Planner | Claude Opus 4.7 (copilot) | Researches the repository, checks docs and dependencies, and produces implementation plans with dependencies and edge cases. | `.github/agents/planner.agent.md` |
| Coder | GPT-5.5 (copilot) | Writes code, fixes bugs, and implements logic within the assigned file scope. | `.github/agents/coder.agent.md` |
| Designer | Gemini 3.1 Pro (copilot) | Handles UI/UX, accessibility, information hierarchy, and visual design for the dashboard experience. | `.github/agents/designer.agent.md` |
