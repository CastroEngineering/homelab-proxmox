# 0001: Jellyfin runs in an unprivileged LXC with rootless Podman

## Context
First service on the host. Needs to be always on, should be cheap in RAM
(16 GB total), and may need GPU transcoding later.

## Options considered
1. VM
2. Unprivileged LXC, Jellyfin installed natively
3. Unprivileged LXC, Jellyfin in a rootless Podman container

## Decision
Option 3, with the container managed by a Podman Quadlet (systemd) unit so it
restarts after a reboot.

## Why
- **LXC vs VM:** TODO (your words: what does an LXC share with the host,
  and why does Jellyfin not need more than that?)
- **Rootless Podman:** TODO (your words: what does running as a normal
  user with no daemon protect against?)
- Quadlet gives declarative, restartable containers I can keep in Git.

## Consequences
- The LXC shares the host kernel, so its isolation is weaker than a VM's.
- Nesting must be enabled on the LXC for Podman to work.
- The GPU can be shared with this LXC later, which a passthrough VM would not allow.
