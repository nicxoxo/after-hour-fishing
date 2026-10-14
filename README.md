# Portfolio

An interactive 3D web portfolio written in Rust.

Instead of a traditional page, the portfolio is presented as a small 3D scene: a beach with a lone fisherman and a sun in the background. The fisherman fishes up objects, and each object corresponds to a section of the portfolio.

> **Status:** early setup. The Rust crate is still the default `cargo new` binary; no rendering code exists yet.

## Scene concept

- **Setting:** a beach, low-poly style, with a fixed third-person camera behind the fisherman.
- **Fisherman:** the single character, fishing from the shore. He has two animations: idle and catch.
- **Sun:** sits in the background.
- **Preload animation:** designed in Figma, an hourglass with falling sand that doubles as the progress bar while the game loads.
- **Languages:** English, Spanish and Catalan.
- **Fallback:** a plain HTML version of the portfolio will exist for accessibility, SEO and devices that can't run the 3D scene.

### Sections and objects

| Section | Object |
| --- | --- |
| Who am I? | ID card |
| Curriculum Vitae | Manuscript |
| Projects | Trophy |
| Contact | Message in a bottle |

The objects are not modeled yet; they will be `.glb` files made in Blender.

### How it plays

1. A welcome screen blurs the scene and waits for input.
2. The fisherman stands with the rod cast into the water. Each object appears as a circular glow on the water.
3. `A` / `D` move the selection left / right; a downward arrow marks the selected glow.
4. `Enter` fishes it up. The catch animation plays and the object jumps to the center-left of the screen, with the section's text beside it like a menu.

## Tech stack

| Area | Choice |
| --- | --- |
| Language | Rust (edition 2024) |
| Target | Web browser |
| Engine | [Bevy](https://bevyengine.org/) |
| Browser backend | WebGL2 first, WebGPU opt-in |
| Web build | [`trunk`](https://trunkrs.dev/), Rust-only, with a small `index.html` shell |
| Platforms | Desktop first; mobile not blocked but not a goal yet |
| 3D models | Blender, exported as glTF binary (`.glb`) |
| Preload animation | Figma SVGs, inline SVG + CSS in `index.html` |
| Hosting | GitHub Pages (to be validated) |

## Project structure

```
.
├── Cargo.toml
├── src/
│   └── main.rs              # entry point (placeholder)
├── assets/
│   ├── fisherman.glb        # fisherman model (exported)
│   ├── sun.glb              # sun model (exported)
│   ├── blender/             # Blender source files (.blend)
│   ├── fisherman/           # fisherman source files (.fbx model + .png texture)
│   ├── boat.svg             # preload animation pieces, exported from Figma
│   ├── hourglass.svg
│   └── sun.svg              # (assets/.ignore/ is git-ignored)
└── docs/
    └── QUESTIONS.md         # open questions and pending decisions
```

## Getting started

Requirements: a recent stable Rust toolchain installed via [rustup](https://rustup.rs/). Edition 2024 needs Rust 1.85 or newer.

```sh
cargo run
```

Right now this just prints `Hello, world!`. Web build instructions (wasm target, `trunk`, dev server) will be added once Bevy is added to the project.

## Roadmap and open questions

The step-by-step plan is in [`docs/TASKS.md`](docs/TASKS.md). Pending decisions and unknowns are listed in [`docs/QUESTIONS.md`](docs/QUESTIONS.md).

## Credits

The fisherman is an adaptation of an open source model licensed under CC Attribution. Author and license details are pending (see [`docs/QUESTIONS.md`](docs/QUESTIONS.md), #29).

## License

Not decided yet. See [`docs/QUESTIONS.md`](docs/QUESTIONS.md), #24.
