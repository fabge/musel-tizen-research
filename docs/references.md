# References and related work

These projects and publications informed the investigation. Their target compatibility must be evaluated independently.

## Samsung TV exploitation and teardown

- [Synacktiv: Samsung Q60T exploit](https://github.com/synacktiv/samsung-q60t-exploit) and [GreHack 2021 slides](https://www.synacktiv.com/sites/default/files/2021-11/GreHack2021_Rooting_Samsung_Q60T_Smart_TV.pdf): browser-to-kernel chain and `/dev/sdp_mem` prior art on a different target.
- [Chris Ritsen: samsung-tv-root](https://github.com/chris-ritsen/samsung-tv-root): later SDB/archive-root research; its expected initial channel was closed on this MUSE_L target.
- [Luminger: samsung-tv-usb-root](https://github.com/Luminger/samsung-tv-usb-root): a hardware-verified root package for its documented Q70R target, not a MUSE_L solution.
- [Reversec/WithSecure: Opening up the Samsung Q60 series Smart TV](https://labs.reversec.com/posts/2019/12/opening-up-the-samsung-q60-series-smart-tv): teardown, SDB, firmware, storage, and recovery research on another 2019 model.
- [SamyGO MUSE_L sibling-model thread](https://forum.samygo.tv/viewtopic.php?t=14654): third-party experiments and reports used as leads during the investigation.
- [Bishop Fox: Samsung Tizen SDB research](https://bishopfox.com/blog/samsung-tizen-os-version-through-9-0): SVE-2025-50109 and later-generation SDB attack surface.
- [Codex hacked a Samsung TV](https://blog.calif.io/p/codex-hacked-a-samsung-tv): related vendor physical-memory driver research on a different platform.

## Browser and platform context

- [Samsung Smart TV web-engine specifications](https://developer.samsung.com/smarttv/develop/specifications/web-engine-specifications.html): browser-engine generation by Tizen TV release.
- [Pwn2Own Tokyo 2019, day one](https://www.thezdi.com/blog/2019/11/6/pwn2own-tokyo-2019-day-one-results): public evidence that the 2019 TV browser generation had been exploited under contest conditions; no reusable MUSE_L chain follows from that result.

## ACR and privacy

- [Watching the Watchers research artifacts](https://github.com/IlgarNEU/Watching-the-Watchers): academic smart-TV ACR network research and endpoint observations. Device-specific behavior still requires local measurement.
- [Samsung support](https://www.samsung.com/de/support/): official model and firmware information; support pages vary by market and model.

## Attribution boundary

The custom MUSE_L application delivery, observed mapping behavior, live-task strategy, and final credential-borrowing demonstration were developed during this investigation. Public projects supplied important background and earlier primitives. No third-party source tree, firmware, signing material, or binary payload is redistributed here.
