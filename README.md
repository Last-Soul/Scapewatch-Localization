# Scapewatch Localization

Every piece of text in [Scapewatch](https://store.steampowered.com/app/4671380/Scapewatch_Idle_MMO/), in all 31 languages, lives here. Most languages started as a machine translation and have only been partly checked by native speakers, so some lines read badly. If you speak one of these languages, you can make the game better for everyone who plays in it.

You do not need to know how to code: you can do everything in your web browser with a free GitHub account.

**The repo:** https://github.com/Puzzle-Drops/Scapewatch-Localization

## How your changes get into the game

1. You open a pull request here with your fix.
2. A maintainer reviews it and merges it into this repo.
3. A sync bot checks for merged changes every few hours. It runs the same checks the game's own translations go through, then copies your change into the game's test server.
4. It ships to everyone with the next game update, and you get credited.

If a change breaks a check (a missing `{0}`, for example), the bot leaves it out and says why in this repo's history. Nothing you do here can break the game.

## How to help

All suggestions go through GitHub, so nothing gets lost and everyone can see what's been fixed.

### 1. Edit it on GitHub in your browser (no tools needed)

1. Make a free GitHub account if you don't have one.
2. Open the `locales` folder and click your language's file (for example `locales/zh-CN.json`).
3. Click the pencil icon (Edit). GitHub makes your own copy automatically.
4. Press Ctrl+F and search for the text you want to fix.
5. Change only the text on the **right** of the colon. Leave the left side alone:

   ```
   "Bank": "Banque",
            ^^^^^^ change this part only
   ```

6. Click **Commit changes**, then **Propose changes**, then **Create pull request**. Say in one line what you changed and why.

You can change as many lines as you like in one pull request.

### 2. Big batches (git)

If you're reworking a whole language, or you already have your own translation patch (like the community zh-CN userscript), clone this repo, edit `locales/<code>.json` and open one pull request. Run the game with your language selected to check that it reads well in place.

### 3. Found a problem you can't fix yourself?

[Open an issue](https://github.com/Puzzle-Drops/Scapewatch-Localization/issues/new/choose) and pick **Translation problem**. Fill in the language, a screenshot or where in the game you saw it, what it says now, and what it should say if you know. Use an issue too for text that still shows in English, or English that's wrong or unclear.

## Where to start

The **[review](review/)** folder has one file per language. It lists the most recent machine-translated lines that haven't been checked by a native speaker yet, with the English next to each one, plus your language's words for the main game terms. That's the most useful place to start: read each line, fix anything wrong, and move on.

After that, the best help is simply playing in your language and fixing whatever reads badly. Older lines were machine translated too.

If you spot the same mistake in many lines (missing accents, the wrong word for a game term), open an issue instead of fixing them one by one. We can fix them all at once.

## What's in this repo

| Path | What it is |
|---|---|
| `locales/<code>.json` | The translation for one language. **This is what you edit.** |
| `en.json` | The English source text. The key on the left is the English, so it's the same on both sides. |
| `en-templates.json` | The English for the keys starting with `@` (sentences with blanks like `{0}`), so you can see what they say. |
| `review/<code>.md` | Lines in that language still waiting for a native speaker's check. |
| `TRANSLATING.md` | The rules: placeholders, names, sentence templates, and things to watch out for. Read this before a big batch. |
| `CONTRIBUTORS.md` | Everyone who has helped. Add your name in your pull request. |

Please don't edit `en.json`, `en-templates.json`, `review/` or the docs. The bot rewrites them from the game. If the English itself is wrong or unclear, open an issue.

## The rules in short

- **Change only the right-hand side.** The key on the left is how the game finds the text.
- **Keep every `{0}`, `{1}`, ... placeholder.** You can move them around to fit your grammar, but the same ones must be there. They're filled in with names and numbers.
- **Don't translate player names.** Keep tier tags like `[T3]` exactly as they are.
- **Use one word for one thing.** If the game calls a task 委托 in one place, it should say 委托 everywhere. Search the file for how something is already translated before you pick a word.
- **No HTML or code.** Plain text only.
- **Don't add new keys.** If some text in the game shows in English, open an issue. It usually needs a change to the game, not just a new line here.

The full rules are in [TRANSLATING.md](TRANSLATING.md).

## Languages

| Code | Language | Lines to review |
|---|---|---|
| `bg` | Български | [444](review/bg.md) |
| `cs` | Čeština | [444](review/cs.md) |
| `da` | Dansk | [444](review/da.md) |
| `de` | Deutsch | [444](review/de.md) |
| `el` | Ελληνικά | [444](review/el.md) |
| `es` | Español (Latinoamérica) | [444](review/es.md) |
| `es-ES` | Español (España) | [444](review/es-ES.md) |
| `fi` | Suomi | [444](review/fi.md) |
| `fil` | Filipino | [444](review/fil.md) |
| `fr` | Français | [444](review/fr.md) |
| `hu` | Magyar | [444](review/hu.md) |
| `id` | Bahasa Indonesia | [444](review/id.md) |
| `it` | Italiano | [444](review/it.md) |
| `ja` | 日本語 | [444](review/ja.md) |
| `ko` | 한국어 | [444](review/ko.md) |
| `ms` | Bahasa Melayu | [444](review/ms.md) |
| `nl` | Nederlands | [444](review/nl.md) |
| `no` | Norsk | [444](review/no.md) |
| `pl` | Polski | [444](review/pl.md) |
| `pt-BR` | Português (Brasil) | [444](review/pt-BR.md) |
| `pt-PT` | Português (Portugal) | [444](review/pt-PT.md) |
| `ro` | Română | [444](review/ro.md) |
| `ru` | Русский | [444](review/ru.md) |
| `sv` | Svenska | [444](review/sv.md) |
| `th` | ไทย | [444](review/th.md) |
| `tr` | Türkçe | [444](review/tr.md) |
| `uk` | Українська | [444](review/uk.md) |
| `vi` | Tiếng Việt | [444](review/vi.md) |
| `zh-CN` | 简体中文 | [444](review/zh-CN.md) |
| `zh-TW` | 繁體中文 | [444](review/zh-TW.md) |

## Credit

Everyone who helps is listed in [CONTRIBUTORS.md](CONTRIBUTORS.md), and translators are credited in the game's Credits screen. Add the name you'd like to be credited as to CONTRIBUTORS.md in your pull request.

## Terms

By opening a pull request or an issue, you agree to the terms in [LICENSE.md](LICENSE.md). In short, Puzzle Drop Studios can use your translation in Scapewatch, and you'll be credited.

Thank you for helping!
