# YINGXUE — Test v2 (Patched)

> A helper script for **AI Dungeon** that adds a little structure, memory, and mood to your stories.  
> Made by a player, for players — not a pro coder’s fortress of jargon. 🦋

---

## 🌸 What is this?

Yingxue is a **state manager + context shaper**.  
It keeps track of story beats (turns, moods, tension, characters) and tries to feed AI Dungeon more *aware, consistent* prompts.

Think of it as:
- A quiet stagehand in the background.
- Tidying up story notes.
- Keeping characters remembered.
- Nudging tone with “tension” and “mood.”

---

## ⚙️ How it works (the simple view)

- **State lives in `state.yingxue`.**  
  This is the little “memory box” the script uses.  
  Inside are things like:
  - `turn` → how many turns have passed.
  - `currentLocation` → where we are.
  - `currentMood` → vibe of the scene (`neutral`, `tense`, etc).
  - `tension` → a number that goes up when drama builds, down when it cools.
  - `characters` → names + relationships it notices in your text.
  - `flags` → small reminders like last action types.

- **Every input is normalized.**  
  Filler words (`um`, `uh`, `er`) get cleaned. Pronouns get aligned. Quoted text is protected so it isn’t touched.

- **Characters are auto-detected.**  
  It scans text for TitleCase words (“Alice”, “Mr. Gray”) and logs them.

- **Pruning keeps it lean.**  
  Long histories are trimmed so your game doesn’t drown in old data.

---

## 🪄 What you can safely tweak

Inside the config at the top of the script:

- `fillerWords` → add/remove words you want scrubbed.  
- `tension.decayRate` / `buildRate` → how fast the “tension meter” rises/falls.  
- `tension.maxTension` / `minTension` → clamp the drama ceiling/floor.  
- `prune.*` → how many items to keep in histories before cutting old ones.

---

## ⚠️ What **not** to break

- **The return shapes.**  
  Input, Context, Output tabs must return `{ text }` (Context can also return `{ text, stop }`). Don’t change that.

- **The `state.yingxue` object shape.**  
  If you remove keys (like `turn`, `characters`, `tension`), other functions will throw errors.

- **Quote protection.**  
  That funky placeholder code (`__QUOTE_0__`) is important. Don’t delete unless you know how to rewire it.

---

## 🧩 Common gotchas

- If you see weird names being logged → that’s the `extractCharacterName` function grabbing false positives. Not game-breaking, just noisy.
- If pruning feels too aggressive or not enough → tweak `prune` numbers.
- If the script “forgets” characters → it’s pruning or never detected them. You can always add manually.

---

## 💡 Tips for new tinkerers

- **Comment often.**  
  Use `//` to write yourself reminders.

- **Experiment small.**  
  Change one config number, test a few turns, then change another.

- **Don’t fear breaking it.**  
  Worst case: copy back the original file from GitHub.  
  (That’s why this README exists!)

---

## 🖤 Closing thought

Yingxue isn’t perfect code. It’s a companion script that grows with your play.  
Treat it like a diary that quietly edits itself, not a strict machine.