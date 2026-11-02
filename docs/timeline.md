# Research timeline

Dates reflect the retained investigation notes. Earlier public research is linked from the references page.

## 18 October 2026 — platform reconnaissance

Initial research surveyed the 2019 Tizen 5.0 attack surface, developer mode, SDB, browser engine, network services, firmware format, hardware routes, and public Samsung TV exploit chains. No working root had yet been demonstrated.

## 22–23 October 2026 — applicability testing

The target's SDB capabilities were measured. The newer public `appinstall` injection route was found closed on plugin `3.7.1_TV_REL`. A sideloaded application became the preferred owner-authorized delivery mechanism.

Research into vendor physical-memory drivers and sibling MUSE_L work led to the custom probe chain. Early failures established that a raw mapping primitive was not enough: access guards, invalid addresses, stale pages, and incorrect static anchors all mattered.

## 25 October 2026 — verified volatile root

The chain discovered live tasks and used a worker associated with a privileged daemon to borrow live credentials. At 20:53, the retained proof showed UID/GID 0, SMACK `System`, and full permitted/effective capabilities.

A hosts-file block was deployed during rooted work. Root remained volatile, and Tizen's zone, SMACK, and UEP restrictions were still observable.

## Later autoroot work — crash

A separate autoroot experiment modified live kernel memory while spawning processes rapidly. The TV crashed and entered a non-booting state. No complete recovery dump existed. The exact cause of the final hardware state was not established.

The follow-up review rejected the earlier claim that a robust, reproducible autoroot had been achieved and warned against running the old payload again.

## Replacement-board phase

The investigation moved to donor/replacement-board work. This reset assumptions about installed files, certificate binding, root state, and device identity. A similarly named RU7099 target must not be silently substituted for the original RU7179 result.

## Current public status

The repository documents a successful research proof and a failed operational extension. It does not provide a persistent jailbreak, a safe installer, proof of complete Samsung data elimination, or compatibility with other models.
