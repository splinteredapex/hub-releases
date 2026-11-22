# SplinteredApex Hub releases

Installers and updates for the SplinteredApex Hub. This repository holds releases only; there is no source code here.

- **Install:** download `Setup.exe` from the [latest release](https://github.com/splinteredapex/hub-releases/releases/latest) and run it. It installs for your Windows user only and needs no administrator rights.
- **Updates:** the Hub checks this repository and updates itself, never while you are on track.
- **Website:** [splinteredapex.com](https://splinteredapex.com)

## `status.json` (maintainers)

The Hub reads [`status.json`](status.json) from the `main` branch once, each time it opens. It is the brake for a release that is already on drivers' PCs. Edit it here on GitHub; the change reaches drivers within about five minutes, the next time they open the Hub.

```json
{
  "v": 1,
  "minimumVersion": "0.1.0-beta.9",
  "message": "One line shown to drivers on an older version.",
  "modules": {
    "livery-maker": { "off": true, "message": "One line shown on that module's page." }
  }
}
```

| Field | Effect |
|---|---|
| `minimumVersion` | Every older version shows a "Time for a new version" screen and can only update or quit. `null` holds nothing back. Publish the fixed release **before** setting this. |
| `message` | Optional. Replaces the built-in line on that screen. Plain text, one line, at most 280 characters. |
| `modules.<id>.off` | `true` closes that module's page with a notice; the rest of the Hub carries on. Remove the entry to switch it back on. Ids: `launch-control`, `replay-maker`, `livery-maker`. |
| `modules.<id>.message` | Optional. Replaces the built-in line on that page. |

Rules:

- Keep `"v": 1`. A file the Hub cannot read holds nothing back, so check the JSON is valid before saving.
- Nothing held back looks like this: `{ "v": 1, "minimumVersion": null, "message": null, "modules": {} }`
- The Hub applies the file only when it opens, never during a session.
