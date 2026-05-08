# opencode Hindsight

An opencode plugin for integrating with vectorize.io's Hindsight AI agent memory system.

This project is starting as an experiment inspired by the official Hindsight opencode plugin. The goal is to keep the familiar Hindsight workflow while making memory access more configurable for real multi-agent development environments.

## Project Intent

Most agent memory integrations assume a single shared memory space or a single global configuration. This repository is intended to explore a more flexible model where each opencode agent can have its own Hindsight configuration and where an agent can optionally read from or write to multiple Hindsight memory banks.

The initial plugin should make it possible to:

- Configure Hindsight access per opencode agent.
- Assign different memory banks to different agents.
- Give one agent access to multiple memory banks for broader context.
- Control read and write behavior independently where useful.
- Support project-level defaults while allowing agent-specific overrides.
- Preserve a simple setup path for users who only need one memory bank.

## Why This Exists

Different agents often need different memory boundaries. A planning agent may benefit from broad product and architecture memory, while an implementation agent may need repo-specific technical history. A review agent may need access to decisions and known pitfalls without writing back every observation.

This plugin aims to make those patterns explicit instead of forcing every agent through one shared memory configuration.

## Early Configuration Direction

The exact configuration shape will evolve as the plugin is built, but the intended model is something like:

```jsonc
{
  "hindsight": {
    "defaults": {
      "banks": ["project"],
      "read": true,
      "write": true
    },
    "agents": {
      "plan": {
        "banks": ["project", "architecture", "product"],
        "write": false
      },
      "build": {
        "banks": ["project", "implementation"]
      },
      "review": {
        "banks": ["project", "decisions", "pitfalls"],
        "write": false
      }
    }
  }
}
```

The important idea is not the final JSON shape, but the capability: memory can be scoped by agent, role, and purpose.

## Planned Capabilities

- Load memory from one or more Hindsight banks at the start of relevant agent sessions.
- Persist useful memories back to the correct bank or banks.
- Allow global defaults with per-agent overrides.
- Support read-only memory banks for reference context.
- Provide clear behavior when no agent-specific configuration exists.
- Keep the plugin install and configuration process straightforward.

## Current Status

This repository is in the earliest planning and scaffolding stage. The README is intentionally provisional and will be updated as the plugin architecture, configuration format, and implementation details become clearer.

## Inspiration

This project will use the official Hindsight opencode plugin as a reference point for the initial integration pattern, while extending the configuration model to support richer per-agent and multi-bank workflows.
