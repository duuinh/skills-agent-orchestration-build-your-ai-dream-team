# Agent team

Mona's Project Pulse dashboard is built by a specialized team of four custom agents, orchestrated via GitHub Copilot CLI in a Codespace. Each agent has a distinct role, model, and file scope to enable efficient, parallel development.

## Team composition

### Orchestrator
- **Model**: Claude Opus 4.7 (copilot)
- **Responsibility**: Coordinates Planner, Coder, and Designer agents. Breaks down complex requests into phases, manages dependencies, and verifies integration. Does not implement—manages the team.
- **Definition**: `.github/agents/orchestrator.agent.md`

### Planner
- **Model**: Claude Opus 4.7 (copilot)
- **Responsibility**: Creates implementation strategies and technical plans. Researches the codebase, documentation, and dependencies. Produces ordered implementation steps, file assignments, dependency mappings, and validation expectations. Does not write code.
- **Definition**: `.github/agents/planner.agent.md`

### Coder
- **Model**: GPT-5.5 (copilot)
- **Responsibility**: Implements code-oriented tasks, fixes bugs, and creates logic within assigned file scope. Writes clear, testable, deterministic code following repository patterns. For Project Pulse, creates launch configuration and support files to make the app runnable.
- **Definition**: `.github/agents/coder.agent.md`

### Designer
- **Model**: Gemini 3.1 Pro (copilot)
- **Responsibility**: Handles UI/UX, accessibility, information architecture, interaction flow, and visual design. Creates a polished Project Pulse dashboard with visible project cards, status badges, clear hierarchy, responsive layout, and deterministic CSS hooks.
- **Definition**: `.github/agents/designer.agent.md`

## Orchestration approach

The Orchestrator follows a structured execution model:

1. Request → Planner for analysis and strategy
2. Parse plan into phases with explicit file scopes
3. Run phases in parallel when file scopes don't overlap and no data dependencies exist
4. Run phases sequentially when work overlaps or depends on earlier output
5. Verify integration and report final outcome

All agents respect git control boundaries—the learner controls all git operations through Copilot CLI prompts.
