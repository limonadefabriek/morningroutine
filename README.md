# 8 Minutes

A no-equipment morning routine that runs in a phone browser. Seven slots, three
rotating day types, a timer that advances itself, and a re-test every two weeks
that decides whether the whole thing steps up or down a level.

Static files only — no build step, no server, no dependencies, no cost.

## The files

| File | What it is |
|---|---|
| `index.html` | The whole app — styling, exercises, drawings, timer, progression |
| `sw.js` | Service worker, so it works with no signal |
| `manifest.webmanifest` | Lets it install to the home screen as an app |
| `icon.svg`, `icon.png` | Home screen icon |

## Putting it on GitHub Pages

1. Create a new repository — call it `morning` or whatever you like. Public is
   simplest; Pages on a private repo needs a paid plan.
2. Upload all five files to the root of the repository.
3. Go to **Settings → Pages**. Under *Source* choose **Deploy from a branch**,
   pick branch `main` and folder `/ (root)`. Save.
4. Wait a minute or two. The URL will be
   `https://<your-username>.github.io/<repo-name>/`.
5. Open that on your phone, then **Share → Add to Home Screen**. It launches
   full-screen with no browser chrome and runs offline from then on.

From the command line instead:

```bash
git init -b main
git add .
git commit -m "Morning routine"
git remote add origin git@github.com:<you>/<repo>.git
git push -u origin main
# then enable Pages in Settings, as above
```

## Changing things

Everything lives in the `<script>` block at the bottom of `index.html`.

- **Swap an exercise** — edit the entry in `EX`, or point the day at a different
  one in `DAYS`.
- **Change the timings** — `dur` on each exercise, and `REST` for the gaps.
  The home screen recalculates the total on its own.
- **Change the progressions** — each exercise has a `prog` array of five
  strings, one per level. The card shows the one matching your current level.
- **Move a figure** — poses are joint coordinates in a 220 × 132 box with the
  floor at y = 122. Nudge a number, reload, look.

After changing anything, bump `CACHE` in `sw.js` (`morning8-v1` → `morning8-v2`)
or the service worker will keep serving the old version.

## Your data

Level, history and re-test numbers live in `localStorage` on the device — they
never leave the phone, and nothing is sent anywhere. Clearing site data resets
them. Changing phones starts fresh.
