# Unsupported Mechanic Report — FD10 (001–027)

Specification reference: `Buddyfight_2D_Unity_Card_JSON_Agent_Spec.md` (Section: Unsupported Mechanic Policy).

---

## 1. Duo Keyword & Restriction Card Ignore ("Loyalty")

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/001",
  "ability_reference": "FD10/001-A01, A02: [Duo] \"Chaos Golem, Yomar\" ... you may ignore the effects of \"Loyalty\" for this ability's call",
  "missing_capability": "RULE_OVERRIDE",
  "what_is_known": "[Duo] requires checking the presence of a specific named partner card on the field. In addition, calling a monster while ignoring a specific named continuous restriction card ('Loyalty') requires ability-scoped rule overriding.",
  "information_needed": [
    "Approved engine taxonomy for [Duo] partner verification.",
    "Approved schema for ignoring named continuous restriction cards (e.g. ignore_restriction: 'Loyalty')."
  ]
}
```

---

## 2. Continuous Attack Redirection to Self

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/002",
  "ability_reference": "FD10/002-A01: when your opponent's cards would attack, change the target of the attack to this card",
  "missing_capability": "ATTACK_REDIRECT",
  "what_is_known": "Continuous passive attack replacement/redirection forcing any opponent attack declaration to change its attack target to this card while conditions are met.",
  "information_needed": [
    "Approved schema for passive attack target redirection (e.g. REDIRECT_ATTACK_TARGET)."
  ]
}
```

---

## 3. Conditional Look-and-Choose Remaining Cards Destination Replacement

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/003",
  "ability_reference": "FD10/003-A01: look at the top three cards of your deck, put one from among them into your hand, and drop the rest. If you have two or more size 3 or greater monsters on your field, or your opponent's drop zone has 6 or more cards, you may put the remaining cards into your gauge instead.",
  "missing_capability": "LOOK_AND_CHOOSE_BRANCH",
  "what_is_known": "Inspects top cards of deck and puts 1 into hand. The remaining looked cards normally go to drop, but may conditionally be redirected to gauge based on field/drop counts.",
  "information_needed": [
    "Approved schema for conditional remaining-card destination replacement in LOOK_AND_CHOOSE."
  ]
}
```

---

## 4. `[OverDrive]` Keyword Ability & `[CHAOS Territory]`

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/004",
  "ability_reference": "FD10/004: [OverDrive] [Pay 1 life during your main phase] Equip up to one 《Chaos》 item from your deck without paying its [Equip Cost], call up to two 《Chaos》 monsters from your deck without paying their [Call Cost], and shuffle your deck. This ability ignores the effects of \"Loyalty\" / [CHAOS Territory]",
  "missing_capability": "KEYWORD_OVERDRIVE",
  "what_is_known": "[OverDrive] is a special activation keyword triggered during main phase. [CHAOS Territory] allows monsters to be placed on the field without standard size limit restrictions under Chaos rules.",
  "information_needed": [
    "Approved engine specification for [OverDrive] keyword ability syntax.",
    "Approved representation for [CHAOS Territory] rules."
  ]
}
```

---

## 5. `CHAOS Drain` Field-Leave Replacement Rule

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/005",
  "ability_reference": "FD10/005: \"CHAOS Drain\" If this card would leave the field, you may destroy a size 3 or less monster on your field. If you do, this card remains on your field.",
  "missing_capability": "REPLACEMENT_RULE",
  "what_is_known": "Intercepts this card leaving the field (by destruction, bounce, drop, etc.), replacing it by destroying a friendly size 3 or less monster to remain on the field.",
  "information_needed": [
    "Approved schema for WOULD_LEAVE_FIELD replacement rule with monster destruction cost."
  ]
}
```

---

## 6. `[Overkill:REBØØT]` Keyword Ability with Turn End

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/005",
  "ability_reference": "FD10/005: [Overkill:REBØØT] [During an attack on your opponent's turn, drop a hand card] Nullify the attack. Then, if your opponent's cards attacked four times or more during this turn, end the turn!!",
  "missing_capability": "KEYWORD_OVERKILL",
  "what_is_known": "Special once-per-game Overkill variant usable during opponent's attack. Nullifies attack and conditionally forces immediate turn end if attack count >= 4.",
  "information_needed": [
    "Approved schema for [Overkill:REBØØT] and END_TURN effect node."
  ]
}
```

---

## 7. Enters Field Specifically "by Card Effects" Trigger

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/007",
  "ability_reference": "FD10/007-A01: When this card enters the field by card effects, if another 《Autodeity Army》 is on your field, for this turn, this card gets [Double Attack].",
  "missing_capability": "TRIGGER_CONDITION",
  "what_is_known": "Trigger filters ENTER_FIELD events specifically to those caused by card effects (excluding standard normal calls).",
  "information_needed": [
    "Approved trigger filter for ENTER_FIELD_BY_EFFECT."
  ]
}
```

---

## 8. Field Position Constraint Keyword `【Left/Right】`

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/009",
  "ability_reference": "FD10/009-A01: 【Left/Right】 [An/Turn] \"The Ruler's Puppet\" When this card enters the field, if you have a monster on your center, charge a gauge and draw a card.",
  "missing_capability": "POSITION_CONSTRAINT",
  "what_is_known": "Ability is only active / can only trigger if this card is currently placed in the Left or Right monster area.",
  "information_needed": [
    "Approved schema for field position constraints on triggered/activated abilities (e.g. position_constraint: [\"LEFT\", \"RIGHT\"])."
  ]
}
```

---

## 9. Partitioned Multi-Type Cost from Drop to Deck Bottom

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/010",
  "ability_reference": "FD10/010-A01: you may put two monsters and a spell from your drop zone on the bottom of your deck. If you do, charge a gauge, heal 1 life, and draw a card.",
  "missing_capability": "COST",
  "what_is_known": "Cost requires selecting exactly two monsters and one spell simultaneously from the drop zone to place on the bottom of the deck.",
  "information_needed": [
    "Approved cost schema for partitioned multi-type card movement."
  ]
}
```

---

## 10. Destroyed Specifically "by Card Effects" Trigger

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/011",
  "ability_reference": "FD10/011-A01: \"Parts Drop\" When this card is destroyed by card effects, draw two cards.",
  "missing_capability": "TRIGGER_CONDITION",
  "what_is_known": "Trigger filters destruction events specifically to those caused by card effects (excluding destruction by battle).",
  "information_needed": [
    "Approved trigger filter for DESTROYED_BY_EFFECT."
  ]
}
```

---

## 11. End-of-Battle Maintenance Cost / Self-Destruction

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/011",
  "ability_reference": "FD10/011-A02: At the end of the battle that this card attacked, you may pay 1 gauge. If you do not, destroy this card.",
  "missing_capability": "TRIGGER_CONDITION",
  "what_is_known": "Triggers at the end of a battle where this card was the attacker, giving an optional cost payment; failure to pay results in self-destruction.",
  "information_needed": [
    "Approved trigger event for BATTLE_END_ATTACKED with optional cost / self-destruction fallback."
  ]
}
```

---

## 12. Call Placement to "Another Area"

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/013",
  "ability_reference": "FD10/013-A02: call up to one 《Autodeity Army》 monster from your hand or deck to another area by paying its [Call Cost].",
  "missing_capability": "CALL_PLACEMENT",
  "what_is_known": "Monster call placement requires selecting an area on the field other than the one currently occupied by this card.",
  "information_needed": [
    "Approved CALL placement parameter for ANOTHER_AREA."
  ]
}
```

---

## 13. Active Flag Condition & Full Board Recycle (`FLAG_IS`, `SET_LIFE`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/014",
  "ability_reference": "FD10/014: You may only cast this card if your flag is \"∞ Infinity the Chaos ∞\". [1/Game] [Counter] Shuffle all cards from your hand and drop zone back into your deck, your life becomes 10, and draw five cards. Then, put this card and one hand card into your gauge, and for this turn, all cards on your field cannot leave the field by, and you cannot take damage from, your opponent's cards.",
  "missing_capability": "FLAG_CONDITION_AND_RECYCLE",
  "what_is_known": "Evaluates current active flag identity. Resolves bulk multi-zone deck recycle (hand + drop), hard-sets life total to 10, draws 5, injects into gauge, and grants universal damage and leave-field immunity.",
  "information_needed": [
    "Approved schema for SET_LIFE to fixed value.",
    "Approved primitive for bulk multi-zone shuffle to deck."
  ]
}
```

---

## 14. Full Gauge Inspection & Multi-Zone Keyword Presence Check

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/015",
  "ability_reference": "FD10/015: look at all of your gauge, reveal up to one monster and item each from among them, and put them into your hand ... if you have a card with [Duo] on your field, in your drop zone, or in the soul of cards on your field, when you would take 5 or more damage, that damage becomes 0.",
  "missing_capability": "GAUGE_INSPECTION",
  "what_is_known": "Inspects all cards in gauge with branching criteria based on initial flag. Condition checks presence of a keyword ([Duo]) across multiple disparate zones (field, drop zone, and souls of field cards) to apply threshold damage negation.",
  "information_needed": [
    "Approved syntax for LOOK_GAUGE and selective retrieval.",
    "Approved condition structure for checking keyword presence across multi-zone scopes (e.g. KEYWORD_EXISTS in [FIELD, DROP, SOUL])."
  ]
}
```

---

## 15. Flag Card Overlay / Flag Evolution

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/016",
  "ability_reference": "FD10/016: put up to one face down card from under your flag on top of your flag, put up to one card with \"Geargod\" in its card name from your deck into your hand, and shuffle your deck.",
  "missing_capability": "FLAG_OVERLAY",
  "what_is_known": "Moves a card from under the flag zone to place on top of the flag, dynamically overlaying/evolving the active flag during gameplay.",
  "information_needed": [
    "Approved engine schema for manipulating the FLAG zone card stack (e.g. MOVE_CARD from UNDER_FLAG to ON_TOP_OF_FLAG)."
  ]
}
```

---

## 16. Search Size 30 or Greater Monster

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/021",
  "ability_reference": "FD10/021: Put up to one size 30 or greater monster from your deck into your hand, and shuffle your deck.",
  "missing_capability": "TARGET_SELECTOR",
  "what_is_known": "Target selector requires filtering monsters by a high size threshold (size >= 30) specific to Chaos flag giants.",
  "information_needed": [
    "Confirmation that standard size_gte parameter supports extreme integer thresholds (>= 30)."
  ]
}
```

---

## 17. Original Size Threshold Condition (`ORIGINAL_SIZE_GTE`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/024",
  "ability_reference": "FD10/024: You may only cast this card if you have three or more originally size 3 or greater monsters on your field.",
  "missing_capability": "CONDITION",
  "what_is_known": "Condition checks the printed / original size stat of monsters on the field (>= 3) rather than their currently modified size.",
  "information_needed": [
    "Approved condition property for checking original/base stats before in-game modifications (e.g. original_size_gte: 3)."
  ]
}
```

---

## 18. Pre-Game Flag Placement Rule (`PRE_GAME_SETUP`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/026",
  "ability_reference": "FD10/026: Before the game, put one \"∞ Infinity the Chaos ∞\" face down under \"the Chaos\".",
  "missing_capability": "PRE_GAME_RULE",
  "what_is_known": "Deck building and game setup rule instructing the player to place a specific extra flag face-down under the active flag prior to the start of the match.",
  "information_needed": [
    "Approved schema for pre-game setup rules positioning cards in the FLAG stack."
  ]
}
```

---

## 19. Flag as Active Field Entity Combatant

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/026",
  "ability_reference": "FD10/026: This card is treated as a card on your field. It cannot be destroyed, leave the flag area, and its abilities cannot be nullified, and it can attack even if you have monsters on your center!",
  "missing_capability": "FLAG_COMBATANT",
  "what_is_known": "A flag card possesses battle stats (10000 Power / 3 Critical / 10000 Defense) and is treated as a permanent on-field card capable of attacking directly despite center monster occupation.",
  "information_needed": [
    "Engine support for flag entities participating in combat phases and attack declarations.",
    "Immunity flags for leaving flag area and nullification."
  ]
}
```

---

## 20. Total Size Cap Modification & Fixed Initial Parameters

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD10/026, FD10/027",
  "ability_reference": "FD10/026: put monsters up to a total size of ∞ / FD10/027: Your initial hand becomes four cards, your initial gauge becomes two cards, and your initial life becomes 10! You may put monsters of up to a total size of 99 on your field.",
  "missing_capability": "GAME_START_RULE",
  "what_is_known": "Overrides foundational game constants: field total size limit raised to 99 or infinite (∞), and starting game parameters overridden (4 hand, 2 gauge, 10 life).",
  "information_needed": [
    "Approved engine configuration properties for non-standard initial hand/gauge/life setup.",
    "Approved representation for infinite/extreme field size limits."
  ]
}
```
