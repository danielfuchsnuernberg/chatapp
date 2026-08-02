# Tin Can

Lightweight chat rooms in a single HTML file. Share a four-letter code, talk. No accounts, no phone numbers, no server of your own to run.

## Use it

1. Open the site, enter your name, tap **New room**.
2. Tap the 🔗 in the message bar to copy the invite link.
3. Send it to whoever you're talking to. They open it, add their name, tap **Join room**.

Conversations are saved on your device per room and come back when you reopen the app, with day separators and original send times. The 🗑 in the header clears the current chat — two taps, so a stray thumb can't wipe it.

## Install on your phone

Safari: **Share → Add to Home Screen**. Chrome: **Install app**. It runs fullscreen with no address bar.

## Deploy

Push these five files to a repo, keeping them together:

```
index.html
manifest.json
apple-touch-icon.png
icon-192.png
icon-512.png
```

Then **Settings → Pages → Source: Deploy from a branch → main / (root)**. Live in a minute at `https://<you>.github.io/<repo>/`.

Home screen install needs HTTPS, which GitHub Pages provides. It won't work from a local `file://` copy.

## How it works

Rooms run over a free public MQTT broker using the room code as a topic — that's why there's no backend and no signup. The broker is public and unauthenticated, so anyone who guesses your code can join the room. Pick a fresh code for anything you'd rather keep to yourselves.

Message history is `localStorage` on each device. Nothing is stored on a server and nothing syncs between devices, so clearing one phone doesn't affect the other. Last 250 messages per room.

## Licence

MIT.
