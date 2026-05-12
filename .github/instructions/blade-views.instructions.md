---
applyTo: 'resources/views/livewire/**/*.blade.php'
---

# Livewire Blade View Standards

- Every Livewire component view must have a **single root `<div>` element**
- Always use `wire:key="{{ $item->id }}"` on elements inside `@foreach` / `@forelse` loops
- Use `wire:model.live.debounce.300ms` for search inputs
- Use `wire:model.blur` for regular form inputs (validate on blur, not on every keystroke)
- Use `wire:submit.prevent` on form elements
- Use `wire:loading` and `wire:target` to show loading states on buttons and inputs
- Use `wire:confirm="..."` on destructive actions (delete buttons)
- Every form input must have a matching `<label>` with `for` attribute
- Use `@error('field')` directives to show validation messages next to each input
- Use `@can` / `@cannot` only for **display decisions** (show/hide buttons) — not for authorization logic
