<p align="center"><strong>EN</strong> | <a href="REFERENCES.zh-CN.md">中文</a></p>

# Research Sources and Attribution

This repository is **independent adaptation research**. It does not claim invention of the original GPU compute-unlock mechanism or of the foundational Windows UEFI workflow.

## Primary references

| Source | Contribution to the research lineage |
|---|---|
| [Zagitta/gpu-unlock](https://github.com/Zagitta/gpu-unlock) | Foundational GPU compute-unlock research and code lineage |
| [JustAResearcher/gpu-unlock-ada](https://github.com/JustAResearcher/gpu-unlock-ada) | Ada-generation unlock research and community findings |
| [RTX 4080 SUPER ASUS success report, issue #70](https://github.com/JustAResearcher/gpu-unlock-ada/issues/70) | Independently reported 16 GB ASUS AD103 Windows UEFI experiment; a useful **different-board reference**, not proof of Gainward compatibility |
| [TOTORONG/AD103_win_unlocker](https://huggingface.co/TOTORONG/AD103_win_unlocker) | Direct Windows UEFI research starting point: preloaded Windows Boot Manager, manual confirmation, logging, graphics recovery and handoff, demonstrated on a **modified non-SUPER 32 GB RTX 4080** |
| [WildFlash1st/cmp90hx-unlock](https://github.com/WildFlash1st/cmp90hx-unlock) | Related CMP/GA102 firmware research in the broader source/reference lineage |

### Other background

- [TianoCore EDK2](https://github.com/tianocore/edk2) — UEFI development interfaces and headers used by the research lineage.
- NVIDIA's public open-kernel-module materials and related firmware-analysis work informed prior projects; that does **not** grant permission to redistribute proprietary NVIDIA firmware assets.

## What this project independently documents

Our new contribution is a **hardware-specific study** of one Gainward RTX 4080 SUPER 16 GB: board/memory compatibility investigation, multi-child UEFI graphics ownership, strict post-GOP handoff checks, varying initial-state admission, USB-first Windows discovery, fail-closed logging/recovery, physical RUN00–RUN06 observations and sanitized FP16/BF16 benchmark results.

Where a behavior was inherited — especially the actual compute-unlock technique, manual `U` authorization and Windows handoff concept — we credit upstream. A different board's success is **not** presented as independent proof of compatibility on ours.

## License and publication boundaries

- The underlying **GPL-2.0-only-derived unlock source** and its modifications carry applicable upstream obligations if distributed. This documentation-only repository does **not** include that code or an EFI binary.
- TOTORONG's **new narrative documents** specify **CC BY-NC 4.0** to the extent of the author's rights. This repository uses independently written prose and links to the original documents instead of copying them wholesale.
- Other upstream material may carry its own notices. Link and attribute the source; do not assume a single license covers everything.
- Independently authored documentation text in **this repository is now licensed under [CC BY 4.0](LICENSE)**, subject to the material ownership and upstream exclusions in [LICENSE-SCOPE.md](LICENSE-SCOPE.md). This does not override any original author's separate license.
- Do not upload private firmware binaries, raw ROM/PROM dumps, machine-specific logs, full research-directory history or unreviewed executable payloads.

Sources are included for **credit, context and further reading**, not as a claim that their authors reviewed or endorsed our Gainward experiment.
