# DeXTerm 🖥️🦀

<p align="center">
  <b>Next-generation, GPU-accelerated terminal emulator engineered for Samsung DeX and Android.</b><br>
  Clean-room architecture written in pure Rust & Kotlin. Bringing the power and finesse of modern desktop terminals to mobile workstations.
</p>

<p align="center">
  <img alt="Language: Rust" src="https://img.shields.io/badge/Core-Rust-b7410e?style=flat-square&logo=rust">
  <img alt="UI: Kotlin" src="https://img.shields.io/badge/UI-Kotlin%20%2F%20Compose-7F52FF?style=flat-square&logo=kotlin">
  <img alt="Platform: Android & Samsung DeX" src="https://img.shields.io/badge/Platform-Samsung%20DeX%20%7C%20Android-008080?style=flat-square">
  <img alt="License: MIT" src="https://img.shields.io/badge/License-MIT-blue?style=flat-square">
</p>

---

## 🌟 Vision

Modern Android devices like the Samsung Galaxy series pack desktop-grade multi-core silicon (Exynos / Snapdragon). When connected to an external display via **Samsung DeX**, they transform into full-fledged desktop workstations.

However, existing terminal options on Android are either legacy command-line wrappers or trapped inside mobile-first touch interfaces with software rendering lag.

**DeXTerm** bridges this gap: a high-performance terminal emulator built from the ground up for desktop mouse-and-keyboard usage, inspired by the power features of **iTerm2**, powered by a **pure Rust engine**, and accelerated via native GPU rendering.

---

## 🔥 Key Architectural Features

- ⚡ **Pure Rust Core (`dexterm-core`):** 
  - Ultra-fast PTY / Unix pseudo-terminal stream processing via Linux kernel `/dev/pts/`.
  - Zero-allocation ANSI / VT100 / XTerm escape sequence state machine (powered by `vte`).
  - Lock-free memory ring buffer for instantaneous scrollback navigation.
- 🎨 **GPU Hardware Accelerated Rendering:** 
  - Text glyph atlas cached directly in GPU memory using OpenGL ES / Vulkan.
  - Silky-smooth 60Hz / 120Hz scrolling on 1080p, 1440p, and 4K external monitors.
- 🖼️ **iTerm2 Inline Images Protocol (`OSC 1337`):** 
  - Direct support for inline image rendering (`imgcat`, Python matplotlib plots, CLI graphics) rendered natively within the terminal grid.
- 🪟 **Desktop-Grade Windowing & Split Panes:** 
  - Nested horizontal and vertical split panes with fluid drag-and-resize boundaries.
  - Multi-tab management, full right-click context menus, and customizable physical keyboard shortcuts (`Cmd/Ctrl + D`, `Ctrl + Shift + T`).
- 🛡️ **Deep Linux Kernel & Root Integration:** 
  - Seamlessly bridges with local user environments (Termux, PRoot, chroot) and Magisk root daemon for direct, unrestricted Linux kernel access.

---

## 📐 System Architecture

```text
┌─────────────────────────────────────────────────────────────┐
│                 Samsung DeX Window Manager                  │
└──────────────────────────────┬──────────────────────────────┘
                               │
            ┌──────────────────▼──────────────────┐
            │       DeXTerm Android Frontend       │
            │   (Kotlin / Jetpack Compose UI)     │
            │  - Split pane layouts & input events │
            │  - Native window resizing & themes  │
            └──────────────────┬──────────────────┘
                               │ JNI (Native Interface)
            ┌──────────────────▼──────────────────┐
            │          DeXTerm Core (Rust)        │
            │  - VT / ANSI parser (vte crate)     │
            │  - 2D Screen grid & scroll buffer   │
            │  - PTY stream controller (nix)      │
            └──────────────────┬──────────────────┘
                               │
        ┌──────────────────────┴──────────────────────┐
        ▼                                             ▼
┌──────────────┐                              ┌───────────────┐
│ GPU Renderer │                              │ PTY Subsystem │
│(GLES/Vulkan) │                              │(/dev/pts/...) │
└───────┬──────┘                              └───────┬───────┘
        │                                             │
   Display Output                                Shell Process
 (External Monitor)                           (zsh / bash / root)
```

---

## 🗺️ Roadmap

- [x] Initial repository setup & license definition.
- [ ] Core Rust PTY and ANSI parser binding (`dexterm-core`).
- [ ] OpenGL ES glyph atlas text renderer.
- [ ] Android frontend with multi-pane layout for Samsung DeX.
- [ ] iTerm2 Inline Images Protocol (`OSC 1337`) integration.
- [ ] Configurable color themes & Nerd Font ligature support.

---

## 📜 Acknowledgments

DeXTerm is a clean-room implementation written from scratch. We proudly acknowledge the software that inspired its feature design:

- **[iTerm2](https://iterm2.com/)** by George Nachman — for setting the gold standard in terminal productivity, UX, and the `OSC 1337` image protocol.
- **[Alacritty](https://github.com/alacritty/alacritty)** & **[WezTerm](https://github.com/wez/wezterm)** — for demonstrating the power of Rust in high-throughput terminal virtualization.

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.
