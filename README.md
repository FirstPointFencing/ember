# Ember — beta (Route 1 PWA)

This is a working, installable version of Ember you can put on your Android phone and share real posts into. It's a **Progressive Web App**: no app store, no build tools, just static files hosted on GitHub Pages.

## What's in here

```
ember-pwa/
├─ index.html              ← the app
├─ manifest.webmanifest    ← makes it installable + registers the share target
├─ service-worker.js       ← lets it install and work offline
├─ icons/                  ← app icons
└─ README.md               ← this file
```

## Step 1 — Put it on GitHub Pages

**The easy way (no command line):**

1. On GitHub, create a new repository — call it something like `ember`. Make it **Public**.
2. On the repo page, click **Add file → Upload files**. Drag in **everything inside this `ember-pwa` folder** (the `index.html`, `manifest.webmanifest`, `service-worker.js`, and the `icons` folder). Commit.
3. Go to **Settings → Pages**. Under "Build and deployment", set **Source: Deploy from a branch**, **Branch: `main`**, folder **`/ (root)`**. Save.
4. Wait ~1 minute. Pages will show a live URL like:
   `https://YOUR-USERNAME.github.io/ember/`

That URL is your app. (Because it lives in a sub-folder, all the file paths in here are relative — don't worry about that, it just works.)

**If you prefer git:**

```
git init && git add . && git commit -m "Ember beta"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/ember.git
git push -u origin main
```
Then enable Pages as in step 3.

## Step 2 — Install it on your Android phone

1. Open the Pages URL in **Chrome** on your phone.
2. Chrome will offer **"Install app"** (or use the ⋮ menu → **Install app / Add to Home screen**). Choose **Install** — this matters, because installing is what registers Ember as a share target.
3. Ember now has its own icon on your home screen and opens full-screen like a real app.

The first launch runs the onboarding; after that it remembers you.

## Step 3 — Share posts into it

Once installed, open Instagram/Facebook/TikTok, tap **Share** on any post → **Share to…** → pick **Ember**. The post lands at the top of your feed, Ember guesses *why* you saved it, and you confirm or change it.

You can also tap **Save something** inside the app and paste a link.

## What works now vs. what's stubbed

- ✅ Install to home screen, full-screen, works offline
- ✅ Share real posts in (Android) — or paste a link
- ✅ The five-a-day feed, treatments, the "why" guess + confirm, reshuffle, culling, Go deeper, let-it-fade
- ✅ Everything saves on your device (survives closing the app)
- ⚠️ **Summaries aren't real yet.** Until we connect a summarizer, a shared card shows what you shared plus a naive on-device guess at the pull. Tap **Original** to open the actual post. Wiring up real summaries + smarter guessing is the next backend step.
- ❌ **iOS**: iPhones don't let a PWA receive shares, so the "share into Ember" flow is Android-only for now. On iPhone you can still install it and paste links.

## Sharing with friends

Just send them the Pages URL. Anyone on Android can install it the same way. Their data stays on their own phone.

## Updating it later

Re-upload the changed files to the repo. One catch: the service worker caches the app, so to force everyone's phone to pull the new version, bump the version string near the top of `service-worker.js` (change `ember-beta-v1` to `ember-beta-v2`, etc.) whenever you push an update.
