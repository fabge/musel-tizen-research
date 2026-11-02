# Samsung MUSE_L / Tizen 5.0 research

Owner-authorized security and privacy research on a Samsung **UE50RU7179UXZG** television running **Tizen 5.0**, firmware **T-MSLDEUC-1500.9**, on the 2019 **MUSE_L** platform.

The headline result is real but narrow: **volatile UID/GID 0 with full permitted and effective capabilities was demonstrated on 25 October 2026**. The proof is preserved in [`evidence/root-session-proof.txt`](evidence/root-session-proof.txt). This was not a persistent jailbreak, a complete bypass of Tizen's security boundaries, or a safe, reusable rooting tool.

This repository publishes the research record, negative results, privacy findings, and failure analysis. It does **not** currently ship an exploit, proprietary firmware, credentials, or the unsafe autoroot experiment.

## Read first

- [Root chain](docs/root-chain.md): how access was obtained and what the result does and does not prove.
- [Platform findings](docs/platform-findings.md): tested interfaces, dead ends, and applicability to other research.
- [Compatibility](docs/compatibility.md): the exact tested target and why nearby model or firmware numbers are insufficient.
- [Privacy and debloating](docs/privacy-and-debloating.md): settings, network blocking, and the dependency problem for native apps.
- [Failure analysis](docs/failure-analysis.md): the later crash, what is known, and what remains unknown.
- [Timeline](docs/timeline.md): the chronology, including wrong turns.
- [References](docs/references.md): related public research and sources.

## Results in brief

- Developer-mode application sideloading worked, but retail SDB exposed no general shell.
- The later public SDB `appinstall` injection route was closed on this TV's plugin.
- A custom application could use the vendor physical-memory device to reach kernel objects.
- Static physical addresses and static credential validation proved unreliable.
- The successful final step borrowed a live privileged credential through a worker task rather than depending on a fixed credential address.
- UID 0 did not remove SMACK, zone, or signed-executable restrictions.
- Root was per-boot. No persistence was established on this model.
- A later autoroot experiment crashed the kernel and preceded a non-booting TV. Its precise causal role in the final hardware state is unresolved.
- Samsung ACR, advertising, and telemetry hosts were blocked through a root-deployed hosts file, but this did not prove that all Samsung collection had stopped.

## Scope and status

This was research on privately owned hardware. It is published so others can learn from both the successful result and the mistakes. It is **not** a compatibility claim for other MUSE_L televisions, including the similarly named RU7099, and it is not an invitation to run historical payloads.

There is no supported installation procedure here. A future safe release would need reproducible read-only checks, exact-build fingerprinting, a recovery strategy, and substantially more validation.

## Contributing

Additional evidence is welcome, especially exact platform/firmware fingerprints, non-destructive reproductions, correction of reported third-party claims, and recovery research. See [CONTRIBUTING.md](CONTRIBUTING.md). Do not submit device identifiers, credentials, proprietary firmware, or unreviewed destructive payloads.

## License

MIT; see [LICENSE](LICENSE). Third-party research remains under its respective license and is linked rather than vendored.
