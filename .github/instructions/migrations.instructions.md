---
applyTo: 'database/migrations/**/*.php'
---

# Migration Standards

- Every migration file must start with `declare(strict_types=1);`
- Use `return new class extends Migration` — never named classes
- Table names must be **plural snake_case** (`products`, `product_categories`)
- Every table must have `$table->id()` (bigint unsigned auto-increment)
- Every table must have `$table->timestamps()`
- Use `$table->softDeletes()` for any resource that must be recoverable
- Every `foreignId()` column must be chained with `->constrained()->cascadeOnDelete()->index()`
- Never use `string()` for columns that will hold long text — use `text()` or `longText()`
- Use `unsignedDecimal(10, 2)` for monetary values
- Use `boolean()` with a `default(false)` — never store booleans as integers
- For nullable foreign keys: `->nullable()->constrained()->nullOnDelete()->index()`
- The `down()` method must always be the exact reverse of `up()`
