# Unsupported Mechanic Report — BFO-RP01

Specification reference: `Buddyfight_2D_Unity_Card_JSON_Agent_Spec.md` (Section: Unsupported Mechanic Policy).

---

## 1. In-Deck Flag Construction and Stacking Evolution (`IN_DECK_FLAG_CONSTRUCTION_AND_EVOLUTION`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "BFO-RP01/S001",
  "ability_reference": "BFO-RP01/S001: You cannot choose this card as your flag during the start of the fight. You may put this card into your deck and use it if your initial flag is \"Dragon Zwei\". / You may use originally monster cards that have \"Dragon\" in its attribute. / [1/Game] If your life would become 0, [Cost] [Put this card on top of your \"Dragon Zwei\" flag], and until the start of your opponent's next turn, all cards on your field cannot be destroyed, leave the field, or [Rest], by your opponent's card effects, and you cannot lose the game.",
  "missing_capability": "IN_DECK_FLAG_CONSTRUCTION_AND_EVOLUTION",
  "what_is_known": "Pre-game deck building rule permitting this flag card to be included in the main deck if initial flag is Dragon Zwei, attribute inclusion rules based on original card attributes, and lethal damage trigger replacing/stacking this flag on top of Dragon Zwei from hand/deck.",
  "information_needed": [
    "Approved schema for main-deck flag inclusion and conditional deck building rules based on initial flag and original attributes.",
    "Approved schema for dynamic flag zone stacking/evolution triggered by lethal damage."
  ]
}
```

---

## 2. Game Loss Immunity and 0-Life/0-Deck Continuation (`GAME_LOSS_IMMUNITY_AND_CONTINUATION`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "BFO-RP01/S001",
  "ability_reference": "BFO-RP01/S001: ...and you cannot lose the game. / (The game will continue even if your life becomes 0 or there are no cards remaining in your deck.)",
  "missing_capability": "GAME_LOSS_IMMUNITY_AND_CONTINUATION",
  "what_is_known": "Overrides fundamental game loss rules; grants temporary game-loss immunity, followed by continuous rule allowing play to proceed even with 0 life or empty deck.",
  "information_needed": [
    "Approved engine representation for temporary CANNOT_LOSE_GAME state modifier.",
    "Approved engine rule for persistent game continuation when life reaches 0 or deck is depleted."
  ]
}
```

---

## 3. Lethal Life Interception and Set to 1 (`REPLACEMENT_LETHAL_LIFE_SET_TO_1`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "BFO-RP01/S002",
  "ability_reference": "BFO-RP01/S002: [1/Turn] If your life would become 0, [Cost] [Drop an 《Evil Demonic Dragon》 monster from this card's soul], your life becomes 1!",
  "missing_capability": "REPLACEMENT_LETHAL_LIFE_SET_TO_1",
  "what_is_known": "Intercepts fatal life reduction (would become 0) with a 1/Turn restriction, pays cost by dropping an Evil Demonic Dragon monster from this set spell's soul, and modifies player's life state to 1.",
  "information_needed": [
    "Approved schema for lethal damage interception replacement triggering SET_LIFE to 1 using soul drop cost with turn limit."
  ]
}
```

---

## 4. Opponent Search Scope Interception and Restriction (`OPPONENT_SEARCH_SCOPE_REPLACEMENT_AND_SECONDARY_EFFECT_COST`)

```json
{
  "status": "UNSUPPORTED_MECHANIC",
  "card_reference": "BFO-RP01/S003",
  "ability_reference": "BFO-RP01/S003: 【Hand】: [Counter] 【Act】 [Cost] [Drop this card], for this turn, the next time your opponent would search their entire deck for a card, they search the top 5 cards of their deck instead. Then, [Cost] [Remove 1 card with the name \"ReAc: Empress\" from your drop zone] draw two cards.",
  "missing_capability": "OPPONENT_SEARCH_SCOPE_REPLACEMENT_AND_SECONDARY_EFFECT_COST",
  "what_is_known": "Activated from hand during Counter timing. Sets a pending one-shot replacement modifying opponent's next deck search this turn to inspect only top 5 cards. Contains a follow-up secondary cost paying drop card removal to draw 2 cards.",
  "information_needed": [
    "Approved schema for intercepting and scoping opponent deck searches.",
    "Approved schema for sequential optional follow-up cost payment within ability resolution."
  ]
}
```
