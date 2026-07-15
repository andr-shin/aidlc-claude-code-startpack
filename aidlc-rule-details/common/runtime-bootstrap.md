# Runtime Bootstrap (런타임 자동 준비)

## Principle
The participant should NEVER have to manually install Python/Node or double-click a setup script.
Whenever a step needs a runtime that is missing, YOU (the agent) install it and continue.

## When
Before any dependency-install, build, test, or run step — especially in the CONSTRUCTION phase
(`construction/build-and-test.md`, `construction/code-generation.md`) — check whether the required
runtime exists. If it is missing, install it automatically first, then proceed.

## How (user-space, no admin, no Gatekeeper)
- Prefer running the bundled bootstrap script non-interactively if it exists in the project root:
  `bash start.sh </dev/null` (macOS/Linux) — invoking via `bash` does NOT trigger macOS Gatekeeper,
  so no security dialog appears. On Windows run `start.bat`.
- If no script is present, install directly:
  - Python: ensure `uv` (`curl -LsSf https://astral.sh/uv/install.sh | sh`; Windows:
    `powershell -c "irm https://astral.sh/uv/install.ps1 | iex"`), then `uv python install 3.12`
    and run via `uv run`.
  - Node.js: download the official prebuilt build into `~/.aidlc/node` and prepend it to PATH
    (mac/linux tarball / Windows zip from nodejs.org).

## CRITICAL: make the tools reachable in YOUR shell (PATH)
`uv` installs to `~/.local/bin` and Node to `~/.aidlc/node/bin` — these are NOT on the default PATH
of a fresh, non-interactive shell, and running `bash start.sh` installs them in a SUBshell whose
exports do not survive. So after ensuring the runtime, in EVERY subsequent build/test/run command you
MUST make them reachable, one of:
- Prepend PATH inline in the same command:
  `export PATH="$HOME/.local/bin:$HOME/.aidlc/node/bin:$PATH" && <your command>` (mac/linux), or
- Use absolute paths: `~/.local/bin/uv ...`, `~/.aidlc/node/bin/node ...`, `~/.aidlc/node/bin/npm ...`.
Do NOT assume `uv`/`node`/`npm` are on PATH just because install succeeded — verify with
`command -v` and fall back to the absolute path. (Windows: the installers add to the User PATH, which
new terminals pick up; within the same session prepend `%USERPROFILE%\.local\bin;%USERPROFILE%\.aidlc\node`.)

## Do NOT
- Do NOT instruct the user to double-click `start.command` or install a runtime by hand as the
  primary path. Do it for them.
- Only if automatic install genuinely fails (offline / locked-down machine), point the user to the
  simple click-only steps in the project's `시작하기.md`.
