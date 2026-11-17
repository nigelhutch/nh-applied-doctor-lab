# NH Applied — Doctor Development Lab

> **NH Applied Doctor — Software Compatibility Diagnosis, Repair and Qualification**
>
> **Find the real fault. Avoid the wrong fix. Prove the result.**
>
> NH Applied Doctor is an evidence-led engineering capability for diagnosing difficult software and GPU compatibility problems, developing targeted repairs where the evidence supports them, and independently qualifying the outcome. Initial cases focus on CUDA-to-AMD portability, HIP and ROCm on AMD Strix Halo.
>
> **[Explore NH Applied Doctor & discuss a compatibility problem](https://nhapplied.co.uk/doctor.html)** · **[Read the public white paper (PDF)](https://nhapplied.co.uk/publications/NH_Applied_Doctor_White_Paper_v1.0_DOI_24310226_PUBLIC.pdf)** · **[Permanent Zenodo DOI: 10.5281/zenodo.24310226](https://doi.org/10.5281/zenodo.24310226)** · [Email NH Applied](mailto:nigel@nhapplied.co.uk?subject=NH%20Applied%20Doctor%20-%20Compatibility%20Enquiry)
>
> **Representative local qualification evidence** (AMD Ryzen AI MAX+ 395, Radeon 8060S / `gfx1151`):
> - CUDA voxelizer: six tested CPU/GPU configurations produced matching outputs, across 14 executions.
> - HIP image filters: nine reference-comparison cases met their defined numerical tolerances.
> - Windows HIP runtime coherence: a controlled missing/mismatched-DLL failure was reproduced, then eight corrected-configuration runs passed 24 bounded GPU operations each.
>
> These are **configuration-specific local results**, not proof of universal CUDA compatibility, an upstream fix in another reporter's environment or a publicly released standalone Doctor software product. NH Applied can discuss **scoped engineering investigations**; the proprietary Doctor product is separate from this public candidate-patch repository.
>
> **Engineering enquiries:** [nigel@nhapplied.co.uk](mailto:nigel@nhapplied.co.uk). Messages to this address are handled by NH Applied.

---

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
