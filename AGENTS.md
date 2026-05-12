# AGENTS.md — Laravel Livewire AI Plugin Canon Registry

> **Purpose**: Single source of truth for every agent and skill in this plugin.
> Copilot reads this file to understand the full agent topology.

---

## Agents (5)

| ID                  | Display Name         | Role                                                                          | Prompt File                               |
| ------------------- | -------------------- | ----------------------------------------------------------------------------- | ----------------------------------------- |
| `orchestrator`      | Laravel Orchestrator | Entry-point router — CoT analysis, task classification, multi-step delegation | `prompts/orchestrator.md`                 |
| `laravel-architect` | Laravel Architect    | Migrations, Models, Services, Actions, DTOs, Domain Logic                     | `prompts/sub-agents/laravel-architect.md` |
| `livewire-expert`   | Livewire Expert      | Livewire v3 Components, Form Objects, Lifecycle Hooks, Computed Properties    | `prompts/sub-agents/livewire-expert.md`   |
| `pest-tester`       | Pest Tester          | TDD feature & unit tests with Pest PHP, Livewire testing helpers              | `prompts/sub-agents/pest-tester.md`       |
| `tailwind-ui`       | Tailwind UI          | Tailwind CSS utility styling inside Blade/Livewire views                      | `prompts/sub-agents/tailwind-ui.md`       |

---

## Agent File Locations

```
.github/agents/
├── orchestrator.agent.md
├── laravel-architect.agent.md
├── livewire-expert.agent.md
├── pest-tester.agent.md
└── tailwind-ui.agent.md
```

---

## Skills (4)

| ID                          | Description                                                   | Skill File                                  |
| --------------------------- | ------------------------------------------------------------- | ------------------------------------------- |
| `create-livewire-component` | Scaffold a full Livewire v3 component (class + blade)         | `.github/agents/livewire-expert.agent.md`   |
| `create-laravel-service`    | Scaffold a typed Service class with constructor DI            | `.github/agents/laravel-architect.agent.md` |
| `create-pest-tests`         | Generate Pest feature + unit tests for a component or service | `.github/agents/pest-tester.agent.md`       |
| `style-blade-view`          | Apply Tailwind utility classes to an existing Blade view      | `.github/agents/tailwind-ui.agent.md`       |

---

## Tools (4)

| ID                   | Description                                         | Definition File                 |
| -------------------- | --------------------------------------------------- | ------------------------------- |
| `read_file`          | Read any file in the Laravel project                | `tools/read-laravel-file.json`  |
| `create_file`        | Write/overwrite a file in the Laravel project       | `tools/write-laravel-file.json` |
| `list_project_files` | List files by path glob inside the project          | `tools/list-project-files.json` |
| `run_artisan`        | Execute an `php artisan` command and capture output | `tools/run-artisan.json`        |

---

## Delegation Routing (Orchestrator Decision Matrix)

| Keyword Signals                                             | Agent Chain                                                             |
| ----------------------------------------------------------- | ----------------------------------------------------------------------- |
| `migration`, `model`, `eloquent`, `database`, `schema`      | `laravel-architect`                                                     |
| `service`, `action`, `dto`, `repository`, `domain logic`    | `laravel-architect`                                                     |
| `livewire`, `component`, `wire:`, `form object`, `dispatch` | `livewire-expert`                                                       |
| `table`, `modal`, `computed`, `lifecycle hook`              | `livewire-expert`                                                       |
| `test`, `pest`, `phpunit`, `assert`, `tdd`, `spec`          | `pest-tester`                                                           |
| `tailwind`, `css`, `style`, `ui`, `layout`, `responsive`    | `tailwind-ui`                                                           |
| `crud`, `resource`, `full feature`                          | `laravel-architect` → `livewire-expert` → `tailwind-ui` → `pest-tester` |

---

## Stack Contract

| Layer     | Technology           | Version |
| --------- | -------------------- | ------- |
| Language  | PHP                  | 8.3     |
| Framework | Laravel              | 11.x    |
| Frontend  | Livewire             | 3.x     |
| CSS       | Tailwind CSS         | 3.x     |
| Testing   | Pest PHP             | 2.x     |
| Database  | PostgreSQL           | 16      |
| Standards | PSR-12, Laravel Pint | latest  |

---

## Conventions

- All classes use **strict types**: `declare(strict_types=1);`
- All methods use **type hints + return types**
- Livewire: use `dispatch()` — never `emit()`
- Livewire: use `#[Validate]` attribute — never `rules()` array in class body
- Livewire: prefer **Form Objects** for forms with > 2 fields
- Models: use `readonly` properties on DTOs
- Tests: use `describe()/it()` blocks with factories — never `setUp()` raw inserts
- Migrations: always add explicit indexes on foreign keys

---

_Auto-generated by gem-team scaffold — do not edit the ID column._
