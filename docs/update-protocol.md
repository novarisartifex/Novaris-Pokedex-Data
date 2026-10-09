# Novaris data update protocol v1

The app keeps its bundled SQLite database as the offline fallback.

1. Fetch `manifest.json` over HTTPS, with a short network timeout.
2. Ignore updates unless `status` is `published` and `latest` points to a compatible package.
3. Compare the manifest's monotonically increasing integer `data_version` with the installed data version.
4. Download the complete `pokedex.db.gzdata` into a temporary file; limit download size and check SHA-256 against the manifest.
5. Decompress and validate the SQLite database (`PRAGMA integrity_check`), required schema, and Pokémon record count.
6. Atomically replace only the active downloaded database after all checks pass; keep the previous working copy for rollback.
7. Preserve all local user settings, favorites and other user-created state. Never overwrite them with the content package.
8. On any error or when offline, continue using the previous valid database.
9. Do not execute remotely downloaded code, HTML, or scripts.

## Future published manifest fields

```json
{
  "schema_version": 1,
  "channel": "stable",
  "status": "published",
  "latest": {
    "data_version": 2743,
    "source_version": "V27.43",
    "min_app_version_code": 10,
    "url": "https://github.com/novarisartifex/Novaris-Pokedex-Data/releases/download/data-v2743/pokedex.db.gzdata",
    "sha256": "<64-character SHA-256>",
    "size_bytes": 0,
    "pokemon_count": 1025
  }
}
```

The example above is **not** an actual release. A real manifest must contain verified size, hash, and compatible database schema. Public GitHub release assets are used for direct downloads. Changes to Android UI, Kotlin/Java, database schema or executable behavior still require an APK update.
