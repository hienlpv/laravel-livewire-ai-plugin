---
applyTo: 'app/Livewire/**/*.php,app/Forms/**/*.php'
---

# Livewire v3 Component Standards

- Every component file must start with `declare(strict_types=1);`
- All public properties must have explicit PHP type declarations
- Use `dispatch()` to fire events — **never** `emit()`
- Use `#[Validate]` attribute on Form Object properties — **never** `protected $rules = []`
- Use `#[Computed]` attribute for computed properties — **never** `getXProperty()` convention
- Use `#[Url]` for properties that should sync to the URL querystring
- Use `#[On('event-name')]` for event listeners instead of `$listeners` array
- Forms with more than 2 fields **must** use a Form Object (`Livewire\Form`)
- Use `$this->authorize()` inside component methods — not in Blade with `@can` for mutations
- The `render()` method must declare `\Illuminate\Contracts\View\View` return type
- Do not inject services in the constructor — use `app()` or method injection
