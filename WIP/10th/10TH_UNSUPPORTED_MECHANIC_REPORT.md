# Unsupported Mechanic Report — 10th (0001–0041)

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

---

## 11. Multi-Type Bounded Retrieval from Looked Cards

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0012",
  "ability_reference": "10th/0012-A01: Look at the top five cards of your deck, put up to two monsters, up to one spell and up to one item from among them into your hand, and shuffle your deck.",
  "missing_capability": "TARGET_SELECTOR",
  "what_is_known": "A single retrieval action from looked cards applies simultaneous upper bounds partitioned by card type (up to 2 monsters, up to 1 spell, up to 1 item).",
  "information_needed": [
    "Approved schema for partitioned multi-type bounded selection from LOOKED_CARDS.",
    "Order of resolution for placing remaining looked cards into bottom of deck vs shuffle."
  ]
}
```

---

## 12. Soul Return to Opponent's Deck with Shuffle

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0013",
  "ability_reference": "10th/0013-A01: Return up to 3 souls from a card on your opponent's field to your opponent's deck, and shuffle your opponent's deck.",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Target souls are removed directly from an opponent's card and returned to the opponent's deck followed by deck shuffle.",
  "information_needed": [
    "Approved syntax for MOVE_CARD from SOUL directly to DECK with target of_target specification."
  ]
}
```

---

## 13. Multi-Zone Face-Down Soul Injection & Cast from Soul

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0015",
  "ability_reference": "10th/0015-A02, A03: choose up to one card from your hand, deck or drop zone, and put it face down in this card's soul ... cast a <Katana World> spell or 《Secret Sword》 from the soul without paying its [Cast Cost]",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Cards can be searched/selected across multiple zones (HAND, DECK, DROP) and inserted face-down into soul. Later, eligible spells/Secret Swords can be cast directly out of the soul without paying cast cost.",
  "information_needed": [
    "Approved CAST effect node referencing SOUL as origin zone.",
    "Engine handling for face-down cards in soul retaining identity for controller inspection and cast eligibility."
  ]
}
```

---

## 14. "Possession" Placement & End-of-Turn De-possession

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0016",
  "ability_reference": "10th/0016-A01, A02: \"Possession\" You may put a size 3《Electrodeity》from your hand on top of this card. The card put on top is treated as an item until it leaves the field ... At the end of each player's turn, equip this card from an item's soul, and return the previously equipped card to hand.",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "A monster is placed on top of an equipped item, temporarily converting the monster into an item. At turn end, the host item re-equips from soul and returns the top card to hand.",
  "information_needed": [
    "Approved schema for card type mutation (monster treated as item while placed on item).",
    "Engine mechanics for re-equipping from soul and returning prior equipped card to hand."
  ]
}
```

---

## 15. Previous Turn Cast Tracking Condition

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0018",
  "ability_reference": "10th/0018-A01: if you cast \"Divine Dragon Creation\" this turn, draw a card",
  "missing_capability": "CONDITION",
  "what_is_known": "Evaluates whether the player has already successfully cast a card with specific name (\"Divine Dragon Creation\") earlier in the current turn.",
  "information_needed": [
    "Approved condition primitive for turn cast history inspection (e.g. PLAYER_CAST_CARD_THIS_TURN)."
  ]
}
```

---

## 16. Final Phase Attack Permission Rule

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0019",
  "ability_reference": "10th/0019-A01: all cards on your field can attack during the final phase",
  "missing_capability": "ATTACK_RULE",
  "what_is_known": "Overrides game rule preventing non-Impact attacks during the Final Phase, granting all friendly cards the ability to declare attacks during that phase.",
  "information_needed": [
    "Approved ATTACK_RULE flag for phase attack permission (e.g. CAN_ATTACK_DURING_FINAL_PHASE)."
  ]
}
```

---

## 17. Cost-Card Stat Evaluation

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0021",
  "ability_reference": "10th/0021-A01: if the card you dropped for this card's [Cast Cost] is size 2 or greater ... if the card you dropped for this card's [Cast Cost] is size 1 or lower ...",
  "missing_capability": "CONDITION",
  "what_is_known": "Branching resolution inspects stats (Size) of the specific card instance consumed during cost payment for this ability.",
  "information_needed": [
    "Approved condition schema for referencing properties of cards consumed during cost payment (e.g. DROPPED_COST_CARD_COMPARE)."
  ]
}
```

---

## 18. Destruction Intercept & Replacement to Soul

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0022",
  "ability_reference": "10th/0022-A01: If a《Folktale》monster on your field would be destroyed, you may pay 1 life. If you do, put it into this card's soul.",
  "missing_capability": "REPLACEMENT_RULE",
  "what_is_known": "Interrupts destruction of another friendly monster; paying 1 life replaces destruction with moving the card into this item's soul.",
  "information_needed": [
    "Approved trigger/replacement structure for WOULD_BE_DESTROYED redirecting destruction destination to SOUL."
  ]
}
```

---

## 19. Multi-Call from Soul to Separate Areas

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0022",
  "ability_reference": "10th/0022-A03: \"Marchen Panic\" Call up to three monsters from this card's soul on separate areas by paying their [Call Cost].",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Calls up to 3 monsters simultaneously from soul, requiring placement onto distinct field areas (LEFT, CENTER, RIGHT).",
  "information_needed": [
    "Approved placement constraint syntax in CALL effect node (e.g. placement: SEPARATE_AREAS)."
  ]
}
```

---

## 20. Initial Flag Condition (`INITIAL_FLAG_IS`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0027",
  "ability_reference": "10th/0027-A01: You may only cast this card if your initial flag is \"Legend World\".",
  "missing_capability": "CONDITION",
  "what_is_known": "Cast condition checks the flag chosen at the start of the game (initial flag) rather than current active flags or card attributes.",
  "information_needed": [
    "Approved condition primitive for checking initial flag (e.g. INITIAL_FLAG_IS)."
  ]
}
```

---

## 21. Center Attack Bypass Rule (`ATTACK_OVER_CENTER`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0027",
  "ability_reference": "10th/0027-A01: During this turn, even if your opponent has a monster on the center, your 《Star》 can attack your opponent.",
  "missing_capability": "ATTACK_RULE",
  "what_is_known": "Grants attack permission directly to opponent player even while opponent has a monster in the center area, for cards with the 《Star》 attribute.",
  "information_needed": [
    "Approved ATTACK_RULE property for ignoring center monster when declaring attacks against opponent (e.g. CAN_ATTACK_PLAYER_DESPITE_CENTER)."
  ]
}
```

---

## 22. Destruction Trigger Burn Modifier (`REGISTER_TRIGGER_MODIFIER`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0027",
  "ability_reference": "10th/0027-A02: When an opponent's card is destroyed by your 《Star》 card effects, deal 2 damage to your opponent! This ability only activates once per turn.",
  "missing_capability": "TRIGGER_RULE",
  "what_is_known": "A delayed or turn-long trigger registered by a spell that triggers whenever an opponent's card is destroyed specifically by a friendly 《Star》 card effect.",
  "information_needed": [
    "Approved schema for spell-granted or delayed turn trigger effects monitoring opponent card destruction by specific source attributes."
  ]
}
```

---

## 23. Distinct Sizes Selection Constraint

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0028",
  "ability_reference": "10th/0028-A01: Put up to two 《Curse Dragon》 monsters of different sizes from your drop zone into your hand or call them by paying their [Call Cost].",
  "missing_capability": "TARGET_SELECTOR",
  "what_is_known": "Selection from drop zone requires chosen cards to have mutually distinct Size values (different sizes). Also offers player choice during resolution to either put into hand or call.",
  "information_needed": [
    "Approved schema for distinct property constraints in target selectors (e.g. distinct_sizes: true).",
    "Resolution branch syntax for choosing between ADD_TO_HAND and CALL for selected cards."
  ]
}
```

---

## 24. Player Transformation Status Condition (`IS_TRANSFORMED_INTO`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0030, 10th/0031",
  "ability_reference": "10th/0030-A01: if you are [Transform] into a card with \"Zetta\" in its card name / 10th/0031-A01: if you are [Transform] into a 《Battleship》",
  "missing_capability": "CONDITION",
  "what_is_known": "Evaluates whether the player is currently under the [Transform] state with an equipped card matching specific card name or attribute criteria.",
  "information_needed": [
    "Approved condition primitive for checking player transformation state and target card properties (e.g. IS_TRANSFORMED_INTO)."
  ]
}
```

---

## 25. Item Soul Extraction & Multi-Zone Soul Injection

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0030, 10th/0031",
  "ability_reference": "10th/0030-A01: put up to one 《Crew Trooper》 monster from your item's soul into your hand, or call it to an open area without paying its [Call Cost] / 10th/0031-A01: put up to one card from your deck or drop zone into that item's soul",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Interactions directly targeting the soul of an equipped item: extracting/calling cards from item soul, or searching across DECK and DROP to inject cards into item soul.",
  "information_needed": [
    "Approved selector/origin syntax for item soul (ITEM_SOUL).",
    "Approved CALL placement parameter for OPEN_AREA."
  ]
}
```

---

## 26. Soul Master's Soul Protection (`PROTECTION_RULE`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0032",
  "ability_reference": "10th/0032: The soul master's souls cannot be dropped or returned to deck by your opponent's card effects.",
  "missing_capability": "PROTECTION_RULE",
  "what_is_known": "While this card is located in a host card's soul, that host card's entire soul stack is continuously protected from being dropped or returned to deck by opponent card effects.",
  "information_needed": [
    "Approved continuous soul protection rule syntax targeting the soul master's soul stack (e.g. SOUL_MASTER_SOULS protection)."
  ]
}
```

---

## 27. Dynamic Target Count Condition (`TARGET_COUNT_GTE`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0034",
  "ability_reference": "10th/0034-A01: If you chose three or more cards, draw a card.",
  "missing_capability": "CONDITION",
  "what_is_known": "A branching effect evaluation inside a single effect block conditioned on whether the player selected at least 3 cards during the immediately preceding target selection step.",
  "information_needed": [
    "Approved condition primitive for checking chosen target count (e.g. TARGET_COUNT_GTE)."
  ]
}
```

---

## 28. Dynamically Bound Effect Scaling from Returned Cards

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0035",
  "ability_reference": "10th/0035-A01: return up to three cards from your hand to your deck, and shuffle it. Then, you gain life and draw cards equal to the number of cards returned.",
  "missing_capability": "EFFECT_TYPE",
  "what_is_known": "Life gain and draw amounts are dynamically bound to the count of cards successfully moved from hand back into the deck.",
  "information_needed": [
    "Approved syntax for dynamically passing returned card count into GAIN_LIFE and DRAW nodes."
  ]
}
```

---

## 29. Active Buddy Attribute Matching Selector

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0035",
  "ability_reference": "10th/0035-A02: choose up to three cards with the same attribute as your buddy",
  "missing_capability": "TARGET_SELECTOR",
  "what_is_known": "Target selector requires dynamically reading the attributes of the player's active buddy monster and filtering targets on field matching any of those attributes.",
  "information_needed": [
    "Approved selector predicate for matching active buddy attributes (e.g. MATCH_BUDDY_ATTRIBUTES)."
  ]
}
```

---

## 30. Movement to Buddy Zone & Trigger from Buddy Zone

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0036",
  "ability_reference": "10th/0036-A01, A02: put this card in your buddy zone ... You may only cast \"Future Card Buddyfight\" once per fight ... At the start of your attack phase, if this card is in your buddy zone, for this turn, a buddy on your field gets critical+2!",
  "missing_capability": "ZONE_AND_TRIGGER",
  "what_is_known": "A spell moves into the BUDDY_ZONE during resolution. Once placed there, it continuously resides in the BUDDY_ZONE and triggers an ability at the start of attack phase. Also introduces a once-per-fight restriction.",
  "information_needed": [
    "Approved schema for moving non-monster cards into BUDDY_ZONE.",
    "Engine handling for triggered abilities activating from the BUDDY_ZONE.",
    "Approved condition schema for COUNT_PER_FIGHT."
  ]
}
```

---

## 31. Deck Search Scope Replacement

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0037",
  "ability_reference": "10th/0037-A01: for this turn, the next time your opponent would look at the entire deck, your opponent looks at the top four cards of the deck instead.",
  "missing_capability": "REPLACEMENT_RULE",
  "what_is_known": "Replacement effect modifying opponent's next deck search action during the turn, constraining the search scope from the entire deck down to the top 4 cards.",
  "information_needed": [
    "Approved schema for deck search replacement rules (e.g. REPLACE_SEARCH_SCOPE with LOOK_TOP_N)."
  ]
}
```

---

## 32. Phase & Damage Threshold Negation

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0038",
  "ability_reference": "10th/0038-A02: During the attack phase of this turn, if you would be dealt 5 or greater damage, that damage is reduced to 0.",
  "missing_capability": "REPLACEMENT_RULE",
  "what_is_known": "Phase-constrained continuous damage replacement rule intercepting damage events during attack phase if incoming damage is >= 5, reducing damage to 0.",
  "information_needed": [
    "Approved DAMAGE_RULE structure for threshold-based damage reduction / negation."
  ]
}
```

---

## 33. Field Stat Reduction Protection

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "10th/0038",
  "ability_reference": "10th/0038-A03: During this turn, the attack, defense and critical of all cards on your field cannot be reduced by your opponent's card effects.",
  "missing_capability": "PROTECTION_RULE",
  "what_is_known": "Turn-long continuous protection preventing opponent card effects from lowering power, defense, or critical of friendly field cards.",
  "information_needed": [
    "Approved STAT_PROTECTION rule preventing stat reduction from opponent effects."
  ]
}
```
