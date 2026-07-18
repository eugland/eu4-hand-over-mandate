# Hand Over the Mandate

EU4 mod: the Emperor of China can voluntarily hand the Mandate of Heaven to a nation of their choosing — any culture, any religion.

Built for **EU4 1.37.x**, requires the **Mandate of Heaven** DLC. Disables ironman/achievements (as any mod does).

## Features

- **"Hand Over the Mandate" decision** — available to the Emperor of China while at peace. Opens an event listing up to **8 candidate nations**, strongest first (ranked by total development).
- **Candidate pool** — any nation bordering the Emperor or any tributary of the Emperor. Any culture, any religion. Excluded: revolutionaries, the shogunate, non-tributary subjects.
- **Clean abdication** — the vanilla "Mandate of Heaven lost" modifier (20 years) and −2 stability are compensated: the abdicating emperor keeps stability and gains +10 prestige.
- **Opened Take Mandate CB** — the vanilla `cb_take_mandate` religion gate (pagan/eastern only) and AI culture gate (East Asian only) are removed. Any nation bordering the Emperor can declare a Take Mandate war.

## Install

1. Copy the `hand_over_mandate` folder into `Documents/Paradox Interactive/Europa Universalis IV/mod/`.
2. Create `hand_over_mandate.mod` next to it (or let the launcher generate one):

   ```
   name="Hand Over the Mandate"
   path="mod/hand_over_mandate"
   supported_version="1.37.*"
   ```

3. EU4 launcher → Playsets → add and enable the mod.

## Testing

Start as any Emperor of China (e.g. Ming), open console (`~`):

```
event ham_events.1
```

Or use the decision from the decisions tab. Script errors, if any, appear in `Documents/Paradox Interactive/Europa Universalis IV/logs/error.log` under `ham_` entries.

## File layout

```
decisions/ham_decisions.txt              decision button
events/ham_events.txt                    candidate list + choice + notify events
common/scripted_triggers/                eligibility rules
common/scripted_effects/                 top-8 ranking + flag cleanup
common/cb_types/zz_ham_cb_types.txt      cb_take_mandate override
localisation/ham_l_english.yml           English text (UTF-8 BOM)
```

## Compatibility

- `common/cb_types/zz_ham_cb_types.txt` fully overrides vanilla `cb_take_mandate`; incompatible with other mods that touch that CB.
- Everything else is additive (`ham_`-prefixed) — no vanilla files replaced.
