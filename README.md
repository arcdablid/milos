# milos &nbsp; [![bluebuild](https://github.com/arcdablid/milos/actions/workflows/build.yml/badge.svg)](https://github.com/arcdablid/milos/actions/workflows/build.yml)

A custom immutable Linux OS based on [Bluefin Developer Experience](https://docs.projectbluefin.io/bluefin-dx/) built using [BlueBuild](https://github.com/blue-build/template).

## Notable additions

- TeamViewer
- Mullvad VPN & web browser
- Yaru theme
- A few extra useful [`ujust` recipes](https://github.com/arcdablid/milos/files/justfiles/justfile.just):
  ```bash
    milos-setup-teamviewer            # Setup teamviewer background service & launch teamviewer
    milos-setup-tailscale             # Setup tailscale (and it systray) by providing an auth-key
  ```

## Installation

To install, you need to rebase from an existing atomic Fedora variant installation.

> [!WARNING] > **Rebasing between different desktop environments may cause issues!**

- First rebase to the unsigned image, to get the proper signing keys and policies installed:
  ```bash
  rpm-ostree rebase ostree-unverified-registry:ghcr.io/arcdablid/milos:latest
  ```
- Reboot to complete the rebase:
  ```bash
  systemctl reboot
  ```
- Rebasing to the signed image should happen automatically shortly after the system comes up again. Manually, it can be done like so:
  ```bash
  rpm-ostree rebase ostree-image-signed:docker://ghcr.io/arcdablid/milos:latest
  ```
- Reboot again to complete the installation
  ```bash
  systemctl reboot
  ```

## Verification

These images are signed with [Sigstore](https://www.sigstore.dev/)'s [cosign](https://github.com/sigstore/cosign). You can verify the signature by downloading the `cosign.pub` file from this repo and running the following command:

```bash
cosign verify --key cosign.pub ghcr.io/arcdablid/milos
```
