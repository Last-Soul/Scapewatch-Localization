# Translating Scapewatch

The rules and gotchas for anyone editing `locales/<code>.json`. If you're only fixing a few lines, the short version in the [README](README.md) is enough.

## How the game finds text

Most keys **are** the English text. When the game wants to show `Bank`, it looks up `"Bank"` in your language's file and shows the value. If a key is missing, the game shows the English. Every key in `en.json` must exist in every language file, so you never need to add one.

Some text is built at runtime from pieces: `Fish 35 Raw Perch`, `received a rare drop: [T3] Aluminum Helmet from Dire Orc!`. The game matches these against patterns and fills in a **template** from your file. Templates are the keys that start with `@`. Their English is in [`en-templates.json`](en-templates.json).

| Key looks like | What it is | Example |
|---|---|---|
| `"Bank"` | Plain text. The key is the English. | `"Bank": "Banque"` |
| `"@rare_drop_chat"` | A sentence template with blanks. | English: `received a rare drop: {0} from {1}!` |
| `"@f:loot_rolls"` | A word or phrase that gets dropped into other sentences. | English: `loot rolls` |
| `"@c:credits_screen"` | One English word with two meanings, split by context. | "Credits" the screen vs "Credits" the currency |
| `"@sh:..."` | A heading in Settings. | |
| `"@b:..."` | A bonus line on an item or skill tooltip. | |

## Placeholders: `{0}`, `{1}`, ...

These are blanks the game fills in: a name, a number, an item. Your translation must contain **exactly the same placeholders, the same number of times**. You can reorder them to fit your grammar:

```
English:  "received a rare drop: {0} from {1}!"          {0} = item, {1} = monster
zh-CN:    "获得了稀有掉落：来自{1}的{0}！"                  order swapped: fine
```

What each placeholder holds is in `en-templates.json` and usually obvious from the English. If a template has `{0}` twice, keep it twice.

**You can't add a case ending to a placeholder.** `{1}` might be "Dire Orc" or "Feeble Dungeon", and the game can't inflect it. In languages with cases (Finnish, Hungarian, Polish, Russian, Turkish, ...), phrase the sentence so the name needs no ending, for example with a colon or brackets: `ritka zsákmányt kapott: {0} ({1})`.

### Plurals

Some templates count things:

```
"{0, plural, one {# day left} other {# days left}}"
```

Keep the `{0, plural, ...}` structure and translate the text inside each branch. `#` is the number. Use the categories your language has (`one`, `few`, `many`, `other` for Polish, Russian, Czech, ...; just `other` for Chinese, Japanese, Korean, ...). `other` must always be there.

### The " +500 Luck XP" tail

The "New Collection!" lines end with a placeholder like `{2}` that is either empty or an already translated ` +500 Luck XP`. Keep it **last**, straight after your final punctuation, with no space before it:

```
"新收藏！获得了{1}掉落的{0}。{2}"
```

## Never translate

- **Player names.** They're placeholders, or a separate part of the line.
- **Tier tags** like `[T3]`, `[C]` and `[Ch]`. They must stay at the start of item names, exactly as in English. Translate the rest of the name: `"[T3] Aluminum Helmet": "[T3] 铝头盔"`.
- **Numbers, `%`, `×`, `/`**, and the developer's name (Puzzle Drop).
- **Anything in `{` `}`** except the text inside plural branches.

## Use one word for one thing

The same game term must use the same word everywhere: a task in the queue, a task in a tooltip and a task in a chat message are all the same word. Before choosing a word, search your file for how it's already translated. Each `review/<code>.md` starts with a table of your language's current words for the main game terms.

If you think a core term is wrong (for example, the word for "Quest" everywhere), say so in Discord or an issue first. Changing it means changing hundreds of lines at once, and it's easier to do that with a script.

## The double-translation trap

The game translates text again when it changes on screen, so **a translation must not look like an English pattern the game recognises**. For example, a Chinese value of `Lv {0}` for "Lvl. {0}" got translated a second time into `等 90`. Use your own language's words, not English abbreviations, and you'll never hit this.

## Lines shown after a player's name

Clan, raid and global chat announcements show as `Name: received a rare drop: ...`. The name is a separate part of the line, so the sentence reads with the player as the hidden subject. If your language needs a gendered verb, use a form that works for anyone (present tense, a passive, or an impersonal phrasing).

The full list of these announcements and their keys:

| English | Key |
|---|---|
| `received a rare drop: {0} from {1}!` | `@rare_drop_chat` |
| `received a rare raid drop: {0} from {1}!` | `@rare_raid_drop_chat` |
| `New Collection! Received {0} as a {1} drop.{2}` | `@collection_drop_chat` |
| `New Collection! Received {0} as a {1} milestone.{2}` | `@collection_milestone_chat` |
| `New Collection! Received {0} from a treasure chest.{1}` | `@collection_chest_chat` |
| `New Collection! Received a SHINY {0} from a task completion.{1}` | `@collection_task_shiny_chat` |
| `New Collection! Received {0} from a task completion.{1}` | `@collection_task_chat` |
| `New Collection! Received {0} from bartering.{1}` | `@collection_barter_chat` |
| `New Collection! Received {0} from plundering.{1}` | `@collection_plunder_chat` |
| `New Collection! Received {0} from {1}.{2}` (a skill or a quest) | `@skilling_collection_chat` |
| `New Collection! Claimed {0}x {1} from the Alms Path.{2}` | `@alms_collection_chat` |
| `New Collection! Unlocked the {0}. +{1} {2}` | `@unlock_collection_chat` |
| `New Collection! Completed the quest: {0}.{1}` | `@collection_quest_done_chat` |
| `completed a quest step: {0} ({1}/{2})` | `@quest_step_chat` |
| `completed the quest: {0}!` | `@quest_done_chat` |
| `completed a task: {0}` | `@task_done_chat` |
| `received the {0} pet!` / `received the SHINY {0} pet!` | `@pet_chat` / `@shiny_pet_chat` |
| `unlocked the {0} Cape!` / `unlocked the Trimmed {0} Cape!` | `@cape_chat` / `@trimmed_cape_chat` |
| `unlocked the MAX CAPE!` / `unlocked the TRIMMED MAX CAPE!` | plain keys |
| `unlocked: {0}` | `@unlocked_chat` |
| `Completed the {0} set and received the {1}!` | `@shard_set_chat` |
| `received the {0}!` (lucky tools) | `@received_the_chat` |
| `has died!` | plain key |
| `Level up! {0} level is now {1}` | `@level_up` |
| `{0} donated {1} bloodcoins to the clan coffer ({2} total)` | `@coffer_donated_chat` |
| `{0} received the {1}!` (raid party) | `@raid_rare_drop` |
| `{0} has joined your lobby ({1}/{2})` / `has left` | `@raid_lobby_joined` / `@raid_lobby_left` |
| `{0} will play {1} from the next run` | `@lobby_role_next_run` |
| `{0} swapped roles with {1}: {0} plays {2}, {1} plays {3}` (and the "from the next run" and "now plays" versions) | `@lobby_role_swap` / `@lobby_role_swap_next` / `@lobby_role_swap_now` |

## Style

- Match the game's tone: short, plain, friendly. Tooltips are small, so shorter is better.
- Buttons and tabs are tiny. If your word is much longer than the English, look for a shorter one.
- Use your language's normal punctuation (full-width `！：（）` in Chinese and Japanese, `« »` in French, and so on), and keep it consistent with the rest of your file.
- Don't use em dashes (—) or en dashes (–), except in Chinese, Japanese, Korean and Russian, where they're normal. Use a comma, colon or full stop instead.

## Checking your work in the game

Change the language in **Settings** (or on the login screen), then play a little and look for anything that's still English, cut off, or reads badly. Screenshots of problems are very welcome in Discord, even if you don't know the fix.

## What the bot checks

Before a change is copied into the game, the bot makes sure that:

- the key already exists (no new or misspelled keys)
- the value isn't empty
- the placeholders match
- there's no HTML (`<` or `>`) unless the English has some
- the whole file still passes the game's own translation checks (tier tags, place names used consistently, plural syntax)

A change that fails is left out, and the bot's commit message in this repo says which line failed and why. Fix it and send it again.
