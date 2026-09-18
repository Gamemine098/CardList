# Buddyfight 2D Unity — Card JSON Specification for Anti Gravity
## Purpose
This document is the content-contract for the agent that imports real Buddyfight cards into JSON. Its job is to produce valid card-definition data only. It is not authorization to write C# rules-engine code, invent game rules, infer missing rulings, or change this schema.

The Unity Rule Engine is data-driven: it resolves structured fields such as `trigger`, `condition`, `cost`, `effects`, `rules`, and `protection`. Card text is display/localization data only. The engine must never parse English or Thai card text to decide gameplay.

## Agent Instructions
- Use only the card image/text/ruling/source supplied for that card. Preserve uncertainty; never fill a gap with a plausible interpretation.
- Output JSON that conforms to this specification and its enums. Do not add ad-hoc keys, aliases, `custom_effect`, embedded scripts, or per-card schema variants.
- Put every resolvable rule in structured fields. `effect_text` must match the supplied wording, but is never the source of gameplay logic.
- Keep card definition (the playable rule object) separate from its `printings[]` (set number, rarity, image, language/art). Reprints add a printing; they do not duplicate abilities.
- Use explicit IDs and references. `id` is an immutable internal card-definition identifier; official set/number belongs in `printings[].card_number`.
- Use an enum exactly as defined. If the necessary enum, effect, trigger, condition, selector, cost, or ruling does not exist, stop and report `UNSUPPORTED_MECHANIC`; do not design a new structure.
- Supply `effect_text.en.plain` and `effect_text.th.plain` only when that language was actually supplied or translated/approved. Do not fabricate translations. `segments[]` is optional presentation metadata.

## Data Model
### Static card definition vs. printing vs. runtime state
`CardDefinition` is immutable content: name, type, stats, worlds, attributes, costs, rules, and abilities. `Printing` is a collectible/display occurrence of a definition in a product. `CardInstance`, zones, current power, rest state, souls, nullification, duration counters, and restriction usage are runtime state and must never be stored in card JSON.

```text
CardDefinition (one playable identity)
├── id: CARD_FD11_001
├── abilities/rules/stats: shared logic
└── printings[]
    ├── FD11/001 + image A
    └── later reprint + image B
```

### Required card shape
```json
{
  "schema_version": 2,
  "id": "CARD_FD11_001",
  "name": { "en": "Verified card name" },
  "type": "MONSTER",
  "worlds": ["ANCIENT_WORLD"],
  "attributes": ["HUNDRED_DEMONS"],
  "stats": { "size": 0, "power": 2000, "critical": 1, "defense": 1000 },
  "call_cost": [],
  "use_restrictions": [],
  "rules": [],
  "abilities": [],
  "printings": [
    {
      "id": "PRINT_FD11_001",
      "set_id": "FD11",
      "card_number": "FD11/001",
      "image": { "path": "cards/fd11/fd11_001.webp" }
    }
  ]
}
```

`worlds[]`, `attributes[]`, `abilities[]`, `rules[]`, `call_cost[]`, and `use_restrictions[]` are always arrays, including when empty. `stats` is required only for card types that have printed stats. The approved top-level card types are `MONSTER`, `SPELL`, `ITEM`, `FLAG`, `IMPACT`, and `BUDDY`.

### Ability and text shape
```json
{
  "id": "CARD_FD11_001-A01",
  "kind": "AUTO",
  "keywords": ["DROP", "DUO"],
  "skill_restrictions": [],
  "trigger": { "type": "PHASE_START", "phase": "ATTACK" },
  "activation_condition": { "type": "CARD_IN_ZONE", "card": "THIS_CARD", "owner": "SELF", "zones": ["DROP"] },
  "optional": true,
  "cost": [],
  "effects": [],
  "effect_text": {
    "en": {
      "plain": "Exact supplied wording.",
      "segments": [
        { "text": "Exact", "style": "KEYWORD" },
        { "text": " supplied wording." }
      ]
    }
  }
}
```

`effect_text.<lang>.plain` is a complete readable line. If `segments[]` is present, concatenate `segments[].text` exactly to produce `plain`. Allowed semantic styles are `KEYWORD`, `RESTRICTION`, `ABILITY_NAME`, `COST`, `ZONE`, `PHASE`, `TURN`, `PLAYER`, `CARD_REFERENCE`, `ATTRIBUTE`, `STAT_MODIFIER`, `DAMAGE`, `EFFECT_SOURCE`, and `EFFECT_IMMUNITY`. Styles do not contain colours; Unity maps each semantic style to the active theme.

## Schema Rules
### Core enums and references
Use uppercase enum values. Use `THIS_CARD`, `THIS_ABILITY`, `SELF`, `OPPONENT`, and `EVENT.*` only where the corresponding schema accepts a reference. A card reference uses `card_id`; never rely on an English name to resolve logic.

Use `MOVE_CARD` only when a card changes zone (for example `HAND` to `DROP`, or `DROP` to `FIELD`). Use `MOVE_POSITION` only when it changes position within a zone/field (for example left to center). Do not collapse both operations into `MOVE`.

Approved common zones: `DECK`, `HAND`, `DROP`, `REMOVE`, `GAUGE`, `LIFE`, `FIELD`, `ITEM_ZONE`, `FLAG_ZONE`, `SOUL`, `SOUL_FACE_UP`, `SOUL_FACE_DOWN`. Field positions are `LEFT`, `CENTER`, and `RIGHT`.

### Effect tree
Every ability has `effects[]`. Its children are effect nodes; arrays run in written order. An effect tree may nest only the approved control nodes below:

```json
{
  "type": "SEQUENCE",
  "effects": [
    { "type": "DRAW", "amount": 1 },
    {
      "type": "IF",
      "condition": { "type": "PLAYER_HAS_CARDS", "player": "SELF", "zone": "DROP", "minimum": 1 },
      "then": [{ "type": "MOVE_CARD", "from": "DROP", "to": "HAND", "target": { "type": "SELECT", "count": 1 } }],
      "else": []
    }
  ]
}
```

Approved control nodes:
- `SEQUENCE`: resolve `effects[]` in order.
- `CHOICE`: controller chooses exactly one `options[]` branch; each branch has an `id` and `effects[]`.
- `IF`: resolve `then[]` or `else[]` from an approved condition.
- `REPEAT`: repeat `effects[]` using explicit `count` or a supported quantified value.

Do not encode choices, timing, a condition, or a duration only in prose.

## Restriction Rules
Restrictions have two locations:
- `use_restrictions[]` on a card: controls using/calling/casting that card.
- `skill_restrictions[]` on an ability: controls activation/resolution of that ability.

Every runtime restriction must include `source`. This lets nullification remove only a restriction granted by the nullified source, while a restriction created independently by another effect remains active.

```json
{
  "type": "NAMED_ABILITY_LIMIT",
  "ability_name": "Ivory Fiend Shadow",
  "count": 1,
  "period": "TURN",
  "source": {
    "kind": "CARD",
    "card_id": "CARD_FD11_001",
    "ability_id": "CARD_FD11_001-A01"
  }
}
```

Allowed `source.kind` values are `CARD`, `EFFECT`, and `RULE`. A restriction from a nullified card ability has `source.kind: CARD` and becomes inactive with that ability. A restriction created by an already-resolved effect has `source.kind: EFFECT` and does not disappear merely because its target card is nullified. The engine tracks successful uses; a failed attempt does not consume a limit.

Use approved restriction types: `ACTIVATION_LIMIT`, `NAMED_ABILITY_LIMIT`, `CARD_USE_LIMIT`, `SET_LIMIT`, and `SPECIAL_SKILL_LIMIT`. Approved periods are `TURN`, `GAME`, and `PHASE` when supported by that type. Encode `[1/Turn]`, `[An/Turn]`, `[Call/1Turn]`, and `[Cn/Turn]` as structured restrictions, never as keyword text alone.

## Effect, Condition, and Trigger Model
An ability is evaluated in this order: check timing/trigger → evaluate activation condition → choose legal targets/choice → pay cost → register restriction use at successful commit → resolve effect tree → emit events and open legal response timing.

Common triggers include `PHASE_START`, `EVENT`, `COUNTER_TIMING`, `ATTACK_DECLARED`, and `DAMAGE_RECEIVED`. The event name and event actor/cause must be explicit, e.g. `{ "type": "EVENT", "event": "HEAL" }`. Conditions use composable nodes such as `AND`, `OR`, `NOT`, `CARD_IN_ZONE`, `CARD_EXISTS`, `EVENT_ACTOR`, `EVENT_CAUSE`, `SHARES_ATTRIBUTE`, `PLAYER_HAS_CARDS`, and `STAT_COMPARE` only when they are in the engine registry.

Common effect primitives include `CALL`, `CAST`, `DRAW`, `DAMAGE`, `NEGATE_ATTACK`, `MOVE_CARD`, `MOVE_POSITION`, `REST`, `STAND`, `DESTROY`, `REMOVE_SOUL`, `ADD_SOUL`, `MODIFY_STAT`, `GRANT_ABILITY`, `CREATE_RESTRICTION`, `PROTECTION`, and `ATTACK_RULE`. A `CALL` must state source zone, targets, destination, and whether call cost is paid. Costs use the same structured primitive vocabulary but live in `cost[]`; they are not post-resolution effects.

### Duration and modifiers
Use a structured `duration`, never informal text. Supported duration forms include:
```json
[
  { "type": "UNTIL_END_OF_TURN" },
  { "type": "UNTIL_END_OF_NEXT_TURN", "anchor_player": "SELF" },
  { "type": "WHILE_CONDITION", "condition": { "type": "CARD_EXISTS", "card_id": "CARD_X", "zones": ["FIELD"] } }
]
```
Continuous effects and replacement effects are modifiers registered by an ability, with an explicit source, condition, scope, and duration. They must be checked by the engine at the appropriate event interception point; they are not one-time text substitutions.

## Attack, Damage, Defense, and Protection Model
### Attack and damage
Attack properties are structured modifiers attached to the attack, not strings in `keywords[]`:
```json
{
  "type": "ATTACK_RULE",
  "target": "THIS_CARD_ATTACK",
  "rules": ["CANNOT_BE_NEGATED", "OPPONENT_CANNOT_COUNTER"]
}
```
```json
{
  "type": "DAMAGE_RULE",
  "source": "THIS_CARD_ATTACK",
  "rules": ["CANNOT_BE_REDUCED"]
}
```

Defense uses explicit effects: `NEGATE_ATTACK`, `MODIFY_NEXT_DAMAGE` (with `occurrences: 1` and duration), `REDIRECT_ATTACK`, and `DAMAGE_PROTECTION`. The engine applies prevention/replacement/modification in its prescribed pipeline; content must not claim priority by prose.

### Generic protection interceptor
Use the generic `PROTECTION` effect, not bespoke `immune[]` flags. It registers an interceptor with a target, action, source scope, optional condition, and duration.

```json
{
  "type": "PROTECTION",
  "target": "THIS_CARD",
  "action": "DESTROY",
  "source": "CARD_EFFECT",
  "duration": { "type": "WHILE_SOURCE_ACTIVE" }
}
```

Approved protection actions include `DESTROY`, `LEAVE_FIELD`, `RETURN_TO_HAND`, `REST`, `REMOVE_SOUL`, `RETURN_SOUL_TO_DECK`, `NULLIFY`, and `MOVE_POSITION`. Source scope is explicit: `CARD_EFFECT`, `CARD`, `RULE`, `BATTLE`, `OPPONENT_CARD_EFFECT`, or `ALL`. `CARD_EFFECT` and `CARD` are intentionally different scopes; do not substitute one for the other.

Stat protection uses its own standard form:
```json
{
  "type": "STAT_PROTECTION",
  "target": "THIS_CARD",
  "stats": ["POWER", "DEFENSE", "CRITICAL"],
  "restriction": "CANNOT_BE_REDUCED",
  "duration": { "type": "WHILE_SOURCE_ACTIVE" }
}
```

## Special Skills, Transformations, and Buddy
`OVERTURN`, `OVERTHROW`, `OVERKILL`, `OVERKILL_REBOOT`, and `OVERDRIVE` are special skills, not ordinary unparameterized keywords. Each uses `SPECIAL_SKILL_LIMIT` with `count: 1`, `period: GAME`, and has a counter lock during its resolution.

```json
{
  "type": "SPECIAL_SKILL",
  "skill": "OVERTURN",
  "skill_restrictions": [{
    "type": "SPECIAL_SKILL_LIMIT",
    "count": 1,
    "period": "GAME",
    "source": { "kind": "CARD", "card_id": "CARD_EXAMPLE", "ability_id": "CARD_EXAMPLE-A01" }
  }],
  "resolution_rules": [{ "type": "COUNTER_LOCK", "player": "OPPONENT", "during": "RESOLUTION" }],
  "effects": []
}
```

Transformations (`TRANSFORM`, `IMPACT_TRANSFORM`, `DRAGONIFY`, `EQUIPMENT_CHANGE`) must reference a dedicated transformation structure supplied by the engine: source card/instance, target representation, placement, retained state, and duration. Buddy mechanics (`BUDDY`, `DOUBLE_BUDDY`, `TRIPLE_BUDDY`, `BUDDYCOST`, `BUDDYGIFT`, `GIFT`, `DUO`) must use their dedicated structured fields and references; do not encode their relationship only in text.

## Keyword Registry
`keywords[]` records an approved printed keyword and helps UI/search. It does not replace mechanics. Parameterized keywords must also have structured data (for example `LIFELINK` needs an explicit amount; multi-attack needs its attack count/rule object; `DUO` needs a referenced card and active condition).

Known registry entries requiring a matching implementation/ruling before use: `DOUBLE_ATTACK`, `TRIPLE_ATTACK`, `QUADRUPLE_ATTACK`, `HEXTUPLE_ATTACK`, `SOULGUARD`, `PENETRATE`, `MOVE`, `LIFELINK`, `LIFELINK_LOSS`, `CHAOS_TERRITORY`, `SET`, `COUNTERATTACK`, `RIDE`, `TRANSFORM`, `IMPACT_TRANSFORM`, `STATION`, `DRAGOD`, `OMNI_LORD`, `AMBUSH`, `CROSSNIZE`, `PURGE`, `WEAPONRY_LINK`, `DOUBLE_BUDDY`, `TRIPLE_BUDDY`, `DRAGONIFY`, `EQUIPMENT_CHANGE`, `RELEASE_CONDITION`, `EVIL_DEITY`, `GREAT_EVIL_DEITY`, `REVERSAL`, `BUDDYCOST`, `BUDDYGIFT`, `GIFT`, `DUO`, `AUTO`, and `CONT`.

If wording/ruling or the engine implementation is not confirmed, do not guess its semantics. Return `UNSUPPORTED_MECHANIC` even when the keyword is listed above.

## Examples
All names, IDs, text, translations, references, and semantics in production JSON must be verified from supplied card data. These examples show schema usage; the FD11/S005 example deliberately encodes only the supplied structural facts rather than inventing unsupplied card effects.

### 1. FD11/001 — Drop call at start of Attack phase
```json
{
  "schema_version": 2,
  "id": "CARD_FD11_001",
  "name": { "en": "Shadow of Dragonic Earth Fiend, Shiroi" },
  "type": "MONSTER",
  "worlds": ["ANCIENT_WORLD", "LEGEND_WORLD"],
  "attributes": ["HUNDRED_DEMONS", "WYDAR_SARKAL", "WILD_DRAGON"],
  "stats": { "size": 0, "power": 2000, "critical": 1, "defense": 1000 },
  "call_cost": [],
  "use_restrictions": [],
  "rules": [],
  "abilities": [{
    "id": "CARD_FD11_001-A01",
    "kind": "AUTO",
    "keywords": ["DROP", "DUO"],
    "skill_restrictions": [{
      "type": "NAMED_ABILITY_LIMIT",
      "ability_name": "Ivory Fiend Shadow",
      "count": 1,
      "period": "TURN",
      "source": { "kind": "CARD", "card_id": "CARD_FD11_001", "ability_id": "CARD_FD11_001-A01" }
    }],
    "trigger": { "type": "PHASE_START", "phase": "ATTACK" },
    "activation_condition": { "type": "CARD_IN_ZONE", "card": "THIS_CARD", "owner": "SELF", "zones": ["DROP"] },
    "optional": true,
    "cost": [{ "type": "PAY_GAUGE", "amount": 1 }],
    "effects": [{
      "type": "CALL",
      "from": "DROP",
      "to": "FIELD",
      "targets": [
        { "type": "THIS_CARD", "maximum": 1 },
        { "type": "DUO", "card_id": "CARD_FD11_002", "maximum": 1 }
      ],
      "pay_call_cost": false
    }],
    "effect_text": {
      "en": {
        "plain": "[Drop]: [An/Turn] \"Ivory Fiend Shadow\" At the start of the attack phase, you may pay 1 gauge. If you do, call up to one each of this card and its [Duo] from your drop without paying their [Call Cost].",
        "segments": [{ "text": "[Drop]", "style": "ZONE" }, { "text": ": " }, { "text": "[An/Turn]", "style": "RESTRICTION" }, { "text": " \"Ivory Fiend Shadow\"", "style": "ABILITY_NAME" }, { "text": " At the start of the attack phase, you may pay 1 gauge. If you do, call up to one each of this card and its [Duo] from your drop without paying their [Call Cost]." }]
      }
    }
  }],
  "printings": [{ "id": "PRINT_FD11_001", "set_id": "FD11", "card_number": "FD11/001", "image": { "path": "cards/fd11/fd11_001.webp" } }]
}
```

### 2. FD11/031 — Flag rules
```json
{
  "schema_version": 2,
  "id": "CARD_FD11_031",
  "name": { "en": "Verified FD11/031 name required" },
  "type": "FLAG",
  "worlds": [],
  "attributes": [],
  "call_cost": [],
  "use_restrictions": [],
  "rules": [
    { "type": "ALLOW_CARD_ATTRIBUTE", "attribute": "HUNDRED_DEMONS" },
    { "type": "ALLOW_GENERIC" }
  ],
  "abilities": [],
  "printings": [{ "id": "PRINT_FD11_031", "set_id": "FD11", "card_number": "FD11/031", "image": { "path": "cards/fd11/fd11_031.webp" } }]
}
```

### 3. FD11/S005 — Counter spell with an exclusive choice and two durations
```json
{
  "schema_version": 2,
  "id": "CARD_FD11_S005",
  "name": { "en": "Verified FD11/S005 name required" },
  "type": "SPELL",
  "worlds": [],
  "attributes": [],
  "call_cost": [],
  "use_restrictions": [],
  "rules": [],
  "abilities": [{
    "id": "CARD_FD11_S005-A01",
    "kind": "ACT",
    "keywords": ["COUNTER"],
    "skill_restrictions": [{
      "type": "ACTIVATION_LIMIT",
      "count": 1,
      "period": "TURN",
      "source": { "kind": "CARD", "card_id": "CARD_FD11_S005", "ability_id": "CARD_FD11_S005-A01" }
    }],
    "trigger": { "type": "COUNTER_TIMING" },
    "cost": [],
    "effects": [{
      "type": "CHOICE",
      "choose": 1,
      "options": [
        { "id": "CURRENT_TURN", "effects": [{ "type": "GRANT_MODIFIER", "modifier_ref": "VERIFIED_EFFECT_A", "duration": { "type": "UNTIL_END_OF_TURN" } }] },
        { "id": "NEXT_TURN", "effects": [{ "type": "GRANT_MODIFIER", "modifier_ref": "VERIFIED_EFFECT_B", "duration": { "type": "UNTIL_END_OF_NEXT_TURN", "anchor_player": "SELF" } }] }
      ]
    }],
    "effect_text": { "en": { "plain": "[Cn/Turn] [Counter] Choose one of the two verified effects.", "segments": [{ "text": "[Cn/Turn]", "style": "RESTRICTION" }, { "text": " " }, { "text": "[Counter]", "style": "KEYWORD" }, { "text": " Choose one of the two verified effects." }] } }
  }],
  "printings": [{ "id": "PRINT_FD11_S005", "set_id": "FD11", "card_number": "FD11/S005", "image": { "path": "cards/fd11/fd11_s005.webp" } }]
}
```

Replace `VERIFIED_EFFECT_A/B` only with an existing engine modifier after the exact printed effect/ruling is supplied. This is not permission to infer the two effects.

### 4. Protection package
```json
{
  "type": "SEQUENCE",
  "effects": [
    { "type": "PROTECTION", "target": "THIS_CARD", "action": "DESTROY", "source": "CARD_EFFECT", "duration": { "type": "WHILE_SOURCE_ACTIVE" } },
    { "type": "PROTECTION", "target": "THIS_CARD", "action": "LEAVE_FIELD", "source": "CARD_EFFECT", "duration": { "type": "WHILE_SOURCE_ACTIVE" } },
    { "type": "PROTECTION", "target": { "type": "SOUL", "of": "THIS_CARD" }, "action": "REMOVE_SOUL", "source": "ALL", "duration": { "type": "WHILE_SOURCE_ACTIVE" } },
    { "type": "PROTECTION", "target": { "type": "ABILITIES", "of": "THIS_CARD" }, "action": "NULLIFY", "source": "ALL", "duration": { "type": "WHILE_SOURCE_ACTIVE" } },
    { "type": "STAT_PROTECTION", "target": "THIS_CARD", "stats": ["POWER", "DEFENSE", "CRITICAL"], "restriction": "CANNOT_BE_REDUCED", "duration": { "type": "WHILE_SOURCE_ACTIVE" } }
  ]
}
```

### 5. Special skill and attack rule
```json
{
  "id": "CARD_EXAMPLE-A01",
  "kind": "SPECIAL_SKILL",
  "keywords": [],
  "skill_restrictions": [{
    "type": "SPECIAL_SKILL_LIMIT",
    "count": 1,
    "period": "GAME",
    "source": { "kind": "CARD", "card_id": "CARD_EXAMPLE", "ability_id": "CARD_EXAMPLE-A01" }
  }],
  "special_skill": "OVERDRIVE",
  "resolution_rules": [{ "type": "COUNTER_LOCK", "player": "OPPONENT", "during": "RESOLUTION" }],
  "effects": [
    { "type": "ATTACK_RULE", "target": "THIS_CARD_ATTACK", "rules": ["CANNOT_BE_NEGATED", "OPPONENT_CANNOT_COUNTER"] },
    { "type": "DAMAGE_RULE", "source": "THIS_CARD_ATTACK", "rules": ["CANNOT_BE_REDUCED"] }
  ]
}
```

## Validation Rules
- JSON parses, uses `schema_version: 2`, and has no unknown fields or enum values.
- Definition `id`, ability IDs, and printing IDs are unique; every `card_id`, `ability_id`, set ID, and image path resolves.
- Required arrays exist. A printing includes `set_id`, `card_number`, and `image.path`.
- Logic is fully represented by trigger, condition, cost, restriction, rule, effect, modifier, or protection data. `effect_text` is not used as logic.
- Every restriction has a valid `source`; a limit has valid `count` and compatible `period`.
- Every target/selector is explicit and legal for its effect. A `CHOICE` has a positive `choose` count and valid options.
- Durations are structured. No unbounded modifier, replacement, or protection is created without a valid duration/condition.
- `MOVE_CARD` and `MOVE_POSITION` are used in the correct domain.
- `segments[]`, when present, concatenate exactly to `plain` and use semantic styles only.
- Parameterized keywords have their matching structured values. Unsupported wording is reported, not approximated.

## Unsupported Mechanic Policy
If a supplied card cannot be represented exactly, return this report instead of card JSON or schema changes:
```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/S005",
  "ability_reference": "printed ability label or text excerpt",
  "missing_capability": "EFFECT_TYPE | CONDITION | TRIGGER | TARGET_SELECTOR | COST | KEYWORD_RULING | REPLACEMENT_RULE",
  "what_is_known": "Only facts explicitly supplied by the card/source.",
  "information_needed": ["Exact official wording", "Relevant official ruling", "Approved engine enum/schema addition"]
}
```
Do not invent a workaround. Do not use free-text logic. Wait for the engine/schema owner to add and document the capability, then encode the card with that approved form.

## Output Checklist
- [ ] I created/updated only card JSON, not engine code or an ad-hoc schema.
- [ ] Each card has one immutable definition ID and one or more distinct printings.
- [ ] Official card number and image are in `printings[]`.
- [ ] `worlds[]`, `attributes[]`, `abilities[]`, and required empty arrays are present.
- [ ] Plain localized text is display-only; structured fields contain all known logic.
- [ ] Every skill/use restriction has source provenance for nullification behavior.
- [ ] Effects use approved tree nodes, events, conditions, targets, costs, durations, and enums.
- [ ] Protection, attack rules, special skills, transformations, and buddy mechanics use their standard structures.
- [ ] I did not guess parameterized keywords, card text, translations, rulings, or effect semantics.
- [ ] Any gap is returned as `UNSUPPORTED_MECHANIC` with the missing information.
