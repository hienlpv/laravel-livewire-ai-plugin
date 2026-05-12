---
mode: agent
description: >
  Scaffold backend-only domain logic without any Livewire UI. Use this for APIs,
  queue jobs, console commands, or pure business logic layers.
---

# Backend Domain Logic Workflow

## Input Required

- **Domain entity** (e.g., `Order`, `Invoice`, `Notification`)
- **Fields** with types
- **Operations** needed (e.g., create, update, cancel, archive)
- **Business rules** (e.g., "cannot cancel a shipped order")
- **Events** to fire (e.g., `OrderCancelled`)

---

## Step 1 — @laravel-architect: Backend Layer

```
Create the backend domain layer for {Entity}:

1. Migration: create_{plural_snake}_table
   Fields: {fields}

2. Eloquent Model: App\Models\{Entity}
3. DTO: App\DTOs\{Entity}Data
4. Service: App\Services\{Entity}Service with: {operations}
5. Actions: App\Actions\{Operation}{Entity}Action for each operation
6. Events: App\Events\{Entity}{Event} for each domain event
7. Factory: Database\Factories\{Entity}Factory
```

---

## Step 2 — @pest-tester: Unit Tests

```
Write Pest unit tests for the {Entity} domain:

File: tests/Unit/Services/{Entity}ServiceTest.php

Cover:
- Each service method (success case)
- Each service method (failure / edge case)
- Business rule enforcement
- Events dispatched correctly
```
