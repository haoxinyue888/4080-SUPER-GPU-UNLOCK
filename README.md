<img width="1448" height="1086" alt="image" src="https://github.com/user-attachments/assets/84867072-132a-440d-8c8a-e853f54fb3ad" />


# RTX 4080 SUPER GPU Unlock — AD103 Research

**An independent, hardware-specific adaptation study for the Gainward GeForce RTX 4080 SUPER 16 GB.**

This repository documents how existing GPU compute-unlock research was studied and adapted to one RTX 4080 SUPER under Windows 11. It focuses on **what required adaptation**, **what failed and why**, **logging and boot safety**, and **what the benchmarks actually showed**.

> **Not a universal unlocker.** This is a research and reproducibility guide, not a ready-to-boot EFI image or a claim that other RTX 4080 SUPER models are compatible. GPU firmware experiments can cause loss of display, failed boots, data loss, or hardware damage.

## Measured result

On one Gainward RTX 4080 SUPER (AD103, 16 GB), an explicitly authorized UEFI experiment completed GPU recovery and handed off to Windows. Two measurements in the successful Windows session showed higher **FP16/BF16 dense GEMM** throughput than the original stock baseline.

| 8192³ dense GEMM | Stock | Unlocked run A | Unlocked run B |
|---|---:|---:|---:|
| FP16 (effective TFLOPS) | 101.303 | 171.552 (+69.3%) | 168.488 (+66.3%) |
| BF16 (effective TFLOPS) | 101.398 | 174.711 (+72.3%) | 170.911 (+68.6%) |

A subsequent normal Windows restart **without the USB unlock step** returned to stock-like results. The improvement was **not persistent across that observed restart**. A later **RUN06** confirmed another successful USB-first Windows handoff, but **no distinct RUN06 benchmark was saved**.

These are *device-resident matrix-multiplication* measurements, not claims about gaming FPS, LLM token speed, general application performance, numerical correctness, or long-term stability. See [results and methodology](docs/RESULTS.md).

## Start here

1. **[Our adaptations](docs/ADAPTATION.md)** — the upstream assumptions we had to revisit and what the real boot attempts taught us.
2. **[Research workflow, logging and safety](docs/WORKFLOW.md)** — a practical checklist for owners investigating their *own* board, including cancellation and recovery boundaries.
3. **[Results and limitations](docs/RESULTS.md)** — what was measured and what remains unverified.
4. **[AI reader guide](AI-READER.md)** — a short evidence-first protocol for an AI helping someone interpret this research.
5. **[Upstream research and credits](REFERENCES.md)** — the original projects, contributors and license distinctions.

## What this repository is — and isn't

- **Includes:** original case-study writing, board-adaptation rationale, selected sanitized observations, validation checkpoints and performance methodology.
- **Does not include:** unlock-capable EFI binaries, proprietary firmware assets, GPU ROM/PROM dumps, private raw logs, device-specific memory addresses, or a universal patch set.
- **Scope:** unlock-related compatibility, failure analysis, logging, manually authorized boot flow and measured compute improvement — not general PC troubleshooting.

The foundational unlock technique is **upstream work**, not an invention of this repository. In particular, the Windows UEFI starting point came from [TOTORONG/AD103_win_unlocker](https://huggingface.co/TOTORONG/AD103_win_unlocker), which documented a *modified non-SUPER RTX 4080 with 32 GB*; see [REFERENCES.md](REFERENCES.md) for the broader source lineage.

## License and attribution

Original explanatory text in this repository is licensed **CC BY 4.0** — reuse and adaptation are welcome with appropriate credit and an indication of changes. See [LICENSE](LICENSE) for the full terms and [LICENSE-SCOPE.md](LICENSE-SCOPE.md) for which material is covered.

The original unlock research and Windows UEFI workflow belong to their respective upstream authors; linking to or discussing those works does **not** relicense their code or documentation. See [REFERENCES.md](REFERENCES.md) for attribution and third-party licensing distinctions. README-embedded images are not included in the CC BY 4.0 grant unless explicitly licensed separately.

**Research status:** Successful hardware-specific Windows handoff and in-session compute improvement on one card; compatibility with other cards, repeated-boot reliability, numerical correctness and sustained stability are **not established**.
