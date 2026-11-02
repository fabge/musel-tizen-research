# Compatibility

## What was actually tested

| Target | Firmware/platform | Result |
|---|---|---|
| Samsung UE50RU7179UXZG | T-MSLDEUC-1500.9, MUSE_L, Tizen 5.0, ARMv7, kernel build dated 2 December 2024 | Volatile UID/GID 0 demonstrated once through the documented chain |
| Samsung UE50RU7172, reported by a third party | Sibling MUSE_L/firmware research | Source of leads and reported negative browser results; not a reproduction of this repository's complete chain |
| Samsung UE50RU7099 | T-MSLDEUC family | No validated result in this repository |
| Q60T, Q70R, QN90B/QN90F, and other public-root targets | Different platforms and chains | Prior art only |

The RU7179 and RU7099 names are easy to conflate. They must be tracked as different devices until the current board has been fingerprinted and tested independently.

## Why the firmware number is insufficient

`1500.9` is a firmware release identifier, not a universal memory layout or Tizen version. Compatibility depends on at least the firmware family, exact build, kernel binary, SoC/platform, driver behavior, and board configuration.

Even on the tested device, accessible physical ranges, stale mappings, and live object locations made static assumptions unreliable. Copying an offset or payload to another unit can crash its kernel or corrupt live state.

## Replacement boards and DUIDs

A replacement mainboard brings different storage and a different device identity. Root state, installed probes, developer-certificate bindings, and files modified on an earlier board do not carry over merely because the television chassis is unchanged.

Any replacement board must start with a fresh read-only fingerprint and a new compatibility assessment.

## Persistence claims

The Q60B/Tizen 6.5 untethered chain encountered during related research does not establish persistence on MUSE_L/Tizen 5.0. No untethered or autoroot solution for the RU7179 is claimed here.
