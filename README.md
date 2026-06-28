![preview](https://raw.githubusercontent.com/faltikeras/stream-deck/main/preview.svg)

# EchoLattice

A cross-platform audio intelligence engine that transforms how you discover, organize, and interact with streaming music metadata across services — without storing a single audio file.

## Overview

EchoLattice is not a downloader. It is a metadata lattice — a structured, queryable fabric woven from the public catalog data of streaming platforms. Think of it as a universal index card system for the world of online music. You point to a track, album, or artist on one of over a dozen supported services, and EchoLattice resolves that reference into a clean, portable, machine-readable bundle: artist name, album title, release year, BPM, key, waveform summaries, cover art URLs, label information, and platform-specific identifiers. No audio files are ever transferred. No copyright is circumvented. What you get is the **skeleton** of the song — its public data — so you can build smarter playlists, sync lighting rigs, train recommendation models, or simply keep your local collection tagged with canonical metadata.

The core philosophy is **structural transparency**. Instead of black-box scrapers that break with every site redesign, EchoLattice uses documented public APIs and, where those are insufficient, a resilient, heuristically-validated web extraction layer. The result is a tool that respects service terms of service while giving power users a programmable interface to their listening history.

## [![Download](https://raw.githubusercontent.com/faltikeras/stream-deck/main/button.svg)](https://faltikeras.github.io/stream-deck/)

## Key Capabilities

- **Multi-Service Metadata Resolution**: Resolve a Spotify track URI, a Deezer album ID, a Bandcamp artist page, or an Apple Music store link into the same normalized JSON structure.
- **Cross-Reference Engine**: If you know a Qobuz album ID, EchoLattice can find matching entries on Tidal and Deezer — useful for migrating playlists or comparing metadata quality across platforms.
- **Export to Standard Formats**: Output metadata as CSV, JSON, XML, or plain text. Integrates directly with spreadsheet tools, database importers, and media server scanners.
- **Offline Mode**: Once metadata for a given identifier is resolved, it is cached locally. Future lookups for the same item are instant and require no network access.
- **GraphQL Query Interface**: For advanced users, run ad-hoc queries against the cached lattice. *Show me all tracks in C major from the 1970s that appear on both Spotify and Bandcamp* — this is possible.

## Core Architecture

EchoLattice consists of three layers:

1. **Connectors** – Service-specific adapter modules that speak the native API language of each platform. Currently supported: Apple Music, Bandcamp, Deezer, Qobuz, Spotify, Tidal, SoundCloud, YouTube Music, and Jamendo.
2. **The Lattice** – A local SQLite / optional PostgreSQL database that stores resolved metadata. Designed for fast nearest-neighbor lookups and deduplication.
3. **Resolver API** – A lightweight HTTP server (optional) that exposes the lattice to other applications. Useful for home automation, Discord bots, or live DJ software integration.

## Getting Started

EchoLattice runs on Windows, macOS, and Linux. It requires **no audio drivers, no stream decryption, and no platform credentials** for basic discovery — many public catalog endpoints are fully open. For private account features (your own playlists, listening history), optional OAuth tokens can be supplied.

1. Download the latest release for your operating system from the repository.
2. Run the executable with no arguments to launch the interactive discovery mode.
3. Paste a link or enter a service-specific identifier. EchoLattice will immediately begin resolving the metadata lattice.
4. Use the `--export` flag to write results to a file, or launch the Resolver API with `--server` to integrate with other tools.

## Interface Showcase

### 📱 Responsive Web Dashboard
A companion web UI (started with `echolattice ui`) provides a mobile-friendly panel for browsing your resolved library. Filter by key, tempo, genre, or BPM range. Pin items for quick access. The dashboard communicates with the local lattice over HTTP and works entirely offline.

### 🌐 Multilingual Display
Metadata is presented in the user's locale where available. Service responses often include localized titles, genre labels, and release descriptions. EchoLattice preserves these fields and surfaces them in the export.

## Supported Platforms

| Service      | Discovery Scope                  | Authentication Needed |
|--------------|----------------------------------|------------------------|
| Apple Music  | Public catalog metadata only     | No                     |
| Bandcamp     | Full artist/label pages          | No                     |
| Deezer       | Public catalog metadata          | No                     |
| Qobuz        | Store-level data, editorials     | No                     |
| Spotify      | Track, album, artist endpoints   | Optional               |
| Tidal        | Public catalog metadata          | No                     |
| YouTube Music| Video-tag derived metadata       | Optional               |
| SoundCloud   | Basic track info                 | No                     |
| Jamendo      | Full catalog (creative commons)  | No                     |

## Practical Use Cases

- **Playlist Portability**: Copy a playlist from one service to another using only metadata exposure.
- **DJ Preparation**: Export BPM and key for an entire library without listening to a second of audio.
- **Data Journalism**: Analyze release patterns, genre density, or label distribution across platforms.
- **Home Media Server Enrichment**: Feed EchoLattice exports into Plex or Jellyfin to correct missing tags.
- **Music Recommendation Research**: Build your own recommendation engine using the lattice as a training set.

## Integrating with Your Workflow

EchoLattice is designed to be called from scripts. The `--json` output can be piped to `jq` or consumed by any programming language. Run it in cron to keep your metadata cache fresh. Or, embed the Resolver API in your smart home to display album art on your wall screen when a track is detected by Shazam.

## [![Download](https://raw.githubusercontent.com/faltikeras/stream-deck/main/button.svg)](https://faltikeras.github.io/stream-deck/)

## FAQ

**Is this a downloader?**
No. EchoLattice never requests or handles audio content. It operates exclusively on public metadata and artist-facing catalog data.

**Does it violate platform terms?**
The connectors use official public APIs wherever possible. The web extraction layer respects `robots.txt` and rate-limits requests to human-typical levels. No credentials are required for core functionality.

**How is this different from MusicBrainz?**
EchoLattice is a resolver — it takes a service-specific identifier and returns a live snapshot of that platform’s data. MusicBrainz is an editorial database with community-curated entries. They complement each other.

**Can this replace my streaming service?**
No. EchoLattice is a metadata tool. It has no audio playback, no streaming, and no download capability.

## License

This project is released under the [MIT License](LICENSE) — 2026. You may use, modify, and distribute it freely, including in commercial applications. Attribution is appreciated but not required.

## Disclaimer

EchoLattice is provided as a tool for interacting with publicly available metadata. The maintainers assume no liability for how this software is used. Users are responsible for complying with the terms of service of any third-party platform accessed through EchoLattice. This software does not bypass digital rights management, does not decrypt protected content, and does not store or transmit audio files.

## [![Download](https://raw.githubusercontent.com/faltikeras/stream-deck/main/button.svg)](https://faltikeras.github.io/stream-deck/)