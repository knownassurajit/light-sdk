# 🔌 Light SDK Core (`light-sdk/sdk`)

The `sdk` module contains the official core Kotlin SDK library for building minimalist Light Phone applications and system integrations.

---

## 🏗️ Structure & Exports

```text
sdk/
├── src/main/java/com/light/sdk/
│   ├── LightSDK.kt        # Core SDK initialization & capabilities registry
│   ├── api/               # Hardware & system service interop APIs
│   └── models/            # Data models & contract specifications
└── build.gradle.kts       # Library publishing & compilation config
```

---

## ⚙️ Compilation & Testing

```bash
./gradlew :sdk:test
```
