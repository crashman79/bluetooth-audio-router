# SinkSwitch – contributor notes

- **App**: Standalone GUI for per-app audio routing (PipeWire/PulseAudio). Primary run: download binary from Releases or `./build.sh` then `./dist/sinkswitch`. Config: `~/.config/sinkswitch/`.
- **Shell**: Use bash for commands/scripts (not fish). For systemd/journal use `--no-pager`.
- **Python**: Use a venv for deps (PEP 668). `build.sh` uses `.venv-build` for PyInstaller.
- **Layout**: `audio-router/` has `run_app.py`, `build.sh`, `run_app.spec`, `src/` (GUI, device_monitor, engine, config_parser, intelligent_audio_router), `config/`, `examples/`. Standalone only (no install script or systemd service).
