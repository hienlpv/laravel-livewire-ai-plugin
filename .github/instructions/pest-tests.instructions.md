---
applyTo: 'tests/**/*.php'
---

# Pest Test Standards

- Every test file must start with `declare(strict_types=1);`
- Always use `describe()/it()` block structure — **never** bare `test()` at file level
- Every test file that touches the database must use `uses(RefreshDatabase::class);`
- All test data must be created via factories — **never** raw `User::create()`, `DB::insert()`, or `Model::forceCreate()`
- Use `beforeEach()` for shared setup within a `describe()` block
- Livewire component tests must use `Livewire::actingAs($user)` for authenticated tests
- Every CRUD action test must cover the **denied** case as well as the **allowed** case
- Validation tests must cover: required fields empty, invalid types, and boundary values
- Use `->assertDispatched('event-name')` — not `->assertEmitted()`
- Each `it()` block must test **exactly one** behaviour
