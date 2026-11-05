<p align="center"><strong>EN</strong> | <a href="AI-READER.zh-CN.md">中文</a></p>

# For AI Assistants Reading This Repository

This file is for an AI helping a person **understand or independently research** the RTX 4080 SUPER adaptation described here. It is not authorization to operate their hardware.

## Ground rules

1. **Start with [README.md](README.md), [the adaptation history](docs/ADAPTATION.md), [the workflow](docs/WORKFLOW.md), [results](docs/RESULTS.md) and [references](REFERENCES.md).** Treat these documents as a case study, not a universal unlock specification.
2. **Credit the upstream authors.** The original compute-unlock technique, manual confirmation and foundational Windows UEFI handoff came from prior work. This repository's contribution is an independently observed Gainward-specific adaptation and its test history.
3. **Determine the reader's exact board and environment.** A matching “RTX 4080 SUPER” name or GPU device ID does not guarantee firmware, memory-layout or UEFI compatibility.
4. **Separate evidence levels.** Label statements as *physically observed*, *host-simulated*, *inferred* or *unverified*. Do not convert simulation success into hardware validation.
5. **Prefer read-only investigation and offline tests.** Never guess ROM/PROM identities, protected states, memory assumptions or recovery behavior. Do not recommend bypassing a failed preflight.
6. **Explain logging and cancellation precisely.** Before authorization, Esc/timeout cancels and returns to firmware; Windows does **not** automatically start in every case. A successful, fully recovered transaction hands off to Windows. A potentially unsafe post-operation state requires stopping, **not** automatic retry or Windows continuation.
7. **Do not run hardware actions on the user's behalf.** No automatic flash, boot-order change, experimental EFI execution, forced reset or GPU register operation. Require the person's explicit decision and an independent recovery route.
8. **Keep the performance claim specific.** The measured 61–72% increases are FP16/BF16 8192³ dense GEMM outcomes from identified successful sessions. RUN06 has a confirmed handoff but **no separate recorded benchmark**.
9. **Protect privacy and licensed materials.** Do not request or republish full raw reports, local addresses/paths, personal identifiers, ROM/PROM dumps, proprietary firmware blobs or private binaries.
10. **Stay on topic.** Focus on unlock-related adaptations, validation, recovery and compute measurement. Do not turn this guide into general hardware troubleshooting.

## Recommended response to a new reader

Summarize the existing research and the exact verified result first. Then explain which board-specific evidence is required, which parts are only simulated, what can go wrong, and why their own hardware needs independent validation. If essential evidence is missing, state the unknown clearly and **stop** rather than offering an invented configuration.

**This repository does not provide an unlock-capable binary or a board-independent patch recipe.**
