# Required Changes to Card Database Structure

## 1. Remove the `printings[]` approach
Do NOT store multiple printings inside the canonical card definition.

A card definition represents one unique card identity, regardless of how many sets contain that card.

Do not duplicate the same card's:
- stats
- worlds
- attributes
- abilities
- effects
- effect text
- image

just because the card appears in another set.

## 2. Separate Card Database and Set Database

Use this structure:

```
database/
├── cards/
│   ├── dragon_prudent_res.json
│   ├── ...
│   └── ...
└── sets/
    ├── fd11.json
    ├── s-ub05.json
    ├── bt01.json
    └── ...
```

`cards/` contains the canonical card definitions.

`sets/` contains only the cards included in each set and their set-specific card numbers.

## 3. Card ID

Every unique card must have a manually-independent, stable `card_id`.

The agent must generate the `card_id`.

Recommended format:

`UPPER_SNAKE_CASE`

Example:

`DRAGON_PRUDENT_RES`

The `card_id` must NOT be based on a set card number.

Do NOT use:

`FD11/S005`

as the canonical `card_id`.

The same card can have different card numbers in different sets.

## 4. Same Card in Multiple Sets

If the same card appears in multiple sets and its actual card definition is identical, use ONE `card_id`.

Example:

FD11/S005
S-UB05/XXX

can both reference:

`DRAGON_PRUDENT_RES`

Example:

cards/dragon_prudent_res.json

```json
{
  "card_id": "DRAGON_PRUDENT_RES",
  "name": {
    "en": "Dragon Prudent \"Re:S\"",
    "th": "ความรอบคอบของมังกร \"Re:S\""
  },
  "image": null,
  "type": "SPELL",
  "worlds": [
    "ANCIENT_WORLD"
  ],
  "attributes": [
    "HUNDRED_DEMONS",
    "DRAGON",
    "DEFENSE"
  ],
  "abilities": []
}
```

sets/fd11.json:

```json
{
  "set_id": "FD11",
  "cards": [
    {
      "card_number": "FD11/S005",
      "card_id": "DRAGON_PRUDENT_RES"
    }
  ]
}
```

sets/s-ub05.json:

```json
{
  "set_id": "S-UB05",
  "cards": [
    {
      "card_number": "S-UB05/XXX",
      "card_id": "DRAGON_PRUDENT_RES"
    }
  ]
}
```

## 5. Different Card Definition = Different Card ID

Do NOT merge cards merely because their names are identical.

If two cards have the same name but different:
- stats
- abilities
- effects
- card type
- world
- attributes
- or other gameplay-relevant rules

they must have different `card_id` values.

## 6. Image Handling

The agent must NOT select, download, rename, or infer card images.

The user will manually assign the canonical image.

The card definition contains only ONE `image` field.

Example:

```json
"image": "fd11/fd11_s005.webp"
```

If the user has not assigned an image yet:

```json
"image": null
```

Do not create duplicate images for different printings.

## 7. Set JSON Must Stay Lightweight

Set files should NOT duplicate the full card definition.

Do NOT put:
- stats
- effects
- abilities
- worlds
- attributes
- effect text
- image

inside the Set JSON.

The Set JSON should only identify the set and reference the canonical cards.

Example:

```json
{
  "set_id": "FD11",
  "cards": [
    {
      "card_number": "FD11/001",
      "card_id": "SHADOW_OF_DRAGONIC_EARTH_FIEND_SHIROI"
    },
    {
      "card_number": "FD11/S005",
      "card_id": "DRAGON_PRUDENT_RES"
    }
  ]
}
```

## 8. Agent Validation

Before creating a new card definition, check whether the card already exists in the database.

If the same card already exists:
- reuse the existing `card_id`
- do NOT create another card JSON
- add the card reference to the appropriate Set JSON

If the identity is uncertain, do NOT automatically merge the cards.

Report the uncertainty instead.

## 9. Important Principle

The database must follow:

ONE UNIQUE CARD
→ ONE `card_id`
→ ONE canonical card JSON
→ ONE canonical image

A card appearing in multiple sets does NOT create multiple card definitions.

Set membership is separate from card identity.
