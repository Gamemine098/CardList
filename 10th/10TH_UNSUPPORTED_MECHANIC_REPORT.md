# Unsupported Mechanic Report — 10th (0001–0010)

Specification reference: `Buddyfight_2D_Unity_Card_JSON_Agent_Spec.md` (Section: Unsupported Mechanic Policy).

---

## 1. Activation from `SOUL` Zone and Host Card Verification (`SOUL_HOST_MATCH`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0001, 10th/0004",
  "ability_reference": "10th/0001-A01: if this card is in the soul of a monster with \"Drum\" in its card name / 10th/0004-A01: call this card from a soul of a 《Dragod》",
  "missing_capability": "CONDITION",
  "what_is_known": "Abilities activate while the card is located in the SOUL zone of another monster on the field. The activation condition requires checking attributes or card name substrings of the host card containing this card in its soul.",
  "information_needed": [
    "Approved engine condition primitive for inspecting host card properties while in soul (e.g. SOUL_HOST_MATCH).",
    "Engine event dispatching confirmation for damage triggers while card is in the soul zone."
  ]
}
```

---

## 2. Stack Call Placement (`ON_TOP_OF` / Call on top of this card)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0001, 10th/0004",
  "ability_reference": "10th/0001-A02: call up to one monster with \"Drum\" in its card name from your deck on top of this card / 10th/0004-A02: call ... on top of this card",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Calling a monster directly on top of an existing monster puts the existing card (and its souls) into the soul of the newly called monster.",
  "information_needed": [
    "Approved placement property syntax in CALL effect node for calling on top of an existing field card.",
    "Engine ruling for automatic soul inheritance vs explicit MOVE_CARD to soul."
  ]
}
```

---

## 3. Continuous Damage Reduction with Source Exception

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0002",
  "ability_reference": "10th/0002-A01: damage dealt to you other than by your card effects is reduced by 3",
  "missing_capability": "REPLACEMENT_RULE",
  "what_is_known": "Continuous damage modification applies to all incoming damage to controller with an explicit exception filter (excluding damage caused by controller's own card effects).",
  "information_needed": [
    "Approved structure for DAMAGE_PROTECTION or DAMAGE_RULE with negative exception scopes (e.g. source_exception: YOUR_CARD_EFFECT)."
  ]
}
```

---

## 4. Keyword Alias & Multi-Zone Target Selection (`D-[G•EVO]`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0004",
  "ability_reference": "10th/0004-A02: D-[G•EVO] ... call ... from your hand or drop zone on top of this card ... (D-[G•EVO] is also treated as [G•EVO])",
  "missing_capability": "KEYWORD_RULING",
  "what_is_known": "D-[G•EVO] is an attack phase counter call ability treated by game rules as [G•EVO] for card effects that check for [G•EVO]. The target monster can be chosen from either HAND or DROP in a single selection action.",
  "information_needed": [
    "Approved engine taxonomy for keyword aliasing (treating D-[G•EVO] as G•EVO).",
    "Standard CALL schema for selecting across multiple source zones ([\"HAND\", \"DROP\"])."
  ]
}
```

---

## 5. Flagless Monster with Deck Construction Permission

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0004",
  "ability_reference": "10th/0004: You may use this card with all flags, and if it is your buddy, you may use 《Dragod》 monsters from all worlds.",
  "missing_capability": "RULE",
  "what_is_known": "Card has no printed world. Deck building rules allow inclusion under any flag, and when chosen as buddy, allows 《Dragod》 monsters of any world to be included in the deck.",
  "information_needed": [
    "Approved deck construction rule primitives (e.g. ALLOW_ALL_FLAGS, BUDDY_RULE with ALLOW_CARD_ATTRIBUTE across all worlds)."
  ]
}
```

---

## 6. Dynamic Scaling Life Gain (`COUNT_CARDS` on Field)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0005",
  "ability_reference": "10th/0005-A01: you gain 1 life for each card on your field",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Life gain amount is dynamically computed from the number of active cards on the controller's field at resolution time.",
  "information_needed": [
    "Approved structure for dynamic integer expressions inside GAIN_LIFE (e.g. COUNT_CARDS node)."
  ]
}
```

---

## 7. Card Name Alias & Link Attack Damage Replacement

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0006",
  "ability_reference": "10th/0006: This card is treated as \"Jackknife \"Gold Ritter\"\" / Damage dealt to you from link attacks become 2 instead.",
  "missing_capability": "REPLACEMENT_RULE",
  "what_is_known": "Card identity treats this card's name as an alias of an existing card for all game mechanics. In addition, incoming damage from link attacks is replaced with a fixed value (2).",
  "information_needed": [
    "Approved rule schema for CARD_NAME_ALIAS.",
    "Approved DAMAGE_RULE replacement syntax for link attack damage."
  ]
}
```

---

## 8. Distinct Name Drop Zone Salvage & Conditional Gauge Charge

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0007",
  "ability_reference": "10th/0007-A01: Put up to two <Dragon World> or 《Dragod》 monsters with different card names from your drop zone into your hand. If you put one or more 《Deity Dragon Tribe》 into your hand, put the top two cards of your deck into your gauge.",
  "missing_capability": "TARGET_SELECTOR",
  "what_is_known": "Drop zone salvage requires selecting up to 2 cards with different card names. Secondary effect checks the attributes of the cards successfully retrieved by the first effect.",
  "information_needed": [
    "Approved schema for distinct name constraint in target selectors (e.g. distinct_names: true).",
    "Approved condition structure for evaluating properties of cards selected during resolution."
  ]
}
```

---

## 9. Attack Rule for "Attacking Alone"

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0008",
  "ability_reference": "10th/0008-A01: if they are attacking alone, their attacks cannot be nullified",
  "missing_capability": "ATTACK_RULE",
  "what_is_known": "Attack property modifier (attack cannot be nullified) is conditioned on whether the attack is declared alone (not a link attack).",
  "information_needed": [
    "Approved condition primitive for solo attack (e.g. ATTACKING_ALONE in ATTACK_RULE condition)."
  ]
}
```

---

## 10. Variable Life Payment & Integer Division Repeat

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0009",
  "ability_reference": "10th/0009-A01: [Cost] [Pay 1 or more life], for every 3 life you paid, put the top card of your deck into your gauge, draw a card, and for this turn and the next turn, damage you take is reduced by 1.(You cannot pay equal to or more than the amount of your life!)",
  "missing_capability": "COST",
  "what_is_known": "Controller chooses any amount of life >= 1 strictly less than current life as cost. The effect repeats based on integer division (paid life / 3) and applies a 2-turn damage reduction duration.",
  "information_needed": [
    "Approved cost primitive for variable life payment with life threshold constraint (PAY_VARIABLE_LIFE).",
    "Approved REPEAT count evaluation using arithmetic division on paid cost."
  ]
}
```
