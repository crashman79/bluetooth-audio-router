# PipeWire/PulseAudio Audio Router - Project Instructions

## Development Guidelines

### Terminal Commands
- Always use `--no-pager` flag with `systemctl` and `journalctl` commands to prevent interactive pager mode
- Example: `journalctl --user -u pipewire-router --no-pager`
- Example: `systemctl --user status pipewire-router --no-pager`

### Fish Shell Compatibility
- User's shell is fish, not bash/zsh
- Do NOT use bash-specific syntax (heredocs, etc.)
- Use `printf` or `echo` instead of heredocs for multiline strings
- Venv activation scripts are NOT compatible with fish - use direct Python path instead:
  - Use: `~/.config/pipewire-router/venv/bin/python3 script.py`
  - Don't use: `source venv/bin/activate`
- When generating terminal commands, ensure they work with fish syntax

### Arch Linux / CachyOS Specifics
- User is running CachyOS (Arch Linux flavor)
- Python package management requires virtual environments due to PEP 668 (externally-managed-environment)
- Do NOT use `pip install --user` or `pip install --break-system-packages`
- Always use `python3 -m venv` for isolated environments
- Use `pacman` for system packages, virtual environments for Python packages
- Package manager is `pacman`, not `apt` or `yum`
- `yay` is also available as AUR helper

## Project Overview
A comprehensive Python-based system for automatic audio stream routing in PipeWire/PulseAudio based on application classes and connected output devices.

## Project Structure
- **src/**: Python source code for routing engine
  - `audio_router.py`: Main CLI interface with generate-config, apply-rules, monitor, list-devices commands
  - `device_monitor.py`: Device detection and monitoring
  - `config_parser.py`: YAML configuration parsing
  - `audio_router_engine.py`: Routing logic engine (pactl-based stream routing)
  - `intelligent_audio_router.py`: Intelligent device classification and automatic config generation
  - `tray_icon.py`: System tray icon (KDE Plasma and Gnome)

- **config/**: Configuration files
  - `routing_rules.yaml`: Auto-generated routing configuration

- **systemd/**: SystemD service files for daemon mode

- **examples/**: Example configurations

## Features Implemented
- Audio device detection and monitoring (PipeWire & PulseAudio)
- **Intelligent device classification** - Automatically detects device types (USB headsets, Bluetooth, analog speakers, HDMI)
- **Auto-generated routing rules** - Creates optimal routing based on connected devices on every service startup
- Application-based stream routing rules with automatic fallback
- YAML configuration format
- CLI and daemon modes
- SystemD integration with auto-config generation on startup
- Device hotplug detection and rule application (every 5 seconds)
- **System tray icon** - Optional tray icon for KDE Plasma and Gnome with pause/resume and config regeneration
- PipeWire auto-routing disabled to prevent conflicts with manual routing

## Usage
```bash
# Auto-generate routing rules based on connected devices
python3 src/audio_router.py generate-config

# List available devices
python3 src/audio_router.py list-devices

# Apply routing rules once
python3 src/audio_router.py apply-rules config/routing_rules.yaml

# Monitor and apply rules continuously (runs as daemon via systemd)
python3 src/audio_router.py monitor config/routing_rules.yaml
```

## Installation
```bash
./install.sh
systemctl --user start pipewire-router
systemctl --user enable pipewire-router
```

## Configuration Format
Routing rules are defined in YAML with the following structure:
```yaml
routing_rules:
  - name: "Rule Name"
    applications:
      - "app1"
      - "app2"
    application_keywords:
      - "keyword1"
    target_device: "device_name"
    enable_default_fallback: true
```
