# Example: Refactoring

Task: *"The `processOrder` function is 300 lines and we need to add a new discount type. Clean it up while you're in there."*

## Bad refactor (one commit, 41 files changed)

```
- Rewrote processOrder into OrderProcessor class with Strategy pattern
  for discounts, payments, and shipping
- Introduced AbstractDiscountStrategy, DiscountStrategyFactory,
  IDiscountRule, and a DiscountRuleRegistry
- Renamed Order.total to Order.grandTotal across the codebase for clarity
- Also fixed the weird rounding in tax calculation (was rounding per-line,
  now rounds the sum -- this looked like a bug)
- Migrated the file to the new style guide while I was in there
- Added the new discount type
- Tests updated to match the new structure
```

**Why it fails:** Structure and semantics changed together -- the rename, the "bug fix", and the restructure are inseparable in one diff, so when something breaks in production, nothing can be reverted alone (`../core/03_EXECUTION_ENGINE.md` section 3.3). The rounding "fix" changed behavior that invoices may depend on -- that's a user decision, not a drive-by (`../playbooks/06_PLAYBOOKS.md` section 10.2). The pattern zoo (factory + registry + strategy for *two* discount types) is abstraction from a single pressure point (`../core/10_TASTE_AND_DESIGN.md` section 3). "Tests updated to match" means the tests were rewritten to pass -- the behavioral baseline was destroyed, not used. And 41 files far exceeds the requested blast radius (Art. IV).

## Good refactor (four commits, sequenced)

```
Commit 1 -- characterization tests (no production change)
  Added 12 tests pinning processOrder's current behavior: each existing
  discount type, stacking order, tax rounding (asserting the CURRENT
  per-line rounding), edge cases found by reading (zero-qty line, 100%
  discount). All pass against the untouched code.

Commit 2 -- structure only (behavior-preserving)
  Extracted three functions from processOrder: applyDiscounts,
  calculateTax, reserveInventory. Pure moves -- same logic, same order,
  no renames outside the file. All 12 characterization tests pass
  unchanged. processOrder is now 60 lines of orchestration.

Commit 3 -- behavior: the new discount type
  Added `volume-tier` discount inside applyDiscounts, following the shape
  of the existing types (a switch case -- three cases don't justify a
  strategy pattern yet; noted the pressure for when a fourth arrives).
  Added 4 tests for the new type and its stacking. All tests pass.

Commit 4 -- nothing. Stopped here.
  Noted in report: tax rounding is per-line, which may or may not be
  intended -- flagged for a product decision, not changed. Order.total
  naming left alone: rename would touch 41 files for zero behavior.
```

**Why it works:** Baseline first -- the characterization tests are the proof instrument for everything after (`../core/03_EXECUTION_ENGINE.md` section 3.2). Each commit is one kind of change, individually revertable. The discovered anomaly (rounding) was *reported*, not silently "fixed" (Art. XI, `../playbooks/06_PLAYBOOKS.md` section 10.2). The abstraction decision ran the `../core/10_TASTE_AND_DESIGN.md` section 3 tree honestly: duplicated shape, unstable concept -> keep it direct, record the pressure. The refactor repaid its cost -- the new discount landed in a 60-line function instead of a 300-line one -- and then it stopped (Art. XII).
