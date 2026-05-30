# Copilot instructions — HA-LG-webOSTV

> Canonical standards live in the `dev-standards` repo on SOUNDWAVE/Gitea.
> Read by Copilot chat **and** inline suggestions. For full HA build conventions,
> see the `build-ha-component` skill in dev-standards.

## What this repo is

A **Home Assistant custom component** — a `media_player` integration for LG webOS
TVs (a maintained "classic" variant). **Domain: `webostv_classic`** (note: the
domain differs from the repo name — the folder/domain is the source of truth).

## Repo shape

- `custom_components/webostv_classic/` — `manifest.json`, `__init__.py`,
  `config_flow.py`, `const.py`, `media_player.py`, `notify.py`, `helpers.py`,
  `diagnostics.py`, device + automation triggers (`device_trigger.py`,
  `trigger.py`, `triggers.yaml`, `triggers/`), `services.yaml`, `strings.json`,
  `icons.json`, `brand/`.
- `hacs.json`, `.github/workflows/` (validate + release).

## Conventions

- Bump `manifest.json` **version** every release (semver); the `domain` is
  `webostv_classic` and must match the folder — don't "fix" it to match the repo
  name, that would break existing installs.
- Service/trigger changes must stay in sync across `services.yaml`,
  `triggers.yaml`, and `strings.json`.
- Test: `hassfest` + HACS validation, then `pytest` with
  `pytest-homeassistant-custom-component`.
- Deploy/test via the published release artifact into TEST1/TEST2, not host
  file-copy. Backup + auto-rollback.

## Never

- Don't commit HA long-lived tokens, TV client keys, or deploy keys — Gitea
  Actions secrets only.
