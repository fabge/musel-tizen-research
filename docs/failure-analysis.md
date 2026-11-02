# Failure analysis

## What happened

After the successful volatile root demonstration, work moved to an automatic-root experiment. The experiment performed additional live-kernel memory changes while repeatedly spawning processes to stimulate PID 1. The TV crashed and subsequently failed to boot normally.

This later experiment is not part of the verified root result. The two events must not be collapsed into either “root never worked” or “root safely worked and autoroot was merely unfinished.”

## What the retained command history supports

The reviewed trace contained no deliberate raw eMMC, boot-partition, MTD, or SPI-flash write and no installed startup persistence. Persistent changes had nevertheless occurred earlier, including a hosts-file replacement and temporary read/write mounting of the root filesystem.

Absence of a deliberate flash-write command is not proof that flash or boot state was undamaged. A kernel crash, an unintended physical-memory write, filesystem state, and independent board failure were not conclusively separated.

## What remains unknown

- The exact corrupted object or operation that caused the panic.
- Whether the non-boot state resulted from memory corruption, persistent storage state, or an independent hardware failure.
- Whether a different recovery path could have restored that board.
- Whether any part of the autoroot approach could be made reliable.

The investigation had no complete recovery image. That prevents a confident diagnosis and makes destructive reproduction unjustifiable.

## Operational conclusions

- Do not rerun the historical autoroot payload.
- Do not automate a physical-memory writer merely because a manual root demonstration succeeded.
- Do not treat a full Linux capability mask as protection against invalid memory access or mandatory access control.
- Do not infer persistence from a read/write mount.
- Obtain a recovery baseline before persistent or high-frequency kernel modifications.
- Keep entry, privilege transition, observation, persistence, and autoroot as separately reviewed stages.

The successful root demonstration remains valid. The operational mistake was extending it into aggressive automation without an adequate recovery position.

## Hardware continuity

The investigation later involved a donor/replacement-board path. Any current television state belongs to that board, not to the storage and device identity used for the original root proof. The old failure and the current board's capabilities need separate records.
