# Novaris Pokédex Data

Versioned, downloadable **content** for the Novaris Android Pokédex.

- [Update manifest](manifest.json) — stable-channel status and version metadata.
- [Update protocol](docs/update-protocol.md) — verification, atomic installation, offline fallback and rollback.

## Current status

The repository structure is initialized, but **no dataset is published yet**. The current Android app still uses its bundled database. A future app build must implement the manifest client before over-the-air content updates work.

## Architecture

Android app repository: https://github.com/novarisartifex/Novaris-Pokedex-Android

Data packages will be published as GitHub Release assets after database conversion and integrity validation. The app will fetch only compatible packages and will not change its UI or local user data.
