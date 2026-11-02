# Root chain

## Verified target

The successful demonstration used a Samsung UE50RU7179UXZG, `19_MUSEL_UHD_BASIC`, Tizen 5.0, ARMv7, firmware T-MSLDEUC-1500.9. The exact tested kernel identified itself as:

```text
Linux Samsung 4.1.10 #1 SMP PREEMPT Mon Dec 2 20:43:49 KST 2024 armv7l
```

These details matter. A matching marketing firmware number on another board is not enough to reuse addresses or payloads.

## Entry point

The TV supported owner-enabled developer mode and installation of a developer-signed application. Retail SDB exposed package and file-transfer operations but no general shell. The later SVE-2025-50109 `appinstall` injection channel returned `closed` on this device.

A custom .NET application therefore supplied the initial owner-authorized code-execution context. This avoided relying on an unpatched browser vulnerability or on an unauthenticated network service.

## Physical-memory primitive

The application obtained physical-memory access through Samsung's `/dev/sdp_mem` interface, a vendor-driver class previously documented on other Samsung TVs. On this MUSE_L unit, the usable mapping behavior had important constraints:

- `0x40000000–0x60000000` was blocked by an interface guard.
- Access above the blocked interval was possible.
- Invalid or insufficiently guarded accesses could raise `SIGBUS`.
- The same linear physical address could expose a current page and a stale or mirror-like page. Agreement with the running kernel was the useful test; bytes from one mapping alone were not reliable validation.
- Static addresses borrowed from another kernel build were not safe anchors.

These observations explain why a payload could have real physical-memory access yet still fail to locate a stable object.

## Task discovery

The successful application located its own task and walked neighboring task structures. During the demonstrated run it identified several hundred task records.

A static `init_task` symbol from another build was tried during earlier work but was not a dependable anchor. Live task validation and known relationships between objects were more useful than assuming symbol addresses from a sibling unit.

The tested task structure placed the pointer to its credential object at offset `0x26c`. The credential objects themselves were observed below the interface's accessible region. That defeated the straightforward plan of directly changing UID fields in a credential.

## Successful privilege transition

The final chain used a different data-only strategy:

1. Locate a worker thread belonging to a live UID-0 daemon.
2. Validate the worker using live task relationships and privileged-memory access checks.
3. Replace the worker's credential pointer with the daemon's live credential pointer.
4. Have that process invoke `capset` after the credential change.

The result was UID/GID 0, SMACK context `System`, and `CapPrm`/`CapEff` set to `0000003fffffffff`. The original output is preserved in the evidence directory.

This was a per-boot, in-memory transition. It did not reflash the TV, install a startup service, or establish persistence.

## What UID 0 did not solve

Root was not equivalent to unrestricted control of the Tizen platform:

- SMACK still constrained access.
- Tizen zone boundaries continued blocking some cross-zone operations.
- UEP signed-executable enforcement remained relevant.
- Some files that appeared accessible still could not be executed.
- Mounting the root filesystem read/write worked during the rooted session, but that did not make arbitrary persistent changes safe or bootable.

The useful lesson is that kernel privilege, mandatory access control, application sandboxing, and boot-chain trust must be analyzed separately.

## Relationship to other public chains

This was not the Q70R USB-root image, the Synacktiv Q60T browser chain, or the newer SDB archive-root chain. Those projects informed the research, but their delivery assumptions did not directly fit this television.

The distinguishing result here is the owner-sideloaded application delivery combined with MUSE_L-specific live task discovery and credential borrowing. It should not be described as a generic Tizen 5.0 root.

## Reproduction status

Only one device and one exact firmware build completed the full chain. No persistence, safe autoroot, or multi-device reproduction was established. The later autoroot experiment is documented separately because it must not be confused with the verified root demonstration.
