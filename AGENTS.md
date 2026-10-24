# AGENTS.md

This repo (`~/Work/zyker-daemon`, GitHub `evedes/zyker-daemon`) is
`zyker-daemon`, a Rust binary crate (`src/main.rs`). `CLAUDE.md` is a symlink
to this file.

## Workflow

Features go through [flow](https://github.com/evedes/zyker-flow): explore,
spec, tickets, build, review, ship. `.flow.json` sets what it guards:

- Protected paths: `src/`, `tests/`, `Cargo.toml`, `Cargo.lock`. These can
  only be edited in a feature's build phase, and only committed in ship.
- Standing gates (`flow gates`): `cargo fmt --check`,
  `cargo clippy --all-targets -- -D warnings`, `cargo test`.
- Feature artifacts live in `flow/<NNN-slug>/`. The standing agreement every
  ticket inherits is `flow/STANDING.md`, and the living spec is
  `flow/specs/*.md`.

Work that touches no protected path (docs, CI, tooling) needs no feature.

## Code

- Keep it plain Rust: stable toolchain, no `unsafe` unless a spec says why.
- Tests come before the code they cover: unit tests next to the code,
  end-to-end tests in `tests/`.
- Keep `cargo fmt --check` and `cargo clippy --all-targets -- -D warnings`
  clean. Run `cargo fmt` only in build, since flow treats it as codegen.
