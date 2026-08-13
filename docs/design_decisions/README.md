# 📐 Light SDK Architecture Decision Records (ADRs)

This directory contains records of significant architectural design decisions made for the Light SDK platform.

---

## ADR-001: Restricted API Sandbox & Dependency Allowlisting

### Context
Standard Android app development permits unrestricted third-party dependency inclusion, reflective API invocation, raw Android `Context` manipulation, and background service creation. On the Light Phone III, unvetted background activity and non-standard UI components threaten battery performance, platform security, and the minimalist user experience.

### Decision
1. The `:plugin` module enforces a compile-time dependency allowlist (`ALLOWED_DEPENDENCIES`). Any unapproved Gradle dependency or file JAR inclusion causes Gradle build configuration to fail.
2. Source files are scanned for prohibited code patterns (e.g. `startActivity`, `LocalContext`, `Class.forName`, `java.lang.reflect`).
3. Tool applications must be written exclusively in Kotlin; `.java` files are rejected.

---

## ADR-002: Declarative Metadata via `lighttool.toml` & Generated Manifests

### Context
Standard Android apps require developers to maintain an `AndroidManifest.xml` file, declaring package IDs, launcher activities, and permissions. In a managed platform like LightOS, allowing arbitrary manifest entries could permit security exploits (e.g., declaring custom intent filters, custom application classes, or unauthorized hardware permissions).

### Decision
1. Developers declare tool metadata strictly within a `lighttool.toml` file at the root of their tool module.
2. The `:plugin` module parses `lighttool.toml` during Gradle configuration and auto-generates `AndroidManifest.xml` under `build/generated/light-sdk/`.
3. Hand-written `AndroidManifest.xml` files in developer repositories are explicitly forbidden and rejected during build validation.

---

## ADR-003: Containerized Offline Build Harness (`builder/`)

### Context
Light Phone tools submitted by community developers must be compiled and signed on Light's remote production servers. Allowing arbitrary remote builds to execute network calls or run arbitrary scripts on build infrastructure creates security risks.

### Decision
1. Remote builds run inside a sandboxed, unprivileged Docker container (`builder/Dockerfile`).
2. The container pre-warms all allowed dependencies into the Docker image layer and executes Gradle with `--offline`.
3. Signing keys are kept strictly separate on a dedicated signing service; the container outputs an unsigned APK alongside a deterministic `recipe.json` audit trail.

---

## ADR-004: Monochrome E-Ink UI Primitives & Contrast Enforcement

### Context
The Light Phone III features a monochrome e-ink display. Standard Android UI widgets, animations, complex gradients, and low-contrast color palettes render poorly on e-ink hardware and waste power.

### Decision
1. The SDK provides Jetpack Compose UI primitives (`:sdk:ui`) featuring custom typography (`LightText`), high-contrast themes (`LightTheme`), and e-ink friendly modal dialogs.
2. Custom Android Lint rules (`:lint-rules`) enforce e-ink contrast rules and flag unauthorized background execution patterns during compile time.
