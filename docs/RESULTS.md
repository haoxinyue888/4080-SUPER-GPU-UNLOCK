# Results and Measurement Boundaries

This study covers **one Gainward RTX 4080 SUPER (AD103, 16 GB)** running Windows 11. These results are evidence for this system's **in-session FP16/BF16 dense GEMM compute performance**, not proof of a universal RTX 4080 SUPER unlock.

## Saved measurements

All values below are **effective TFLOPS** for 8192 × 8192 × 8192 matrix multiplication.

| Observation | FP16 | BF16 | Meaning |
|---|---:|---:|---|
| Original stock baseline | **101.303** | **101.398** | Before successful experimental unlock |
| Second stock-like reading | 104.870 | 104.907 | After an earlier unsuccessful physical attempt and power-off |
| Successful unlocked Windows session — A | **171.552 (+69.3%)** | **174.711 (+72.3%)** | First saved RUN02-session measurement |
| Successful unlocked Windows session — B | **168.488 (+66.3%)** | **170.911 (+68.6%)** | Independent repeat within the same RUN02 session |
| Normal restart without USB unlock | 102.698 | 98.965 | Returned to approximately stock-like compute throughput |
| Later successful handoff (RUN05-associated) | **163.409 (+61.3%)** | **169.331 (+67.0%)** | Separate saved post-handoff measurement |

All percentage changes above use the **first** stock baseline for the matching precision.

**RUN06:** the experimental USB-first boot, GPU recovery and Windows handoff succeeded according to the saved preboot report and user-confirmed Windows start. **No separately identified RUN06 GEMM result is available**; do not attach RUN05's numbers to RUN06.

## Benchmark method

- **Operation:** PyTorch CUDA `torch.mm` using FP16 or BF16 matrices already resident on the GPU.
- **Size:** 8192³, with a preallocated output.
- **Warmup:** 12 multiplications.
- **Timing:** 5 groups of 15 multiplications per precision; median of timed groups.
- **Effective throughput:** `2 × N³ / elapsed_seconds`, reported in TFLOPS.
- **TF32:** disabled.
- The stock and postboot measurements retained the same core multiplication and timing method.

This approach primarily measures GPU-side dense matrix computation. **It does not measure** gaming frame rates, model inference throughput, VRAM capacity, display features or a general-purpose application speedup.

## What the evidence supports

**Observed:**
- A manually authorized preboot operation successfully reached Windows on this particular GPU.
- Two same-session RUN02 measurements showed roughly **66–72% higher** FP16/BF16 GEMM throughput versus the first stock baseline.
- A later RUN05-associated saved measurement again showed elevated throughput.
- A normal Windows restart **without repeating the USB unlock step** reverted to stock-like throughput.
- RUN06 confirmed the first-scan boot/handoff path, **not a new benchmark**.

**Not established:**
- Compatibility with other RTX 4080 SUPER boards or VBIOS variants.
- Successful unlock on every restart or from every initial hardware state.
- Long-duration stability, exhaustive numerical correctness or absence of hardware risk.
- Improved FPS, LLM tokens/second or other real-application performance.
- Persistence through future cold boots, sleep/resume, driver changes or other lifecycle events.

Raw JSON, hardware logs and ROM/PROM data are intentionally **not** part of this repository. The table transcribes reviewed numeric outcomes without private machine metadata.

For the causes behind individual attempts, see [our adaptations](ADAPTATION.md). For the prerequisite and logging boundaries, see [the research workflow](WORKFLOW.md).
