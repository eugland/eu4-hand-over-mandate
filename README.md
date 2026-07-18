# Hand Over the Mandate

EU4 mod: in the golden age, Yao yielded the throne to Shun, and Shun to Yu — not to their sons, but to the most capable, and Heaven approved. This mod lets the Emperor of China follow the way of the sage-kings and voluntarily offer the Mandate of Heaven to a nation of their choosing — any culture, any religion. The chosen nation may accept or refuse. A Mandate freely given is never lost.

Built for **EU4 1.37.x**, requires the **Mandate of Heaven** DLC. Disables ironman/achievements (as any mod does).

## Features

- **"Hand Over the Mandate" decision** — available to the Emperor of China while at peace. Opens an event listing up to **8 candidate nations**, ranked exactly by total development (strongest first).
- **Candidate pool** — any nation bordering the Emperor or any tributary of the Emperor. Any culture, any religion. Excluded: revolutionaries, the shogunate, non-tributary subjects.
- **Consent** — the chosen nation receives the offer and may accept or refuse. A refuser is excluded when the Emperor picks again. AI accepts unless it is at war with the Emperor or despises them (opinion below −50).
- **Clean abdication** — the vanilla "Mandate of Heaven lost" modifier and −2 stability are compensated: the abdicating emperor keeps stability and gains +10 prestige.
- **5-year cooldown** — after a completed handover the decision is locked for 5 years, so the Mandate cannot ping-pong.
- **AI emperors participate** — an AI Emperor of China abdicates when the dynasty is collapsing (Mandate below 20), preferring the strongest candidate.
- **Diplomatic fallout** — the new Emperor is deeply grateful to the abdicator (+100, 20 yrs); passed-over candidates resent the new Emperor (−25, 10 yrs); refusing the offer slights the old Emperor (−10, 5 yrs).
- **Tributaries may follow the Mandate** — after the handover the old Emperor chooses whether their tributaries transfer to the new Son of Heaven or stay.
- **Opened Take Mandate CB** — the vanilla `cb_take_mandate` religion gate (pagan/eastern only) and AI culture gate (East Asian only) are removed. Any nation bordering the Emperor can declare a Take Mandate war.

## Install

1. Copy the `hand_over_mandate` folder into `Documents/Paradox Interactive/Europa Universalis IV/mod/`.
2. Create `hand_over_mandate.mod` next to it (or let the launcher generate one):

   ```
   name="Hand Over the Mandate"
   path="mod/hand_over_mandate"
   picture="thumbnail.png"
   supported_version="1.37.*"
   ```

3. EU4 launcher → Playsets → add and enable the mod.

## Steam Workshop upload

EU4 launcher → **All installed mods** → Hand Over the Mandate → **Upload to Paradox Mods / Steam Workshop** (requires the launcher signed in to a Paradox account linked to Steam). `thumbnail.png` is used automatically.

## Testing

Start as any Emperor of China (e.g. Ming), open console (`~`):

```
event ham_events.1
```

Or use the decision from the decisions tab. Script errors, if any, appear in `Documents/Paradox Interactive/Europa Universalis IV/logs/error.log` under `ham_` entries.

## Event flow

```
decision → ham_events.1 (menu, top-8 by development)
             └─ offer → ham_events.4 (candidate: accept / refuse)
                          ├─ accept  → transfer + ham_events.3 (old emperor:
                          │            release tributaries to new emperor or keep)
                          └─ refuse  → ham_events.5 (old emperor: pick another / give up)
```

## File layout

```
decisions/ham_decisions.txt              decision (cooldown, AI weighting)
events/ham_events.txt                    menu, offer, refusal, tributary events
common/scripted_triggers/                eligibility rules
common/scripted_effects/                 exact top-8 ranking + flag cleanup
common/opinion_modifiers/                diplomatic fallout modifiers
common/cb_types/zz_ham_cb_types.txt      cb_take_mandate override
localisation/ham_l_<lang>.yml            english, french, german, spanish (UTF-8 BOM)
thumbnail.png                            launcher/Workshop thumbnail
```

## Compatibility

- `common/cb_types/zz_ham_cb_types.txt` fully overrides vanilla `cb_take_mandate`; incompatible with other mods that touch that CB.
- Everything else is additive (`ham_`-prefixed) — no vanilla files replaced.
