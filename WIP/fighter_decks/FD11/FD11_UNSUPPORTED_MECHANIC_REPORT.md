# Unsupported Mechanic Report — FD11 (001–031, S005)

Specification reference: `Buddyfight_2D_Unity_Card_JSON_Agent_Spec.md` (Section: Unsupported Mechanic Policy).

---

## 1. `GREAT_EVIL_DEITY` (Composite Two-Card Monster)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/003, FD11/004",
  "ability_reference": "[Great Evil Deity] (This card and a different [Great Evil Deity] must be together to be put in your buddy area or called, and they are treated as one monster on your field.)",
  "missing_capability": "KEYWORD_RULING",
  "what_is_known": "Two physical cards (Sky Half FD11/003 and Earth Half FD11/004) form one composite monster identity on field or in buddy area. FD11/003 has Size 3, Crit 3, Def 6000 (no printed power). FD11/004 has Power 1,000,000, Call Cost 3 gauge (no printed size, crit, or def).",
  "information_needed": [
    "Approved engine schema for composite 2-card monster pair (whether defined in top-level rules[], composite_definition, or buddy structure).",
    "Runtime state handling for call timing, buddy zone placement, shared soul/damage, and field removal."
  ]
}
```

---

## 2. Dynamic Ability Inheritance from Zone (`REMOVE` and `SOUL`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/003, FD11/005",
  "ability_reference": "FD11/003-A01: gets the \"Thunder Mine\" of all monsters in your remove zone with different card names / FD11/005-A01: gets all \"Thunder Mine\" of cards in its soul",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Continuously copies and grants all distinct 'Thunder Mine' abilities from external zones (REMOVE zone on 003, SOUL zone on 005) to THIS_CARD while active on field.",
  "information_needed": [
    "Approved effect primitive name and syntax for copying/granting abilities across zones (e.g. GRANT_ABILITY with ability_source).",
    "Specification for deduplication filter by card name (e.g. distinct: CARD_NAME)."
  ]
}
```

---

## 3. Choice Node Inside Cost Array

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/004",
  "ability_reference": "EVIL_DEITY_OF_CATACLYSM_HYAKUGAN_YAMIGEDO_EARTH_HALF_RE_B-A01: [Cost] [Remove a monster with \"Thunder Mine\" from your drop or return it to the bottom of your deck]",
  "missing_capability": "COST",
  "what_is_known": "Cost payment requires player choice between two valid destinations (MOVE_CARD to REMOVE vs MOVE_CARD to DECK_BOTTOM) for 1 Thunder Mine monster from Drop.",
  "information_needed": [
    "Confirmation whether CHOICE control node is supported inside cost[] array.",
    "If not, approved cost branching syntax for destination choice."
  ]
}
```

---

## 4. Replacement Effect with Cost and Reaction Cast

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/004",
  "ability_reference": "EVIL_DEITY_OF_CATACLYSM_HYAKUGAN_YAMIGEDO_EARTH_HALF_RE_B-A02: \"Immortal Hyakugan\" If this card would be destroyed or leave the field by your opponent's cards, [Cost] [Mill five cards], this card remains on the field. If cards milled for this ability's cost are spells with [Set], you may cast them by paying their [Cast Cost].",
  "missing_capability": "REPLACEMENT_RULE",
  "what_is_known": "Intercepts DESTROY or LEAVE_FIELD caused by opponent cards. Pays cost of milling 5 cards from deck top. Replaces leave-field event with remain on field. Inspects cards milled specifically for this cost; if any are Set spells, opens optional cast timing paying cast cost.",
  "information_needed": [
    "Approved replacement interceptor schema (trigger event vs modifier registration).",
    "Tracking mechanism for cost-milled cards referenced in downstream conditional effects (e.g. COST_MILLED_CARDS).",
    "Execution pipeline for casting spells during/immediately after replacement resolution."
  ]
}
```

---

## 5. Multi-Attack Attack Rule Representation

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/001, FD11/004, FD11/005, FD11/007, FD11/008, FD11/030",
  "ability_reference": "[Double Attack], [Triple Attack]",
  "missing_capability": "KEYWORD_RULING",
  "what_is_known": "Spec section 226 states: 'multi-attack needs its attack count/rule object'. Section 228 lists DOUBLE_ATTACK and TRIPLE_ATTACK under registry entries needing matching implementation.",
  "information_needed": [
    "Confirmed attack rule object format: ATTACK_RULE with rules: [\"DOUBLE_ATTACK\"] vs MULTI_ATTACK with count: 2/3."
  ]
}
```

---

## 6. `SOULGUARD` Keyword / Replacement Interceptor

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/005, FD11/007, FD11/008",
  "ability_reference": "[Soulguard]",
  "missing_capability": "KEYWORD_RULING",
  "what_is_known": "Standard Buddyfight mechanic: when this card would leave the field, controller may put a card from this card's soul into the drop zone to keep it on the field.",
  "information_needed": [
    "Approved schema structure: whether a keyword tag [\"SOULGUARD\"] with effect type SOULGUARD is sufficient, or if an explicit replacement interceptor node is required."
  ]
}
```

---

## 7. Calling "On Top Of" Existing Card

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/007",
  "ability_reference": "LIGHT_SPECTER_YAMIGEDO_MIKAZUCHI-A01: call up to one monster with \"Yamigedo\" in its card name from your hand or drop zone on top of this card without paying its [Call Cost].",
  "missing_capability": "CALL_POSITION",
  "what_is_known": "Calls a monster to the same position/slot directly over THIS_CARD. Underlying card and its souls become soul of the called monster under standard Buddyfight rules.",
  "information_needed": [
    "Approved schema for specifying calling on top of a card (e.g. position: { type: \"ON_TOP_OF\", target: \"THIS_CARD\" }).",
    "Engine ruling on automatic soul transfer for on-top calls."
  ]
}
```

---

## 8. Target Selection Inside Cost Clause

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/008, FD11/013",
  "ability_reference": "INV_STERN_SPIRIT_KOKUJO_YAMIGEDO-A02, YAMIGEDO_SD-A01",
  "missing_capability": "COST_TARGETING",
  "what_is_known": "Target selection occurs within or precedes the [Cost] clause, and the selected entity is referenced both in the cost movement (e.g. put THIS_CARD into chosen card's soul) and the following effect (e.g. stand chosen card).",
  "information_needed": [
    "Standard schema pattern for capturing a target inside cost[] and passing target reference into effects[]."
  ]
}
```

---

## 9. Ability Active from Soul of Specific Attribute Host

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/010, FD11/013, FD11/028",
  "ability_reference": "FD11/010-A02: 【Soul:《Hundred Demons》/Field】 / FD11/013-A02, FD11/028-A02: 【Soul:Monster】",
  "missing_capability": "CONDITION",
  "what_is_known": "Ability is active while THIS_CARD is in the SOUL of a host matching specific criteria (attribute 《Hundred Demons》 on 010, type MONSTER on 013 and 028).",
  "information_needed": [
    "Approved condition syntax for host card filtering while in soul (e.g. host_card_type, host_attribute)."
  ]
}
```

---

## 10. Post-Call Relocation of Trigger Card into Called Monster's Soul

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/011",
  "ability_reference": "HASTED_EVOLUTION_YAMIGEDO_RE_B-A01: Then, you may remove this card or put it into the soul of the monster called by this ability.",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "After dropping THIS_CARD to pay cost and calling a monster (or two Great Evil Deity cards), effect offers a choice to remove THIS_CARD from drop or insert it into the newly called monster's soul.",
  "information_needed": [
    "Approved reference selector for targeting the entity spawned by a preceding CALL effect (e.g. CALLED_CARD / EVENT_TARGET).",
    "Handling when two monsters are called simultaneously (Great Evil Deity pair): which monster receives the soul."
  ]
}
```

---

## 11. Unavoidable / Unreducible Damage Parameterized by BuddyGift Count

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/016",
  "ability_reference": "EVIL_SORCERY_IVORY_FIEND_CURSE-A01: For this turn, the next time your opponent would take damage from your cards' \"Thunder Mine\", for each of your face up BuddyGift, that damage cannot be reduced nor avoided.",
  "missing_capability": "DAMAGE_RULE",
  "what_is_known": "Modifies the next N occurrences of Thunder Mine damage dealt to opponent so it cannot be reduced or avoided, where N equals the number of controller's face-up BuddyGift cards.",
  "information_needed": [
    "Approved schema for quantifying occurrences based on face-up BuddyGift cards (e.g. COUNT_BUDDYGIFT with state: FACE_UP).",
    "Damage interception rules for 'cannot be avoided' (preventing damage replacement/prevention shields)."
  ]
}
```

---

## 12. Combined Card Count Condition Across Multiple Zones

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/018",
  "ability_reference": "DEMONIC_WAY_OF_HUNDRED_DEMONS_AKISHOKI_RE_S-A01: if you have a total of 10 or more cards in your drop and remove zone, draw a card.",
  "missing_capability": "CONDITION",
  "what_is_known": "Evaluates the combined total number of cards across multiple distinct zones (DROP and REMOVE) belonging to controller, comparing against a threshold (>= 10).",
  "information_needed": [
    "Approved schema for multi-zone card count aggregation (e.g. COUNT_CARDS_COMPARE with zones: [\"DROP\", \"REMOVE\"])."
  ]
}
```

---

## 13. Conditional Action Based on Intermediate Search Result Count

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/019, FD11/022",
  "ability_reference": "CATACLYSMIC_INVASION_RE_S-A01, EVIL_DEITY_SORCERY_VICIOUS_CATACLYSMIC_CIRCLE-A01: Put up to two... into hand. If you put two, drop a hand card.",
  "missing_capability": "CONDITION",
  "what_is_known": "Inspects the quantity of cards actually added to hand during the immediately preceding search step; executes a required discard only if exactly 2 cards were taken.",
  "information_needed": [
    "Approved node syntax for querying previous effect result count (e.g. PREVIOUS_RESULT_COUNT_EQUALS vs inline branched outcome)."
  ]
}
```

---

## 14. Phase Termination and Turn Attack Counter

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/020",
  "ability_reference": "GEDO_SHIELD_RE_B-A01: Then, if your opponent's cards attacked three times or more during this turn, end the phase!!",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Checks the cumulative number of attack declarations by opponent cards in the current turn (>= 3). If satisfied, forcibly terminates the active attack phase (END_PHASE).",
  "information_needed": [
    "Approved condition structure for querying turn attack history (e.g. ATTACK_COUNT_THIS_TURN).",
    "Approved effect primitive to terminate phase (e.g. END_PHASE) and cleanup of active battle/attack sequence."
  ]
}
```

---

## 15. Dynamic Heal Based on Target Card Stat and Destruction Shield

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/023",
  "ability_reference": "HUNDRED_DEMONS_SORCERY_THUNDERBOLT_EXPLODING_CIRCLE-A01: Choose a monster on your field. You gain life equal to the chosen monster's size, and for this turn, the next time that card would be destroyed, nullify its destruction.",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Heals player by a variable amount derived from an active field card's size (stat: SIZE). Registers a 1-occurrence destruction prevention shield on that chosen card for the duration of the turn.",
  "information_needed": [
    "Syntax for dynamic heal scaling from a target card's stat (CARD_STAT selector).",
    "Explicit occurrence tracking on PROTECTION nodes (e.g. occurrences: 1)."
  ]
}
```

---

## 16. Damage Target Choice Between Self and Opponent

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/028",
  "ability_reference": "EVOLUTION_FUTURE-A02: nullify the attack, and deal 1 damage to you or your opponent.",
  "missing_capability": "TARGET_SELECTOR",
  "what_is_known": "Damage effect allows the controller to choose whether to deal 1 damage to SELF or OPPONENT.",
  "information_needed": [
    "Standard syntax for player-target branching on DAMAGE effect (e.g. CHOICE with DAMAGE to SELF vs OPPONENT)."
  ]
}
```

---

## 17. Multi-Zone Mass Return and Absolute Life Setting

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/029",
  "ability_reference": "THE_CONVULSION-A01: Return all cards from your hand, gauge and drop zone to your deck, and shuffle it. Then, draw six cards, put the top two cards of your deck into your gauge, and your life becomes 10!!",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Mass-moves all cards across HAND, GAUGE, and DROP back to DECK. Sets player's life to fixed absolute value 10 (not delta heal/damage).",
  "information_needed": [
    "Approved primitive for setting life to an absolute number (e.g. SET_LIFE value: 10).",
    "Mass-move primitive for clearing entire zones to deck."
  ]
}
```

---

## 18. Item Attack with Monster in Center

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/030",
  "ability_reference": "GIANT_CLAW_OF_EVIL_DEITY_GOKURAI-A02: This card can attack even if there is a monster on your center.",
  "missing_capability": "ATTACK_RULE",
  "what_is_known": "Continuous weapon rule enabling weapon card to declare attacks even when the center field slot is occupied by an allied monster.",
  "information_needed": [
    "Approved attack rule enum string (e.g. CAN_ATTACK_WITH_MONSTER_IN_CENTER vs ATTACK_RULE property)."
  ]
}
```

---

## 19. Position-Specific Absolute Damage Immunity

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/030",
  "ability_reference": "GIANT_CLAW_OF_EVIL_DEITY_GOKURAI-A03: You cannot take damage if a size 3 monster with \"Hyakugan\" in its card name is on your center.",
  "missing_capability": "DAMAGE_PROTECTION",
  "what_is_known": "Continuous effect: while controller has an active size 3 monster with 'Hyakugan' in center position, controller takes 0 damage from all sources.",
  "information_needed": [
    "Field position filter syntax for damage protection triggers (position: CENTER).",
    "Immunity scope for absolute damage nullification (source: ALL vs separate battle and effect branches)."
  ]
}
```

---

## 20. Non-Nullifiable Spell Casting Property

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD11/S005",
  "ability_reference": "This card cannot be nullified.",
  "missing_capability": "PROTECTION",
  "what_is_known": "Static card rule preventing the spell's cast from being negated/nullified by opponent counter cards during resolution timing.",
  "information_needed": [
    "Approved representation: top-level rules[] with type CANNOT_BE_NULLIFIED vs PROTECTION on THIS_CARD."
  ]
}
```
