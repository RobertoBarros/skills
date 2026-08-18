---
name: bootstrap-sbx
description: Installs runtimes, dependencies, services, and tools for projects opened in Docker Sandboxes while avoiding unnecessary workspace changes. Use when preparing, configuring, or repairing a Linux/SBX development environment so an existing project can be installed, tested, and run.
---

# Bootstrap SBX

Prepare the project idempotently. Prioritize `mise`, keep tools and configuration outside the workspace, and preserve version-controlled files.

## Safety rules

- Work only on Linux inside Docker Sandboxes. If the environment does not match, explain why and stop.
- Do not perform a full system upgrade, run migrations or seeds, create databases, or execute destructive commands.
- Do not create `mise.toml`, `.tool-versions`, helper scripts, or `.gitignore` entries.
- Keep runtimes, caches, Python environments, tools, and configuration in the user's home directory. Reuse existing global `mise` configuration.
- Preserve existing lockfiles with frozen, immutable, or equivalent modes. Allow only essential workspace artifacts, such as `node_modules` or a missing lockfile that the package manager must generate.
- Before creating or modifying any other version-controlled file, show the expected change and request authorization.
- Never assume a download failure is a project failure. If the sandbox network policy blocks an operation, report the exact domains observed in URLs or errors so they can be allowed on the host.

## Workflow

### 1. Inspect the environment and record the baseline

1. Confirm Linux, user, home directory, shell, architecture, `sudo` access, connectivity, and package manager (`apt`, `dnf`, `yum`, `apk`, or equivalent).
2. Record `git status --short`, relevant ignored files, and versions of available tools. Do not clean pre-existing changes.
3. Read `README`, `AGENTS.md`, development documentation, CI configuration, Dockerfiles, Compose files, manifests, version files, and lockfiles first.
4. Internally produce a minimal list of runtimes, system libraries, package managers, and services proven necessary by those files.

### 2. Prepare system packages

1. Update package manager indexes only.
2. Install only compilers, headers, clients, libraries, and services required by the detected dependencies.
3. Make installation non-interactive and check whether each package already exists before installing it.

Do not run `apt upgrade`, `dnf upgrade`, a general `yum update`, or an equivalent command.

### 3. Install runtimes with mise

1. Reuse `mise` when available. Otherwise, install the official version in the user's home directory and activate it in the current session.
2. Respect versions declared in project files, CI configuration, Dockerfiles, and lockfiles, in that order.
3. When no version is declared, choose a stable version compatible with the manifests and dependencies. Briefly record the inference.
4. Install Ruby, Node.js, Python, and other runtimes through `mise`. If a missing version must be configured, set it globally in the sandbox, never in the project.
5. Install Node.js 18 or newer through `mise` when Node is required by the project or to install Hunk.

### 4. Install RTK and Hunk

1. If `rtk` is missing, install it from the official `https://github.com/rtk-ai/rtk` repository using the project's current published installation method. Do not install the unrelated package with the same name from crates.io.
2. Run `rtk init -g --codex` and validate it with `rtk --version` and `rtk gain`.
3. Afterward, prefix compatible commands with `rtk`.
4. Ensure Node.js 18+ is available and install Hunk with `npm install -g hunkdiff` only when `hunk` is missing or invalid. Validate it with `hunk --version`.
5. Keep binaries and global configuration for these tools in the user's home directory.

### 5. Install project dependencies

Use the package manager proven by manifests and lockfiles:

- Ruby: use the Bundler version compatible with `Gemfile.lock`; run `bundle install` without updating gems.
- JavaScript: use Yarn, npm, or pnpm according to the lockfile and `packageManager` field; use immutable or frozen mode when a lockfile exists.
- Python: use pip, Poetry, or uv according to the project files; create environments in the user's home directory, outside the workspace.
- Other ecosystems: use the package manager and reproducible mode specified by the project.

Do not replace package managers or regenerate existing lockfiles.

### 6. Prepare services

1. Install only services proven necessary, such as PostgreSQL or Redis.
2. Start services through the mechanism available in the sandbox and verify their health, port, and client.
3. Do not create users, databases, or schemas, and do not run migrations or seeds.
4. If the project depends on an unavailable external service, report exactly what is missing.

### 7. Verify and finish

1. Validate runtime and package manager versions, dependency resolution, service health, `rtk --version`, `rtk gain`, and `hunk --version`.
2. Run the project's documented primary verification commands, prioritizing quick, non-destructive checks. Do not start a persistent server unless necessary.
3. Repeat idempotency-sensitive checks to confirm that a second run would not perform unnecessary installations or changes.
4. Compare the final `git status --short` with the baseline. Stop and request authorization if any unexpected version-controlled change appears.
5. Summarize the runtimes, dependencies, services, and tools prepared. Report inferences, failed checks, and domains blocked by the network.

## Acceptance criteria

- Project dependencies are installed and basic commands work.
- Required services are active and healthy, without creating databases or running migrations.
- RTK and Hunk are available on `PATH` and validated.
- Repeated execution is safe and performs no unnecessary work.
- No unexpected files are created or modified in the project.
