# clone-lin-curve-getyd

Experimental LIN clone of Curve Finance 3pool `get_y_D` / `_calc_withdraw_one_coin` (i64-positive scale: `SCALE=1e9`, `N=3`, 128-bit Newton `(a*b+add)/d`, fail-closed if the quotient does not fit i64).

- **Upstream:** [curvefi/curve-contract](https://github.com/curvefi/curve-contract) `contracts/pools/3pool/StableSwap3Pool.vy` commit `bae23a2fc9a0302d174ea1ffce8219a44a92149c`. Curve.Fi publishes that tree as informational-only (no reproduction license); this repository does **not** vendor the Vyper source. Hashes only: sha256 `03e0bf29ae2fe945a3629b8085062da8f9d9d25957e86001dfc3df68c895f9dc`, git blob `04d170189a1b5ddfecfc0af9ea3fe23eb0840423`.
- **LIN kernel:** [`src/lin_curve_getyd.lin`](src/lin_curve_getyd.lin) (sha256 `cb284492064d5594b5a895638104c9ca85b94ad403f2002669bcbd1ff0c19152`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/curve_getyd_c11.c`](test/oracles/curve_getyd_c11.c)
- **Proofs (lin-open only):** `make curve-getyd-proof` in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open) `examples/curve_getyd/` and `python3 test/prove_curve_getyd_external.py` (22 PASS / 0 FAIL / 1 SKIP JIT this run)
- **Class:** EXPERIMENTAL. Not Ethereum Curve 3pool uint256. Not `RATES`/`PRECISION`/`get_D`/`get_y`/`get_dy`/`exchange`. Not a production pool replacement.

Distinct from [clone-lin-curve-gety](https://github.com/kbelludoo/clone-lin-curve-gety) (`get_D`/`get_y`) and [clone-lin-curve-getdy](https://github.com/kbelludoo/clone-lin-curve-getdy) (`get_dy`).

Named goldens (i64-positive, equal `1e9` balances): identity `get_y_D` → **1000000000**; 10% LP burn `D1` → **2700000000**; `y` after 10% at `A=100` → **700367933**; no-fee `dy0` → **299632067** (haircut **367933** vs constant-sum 300000000); `A=2000` `dy0` → **299981370**; 0.04% fee path → **299572241**; naive i64 `D^2` wraps to **-8838116264523025375**.
