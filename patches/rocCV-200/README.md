# rocCV #200 — V17 immediate GPU-launch error-check candidate

**Status: experimental review candidate.** Not a merged upstream fix, and not production-qualified.

- Upstream issue: [ROCm/rocCV #200](https://github.com/ROCm/rocCV/issues/200)
- Upstream source (pinned): [`54613b57a140bddb16a30fee63c22cf88c24bb7b`](https://github.com/ROCm/rocCV/tree/54613b57a140bddb16a30fee63c22cf88c24bb7b) (rocCV 0.4.0)
- Candidate: [`V17_ROCCV_43_SITES_LAUNCH_CHECK_CANDIDATE.patch`](V17_ROCCV_43_SITES_LAUNCH_CHECK_CANDIDATE.patch)
- Patch SHA-256: `17422028E8B6CA27BCF990A74EEE298F25ED53D14BD8994FAAFF2D6F85058A34` (24,083 bytes)

## What it changes

For each of the 43 inventoried HIP kernel-launch expressions in 21 rocCV operator source files, the patch places `HIP_VALIDATE_NO_ERRORS(hipGetLastError());` immediately after the launch. It also adds `#include "core/hip_assert.h"` where required. The existing kernel algorithms and launch geometry are otherwise unchanged. Source changes were checked to reverse exactly to the originals after removal of the inserted checks and includes.

This surfaces launch-time HIP errors to the calling operator without an added GPU synchronization. It **does not add code objects for unsupported GPU architectures**, and cannot by itself make the reporter's `gfx1036` run supported kernels.

## Reproduced local evidence

**Environment:** Radeon 8060S / `gfx1151` on AMD Strix Halo, Ubuntu 24.04 WSL2, ROCm 7.2.1, rocCV at the pinned commit. Libraries compiled as disposable, separately identified candidates. No driver update, system installation, ACE change, or Doctor V26 modification.

**V16C — controlled Flip launch-failure A/B:**

- Both disposable baseline and patched source variants were given the same test-only invalid launch geometry, `dim3 block(64, 32)` = 2,048 threads/block, above the observed 1,024 threads/block device limit.
- Baseline real C++ `Flip` returned normally despite pending `hipErrorInvalidConfiguration`; its output remained unwritten.
- Patched real C++ `Flip` immediately threw `Internal HIP Error: hipErrorInvalidConfiguration` for that same invalid geometry.
- The independent V16C acceptance receipt is [available here](evidence/V16C_INDEPENDENT_CONTROLLED_LAUNCH_AB_ACCEPTANCE.json) (SHA-256 `D2D6ABFA23A4C13B38AFFC06056B44E42A9FB12F5B3BAE2FC1213622A6146164`).

**V17 — complete candidate compilation and Flip positive GPU regression:**

- All 43 site insertions in 21 source files passed source roundtrip and hash-bound manifest checking.
- The complete patched rocCV shared library compiled for `gfx1151` with AMD Clang 22.
- The real GPU Flip positive regression returned 64/64 correct U8 pixels with `hipSuccess`.
- The independent V17 acceptance receipt is [available here](evidence/V17_INDEPENDENT_FULL_43_LAUNCH_SITE_CANDIDATE_ACCEPTANCE.json) (SHA-256 `0C2E257D45596BE375C9716657C8BADD06EBDC54F4104525E13C138DA90EDD38`).

These receipts record independent **artifact and execution-receipt audits**, not independent GPU re-execution.

## Explicit verification limits

- The other 42 launch sites were **compiled**, not each exercised by a real GPU runtime test.
- The reporter's `gfx1036` / `hipErrorInvalidImage` missing-code-object failure was **not reproduced** on our hardware.
- The original reporter environment, TheRock build, Python binding behavior, and all other operators have **not been validated** with this candidate.
- This patch is **not** an upstream-accepted or merged repair and no production suitability is claimed.
- An earlier incompatible-target negative control crashed; its failure receipt was preserved and the test was not repeated. That crash is not counted as qualifying evidence.

## Applying for review

Use only a **disposable** checkout of the pinned upstream commit; review the diff and confirm applicability before applying. For example:

```bash
git checkout 54613b57a140bddb16a30fee63c22cf88c24bb7b
git apply --check /path/to/V17_ROCCV_43_SITES_LAUNCH_CHECK_CANDIDATE.patch
git apply /path/to/V17_ROCCV_43_SITES_LAUNCH_CHECK_CANDIDATE.patch
```

These commands are for independent reviewers; this repository does not claim to have verified their operation on every Git configuration. Validate separately for your own compiler, target GPU, relevant operators, and error paths before considering upstream integration.

## Licence and attribution

rocCV is MIT-licensed. This repository also uses the MIT licence; the [original AMD rocCV copyright and MIT licence notice](UPSTREAM_LICENSE.txt) is retained separately alongside this derivative patch. Preserve all applicable upstream copyright and licence notices in redistributed copies.

**Provided as-is, without warranty.** This is voluntary experimental assistance to upstream maintainers, not a certification, safety guarantee, or claim that issue #200 has been fully resolved.
