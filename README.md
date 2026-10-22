# Fawn

**Models evolve. The runtime makes them useful.**

Fawn is a minimal, extensible, workspace-first coding companion built for developers who value simplicity, transparency, autonomy, and control.

AI models are constantly improving, but an effective coding companion is more than the model behind it. The runtime determines how models understand projects, interact with tools, execute commands, manage context, and turn instructions into useful work.

**Fawn focuses on building that runtime well.**

Inspired primarily by [Pi](https://github.com/earendil-works/pi), with ideas drawn from OpenCode, Goose, and other coding agents, Fawn embraces a small, composable architecture rather than a feature-heavy assistant.

Its goal is to provide the essential capabilities of a dependable coding companion while remaining understandable, adaptable, and independent of any particular model provider.

## Philosophy

Fawn is guided by a few principles:

- **Runtime over model dependency.** Models should be replaceable without redesigning the agent. A consistent runtime provides the foundation for conversation, tools, and execution.
- **Minimalism with purpose.** Keep the core focused. Every abstraction, dependency, and feature should justify the complexity it introduces.
- **Transparency by design.** Model responses, tool calls, commands, file changes, and execution outcomes should be observable rather than hidden behind automation.
- **Developer autonomy.** Ordinary coding operations should proceed without repetitive approvals or unnecessary interruptions, while consequential authority remains explicit.
- **Workspace-first operation.** The selected workspace defines the project's context, working directory, and file-operation boundaries.
- **Ephemeral by default.** Conversations exist in memory for the active process. Fawn does not require persistent sessions, saved transcripts, or conversation recovery infrastructure.
- **Extensibility through composition.** Clear responsibilities and stable interfaces allow capabilities to evolve independently without complicating the foundation.

The goal is not to build an assistant that does everything. It is to build a coding companion that does the essential things reliably and can grow without losing its simplicity.

## Architecture

Fawn separates its responsibilities into four focused packages:

| Package | Responsibility |
|---|---|
| **`@fawn/ai`** | Unified model communication, streaming, and provider-independent interfaces |
| **`@fawn/agent`** | Neutral agent runtime, conversation state, tool calling, events, and lifecycle management |
| **`@fawn/core`** | Workspace management, permissions, coding tools, operating modes, and project context |
| **`@fawn/code`** | Developer-facing coding application, command-line interaction, and terminal interface |

The model layer remains independent of agent orchestration. The agent runtime remains independent of coding-specific tools and workspace policies. The coding core provides those capabilities without depending on how they are presented to the user.

This separation keeps the system understandable, testable, and adaptable while allowing the application to remain small.

## The Coding Experience

Fawn is designed around a straightforward workflow: select a workspace, describe what needs to be done, and let the agent work while maintaining visibility and control.

The initial experience focuses on:

- Exploring and understanding codebases.
- Listing, reading, and searching project files.
- Editing and writing code.
- Executing local commands and running tests.
- Streaming model responses and tool activity.
- Loading project guidance from `AGENTS.md` and README files.
- Maintaining conversational context throughout the active process.
- Handling errors, interruptions, and cancellation without losing conversation integrity.
- Providing a focused, interactive terminal experience.

Fawn provides two operating modes:

- **Explore.** Inspect, search, understand, and plan without modifying project files or executing shell commands.
- **Work.** Modify authorized files, execute permitted operations, and complete coding tasks with minimal interruption.

Modes can be switched without changing the selected model, recreating the agent, or discarding the conversation.

Fawn aims to make exploration and implementation feel like two parts of the same continuous workflow.

### Execution and trust

Fawn follows a **Workspace-First Permission Model** built around `allow`, `ask`, and `deny` decisions.

In Work mode, ordinary file operations inside the active workspace are permitted automatically. Shell execution requires approval by default, with an explicit option to temporarily authorize trusted execution.

Built-in file tools enforce workspace boundaries, including restrictions against accessing files outside the selected root through symlinks.

**Fawn does not include a sandbox in its MVP.**

Shell commands execute with the privileges of the developer's operating-system account. The workspace determines where commands start, but it does not isolate their filesystem, network, or subprocess access.

Permissions provide control over what Fawn authorizes; they are not a substitute for operating-system isolation.

Fawn is therefore intended for developers who understand and control their local execution environment. Stronger execution isolation may be introduced separately as the project evolves.

## Built to Evolve

Fawn begins with a unified OpenAI-compatible model interface supporting OpenAI, Ollama, and LM Studio.

Its agent runtime remains independent of those providers, allowing the model layer to evolve without requiring changes to conversation management, tool execution, or workspace behavior.

The same philosophy applies throughout the system: preserve clear responsibilities, keep extension boundaries small, and introduce new capabilities only when they serve a demonstrated need.

Features such as additional provider protocols, richer integrations, advanced tooling, persistent conversations, and isolated execution environments may be explored as the project matures.

**Extensibility should be a property of the architecture, not an excuse for unnecessary complexity.**

---

**Fawn is built on a simple conviction: models will keep changing, but the runtime that turns their capabilities into useful work should remain understandable, dependable, and yours to control.**