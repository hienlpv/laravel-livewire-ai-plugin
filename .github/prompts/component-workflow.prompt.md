---
mode: agent
description: >
  Scaffold a standalone Livewire v3 component (class + blade view + Tailwind styling + Pest test).
  Use this for non-CRUD components like dashboards, wizards, or custom interactive widgets.
---

# Standalone Livewire Component Workflow

## Input Required

- **Component name** (e.g., `DashboardStats`, `ProductWizard`, `OrderSummary`)
- **Purpose**: brief description of what this component does
- **Properties**: list of public properties with types
- **Actions/Methods**: list of user-triggered methods
- **Events dispatched**: list of events this component fires
- **Events listened to**: list of events this component reacts to

---

## Step 1 — @livewire-expert: Component Class + View

```
Create a standalone Livewire v3 component:

Component name: {ComponentName}
Purpose: {purpose}

Class: App\Livewire\{ComponentName}
- Properties: {properties}
- Methods: {methods}
- Dispatches: {events}
- Listens for: {listeners}
- Use Form Object if any form fields > 2

View: resources/views/livewire/{kebab-name}.blade.php
- Single <div> root
- wire:key on all list items
- wire:model.blur on form inputs
- wire:loading on submit buttons
```

---

## Step 2 — @tailwind-ui: Styling

```
Style resources/views/livewire/{kebab-name}.blade.php

Apply mobile-first Tailwind CSS:
- Responsive layout
- Dark mode variants on all colours
- Focus rings on all interactive elements
- wire:loading spinner on submit/action buttons
- Accessible labels and sr-only for icon-only buttons
```

---

## Step 3 — @pest-tester: Feature Test

```
Write a Pest feature test for App\Livewire\{ComponentName}:

File: tests/Feature/Livewire/{ComponentName}Test.php

Cover:
- Component renders successfully
- Each public method works correctly
- Each event is dispatched when expected
- Validation errors shown when applicable
- Authorization denied when user lacks permission (if applicable)
```
