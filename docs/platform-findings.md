# Platform findings and dead ends

This page separates measurements on the UE50RU7179 from reports about sibling televisions. A negative result is specific to the tested interface and firmware; it is not a proof that the whole platform is secure.

## SDB and developer mode

Measured on the target:

- Developer-mode application installation worked with a certificate bound to the TV.
- SDB reported version 2.2.31 with plugin `3.7.1_TV_REL`.
- `sdbd_rootperm`, `rootonoff`, `intershell`, and `appcmd` support were disabled.
- Package listing, DUID retrieval, ordinary application uninstall, and file push worked through their supported paths.
- General shell commands and the later public `appinstall` injection channel returned `closed`.
- The SDB core version alone did not predict whether a TV plugin exposed an injection-capable verb.

An `appuninstall` command-injection test was proposed but was not established as a working route. It should not be listed as a vulnerability in this firmware.

## Browser and web runtime

The platform used SamsungBrowser 2.2 with a Chromium 63/V8 6.3-generation engine. Consequently, WebKit/JSC jailbreak techniques were structurally irrelevant.

The Synacktiv Q60T chain was valuable prior art, but its CVE-2020-6383 browser stage could not simply be copied to this older engine. Reports from a sibling MUSE_L unit said CVE-2020-6383, CVE-2018-6065, and CVE-2018-17463 probes did not produce the expected result. Those are third-party results, not independent measurements on this TV.

No browser exploit was needed for the successful root demonstration.

## Network services

Research and sibling-model reports covered the remote API on ports 8001/8002, DIAL/web service on 8080, UPnP/DLNA services, screen sharing, and SDB on 26101.

The useful conclusions were limited:

- The remote API exposed device metadata and a user-approved remote-control channel, not a shell.
- DIAL application launching did not provide the desired arbitrary browser-URL delivery on the reported sibling unit.
- No public command-injection or code-execution result was established for the enumerated retail services on this exact target.
- A closed or filtered port on one model must not be generalized to every Tizen television.

## Kernel and vendor drivers

The successful privilege escalation used a vendor physical-memory interface rather than a generic Linux 4.1 exploit. Kernel age alone was a poor predictor: Samsung backports fixes without necessarily changing the upstream version string.

Generic possibilities such as Dirty COW remained hypotheses, not verified routes. The meaningful result on this device was the behavior of `/dev/sdp_mem`, including its guarded address interval and the unreliability of naive static physical-memory assumptions.

## Firmware and recovery research

Public Q60T firmware-decryption material did not decrypt T-MSLDEUC images. No MUSE_L release key or decrypted recovery image was available in this investigation.

Reports about other 2019 Samsung boards described unencrypted eMMC contents and VDFS root filesystems, but no full recovery dump was obtained from this television before the failure. That missing recovery baseline became the central operational limitation.

## Techniques ruled out or found inapplicable

- Android/Google TV ADB debloat scripts: wrong operating system.
- Pre-Tizen SamyGO telnet methods: different platform generation.
- Tizen mobile, wearable, and TizenRT CVEs: different products or components.
- Host-side SDB client vulnerabilities: attack the development computer, not the TV.
- Public Q70R USB-root artifacts: different validated target and firmware family.
- Public newer-TV SDB archive-root chains: their initial injection channel was closed here.
- iOS-era WebKit/JSC exploits: wrong browser engine.

## Research lessons

The most transferable findings are methodological:

1. Fingerprint the exact board, firmware, and kernel build.
2. Distinguish a supported SDB operation from a general shell.
3. Treat sibling-model reports as leads, not measurements.
4. Validate live kernel objects instead of trusting one static address.
5. Separate root, SMACK, UEP, zones, mounts, and persistence into different milestones.
6. Establish recovery before automating a physical-memory writer.
