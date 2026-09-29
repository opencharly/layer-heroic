# heroic

Heroic Games Launcher layer for OpenCharly images.

The `heroic` candy installs the [Heroic Games
Launcher](https://heroicgameslauncher.com/) from its GitHub-release RPM (the
`heroic` package and the `/usr/bin/heroic` launcher) alongside the MangoHud FPS
overlay and Feral GameMode performance optimizer from the Fedora repos. It
targets a Sway desktop (`pod-sway`).

Heroic manages the Epic Games Store (via Legendary), GOG (via gogdl), and
Amazon Prime Gaming (via Nile) stores, and manages its own Wine/Proton
runners independently of Steam. Heroic config and Wine/Proton tools persist in
the `heroic-config` volume; game installs and prefixes persist in the
`heroic-games` volume.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `heroic` |
| Requires | `pod-sway` |
| Package | `heroic` (GitHub-release RPM, pinned to `2.20.1`) |
| Extra packages | `mangohud`, `gamemode` (Fedora repos) |
| Volumes | `heroic-config` → `~/.config/heroic`, `heroic-games` → `~/Games/Heroic` |
| Install files | `charly.yml` (`run:` step) |
| Service / port | none (on-demand GUI) |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list — typically with
a Sway desktop and a VNC/streaming path:

```yaml
my-gaming:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-sway-desktop-vnc:v2026.243.1835'
      - '@github.com/opencharly/layer-steam:v2026.243.0507'
      - '@github.com/opencharly/layer-heroic:v2026.243.2108'
```

After the image is built, launch it inside the desktop session:

```bash
heroic --fullscreen     # controller-friendly full-screen UI
heroic --no-gui         # start minimized to the system tray
heroic --version
```

## Layout

- `charly.yml` — the `heroic:` candy entity: the `pod-sway` require, the Fedora
  `distro:` packages, the `volume:` definitions, the `HEROIC_VERSION` var, the
  `run:` install step, the `check:` assertions, and the embedded `skill:` entity.
- `CHANGELOG/` — per-CalVer release notes.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:heroic` — the Heroic Games Launcher
- Runtime parent: `/charly-selkies:sway` (Wayland compositor)
- Desktop composition: `/charly-selkies:sway-desktop-vnc`
- Sibling launcher: `/charly-selkies:steam`
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
