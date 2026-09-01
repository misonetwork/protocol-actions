# Protocol Actions

Composable, custody-agnostic actions for the Miso protocol. Each top-level directory is an independently publishable Sui Move 2024 package:

- `composition_royalty_pool` creates and funds canonical Composition royalty pools.
- `recording_royalty_pool` creates and funds canonical Recording royalty pools.
- `release_revenue_distributor` splits Release revenue across its immutable tracklist.
- `composition_routed_stake` manages Composition-owned Recording-share stakes whose rewards are permissionlessly swept to the Composition pool.

Production APIs accept the protocol's raw admin capabilities. They contain no Vault dependency, installation state, package witness, plugin endpoint, or `entry` function. Created pools and routed stakes are returned unshared so callers can compose registration before sharing. Released principal is returned as a `Balance` so the caller controls its next safe destination.

## Capability invariant

Production construction issues exactly one share type, one `TreasuryCap`, and one protocol object for each Composition or Recording admin capability. Tests sometimes create multiple same-typed fixtures to exercise address-level defenses; those fixtures are intentionally stronger than the reachable production model and are not evidence that duplicate same-type production caps can exist.

## Accumulator testing

The Move VM covers direct positive redemption after `send_funds` and a transaction boundary, plus empty, zero, and overdraw behavior. It cannot expose a positive `settled_funds_value` consensus snapshot, so composing that reader into each redemption action still requires a Sui network E2E across a real commit boundary; tests do not fake the reader result.

## Build

Run in each package directory:

```sh
sui move build
sui move test --coverage
sui move coverage source --module <module-name>
```

Licensed under Apache-2.0.
