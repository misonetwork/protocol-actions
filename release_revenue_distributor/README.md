# Release Revenue Distributor

Raw-cap actions accept the Release capability as `admin_cap`, receive or redeem Release-held revenue, and route it to the Recording addresses fixed by the immutable tracklist. One event is emitted per track and one summary event per distribution. Flooring remainder returns to the Release.

The balance-splitting primitive is intentionally private: the package exposes no public donation path unrelated to Release custody. A positive `settled_funds_value` reader snapshot requires a network E2E across a real consensus commit.

```sh
sui move build
sui move test --coverage
```
