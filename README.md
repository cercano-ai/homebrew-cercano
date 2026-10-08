# Cercano Homebrew tap

Canonical Homebrew tap for the standalone
[Cercano](https://github.com/cercano-ai/Cercano) agent. It installs the
two-binary macOS standalone (`cercano` and `cercano-cli`) published by the
Cercano release pipeline.

## Install

```sh
brew install cercano-ai/cercano/cercano
```

This installs two binaries:

| Binary | Role |
|---|---|
| `cercano` | the agent, which does the work |
| `cercano-cli` | the terminal client you interact with |

Start the terminal client with `cercano-cli`. The client launches the agent
automatically the first time you use it; nothing is installed as a background
service, and no agent is started by installation itself.

## Requirements

- **Apple Silicon (`arm64`) only.** The formula refuses installation on Intel
  Macs rather than installing binaries that cannot run on them.
- **macOS 12 (Monterey) or later.** The binaries are built against the macOS
  12 deployment target, and Homebrew refuses installation on older systems.

## Upgrading

```sh
brew upgrade cercano
```

A successful upgrade restarts a running agent for you after it finishes
in-flight work; if no agent is running, nothing is started. If the
post-install restart reports a failure, the new files are already installed —
only the restart did not complete. Retry it:

```sh
cercano restart-after-upgrade
```

## Known issue

The current v0.20.3 standalone's post-install restart can fail during process
discovery when an unrelated same-user process exits while being inspected
(`inspect candidate PID ...: no such file or directory`). Installation itself
succeeds and both installed binaries work — `brew test`, code signature
verification and both binaries pass. Only the automatic post-install restart
is affected. This is tracked in
[cercano-ai/Cercano#55](https://github.com/cercano-ai/Cercano/issues/55); use
the retry command above if you hit it.

## History

This repository previously hosted a pre-standalone v0.9.x single-binary
formula for the co-processor-era product. Its history is retained unchanged
for reference; the current formula is the tested standalone release above.
The personal `bryancostanich/homebrew-tap` repository is separate (Lattice /
personal) and is not this project's publishing destination.

Do not delete your configuration (`~/.config/cercano/`) or saved conversations
when changing installation methods; they are deliberately kept outside the
Homebrew installation.
