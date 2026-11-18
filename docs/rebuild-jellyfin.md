# Runbook: rebuild Jellyfin from nothing

## 1. Create the container (Proxmox web UI > Create CT)
Debian template, **unprivileged**, **Nesting on**, 2 cores, 2048 MiB RAM,
512 MiB swap, 16 GiB disk, bridge `vmbr0`, static IP, set **Start at boot**.

## 2. Install Podman (inside the container)
    apt update && apt full-upgrade -y
    apt install -y podman uidmap dbus-user-session

## 3. Create the service user
    adduser media
    loginctl enable-linger media

## 4. As user `media`
    su - media
    export XDG_RUNTIME_DIR=/run/user/$(id -u)
    mkdir -p ~/jellyfin/config ~/jellyfin/cache ~/media ~/.config/containers/systemd

## 5. Install the unit and start it
Copy `guests/jellyfin/jellyfin.container` to `~/.config/containers/systemd/`, then:

    systemctl --user daemon-reload
    systemctl --user start jellyfin.service

## Verify
- `systemctl --user status jellyfin.service` shows active (running)
- Web UI answers on port 8096
- Reboot the host; the UI comes back without any action

## Notes
Config lives in `~/jellyfin/config`. It is NOT in this repo (contains user data
and keys). Back it up separately.
