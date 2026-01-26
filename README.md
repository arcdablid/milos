# milos &nbsp; [![bluebuild](https://github.com/arcdablid/milos/actions/workflows/build.yml/badge.svg)](https://github.com/arcdablid/milos/actions/workflows/build.yml)

A custom immutable Linux OS based on [The Bazzite Developer Experience](https://github.com/ublue-os/bazzite-dx) built using [BlueBuild](https://github.com/blue-build/template).

## Notable additions & features

- Ghostty
- TeamViewer
- VirtualBox (script by [by ettfemnio & Preston Petrie](https://github.com/ettfemnio/bazzite-virtualbox/blob/main/build.sh))
- Curated list of extra [system packages, flatpaks, gnome extensions & fonts](https://github.com/arcdablid/milos/recipes/recipe.yml)
- A few extra useful [`ujust` recipes](https://github.com/arcdablid/milos/files/justfiles/justfile.just):
  ```bash
    milos-setup-chezmoi               # Shortcut to setup dotfiles using chezmoi.
    milos-setup-linger                # Enable linger for current user
    milos-vboxusers-add-current-user  # Add vboxusers group to system if not there already and current user to it.
    milos-clean                       # Clean up old packages and Docker/Podman images and volumes.
    milos-setup-podman-syncthing      # Add syncthing for current user via a quadlet.
    milos-setup-teamviewer            # Setup teamviewer background service & launch teamviewer
    milos-setup-tailscale             # Setup tailscale (and it systray) by providing an auth-key
  ```

## Installation

To install, you need to rebase from an existing Bazzite or other atomic Fedora installation.

> [!WARNING] > **Rebasing between different desktop environments may cause issues!**

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/arcdablid/milos:latest
  ```
  or
  ```
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/arcdablid/milos-nvidia:latest
  ```
- Reboot to complete the rebase:
  ```
  systemctl reboot
  ```
- Rebasing to the signed image should happen automatically shortly after the system comes up again. Manually, it can be done like so:
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/arcdablid/milos:latest
  ```
  or
  ```
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/arcdablid/milos-nvidia:latest
  ```
- Reboot again to complete the installation
  ```
  systemctl reboot
  ```

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/arcdablid/milos
```

or

```bash
cosign verify --key cosign.pub ghcr.io/arcdablid/milos-nvidia
```
