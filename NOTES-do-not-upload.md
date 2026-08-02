# Your notes — don't commit this file

Keep this off GitHub. The public `README.md` is deliberately bland.

## Test mode

The bot is hidden. On the lobby screen, **tap the app name three times quickly** and the "Try it out" button appears. Three slow taps won't do it, so nobody finds it by accident.

## Where the material lives

All near the top of the `<script>` in `index.html`:

| What | Name | Notes |
|---|---|---|
| Punchlines by category | `LINES` | greeting, question, plans, food, angry, etc. |
| Meme captions | `CAPS` | top/bottom pairs for the GIFs |
| Emoji cast | `SUBJ` | the subject of GIFs and stickers |
| Emoji sets | `EMO_SETS` | the walls of emoji |
| Word banks | `ADJ` `NOUN` `VERB` `PLACE` `TIME` | feed the generated lines |
| The bot's script | `BOT` | fourteen messages of escalating concern |

In-jokes, local place names and people you both know land much harder than the generic stuff. That's the single best edit you can make.

## The mix

Roughly: text 71%, GIF 13%, emoji wall 7%, sticker 5%, voice note 4%. Change the thresholds at the top of `compose()`.

The text has ten generators — curated lines, mad-libs, autocorrect, keysmash, system messages, prophecy, corporate email, stage directions, wrong number, broadcast. Drop one you don't like by removing its name from `TEXT_MODES`.

## The leak guard

`tooSimilar()` rejects any output that keeps three of your words in a row and regenerates. Short messages skip the autocorrect mode entirely, because there isn't enough there to mangle. Don't remove this — without it your real message occasionally arrives intact.

## What still gives it away

- **Your repo is public.** Anyone who finds it can read `index.html`. The obvious names are gone but the material is right there. Send the Pages link, not the repo link — and give the repo a boring name.
- **View source** on a desktop browser shows everything. Unlikely on a phone, trivial on a laptop.
- The tap-the-name trick, if they watch you do it.

If you want it properly hidden, a private repo with Pages needs a paid GitHub plan. Otherwise assume a curious technical friend will work it out.

## One practical thing

Tell them eventually. It's a good joke for an evening, less good if they're trying to sort out actual plans and think you've had a stroke. Worth making sure they've got another way to reach you while it's running.
