# NH Applied — Doctor Development Lab

Public engineering **candidate patches and independently audited qualification evidence** for CUDA-to-AMD / HIP / ROCm compatibility investigations. This is a development and validation repository, not the production Doctor product or ACE's governed execution repository.

## Published candidate

### [rocCV issue #200 — immediate kernel launch-error checks (V17)](patches/rocCV-200/README.md)

- [Read the candidate patch](patches/rocCV-200/V17_ROCCV_43_SITES_LAUNCH_CHECK_CANDIDATE.patch)
- [Validation, applicability and test limitations](patches/rocCV-200/README.md)
- [V16C controlled launch-failure A/B receipt](patches/rocCV-200/evidence/V16C_INDEPENDENT_CONTROLLED_LAUNCH_AB_ACCEPTANCE.json)
- [V17 complete-library build and Flip regression acceptance](patches/rocCV-200/evidence/V17_INDEPENDENT_FULL_43_LAUNCH_SITE_CANDIDATE_ACCEPTANCE.json)
- [Upstream rocCV MIT copyright and licence notice](patches/rocCV-200/UPSTREAM_LICENSE.txt)

**Status:** 43 launch sites patched across 21 source files; complete library builds for `gfx1151`; Flip positive GPU regression passes 64/64. Only the Flip launch-error path has been A/B runtime-tested. **Reporter `gfx1036` reproduction, all remaining launch-site runtime paths and upstream acceptance are not verified.**

Candidates are shared voluntarily **as-is, without warranty** for independent engineering review. The root [MIT licence](LICENSE) applies to the repository's NH Applied contributions; upstream copyright and licensing are preserved alongside derivative patches.

Project context: [NH Applied](https://nhapplied.co.uk/) · [Upstream rocCV issue #200](https://github.com/ROCm/rocCV/issues/200).
