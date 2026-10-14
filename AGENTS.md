# AGENTS.md

Guidance for AI coding agents working in this repository.

## Project summary

An interactive 3D web portfolio written in Rust. The scene is a beach with a lone fisherman and a sun in the background. The fisherman fishes up objects, each one standing for a section of the owner's portfolio. A preload animation designed in Figma is shown while the game loads.

See [`README.md`](README.md) for the full overview.

## Current state

- `src/main.rs` is still the `cargo new` placeholder. No rendering, engine, or web code exists yet.
- `Cargo.toml` has no dependencies.
- Assets so far: fisherman and sun models (`.glb`, plus Blender sources) and three SVGs (`boat`, `hourglass`, `sun`).
- **Engine: Bevy** (decided by the owner). Web build: `trunk`, Rust-only with a small `index.html` shell, WebGL2 first with WebGPU opt-in, desktop first. See "Resolved" in [`docs/QUESTIONS.md`](docs/QUESTIONS.md). Bevy is not yet in `Cargo.toml`.

## Design decisions (from the owner)

Full list in the "Resolved" section of [`docs/QUESTIONS.md`](docs/QUESTIONS.md). The essentials:

- Low-poly style, fixed third-person camera, fisherman fishing from the shore. Fisherman animations: idle and catch.
- Sections and objects: Who am I? (ID card), Curriculum Vitae (manuscript), Projects (trophy), Contact (message in a bottle).
- Controls: `A` / `D` select, `Enter` fishes. A welcome screen blurs the scene until the user gives input.
- After a catch, the object sits center-left and the section text appears beside it.
- Preload animation: an hourglass whose falling sand is the real progress bar.
- Content in English, Spanish and Catalan. A plain HTML fallback page is required.
- Colors: the owner provides the palette when needed. Don't invent colors.
- Hosting: GitHub Pages. No CI.

## Ground rules

1. **Do not assume details.** If a requirement, design detail, or technical choice is not stated by the owner or clear from the repo, do not invent it. Add the question to [`docs/QUESTIONS.md`](docs/QUESTIONS.md) and either ask or move on with work that doesn't depend on the answer.
2. **Keep `docs/QUESTIONS.md` current.** When a question is answered, move it to the "Resolved" section with the answer and the date, and update `README.md` / `AGENTS.md` if the answer changes something documented there.
3. **Don't touch source assets without being asked.** Files in `assets/` (`.blend`, `.fbx`, `.png`, `.glb`, `.svg`) are authored by hand in Blender and Figma. Don't modify, re-export, rename, or delete them unless the owner asks. `assets/` is committed; `assets/.ignore/` is git-ignored.
4. **Ask before adding dependencies.** Any new crate, wasm toolchain, bundler, or JS tooling needs the owner's approval.
5. **Commits.** Only commit when asked. The default branch is `main`. There is no CI.
6. **Attribution.** The fisherman model requires CC Attribution credit; keep the credit in place once the details are known.

## Conventions

- Rust edition 2024 (see `Cargo.toml`).
- Format with `cargo fmt` and keep `cargo clippy` warnings clean before handing work back.
- Load runtime 3D models from the `.glb` files in `assets/`. The `.blend` and `.fbx` files are sources, not runtime assets.

## Commands

```sh
cargo build
cargo run
cargo fmt
cargo clippy
```

Web build and serve commands (`trunk`) will be added once Bevy is added to the project.

## Layout

| Path | Purpose |
| --- | --- |
| `src/` | Rust source |
| `assets/*.glb` | Runtime 3D models (exported from Blender) |
| `assets/blender/` | Blender source files (`.blend`; `.blend1` files are Blender auto-backups) |
| `assets/fisherman/` | Fisherman source model (`.fbx`) and texture (`.png`) |
| `assets/*.svg` | SVG assets exported from Figma |
| `docs/QUESTIONS.md` | Open and resolved questions |
| `docs/TASKS.md` | Phased task list; check items off as they are done |
