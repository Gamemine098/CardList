# Unsupported Mechanic Report — Re:TH (001–039)

Specification reference: `Buddyfight_2D_Unity_Card_JSON_Agent_Spec.md` (Section: Unsupported Mechanic Policy).

---

## 1. Stacking Monster Over Item as Equipped Item & Auto Re-Equip from Soul (`STACK_MONSTER_AS_ITEM_OVER_ITEM`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/001TH",
  "ability_reference": "Re:TH/001TH: At the end of each player's turn, equip this card from an item's soul, and return the previously equipped card to hand. / [Counter] 【Act】 [An/Turn] \"Kagura-bell of Worship\" If this card is equipped as an item, put a size 3 《Electrodeity》 from your hand on top of this card. The card put on top is treated as an item until it leaves the field.",
  "missing_capability": "STACK_MONSTER_AS_ITEM_OVER_ITEM",
  "what_is_known": "Places a size 3 monster card from hand over this equipped item, converting its card type to ITEM until it leaves the field. At turn end, auto-equips this card from soul and returns the top equipped card to hand.",
  "information_needed": [
    "Approved schema for stacking cards over items with temporary card type mutation to ITEM.",
    "Approved schema for automatic soul-to-equipped transition with previous host return."
  ]
}
```

---

## 2. Multi-World Attribute Presence in Drop Zone & Continuous Attack Redirection (`MULTI_WORLD_TREATMENT_IN_DROP_ZONE`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/002TH",
  "ability_reference": "Re:TH/002TH: If your flag is \"Thunder Emperor's Fangs\", this card is also regarded as <Magic World>, <Dungeon World> and <Hero World> in the drop zone. / When your opponent's cards attack, change the target of the attack to this card.",
  "missing_capability": "MULTI_WORLD_TREATMENT_IN_DROP_ZONE",
  "what_is_known": "Continuously confers multiple additional world attributes to this card while residing in the drop zone under specific flag conditions. Also redirects any opponent attack declaration to this card.",
  "information_needed": [
    "Approved schema for continuous multi-world attribute identity in DROP zone.",
    "Approved schema for passive attack target redirection."
  ]
}
```

---

## 3. Replacement Rule: Intercept Leave-Field to Item Soul (`REPLACEMENT_LEAVE_FIELD_TO_ITEM_SOUL`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/003TH",
  "ability_reference": "Re:TH/003TH: If a 《Folktale》 monster on your field would be destroyed or returned to hand, you may pay 1 life. If you do, put it into this card's soul.",
  "missing_capability": "REPLACEMENT_LEAVE_FIELD_TO_ITEM_SOUL",
  "what_is_known": "Intercepts destruction or hand-bounce of a friendly Folktale monster, paying 1 life to redirect it into this item's soul instead.",
  "information_needed": [
    "Approved schema for WOULD_LEAVE_FIELD redirection to host item soul."
  ]
}
```

---

## 4. Continuous Total Field Size Cap Override to 4 (`TOTAL_SIZE_CAP_EXPANSION_TO_4`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/005TH",
  "ability_reference": "Re:TH/005TH: You may put monsters of up to a total size of 4 on your field. / Items on your field cannot be destroyed, be returned to hand, or leave the field, by card effects.",
  "missing_capability": "TOTAL_SIZE_CAP_EXPANSION_TO_4",
  "what_is_known": "Expands continuous total field monster size capacity to 4 and grants total leave-field immunity to all friendly items.",
  "information_needed": [
    "Approved schema for continuous total field size cap override to 4."
  ]
}
```

---

## 5. Continuous Total Field Size Cap Override to 6 (`TOTAL_SIZE_CAP_EXPANSION_TO_6`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/007TH",
  "ability_reference": "Re:TH/007TH: If you have a 《MAX Dragon》 monster on your field, this card cannot leave the field by your opponent's card effects, and you may put monsters up to a total size of 6 on your field.",
  "missing_capability": "TOTAL_SIZE_CAP_EXPANSION_TO_6",
  "what_is_known": "Expands continuous total field monster size capacity to 6 while controlling a MAX Dragon monster.",
  "information_needed": [
    "Approved schema for conditional continuous total field size cap override to 6."
  ]
}
```

---

## 6. Continuous Mass Nullification of Opponent Field Cards and Souls (`MASS_NULLIFY_OPPONENT_CARDS_AND_SOULS`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/009TH",
  "ability_reference": "Re:TH/009TH: If there are 《Star》 on your left and right, nullify all abilities of cards on your opponent's field and in the soul of your opponent's cards.",
  "missing_capability": "MASS_NULLIFY_OPPONENT_CARDS_AND_SOULS",
  "what_is_known": "Continuously nullifies all abilities of all opponent cards on field and all cards contained inside their souls while Star cards occupy Left and Right.",
  "information_needed": [
    "Approved schema for continuous soul and field ability nullification across opponent zone."
  ]
}
```

---

## 7. Counter-Act Call From Hand & Attack Redirection (`COUNTER_CALL_FROM_HAND_AND_REDIRECT_ATTACK`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/011TH",
  "ability_reference": "Re:TH/011TH: [Counter] 【Act】 During an attack on your opponent's turn, if you have a 《Darkhero》 on your field, call this card from your hand, and change the target of the attack to this card.",
  "missing_capability": "COUNTER_CALL_FROM_HAND_AND_REDIRECT_ATTACK",
  "what_is_known": "Calls self from hand during opponent attack as Counter timing and redirects attack target to self.",
  "information_needed": [
    "Approved schema for in-attack Counter call and redirection from hand."
  ]
}
```

---

## 8. Hand-Reveal Replacement Protection from Discard/Bounce (`HAND_REVEAL_REPLACEMENT_PROTECTION`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/014TH",
  "ability_reference": "Re:TH/014TH: If your hand cards would be dropped or returned to your deck by your opponent's card effects, you may reveal this hand card and pay 1 life. If you do, your hand cards cannot be dropped by that effect.",
  "missing_capability": "HAND_REVEAL_REPLACEMENT_PROTECTION",
  "what_is_known": "Replaces hand discard or deck-bounce by revealing this card from hand and paying 1 life.",
  "information_needed": [
    "Approved schema for hand-reveal replacement abilities protecting the hand zone."
  ]
}
```

---

## 9. Inspect Face-Down Souls and Cast Secret Sword from Soul with Alternate Cost (`CAST_FROM_FACE_DOWN_SOUL`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/019TH",
  "ability_reference": "Re:TH/019TH: [Counter] 【Act】 [1/Turn] Put a 《Secret Sword》 card from your hand, deck or drop zone, face down into this card's soul. If you searched your deck, shuffle it. If you put from your hand, draw a card. / You may look at this card's soul and cast 《Secret Sword》 cards from its soul by paying 1 gauge instead of its [Cast Cost].",
  "missing_capability": "CAST_SECRET_SWORD_FROM_SET_SOUL",
  "what_is_known": "Loads Secret Sword into face-down soul from hand/deck/drop, and allows looking at face-down souls to cast them directly for 1 gauge.",
  "information_needed": [
    "Approved schema for inspecting and casting face-down soul cards with substitute gauge costs."
  ]
}
```

---

## 10. Dynamic Size Alteration on Called Monster (`DYNAMIC_SIZE_MUTATION_ON_CALL`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/020TH",
  "ability_reference": "Re:TH/020TH: [Counter] 【Act】 [1/Turn] If this card is on your center, you may drop a hand card. If you do, call up to one size 3 《Demon Lord》 monster from your deck to an open area on your field by paying its [Call Cost], and shuffle your deck. That card becomes a size 0 until it leaves the field.",
  "missing_capability": "DYNAMIC_SIZE_MUTATION_ON_CALL",
  "what_is_known": "Calls a size 3 Demon Lord from deck and modifies its size attribute to 0 until it leaves the field.",
  "information_needed": [
    "Approved schema for dynamic size alteration on called monsters lasting until leave-field."
  ]
}
```

---

## 11. Counter-Call from Hand with Attack Redirection & On-Destruction Soul Jump (`COUNTER_CALL_FROM_HAND_AND_REDIRECT_ATTACK`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/030TH",
  "ability_reference": "Re:TH/030TH: [Counter] 【Act】 During the attack on your opponent's turn, you may pay 1 gauge. If you do, call this card from your hand, and change the attack target to this card. / When this card is destroyed, you may put this card into the soul of a 《Shadow Shade》 monster on your field.",
  "missing_capability": "COUNTER_CALL_FROM_HAND_AND_REDIRECT_ATTACK",
  "what_is_known": "Calls itself from hand as Counter during opponent's attack declaration and forces attack target redirection. Also on destruction trigger, moves itself directly into the soul of another monster on the field.",
  "information_needed": [
    "Approved schema for Counter-Act call from hand with in-progress attack target redirection.",
    "Approved schema for on-destruction trigger moving destroyed card into another card's soul instead of drop."
  ]
}
```

---

## 12. Buddy Zone Stand Action and Rest-Immunity (`BUDDY_ZONE_STAND`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/032TH",
  "ability_reference": "Re:TH/032TH: 【Act】 You may put this card into the drop zone of your 《Star Dragon World》 flag. If you do, [Stand] all cards on your field and in your buddy zone, and for this turn, all cards on your field and in your buddy zone cannot be [Rest] by your opponent's card effects.",
  "missing_capability": "BUDDY_ZONE_STAND",
  "what_is_known": "Targets cards in the buddy zone to [Stand] them and confers [Rest]-immunity to buddy zone cards.",
  "information_needed": [
    "Approved schema for targeting and changing position of cards in BUDDY zone.",
    "Approved schema for continuous Rest-prevention effect on buddy zone cards."
  ]
}
```

---

## 13. OverDrive Keyword Ability with Restriction Override (`KEYWORD_OVERDRIVE_AND_IGNORE_RESTRICTION`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "Re:TH/035TH",
  "ability_reference": "Re:TH/035TH: [OverDrive] [Call Cost] [Pay 2 gauge & Put the top card of your deck into its soul] (When this card is [Overturn] or [Overthrow] called, this ability activates! This ability cannot be nullified and its activation cannot be prevented by your opponent's cards) (Ignore this card's \"Loyalty\")",
  "missing_capability": "KEYWORD_OVERDRIVE_AND_IGNORE_RESTRICTION",
  "what_is_known": "Implements the [OverDrive] keyword trigger (activates on Overturn/Overthrow call, un-nullifiable) and explicitly ignores the card's 'Loyalty' restriction.",
  "information_needed": [
    "Approved schema for [OverDrive] keyword ability trigger and non-nullifiable flag.",
    "Approved schema for ignoring keyword restrictions like 'Loyalty' during call."
  ]
}
```


