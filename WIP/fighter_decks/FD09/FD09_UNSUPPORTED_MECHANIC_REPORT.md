# Unsupported Mechanic Report — FD09 (001–028)

Specification reference: `Buddyfight_2D_Unity_Card_JSON_Agent_Spec.md` (Section: Unsupported Mechanic Policy).

---

## 1. Area Stacking (`AREA_STACKING`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/001",
  "ability_reference": "FD09/001: 【Left/Right】 [Duo] \"Thunder Flares Elf Knight, Eden\" ... You may have one more of this card's [Duo] on this card's area, and this card and its [Duo] cannot be [Rest] by your opponent's card effects.",
  "missing_capability": "AREA_STACKING",
  "what_is_known": "Permits placing a second monster (the Duo partner) onto the same field area (Left or Right), sharing area occupancy, and grants Rest immunity to both.",
  "information_needed": [
    "Approved schema for multi-card area stacking rules."
  ]
}
```

---

## 2. Dynamic World Mutation (`WORLD_MUTATION`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/001",
  "ability_reference": "FD09/001: search your deck for up to one card, put it into your drop or soul of your item, shuffle your deck, and for this turn, the world name of this card on the field is regarded as the same as that card's, and you draw up to two cards.",
  "missing_capability": "WORLD_MUTATION",
  "what_is_known": "Searches deck for any card, puts it into drop or item soul, dynamically copies the world identity of that card onto this monster, and draws up to 2.",
  "information_needed": [
    "Approved schema for temporary world attribute mutation (e.g. COPY_WORLD_FROM_SEARCHED_CARD)."
  ]
}
```

---

## 3. Solo Attack Opposing Monster Ability Nullification & Counter Lock (`ATTACK_RESTRICTION_AND_NEGATION`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/002",
  "ability_reference": "FD09/002: When this card attacks your opponent's monster alone, nullify the abilities of the monster in battle with this card, and your opponent cannot use [Counter].",
  "missing_capability": "BATTLE_PHASE_RESTRICTION_AND_NEGATION",
  "what_is_known": "Attacking an opponent's monster alone triggers an ability nullification on opposing cards in the battle, while simultaneously placing a restriction forbidding the opponent from using Counter abilities.",
  "information_needed": [
    "Approved schema for in-battle defender ability nullification and opponent counter-action lockout."
  ]
}
```

---

## 4. Distinct Worlds Count in Drop Zone Condition (`DISTINCT_WORLDS_IN_DROP_COUNT`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/002",
  "ability_reference": "FD09/002: \"Crimson Thunder Howling\" When this card's attack destroys your opponent's monster, if your drop zone has 3 or more different world names, you heal 2 life, and if six or more, deal 2 damage to your opponent!!",
  "missing_capability": "DISTINCT_WORLDS_IN_DROP_COUNT",
  "what_is_known": "Evaluates the count of unique world attributes among all cards present in the drop zone (e.g., >= 3 and >= 6 distinct worlds).",
  "information_needed": [
    "Approved schema for DISTINCT_WORLDS condition check in game state queries."
  ]
}
```

---

## 5. `[Station]` Keyword Ability & Soul Mass-Loading (`STATION_MECHANIC`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/003",
  "ability_reference": "FD09/003: [Station] [Pay 3 gauge] / When you [Station], put up to two monsters from your drop zone into this card's soul. / At the end of turn, put up to three 《Crew Trooper》 or 《Thunder Empire》 monsters from your field into this card's soul. / [1/Turn] [Counter] 【Act】 During each player's attack phase, you may call up to one monster from this card's soul by paying its [Call Cost].",
  "missing_capability": "STATION_AND_SOUL_CALL",
  "what_is_known": "[Station] is a specialized item/ride mechanic with custom soul placement triggers from drop/field, providing special attack phase soul calling.",
  "information_needed": [
    "Approved schema and keyword specification for [Station].",
    "Approved action for calling monsters directly from an item's soul during attack phase."
  ]
}
```

---

## 6. Continuous Area Effect from Remove Zone & Lingering Fight Buff (`REMOVE_ZONE_CONTINUOUS_AND_FIGHT_BUFF`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/004",
  "ability_reference": "FD09/004: 【Field/Remove Zone】 The size of all originally size 1 《Thunder Empire》 on your field are reduced by 1. / 【Field/Hand】 [OverDrive] [During your attack phase, remove this card & Drop a hand card] Call up to one 《Thunder Empire》 from your deck by paying its [Call Cost], and shuffle your deck. Then, during this fight, all cards on your field get power+10000 and critical+1.",
  "missing_capability": "REMOVE_ZONE_PASSIVE_AND_FIGHT_DURATION_BUFF",
  "what_is_known": "Applies a continuous size-reduction effect across the field while residing in the remove zone. Also grants a fight-long stat boost ('during this fight') triggered by [OverDrive].",
  "information_needed": [
    "Approved schema for continuous static abilities originating from the remove zone.",
    "Approved duration taxonomy for FIGHT_DURATION / THIS_FIGHT."
  ]
}
```

---

## 7. `[Overturn]` Total Board/Zone Reset and Redraw (`OVERTURN_BOARD_RESET`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/005",
  "ability_reference": "FD09/005: [Overturn] [Pay 2 gauge during your main phase] Nullify all abilities of cards on the field, and return all other cards from each player's hand, gauge, drop zone, and field to their owner's decks, and shuffle the decks! Then, each player draws six cards, and put the top two cards of their deck into their gauge!!",
  "missing_capability": "OVERTURN_TOTAL_RESET",
  "what_is_known": "Mass game-state reset affecting all zones (field, hand, drop, gauge) of both players, followed by standardized redraw and regauge.",
  "information_needed": [
    "Approved schema for [Overturn] keyword ability.",
    "Approved schema for multi-zone board reset and ability nullification on entire field."
  ]
}
```

---

## 8. Field-Leave Replacement Self Drop (`FIELD_LEAVE_REPLACEMENT`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/006",
  "ability_reference": "FD09/006: 【Field】 If another 《Thunder Empire》 would leave your field, you may drop this card. If you do, that card remains on the field.",
  "missing_capability": "FIELD_LEAVE_REPLACEMENT",
  "what_is_known": "Intercepts another friendly Thunder Empire card leaving the field (by destruction, return to hand, etc.), substituting the leave effect by sending this card to the drop zone instead.",
  "information_needed": [
    "Approved schema for WOULD_LEAVE_FIELD replacement rule sacrificing another designated card."
  ]
}
```

---

## 9. Specific Named Loss Condition Immunity & Mass Zone Deck Shuffle (`SPECIFIC_LOSS_CONDITION_IMMUNITY`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/014",
  "ability_reference": "FD09/014: [1/Game] [Counter] Shuffle all cards from your hand and drop zone into your deck. Then, draw 4 cards and charge 2 gauge. Then, you do not take damage until the end of this turn, and you do not lose the game from the effects of \"World Linking Key the First, Drago-Uno\" for the rest of this fight. Remove this card.",
  "missing_capability": "SPECIFIC_LOSS_CONDITION_IMMUNITY",
  "what_is_known": "Mass zone return to deck, turn-long damage prevention, fight-long immunity against losing the game to a specific named card effect, and removing self.",
  "information_needed": [
    "Approved schema for immunity against specific named game loss effects.",
    "Approved schema for mass simultaneous hand + drop shuffle into deck."
  ]
}
```

---

## 10. Full Gauge Inspection & Ignore Named Restriction Card on Call (`INSPECT_ALL_GAUGE_AND_IGNORE_RESTRICTION`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/015",
  "ability_reference": "FD09/015: look at all of your gauge, reveal up to one monster and item each from among them, and put them into your hand / If you would call a monster with [Duo], you may call it while ignoring the effects of \"Loyalty\".",
  "missing_capability": "INSPECT_ALL_GAUGE_AND_IGNORE_RESTRICTION",
  "what_is_known": "Inspects all cards in gauge to retrieve cards to hand, and provides permission to ignore named continuous restriction cards ('Loyalty') during call.",
  "information_needed": [
    "Approved schema for INSPECT_ALL_GAUGE search/salvage actions.",
    "Approved schema for ability-scoped ignore named continuous restriction cards."
  ]
}
```

---

## 11. Special Keyword History Check & Final Phase Attack Permission (`SPECIAL_KEYWORD_HISTORY_AND_FINAL_PHASE_ATTACK`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/018",
  "ability_reference": "FD09/018: [Cn/Turn] [Counter] [Stand] all 《Thunder Empire》 on your field, and if you have used [Overturn], [Overthrow], or [OverDrive] this game, draw a card, and for this turn, all monsters that were affected by this card's ability can also attack during your final phase.",
  "missing_capability": "SPECIAL_KEYWORD_HISTORY_AND_FINAL_PHASE_ATTACK",
  "what_is_known": "Queries match history for activation of special keyword mechanics ([Overturn], [Overthrow], [OverDrive]), and grants attack permission to affected monsters during final phase.",
  "information_needed": [
    "Approved schema for match history keyword usage queries.",
    "Approved schema for granting final phase attack permissions."
  ]
}
```

---

## 12. Paid Cost Scaled Variable Mass Debuff (`STAT_DEBUFF_SCALED_BY_PAID_COST`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/024",
  "ability_reference": "FD09/024: [Counter] For this turn, all cards on your opponent's field get power-3000, defense-3000, and critical-1 for each card dropped by this card's [Cast Cost]!",
  "missing_capability": "STAT_DEBUFF_SCALED_BY_PAID_COST",
  "what_is_known": "Variable cost payment dynamically scales the magnitude of power, defense, and critical debuffs applied to all cards on the opponent's field.",
  "information_needed": [
    "Approved schema for variable cost multipliers affecting mass stat reduction effects."
  ]
}
```

---

## 13. One-Time Next Damage Reduction Interception Shield (`NEXT_DAMAGE_REDUCTION_SHIELD`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/025",
  "ability_reference": "FD09/025: [Counter] 【Act】 During your opponent's turn, if you have two or more different world names of cards on your field, you may put this card from the field into the drop zone. If you do, for this turn, the next time damage would be dealt to you, it is reduced by 3.",
  "missing_capability": "NEXT_DAMAGE_REDUCTION_SHIELD",
  "what_is_known": "One-time replacement/interception shield that reduces the next instance of incoming player damage by 3 during the turn.",
  "information_needed": [
    "Approved schema for NEXT_TIME_DAMAGE_DEALT interception and reduction shield."
  ]
}
```

---

## 14. Dynamic Cost Reduction Scaled by Attack Counter & Unreducible Damage (`COST_REDUCTION_SCALED_BY_ATTACK_COUNT_AND_UNREDUCIBLE_DAMAGE`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "FD09/027",
  "ability_reference": "FD09/027: [Cast Cost] [Pay 12 gauge. The gauge cost is reduced by the number of times your cards attacked during this turn] / Deal 20 damage to your opponent!! This damage cannot be reduced.",
  "missing_capability": "COST_REDUCTION_SCALED_BY_ATTACK_COUNT_AND_UNREDUCIBLE_DAMAGE",
  "what_is_known": "Reduces gauge cast cost dynamically based on attack counter during turn, and deals direct damage that cannot be reduced.",
  "information_needed": [
    "Approved schema for dynamic cast cost reduction scaled by attack counter.",
    "Approved schema for unreducible damage specification."
  ]
}
```
