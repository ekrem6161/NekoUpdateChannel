# NekoUpdateChannel

The **update channel** for the NekoHub application. On startup, NekoHub downloads `repos.json` from this repository and learns which projects it should manage.

- Raw file: `https://raw.githubusercontent.com/ekrem6161/NekoUpdateChannel/main/repos.json`
- To add a new project, append an entry to `repos.json` and push to `main`.

## repos.json schema

| Field | Required | Description |
|---|---|---|
| `name` | ✅ | Project name (also used as the folder name) |
| `url` | ✅ | GitHub repository URL (ZIP and `VERSION.TXT` are fetched from here) |
| `fqbn` | ❌ | Arduino board identifier, e.g. `arduino:avr:uno`. If empty, firmware is not managed |
| `firmwarePath` | ❌ | Sketch folder inside the repo, e.g. `firmware/NekoM550D` |
| `pcApp` | ❌ | PC application folder inside the repo, e.g. `pc/NekoM550D.Monitor`. If empty, the PC application is not managed |

### Example

```json
[
  {
    "name": "NekoM550D",
    "url": "https://github.com/ekrem6161/NekoM550D",
    "fqbn": "arduino:avr:uno",
    "firmwarePath": "firmware/NekoM550D",
    "pcApp": "pc/NekoM550D.Monitor"
  }
]
```

## Versioning rule

Every project repository must contain a `VERSION.TXT` file at its **root**, with only the version number inside:

```
1.2.8
```

NekoHub compares this file against the installed version. Publishing a new release = bump the contents of `VERSION.TXT` and push.

## Project types

- **Firmware only:** `fqbn` and `firmwarePath` set, `pcApp` empty.
- **PC application only:** `pcApp` set, `fqbn` and `firmwarePath` empty.
- **Both:** all fields set (e.g. NekoM550D).
