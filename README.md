# Ledgerly presets

The bank and e-wallet presets offered in the Ledgerly app. The app downloads `presets.json` from this
repository (raw link) whenever someone opens **Automations → Presets**, so changes here reach phones
without an app update. Presets are only offered: rules people already added never change.

## Editing a preset

1. Edit `presets.json` (one entry per bank or e-wallet in `presets`).
2. Every rule needs at least one real sample message (anonymise card numbers and names) with what the
   rule must read from it (`amount`, `merchant`, `type`, `category`). Rules that misread a sample are
   dropped by the app.
3. Raise the preset's `updatedAt` (shown to people as "Last updated") and the file's `catalogVersion`.
   Phones only take a catalog with a higher `catalogVersion` than the one they have.
4. Copy the same file to the app's `app/src/main/assets/presets.json` and run `BundledPresetsTest`, which
   runs every sample through Ledgerly's real parser. Publish here only when it passes.

## Fields

| Field | Meaning |
|---|---|
| `id` | Stable id, e.g. `jo-arab-bank` (never reuse for another bank) |
| `name` | The bank's or e-wallet's name |
| `kind` | `bank` or `wallet` |
| `updatedAt` | Date the preset last changed (`yyyy-MM-dd`) |
| `senders` | SMS sender IDs / numbers; used to suggest the preset from the caller ID |
| `rules[].keyword` | Text a message must contain |
| `rules[].actions` | What to read or set (same format as the app's SMS rules) |
| `rules[].samples` | Real messages and what must be read from them |

The file holds only patterns and category names, nothing private. Keep two-factor login on for this
GitHub account: whoever can edit this repository can change the presets everyone is offered.
