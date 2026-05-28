# Agent Instructions — Decommissioned

Decommissioned is a Unity social-deduction VR game for Meta Quest that serves as a reference and template for multiplayer VR experiences using the Meta XR, Interaction, Avatars, and Platform SDKs together with Photon Voice / Photon Realtime and Unity Netcode for GameObjects. A published version is on the [Horizon Store](https://www.meta.com/en-gb/experiences/decommissioned/5756827011021749/).

## Source-of-truth files (read these first, do not duplicate their contents in this file)

For setup, build steps, SDK versions, and project layout, read:

- `README.md` — official setup, dependencies, and editor-play instructions
- `Documentation/Configuration.md` — Meta Quest + Photon configuration (App IDs, Data Use Checkup, Photon AppIDs)
- `Documentation/CodeStructure.md`, `Documentation/Multiplayer.md`, `Documentation/Avatars.md`, `Documentation/Armbands.md` — system-level docs
- `ProjectSettings/ProjectVersion.txt` — pinned Unity editor version
- `Packages/manifest.json` — Unity package versions (Meta XR Core, Interaction, Avatars, Platform, etc.)
- `.gitattributes` — Git LFS filters; run `git lfs install` before cloning
- `LICENSE` — license terms (MIT for most of the project; embedded packages have their own)

## Quest / Horizon-specific notes

- Photon Voice 2 and the `com.community.netcode.transport.photon-realtime@<sha>` package are embedded under `Packages/` because they have been **modified**. Do not "upgrade" by bumping versions — re-import from the Asset Store and re-apply the patches.
- The URP version in use is the **Application SpaceWarp (ASW) fork** of URP. Replacing it with stock URP will break ASW and frame timing.
- Never commit your Meta or Photon App IDs / API keys — `Documentation/Configuration.md` is the per-developer setup contract.
- The bundled XR FPS Simulator captures the mouse during play mode; hold **Left Alt** to release it. See `Packages/com.meta.utilities.input/README.md#mouse-capture`.

## Meta Quest tooling

This repository is part of the Meta Quest / Horizon OS ecosystem (a sample, library, template, or related project — the bespoke intro above describes which). Use that intro and the source-of-truth files it references for project-specific decisions; don't restate or invent facts from memory.

When the user asks anything about Quest device behavior, build / deploy / debug / capture flows, on-device performance, or Horizon OS APIs, reach for these tools instead of generic Unity answers:

- **`hzdb`** — Quest-aware ADB wrapper (device list, install / launch / stop, logs, screenshots, Perfetto traces, on-device docs search). Already wired up as an MCP server via `.mcp.json`, `.vscode/mcp.json`, and `.cursor/mcp.json`. Also runnable directly: `npx -y @meta-quest/hzdb <subcommand>`.
- **Meta Quest Agentic Tools** — the full skill set, including Unity-specific skills: [github.com/meta-quest/agentic-tools](https://github.com/meta-quest/agentic-tools). Install per your client (Claude Code: `/plugin install meta-vr@meta-quest`; Gemini CLI: `gemini extensions install https://github.com/meta-quest/agentic-tools`; Cursor / VS Code: install the **Meta Horizon** extension from the Marketplace).

A few behavior expectations:

- **Read this repo's files first.** Before answering anything project-specific, read `README.md` and whichever source-of-truth files the intro above points at. Don't restate their contents in chat — quote or link instead.
- **Use `hzdb` for device-side work.** Anything that touches an attached Quest (install, launch, logs, screenshot, capture, manifest inspection) goes through `hzdb`, not raw `adb`.
- **Check live Horizon OS docs before answering API questions.** `hzdb docs search "..."` queries the live docs; training data on Horizon OS APIs goes stale fast.
- **Don't fabricate SDK / engine versions.** If a version isn't visible in this repo's files, say so rather than guessing.
