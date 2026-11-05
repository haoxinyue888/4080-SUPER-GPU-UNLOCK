# Research Workflow, Logging and Boot Safety

For RTX 4080 SUPER owners researching a similar adaptation, this is a **decision workflow**, not a validated universal instruction to execute an EFI image. The implementation described in this repository was tested on **one Gainward 16 GB card**.

**Risk:** Experimental GPU firmware operations may cause loss of display, boot failure, data loss or hardware damage. An offline test pass is not hardware certification. Never automate a hardware-changing operation from an AI response.

## 1. Establish the reference and your own hardware

- Read the [original projects](../REFERENCES.md) and distinguish an Ada GPU study, a particular Windows UEFI port, and an independent success report.
- Identify the actual GPU model, board/vendor revision, memory configuration, firmware view and UEFI environment.
- Start with **read-only inspection**. Record what was physically measured; do not use someone else's card-specific configuration as a default.
- Compare observations with the upstream implementation's assumptions. A matching marketing name alone is insufficient.
- If a required identity, firmware, graphics-driver ownership or memory-layout check is unknown, **stop rather than guess**.

## 2. Reproduce the research offline first

- Define precisely which assumptions need adaptation for the board. Keep the original GPU-unlock mechanism credited to its authors.
- Preserve independent identity, resource-containment and hardware-recovery checks.
- Simulate **success, refusal, missing device/loader, unexpected graphics ownership, logging failure and unsuccessful recovery** before considering a physical experiment.
- Do not assume a simulated successful boot proves real firmware behavior. Do not disable a failing guard just to proceed.

## 3. Prepare logging and recovery

Our experimental UEFI application wrote a **new numbered `RUNnn/REPORT.TXT`** for each launch. Each report recorded stage checks, important readbacks, attempt state, recovery evidence and a final status. Existing runs were not overwritten.

Before any physical test, ensure:

- Reports can be written and flushed reliably; failures to log should prevent an experiment from starting.
- The original, unmodified Windows Boot Manager remains independently bootable.
- A known working, non-experimental boot path and a recovery plan are available.
- The experimental image and any required locally obtained assets are verified against their intended fingerprints.
- The person at the machine understands that a post-operation failure may require **physical power-off**, not a software retry.

**Do not publish raw reports.** They can contain local hardware addresses, device paths and other host-specific details. Share only manually reviewed, redacted observations.

### How to read a report

These final-state fields were particularly useful in our case:

| Field / observation | Interpretation |
|---|---|
| `stage` | Where validation or execution ended |
| `attempted=0` | No GPU unlock transaction began |
| `driver_release=0` | UEFI graphics-driver ownership was not released |
| `clean=1` | The program reported its required cleanup conditions as satisfied; **not** a universal safety certificate |
| Windows loader discovery and preload status | Whether a valid Windows boot image was available before any GPU operation |
| Post-recovery and handoff status | Whether the experimental flow could continue toward Windows |

A success marker or register readback **alone** does not establish a compute-speed improvement; use a separate Windows benchmark.

## 4. Manual authorization and the three outcomes

**The manual `U` confirmation and the concept of Windows UEFI handoff already existed in the upstream TOTORONG implementation.** We retained that model and adapted validation/recovery to our hardware.

| Situation | Observed or implemented behavior |
|---|---|
| **No authorization / Esc / 30-second timeout, before GPU work** | The application cancels and returns control to UEFI firmware without beginning the GPU transaction. **Automatic Windows startup is not guaranteed.** |
| **Preflight refusal** | The refusal is logged. The user can inspect it and return to firmware; the GPU transaction does not start. |
| **Successful manually approved operation** | After required GPU/resource/graphics recovery checks, the application launches the preloaded Windows Boot Manager. |
| **Unsafe state after graphics-driver release or hardware work** | The application **halts**, rather than guessing that Windows can boot safely. Follow the physical recovery instruction; do not automatically repeat the experiment. |

**USB-first boot is separate from unattended unlock.** Even when UEFI is configured to offer the USB first, the experimental GPU operation still requires an explicit, local `U` keypress. The existing Windows boot entry should remain untouched.

Our RUN06 verified the successful first-scan Windows discovery and handoff. It **did not** physically exercise the extra delayed-discovery/storage-connection fallback; those paths were tested in simulated host scenarios.

## 5. Measure the specific effect — then report uncertainty

- Record a stock dense-GEMM baseline and use the same multiplication and timing method after the experimental boot.
- Repeat postboot measurements instead of reporting a single peak.
- Distinguish firmware progress, successful Windows boot and measured compute improvement as **three separate claims**.
- Note behavior after an ordinary restart. In our case, a restart without the unlock step returned performance to stock-like levels.
- Clearly label untested boards, reboot reliability, sustained stability and application-level benefits as **unverified**.

See [our adaptation history](ADAPTATION.md), [benchmark details](RESULTS.md) and [the AI reader guide](../AI-READER.md).
