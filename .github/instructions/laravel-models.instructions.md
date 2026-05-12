---
applyTo: 'app/Models/**/*.php'
---

# Laravel Model Standards

- Every model file must start with `declare(strict_types=1);`
- Use `final class` where the model is not intended to be extended
- `$fillable` must be an explicit array — never use `$guarded = []`
- `$casts` must declare every non-string attribute (booleans, enums, dates, JSON)
- Every `BelongsTo` relationship must have a corresponding `->index()` in the migration
- Use `SoftDeletes` trait for any resource that should not be permanently deleted
- Every relationship method must declare a typed return (`BelongsTo`, `HasMany`, etc.)
- Local scopes must return `Builder` and accept `Builder $query` as first parameter
- Do not put business logic in models — delegate to `App\Services`
