# Contributing

Corrections and independently obtained evidence are welcome.

## Evidence standard

Label each claim as one of:

- **Measured:** directly observed on an identified target and exact firmware/kernel build.
- **Reported:** obtained from a named third-party source but not independently reproduced.
- **Inferred:** a conclusion from measurements, with the reasoning and uncertainty stated.
- **Hypothesis:** a proposed explanation or untested route.

Include the model, board/platform, complete firmware string, kernel build, and whether the observation survived a reboot. Do not silently turn a sibling-model result into support for another model.

## Safety and privacy

Research only hardware you own or are authorized to test. Do not submit credentials, DUIDs, certificates, private network addresses, personal data, proprietary firmware, or copied vendor binaries. Do not submit payloads intended for destructive persistence or unauthenticated remote access.

Changes that write physical memory, remount system filesystems, alter boot state, or remove platform packages require particularly strong justification and a recovery plan. A successful read-only probe does not validate a writer.

## Scope

The most valuable contributions are reproducible fingerprints, corrections to compatibility claims, recovery research, application-dependency observations, and network measurements with clearly stated methods.
