# Standing agreement for zyker-daemon tickets

Every ticket in `work/*/tickets/` inherits this. Tickets only state what is
specific to them.

## Definition of Ready (`flow check` enforces the ticket sections)

- Title and desired end state are specific.
- Context says why, and which spec section the ticket implements.
- Entry points name the files/modules to start from.
- In scope and out of scope are stated.
- `## Verification steps` holds runnable commands.
- The spec and ticket set are approved by the user (`flow approve`).

## Definition of Done

- The ticket's gate holds and its verification commands pass.
- Standing gates pass (`flow gates` runs them; they are listed in `.flow.json`).
- Tests were written before the code they cover, from the acceptance criteria:
  unit tests in the module they cover, behaviour seen from outside the
  process (CLI, signals, sockets, files it writes) in `tests/`.
- Behaviour was checked against the running daemon (`cargo run`), not only in
  tests.
- No `unwrap`/`expect` on runtime input outside tests; errors reach the log or
  the exit code with enough context to act on.
- New dependencies are named in the ticket; `Cargo.lock` changes only with them.
- No out-of-scope surfaces touched; existing conventions followed (`AGENTS.md`).
- Docs the change makes stale (`AGENTS.md`, README) are updated in the same commit.
- Lands as one commit with its `work/` folder.

## Working agreement

- On real ambiguity, stop and ask; don't guess at behaviour the spec doesn't cover.
- Note any deviation from a ticket in `review.md`.
