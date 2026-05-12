---
applyTo: '**'
---

# Laravel Livewire AI Plugin — Global Copilot Instructions

This repository is a **GitHub Copilot multi-agent extension** for PHP Laravel 11 + Livewire v3 development.

---

## Agent Architecture

This plugin uses one Orchestrator and four specialist sub-agents. **Always start with the Orchestrator** unless you are explicitly targeting a specific sub-agent.

| Agent             | File                                        | Invoke for                         |
| ----------------- | ------------------------------------------- | ---------------------------------- |
| Orchestrator      | `.github/agents/orchestrator.agent.md`      | Any new task — let it route        |
| Laravel Architect | `.github/agents/laravel-architect.agent.md` | Migrations, Models, Services, DTOs |
| Livewire Expert   | `.github/agents/livewire-expert.agent.md`   | Livewire components, Form Objects  |
| Pest Tester       | `.github/agents/pest-tester.agent.md`       | Pest PHP feature & unit tests      |
| Tailwind UI       | `.github/agents/tailwind-ui.agent.md`       | Tailwind CSS styling in Blade      |

Full agent topology: see [AGENTS.md](../AGENTS.md)

---

## Stack — Hard Requirements

| Layer     | Technology           | Version  |
| --------- | -------------------- | -------- |
| Language  | PHP                  | **8.3**  |
| Framework | Laravel              | **11.x** |
| Frontend  | Livewire             | **v3**   |
| CSS       | Tailwind CSS         | **3.x**  |
| Testing   | Pest PHP             | **2.x**  |
| Database  | PostgreSQL           | 16       |
| Standards | PSR-12, Laravel Pint | latest   |

---

## Global Code Rules

These rules apply to **all generated PHP files** in this project:

1. Every PHP file begins with:

   ```php
   <?php

   declare(strict_types=1);
   ```

2. All class methods have **typed parameters and return types**

3. No `mixed` types unless absolutely unavoidable

4. Livewire: `dispatch()` — **never** `emit()`

5. Livewire: `#[Validate]` — **never** `protected $rules = []`

6. Livewire: `#[Computed]` — **never** `getXProperty()` convention

7. Tests: `describe()/it()` — **never** bare `test()` at file level

8. Tests: factories always — **never** raw model creation

---

## Workflow Prompts

Use these prompts for guided multi-agent workflows:

| Prompt                                         | Use Case                          |
| ---------------------------------------------- | --------------------------------- |
| `.github/prompts/crud-workflow.prompt.md`      | Full CRUD resource (all 4 agents) |
| `.github/prompts/component-workflow.prompt.md` | Standalone Livewire component     |
| `.github/prompts/backend-workflow.prompt.md`   | Backend domain logic only         |

---

## Directory Map

```
.github/
├── agents/                    # VS Code agent definition files (.agent.md)
│   ├── orchestrator.agent.md
│   ├── laravel-architect.agent.md
│   ├── livewire-expert.agent.md
│   ├── pest-tester.agent.md
│   └── tailwind-ui.agent.md
├── instructions/              # File-scoped coding standards
│   ├── laravel-models.instructions.md        (applyTo: app/Models/**)
│   ├── livewire-components.instructions.md   (applyTo: app/Livewire/**)
│   ├── blade-views.instructions.md           (applyTo: resources/views/livewire/**)
│   ├── pest-tests.instructions.md            (applyTo: tests/**)
│   └── migrations.instructions.md            (applyTo: database/migrations/**)
└── prompts/                   # Reusable workflow prompts
    ├── crud-workflow.prompt.md
    ├── component-workflow.prompt.md
    └── backend-workflow.prompt.md

agent-manifest.json            # Plugin manifest (orchestrator + agents + tools)
AGENTS.md                      # Canon registry — agent/skill/tool index
prompts/                       # Full system prompts (source of truth)
│   ├── orchestrator.md
│   └── sub-agents/
│       ├── laravel-architect.md
│       ├── livewire-expert.md
│       ├── pest-tester.md
│       └── tailwind-ui.md
tools/                         # Tool JSON definitions
│   ├── definitions.json
│   ├── read-laravel-file.json
│   ├── write-laravel-file.json
│   ├── list-project-files.json
│   └── run-artisan.json
```

---

## Security Rules

- Never generate code that stores plaintext passwords
- Always use Laravel's `Hash::make()` for password storage
- Always validate and sanitise user input via Form Requests or `#[Validate]`
- Policies must be deny-first — default to `false` before applying role checks
- Never expose model primary keys in URLs without authorisation checks
- Use `findOrFail()` over `find()` to prevent silent null access
