# Testgen Enhancements

## #225: --no-tests CLI Flag
**Status**: Implemented

Allows scaffolding without the `tests/` directory:
```bash
soroban-forge new mycontract --template token --no-tests
```

## #226: Cross-Contract Call Test Generation
**Status**: Planned

Automatically generate mock contracts and integration tests for cross-contract calls.

## #227: Authorization Tree Assertion Generation
**Status**: Planned

Generate explicit assertions over authorization tree for `require_auth()` calls.

## #228: Ledger Time Helper
**Status**: Planned

Generate `advance_ledger(&env, n)` helper for time-dependent tests:
```rust
advance_ledger(&env, 100); // Fast-forward 100 ledgers
```

## #101: i128 Arithmetic Overflow Test Generation
**Status**: Implemented

For every entrypoint taking an `i128` argument, generates
`tests/forge_overflow.rs` with two tests per argument — calling the
entrypoint with a value near `i128::MAX / 4` and near `i128::MIN / 4`.
Relies on cargo's `dev`-profile default of `overflow-checks = true`
(what `cargo test` builds against) to turn a silent overflow into a
panicking test failure.
```
