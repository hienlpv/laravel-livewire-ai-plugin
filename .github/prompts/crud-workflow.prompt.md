---
mode: agent
description: >
  Full CRUD scaffold for a Laravel + Livewire resource. Runs all four agents in sequence:
  laravel-architect (backend) → livewire-expert (components) → tailwind-ui (styling) → pest-tester (tests).
---

# Full CRUD Workflow

## Input Required

Before starting, collect:

- **Resource name** (e.g., `Product`, `BlogPost`, `OrderItem`) — singular PascalCase
- **Fields** — name and type for each field (e.g., `name: string`, `price: decimal`, `stock: integer`)
- **Soft deletes?** — yes / no
- **Authorization?** — yes / no (creates a Policy with `admin` role gate)
- **Search fields** — which fields should be searchable in the table

---

## Step 1 — @laravel-architect: Backend Layer

Delegate to `@laravel-architect`:

```
Create the full backend layer for {Resource}:

1. Migration: create_{plural_snake}_table
   Fields: {fields}
   Soft deletes: {yes|no}

2. Eloquent Model: App\Models\{Resource}
   - $fillable for all fields
   - $casts for non-string types
   - Relationships (if any)
   - Local scopes: scopeSearch(Builder, string)

3. DTO: App\DTOs\{Resource}Data (readonly, from() + toArray())

4. Service: App\Services\{Resource}Service
   - paginate(int $perPage, ?string $search): LengthAwarePaginator
   - create({Resource}Data $data): {Resource}
   - update({Resource} $model, {Resource}Data $data): {Resource}
   - delete({Resource} $model): bool

5. Action classes:
   - App\Actions\Create{Resource}Action
   - App\Actions\Update{Resource}Action
   - App\Actions\Delete{Resource}Action

6. Policy: App\Policies\{Resource}Policy (if authorization enabled)
   - viewAny, view, create, update, delete
   - Deny-first; admin role required for create/update/delete

7. Factory: Database\Factories\{Resource}Factory
8. Seeder: Database\Seeders\{Resource}Seeder (20 records)
```

---

## Step 2 — @livewire-expert: Livewire Components

Delegate to `@livewire-expert` (after architect completes):

```
Create three Livewire v3 components for {Resource}:

Read these files first:
- app/Models/{Resource}.php
- app/Services/{Resource}Service.php
- app/Forms/{Resource}Form.php (if it exists)

1. App\Livewire\{Resource}Table
   - Uses WithPagination + #[Url] for search + perPage
   - #[Computed] products(): LengthAwarePaginator via {Resource}Service
   - Methods: openCreate(), openEdit(int $id), delete(int $id)
   - #[On('product-saved')] to close modal + clear computed cache
   - View: resources/views/livewire/{kebab-resource}-table.blade.php

2. App\Forms\{Resource}Form (Form Object)
   - #[Validate] on all fields
   - fill({Resource} $model): void
   - save(?int $id = null): {Resource}

3. App\Livewire\{Resource}FormModal
   - public {Resource}Form $form
   - #[On('{kebab-resource}-form-open')] open(?int $id): void
   - save(): void (dispatches '{kebab-resource}-saved')
   - View: resources/views/livewire/{kebab-resource}-form-modal.blade.php
```

---

## Step 3 — @tailwind-ui: Styling

Delegate to `@tailwind-ui` (after livewire-expert completes):

```
Style these two Blade views:

Read these files first:
- resources/views/livewire/{kebab-resource}-table.blade.php
- resources/views/livewire/{kebab-resource}-form-modal.blade.php

Apply:
1. {kebab-resource}-table.blade.php:
   - Responsive table with overflow-x-auto
   - Alternating row hover states
   - Status badges with @class() conditional colours
   - Toolbar with search input (left) + "Add {Resource}" button (right)
   - Dark mode variants for all colour classes

2. {kebab-resource}-form-modal.blade.php:
   - Backdrop with blur + click-outside-to-close
   - Centred dialog panel (max-w-lg)
   - Form inputs with focus rings, error states, and sr-only labels
   - Footer with Cancel + Save buttons (Save shows wire:loading spinner)
   - Dark mode variants for all colour classes
```

---

## Step 4 — @pest-tester: Tests

Delegate to `@pest-tester` (after all files are created):

```
Write Pest PHP tests for {Resource}:

Read these files first:
- app/Livewire/{Resource}Table.php
- app/Livewire/{Resource}FormModal.php
- app/Services/{Resource}Service.php

1. tests/Feature/Livewire/{Resource}TableTest.php
   - renders for authenticated user
   - paginates
   - filters by search
   - resets page on search change
   - admin can open create modal
   - admin can open edit modal
   - admin can delete (dispatches event, record soft-deleted)
   - non-admin delete is forbidden

2. tests/Feature/Livewire/{Resource}FormModalTest.php
   - populates form for editing
   - resets form for creation
   - creates record with valid data
   - updates record with valid data
   - validation errors for empty required fields
   - validation errors for invalid values

3. tests/Unit/Services/{Resource}ServiceTest.php
   - paginates
   - filters by search
   - creates from DTO
   - updates from DTO
   - soft deletes
```
