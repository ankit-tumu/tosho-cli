# tosho-cli

[![Linux](https://img.shields.io/badge/platform-linux-FCC624?logo=linux&logoColor=black)](https://www.kernel.org)
[![Bash](https://img.shields.io/badge/shell-bash-4EAA25?logo=gnu-bash&logoColor=white)](https://www.gnu.org/software/bash/)
[![License: Open Source](https://img.shields.io/badge/license-Open%20Source-blue.svg)](#license)

A Linux CLI anime streaming tool.

Search anime on AniList, resolve seasons via AniMap/AniDB mappings, discover releases on AnimeTosho, and stream through TorBox + mpv. Supports Syncplay for synchronized group watching.

## Features

- **Season-Safe Matching**: Queries AnimeTosho directly by AniDB AID/EID resolved via AniMap, preventing multi-season contamination.
- **TorBox Cache Pre-Checking**: Instantly checks torrent hashes against the TorBox cache for immediate playback.
- **Batch Episode Extraction**: Seamlessly extracts and plays individual episodes from multi-episode batch releases.
- **Interactive UI**: Fast, interactive terminal interface powered by `fzf` for searching and release selection.
- **mpv IPC Playback Controller**: Built-in playback controller supporting next, previous, replay, and episode selection navigation.
- **Syncplay Integration**: Group watching support via Syncplay rooms.

## Dependencies

### Required
- `curl` — API queries and downloads
- `jq` — JSON parsing
- `fzf` — Interactive fuzzy selection
- `mpv` — Video playback

### Recommended & Optional
- `socat` or `nc` — Recommended for mpv IPC communication
- `python3` — Fallback for mpv IPC if `socat` or `nc` is unavailable
- `syncplay` — Optional, required for group watching (`--sync`)

## Installation

### One-Line Install
If you're hosting this on GitHub, users can install it instantly (no `sudo` required, installs to `~/.local/bin`):
```bash
curl -sSL https://raw.githubusercontent.com/ankit-tumu/tosho-cli/main/install.sh | bash
```

### Manual Compile / System-wide (default `/usr/local/bin`)
```bash
git clone https://github.com/ankit-tumu/tosho-cli.git
cd tosho-cli
sudo make install
```

### User-local (`~/.local/bin`)
Make sure `~/.local/bin` is in your `$PATH`:
```bash
make install PREFIX=~/.local
```

### Manual Copy
```bash
cp tosho-cli ~/.local/bin/
chmod +x ~/.local/bin/tosho-cli
```

## Setup

On first run, `tosho-cli` will prompt for your TorBox API key and optional Syncplay settings. Configuration is saved to:
```
~/.config/tosho-cli/config
```

## Usage

```bash
tosho-cli "Frieren"
tosho-cli --sync "One Piece"
tosho-cli --help
```

### Playback Controls
During playback, an interactive menu appears in the terminal. Select with arrow keys/mouse or press the corresponding number:
- `1` — **Next** episode
- `2` — **Replay** current episode
- `3` — **Previous** episode
- `4` — **Select Ep** — pick a specific episode
- `5` — **Quit**

## Configuration

Config file location: `~/.config/tosho-cli/config`

```bash
# Required
TORBOX_KEY="your_torbox_api_key_here"

# Syncplay Settings
SYNCPLAY_SERVER="syncplay.pl:8999"      # host:port
SYNCPLAY_ROOM="anime-lounge"            # Room name
SYNCPLAY_USER="username"                # Defaults to $USER

# Service Endpoints
ANILIST_API_URL="https://graphql.anilist.co"
ANIMETOSHO_URL="https://feed.animetosho.xyz"
ANIMETOSHO_JSON_PATH="/json"
ANIMAP_API_BASE="https://animap.id"
TORBOX_API_BASE="https://api.torbox.app"
TORBOX_API_VERSION="v1"

# TorBox Polling Settings
TORBOX_MAX_WAIT=180                     # Maximum wait time in seconds
TORBOX_POLL_INTERVAL=2                  # Polling interval in seconds

# mpv Preferred Tracks (ISO-639-1 / ISO-639-2)
MPV_AUDIO_LANGS="jpn,ja,eng,en"
MPV_SUB_LANGS="eng,en"
```

## Uninstall

```bash
# System-wide
sudo make uninstall

# User-local
make uninstall PREFIX=~/.local
```

## License

Open source. Distributed under the MIT License.
