# Privacy and debloating

## Goal

The investigation aimed to keep native Plex, Prime Video, ARD Mediathek, and ZDFmediathek usable while removing Samsung ACR, advertising, telemetry, recommendations, account integration, and related services.

Root and privacy are related but separate goals. UID 0 provides an opportunity to change the system; it does not identify every collector, prove that collection has stopped, or make arbitrary package removal safe.

## Settings already applied

The following were configured during the investigation:

- ACR / Viewing Information Services disabled.
- Interest-based advertising disabled.
- Additional Samsung terms, including the supplemental privacy notice, declined.
- No Samsung account signed in.
- Automatic Smart Hub application updates disabled, followed by a reboot.

These are useful controls but not proof of zero collection. Independent academic research has reported ACR-like network behavior after opt-out on a tested Samsung/Tizen device; that result should not be generalized to every model without measurement.

## Hosts-file blocking

A Samsung ACR/ads/telemetry blocklist was deployed to `/etc/hosts` during the rooted session. A sanitized copy is in [`config/hosts.samsung-blocklist`](../config/hosts.samsung-blocklist).

The deployment proves that a local block was installed. It does not prove complete coverage, persistent enforcement after reboot or replacement-board service, or absence of direct-IP and alternate-channel traffic. Some entries were broad research candidates rather than endpoints individually confirmed on this television.

Blocking all Samsung infrastructure indiscriminately is likely to break firmware updates, application services, DRM-related dependencies, time synchronization, or other platform functions. Changes should be incremental and tested against real application playback.

## Why package deletion is risky

The native applications still depend on Tizen's application framework, launcher/package manager, networking, media pipeline, codecs, and—especially for Prime Video—DRM components. Package names such as `org.tizen.*` or `com.samsung.*` do not distinguish disposable Samsung cloud features from required local platform services.

A service-by-service dependency map and reversible changes are preferable to a generic removal list. Ordinary SDB uninstall support for third-party packages does not imply that protected platform packages can or should be removed.

## Stronger privacy architectures

The only straightforward strong guarantee against future Samsung network collection is to keep the Samsung TV offline and use an external application device. Merely adding an external streamer while leaving the TV online is weaker because smart-TV ACR may inspect HDMI input.

If native Tizen applications are mandatory, the realistic objective is reduced Samsung processing with measured network controls, not an unsupported promise of complete independence.

## Recommended measurement model

Before and after each change, compare destinations, timing, and upload volume during:

- Idle Smart Hub use.
- HDMI input with controlled on-screen content.
- Each required streaming application.
- Offline/LAN-isolated operation.

DNS logs alone are insufficient. They miss direct-IP traffic and may miss encrypted DNS. Prefer controlled egress, destination capture, and application-level functional tests.

Local blocking cannot erase data already collected or change server-side retention. Account deletion and Samsung-side records are separate processes.
