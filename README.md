# Lost in Transit

A chat app where what you type and what your friend receives are two completely different things.

You type *"How are you today?"* — they receive *"Why does your dad have a key to my flat?"*

Works on two real phones. One HTML file. No build step, no backend to run.

## Play

1. Open the site, enter your name, tap **New room**.
2. Tap the 🔗 icon in the message bar to copy your invite link.
3. Send it to your friend. They open it, add their name, tap **Join room**.
4. Talk. Try to hold a conversation. You will fail.

It behaves like a completely normal chat app. You see exactly what you typed. You have no idea what landed on their phone, and they have no idea what landed on yours — you're both just reading nonsense and replying in good faith. That's the whole game.

There's also **solo mode**, which pairs you with a bot who slowly loses his grip over fourteen messages.

## How the scramble works

Every message gets replaced with something else, and there are five kinds of "something else":

| | |
|---|---|
| **Text** (~71%) | ten different generators, below |
| **GIF** (~13%) | meme-captioned animated cards |
| **Emoji wall** (~7%) | `🚨🫠📠📠` |
| **Sticker** (~5%) | one enormous emoji, no bubble |
| **Voice note** (~4%) | a waveform and a duration. Tapping it plays nothing. It always plays nothing. |

The text generators each have a different failure mode: curated punchlines matched to what you meant, mad-libs, autocorrect that's given up, keysmash-then-composure, automated system messages, prophecy, corporate email, stage directions, wrong-number energy, and broadcast commentary. Emoji get sprinkled on top of roughly half of them.

Some shape carries over even though meaning doesn't. Questions come out as questions, ALL CAPS stays shouting, and `!!` survives. Long messages get a second unrelated thought tacked on.

### The leak guard

The one thing that must never happen is your actual message arriving. Anything that keeps three of your words in a row gets rejected and regenerated, and short messages skip the autocorrect mode entirely since there isn't enough there to mangle. Currently zero leaks across 27,000 generated messages.

### The GIFs are generated, not fetched

No Giphy, no Tenor, no API key to leak in a public repo, nothing to break when a key expires. Each GIF is built in CSS at send time: animated gradient, a subject emoji doing one of seven animations, drifting confetti, and Impact-style captions. The spec is a few bytes of JSON over the wire and gets rebuilt on your friend's phone.

### Making it yours

The `JOKES` object and the `CAPS` caption pairs are where the personality lives, and `SUBJ` is the emoji cast list. Add in-jokes, local place names, people you both know. Specific is always funnier than generic.

## How the connection works

Rooms run over a free public MQTT broker (EMQX, falling back to HiveMQ) using a room code as the topic. No account, no API key, no server of your own.

The scramble happens **before** anything is transmitted, so only the nonsense ever hits the wire. Your friend's device could not show them your original message even if they tried.

That said: the broker is public and unauthenticated. Anyone who guesses your four-letter room code can read the traffic. Don't put anything real in there — which is convenient, because nothing you type arrives intact anyway.

## Install it on your phone

Open the site in Safari, tap **Share → Add to Home Screen**. It launches like a real app — no address bar, no tab bar, full screen, its own icon. Android is the same via Chrome's **Install app**.

Launching from the icon drops any `?room=` link, so the app remembers your name and last room code and puts them back for you.

## Deploy

Push all five files to a repo, keeping them in the same folder:

```
index.html
manifest.json
apple-touch-icon.png
icon-192.png
icon-512.png
```

Then **Settings → Pages → Source: Deploy from a branch → main / (root)**. Live in about a minute at `https://<you>.github.io/<repo>/`.

Home screen install needs HTTPS, which GitHub Pages gives you for free. It won't work off a local `file://` copy.

## Licence

MIT. Do whatever you like with it.
