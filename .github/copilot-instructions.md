# SinkSwitch – contributor notes

- **App**: GUI for per-app audio routing (PipeWire/PulseAudio). Primary distribution: **Flatpak** from GitHub Releases (`*.flatpak`). Local dev build path is Flatpak (`./build.sh` or `./build-and-run.sh`). Config: `~/.config/sinkswitch/` (Flatpak: app sandbox).
- **Shell**: Use bash for commands/scripts (not fish). For systemd/journal use `--no-pager`.
- **Python**: Use a venv for deps (PEP 668) when running from source. CI: `.github/workflows/release.yml` builds Flatpak only.
- **Layout**: Repo root has `run_app.py`, `build.sh`, `build-and-run.sh`, `src/` (GUI, device_monitor, engine, config_parser, intelligent_audio_router), `config/`, `examples/`, `tests/`. Standalone app model (no install script or systemd service).
