<p align="center"><strong>EN</strong> | <a href="ADAPTATION.zh-CN.md">中文</a></p>

# What We Adapted for the Gainward RTX 4080 SUPER

This is an **independent board-specific case study**, not a new GPU unlock method. The foundation came from earlier GPU-unlock research and the Windows UEFI implementation documented by TOTORONG for a **modified, non-SUPER 32 GB RTX 4080**. See [upstream credits](../REFERENCES.md).

Our tested target was **one Gainward RTX 4080 SUPER (AD103, 16 GB)** using the same GPU for both display output and CUDA work. Another manufacturer's 4080 SUPER — or even another revision of the same model — must be validated independently.

## Upstream foundation versus our adaptations

| Area | Already present upstream | Our Gainward-specific work |
|---|---|---|
| Compute-selector unlock | Underlying GPU firmware approach | Verified applicability to this board through inspection and real testing |
| Windows UEFI flow | Preload Windows; explicit manual confirmation; graphics recovery and Windows handoff | Adapted board preflight, graphics ownership and return-to-Windows checks |
| Board configuration | Assumptions tied to upstream tested hardware | Matched actual **16 GB** memory geometry, GPU identity and verified ROM/PROM evidence |
| Graphics-driver ownership | Single-GPU driver-release flow | Accounted for an additional verified UEFI graphics child on our motherboard |
| Startup-state checks | Reference-card conditions | Investigated varying cold-start observations and adopted bounded, rechecked admission logic |
| Boot manager discovery | Windows loader preloading | Added bounded discovery retries for a USB-first boot that initially could not find Windows |
| Diagnostics | Existing status logging | Used durable, numbered reports and explicit final-stage evidence to isolate actual failures |

None of the above means a particular adaptation is universally safe. **Do not simply copy board identities, checksums, register values or an EFI binary from another card.**

## The hardware testing journey

| Run | What happened | What it taught us |
|---|---|---|
| **RUN00** | The initial preflight refused an unexpected second UEFI graphics-driver child. **No unlock started.** | Valid device ownership can have a more complex shape than the original verifier expected; verify the *real* driver/device relationship rather than bypassing it. |
| **RUN01** | The experimental firmware work and graphics reconnection proceeded, but a strict post-reconnection PCI command comparison rejected the handoff. The system stopped. | The returning UEFI graphics driver may legitimately change a narrowly defined part of its operating state; the validation required a precise, tested exception, not a blanket relaxation. |
| **RUN02** | The corrected candidate completed recovery and handed off to Windows. Two same-session FP16/BF16 benchmarks showed substantial improvement. | A successful firmware readback alone is not proof of compute acceleration: measure from Windows as separate evidence. |
| **RUN03** | After an ordinary restart, the initial GPU selector observations differed from the earlier successful boot. The preflight **refused before modifying the GPU**. | Previously measured startup values must not become unjustified universal assumptions. A later bounded adaptation was tested in simulation; it is not proof that all startup states are safe. |
| **RUN04** | During a USB-first boot, the Windows preload stage could not find a Windows Boot Manager; the GPU transaction **did not start**. | Windows loader discovery needs verification before releasing the only active display GPU. |
| **RUN05** | After returning to firmware and launching again, Windows was found and the manually approved experiment reached Windows. A saved benchmark showed elevated throughput. | Successful second-launch discovery identified a practical boot-path problem, but did not by itself explain its root cause. |
| **RUN06** | An improved candidate found the Windows boot loader on its **first scan**, completed the manual operation, recovered graphics and handed off successfully. | The normal first-scan path was physically verified. The added delayed-discovery and storage-driver fallback paths had **simulation coverage only**; RUN06 did not invoke them. |

The bounded Windows discovery improvement passed **69/69 host-simulated scenarios**. Those are software-model results, not evidence that every motherboard's UEFI storage-driver path behaves the same way.

## What was central to the outcome

1. **Evidence before adaptation.** Establish the exact card, memory geometry, firmware identity and read-only initial state before changing assumptions.
2. **Fail-closed validation.** Unexpected ownership, firmware mismatches, missing Windows boot image or unclear cleanup stopped an attempt rather than being ignored.
3. **Logging of every decision.** Reports distinguished `attempted=0` preflight refusals from attempted hardware operations.
4. **Orderly handoff.** A successful unlock wasn't considered complete until GPU/graphics recovery and the Windows handoff had been checked.
5. **Independent Windows measurement.** Benchmark results were collected after the observed boot; later restart behavior was documented separately.

**Scope:** these findings concern the unlock implementation and its directly observed compute effect. This is not a general guide to PC tuning, GPU drivers or motherboard maintenance.

Continue with the [research workflow and safety boundaries](WORKFLOW.md) or the [measured results](RESULTS.md).
