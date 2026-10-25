# merge-manza-config

Public configuration repo for **Merge Manza** ([game repo](https://gitlab.com/MagicalCoder-12/merge-manza) — private).

This repo intentionally contains no game source. It only hosts files the shipped game fetches over HTTPS, so it must stay **public**.

## update.json

Fetched by the game's `UpdateChecker` autoload on startup (non-editor builds) from:

```
https://gitlab.com/MagicalCoder-12/merge-manza-config/-/raw/main/update.json
```

| Field            | Meaning                                                                 |
|------------------|-------------------------------------------------------------------------|
| `latest_version` | Newest published version of the game.                                   |
| `min_version`    | Oldest version allowed to run without an update prompt.                 |
| `force`          | When `true`, the update prompt is non-dismissable for outdated builds.   |

Current state:

```json
{"latest_version": "1.0.1", "min_version": "1.0.0", "force": true}
```

## How to roll an update

1. Upload a new build to the Play Store.
2. Update `update.json` here (e.g. `latest_version: "1.0.2"`).
3. Commit to `main`. Changes go live immediately (raw file is served on push).

Notes:

- Version comparison is semver-style (`X.Y.Z` parsed numerically), so keep the format.
- The check **fails open**: if this URL is unreachable, the game runs normally.
- Raw access requires this project to remain public; do not flip it to private.
