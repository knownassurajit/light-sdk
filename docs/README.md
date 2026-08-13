# 📖 Light SDK Documentation Index (`light-sdk/docs`)

Welcome to the technical documentation library for the **Light SDK** platform. This directory contains technical guides, system setup instructions, metadata specifications, and architectural decision records for building applications on the Light Phone III.

---

## 🗺️ Documentation Directory Map

| Document | Topic & Focus |
|---|---|
| 📱 [**System App Setup Guide**](./system_app/README.md) | Step-by-step instructions for running the `:sdk:emulator` app as a privileged UID 1000 system app on an Android Virtual Device (AVD). Includes AOSP platform test key generation instructions (`platform.jks`), `adb remount` configuration, and launcher setup. |
| 🏷️ [**Tool Metadata Specification**](./tool_metadata/README.md) | Comprehensive schema reference for `lighttool.toml`. Explains package ID formatting, label guidelines, versioning requirements, permission allowlisting, and orientation locks. |
| 🏗️ [**Repository Architecture**](./repo/README.md) | Architectural layout of `light-sdk` Gradle modules (`:tool`, `:plugin`, `:lint-rules`, `:sdk`, `builder`) with dependency relationships and Mermaid diagrams. |
| 📐 [**Design Decisions (ADRs)**](./design_decisions/README.md) | Architecture Decision Records explaining platform design trade-offs: API sandboxing, TOML manifest generation, containerized offline builds, and e-ink contrast enforcement. |
| 🌐 [**Master System Overview**](../OVERVIEW.md) | High-level extended elaboration of the entire `light-sdk` platform, security model, codebase audit, and hyperlinked navigation. |

---

## 🚀 Quick Reference

- **Creating a Tool**: Start by editing `tool/lighttool.toml` and modifying [`HomeScreen.kt`](../tool/src/main/kotlin/com/thelightphone/sample/HomeScreen.kt).
- **Testing on Emulator**: Set up an Android Virtual Device (API 34, 1080x1240 display) and follow the [System App Setup Guide](./system_app/README.md).
- **Checking Allowed Dependencies**: Refer to [`LightSdkPlugin.kt`](../plugin/src/main/kotlin/com/thelightphone/plugin/LightSdkPlugin.kt) for the active dependency allowlist.
