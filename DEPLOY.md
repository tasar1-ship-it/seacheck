# Deploy Sea Check to GitHub Pages

Target URL when done: **https://tasar1-ship-it.github.io/seacheck/**

This folder is the complete app. Pick ONE of the two routes below.

---

## Route A — new dedicated repo (same as SailStrong)

Run from inside this `seacheck` folder on your Mac:

```bash
cd path/to/seacheck

git init
git add .
git commit -m "Sea Check v2 (PWA)"
git branch -M main

# creates the repo under your org and pushes (needs GitHub CLI `gh`, already
# authenticated on your Mac). If you don't use gh, create the empty repo
# "seacheck" in the tasar1-ship-it org on github.com first, then skip this line.
gh repo create tasar1-ship-it/seacheck --public --source=. --remote=origin --push

# if you created the repo manually instead of using gh:
# git remote add origin https://github.com/tasar1-ship-it/seacheck.git
# git push -u origin main
```

Then on github.com: repo **Settings -> Pages -> Source: Deploy from a branch ->
Branch: main / root -> Save**. Live in ~1 minute at the URL above.

## Route B — your existing publish.sh workflow

If `~/Library/Scripts/publish.sh` expects an app folder in your `pub` bucket,
drop this whole `seacheck` folder in and run publish.sh the way you do for the
other apps. (I couldn't verify publish.sh's exact interface from here, so
double-check the folder-name / slug argument it expects.)

---

## After it's live — put it on Lukas's phone

1. Open **https://tasar1-ship-it.github.io/seacheck/** in Safari on his iPhone.
2. Share button -> **Add to Home Screen**.
3. It launches full-screen with the compass icon, works offline, and saves
   his checks/photos/points on the phone.

## Files in this bundle
- index.html          the app
- manifest.json       PWA metadata (name, icons, standalone)
- sw.js               service worker (offline cache)
- icon-192.png / icon-512.png / apple-touch-icon.png   home-screen icons

## Notes
- Storage is per-device (browser localStorage). His phone keeps its own list;
  it does not sync to other devices.
- Photos are compressed to thumbnails; Safari's ~5 MB store holds plenty, and
  the app warns if it ever fills up.
