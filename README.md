# Punch Lab

Installable app (PWA) for measuring punch speed, rotation sequencing and a Power Index with MediaPipe pose tracking. Runs entirely on the device: no account, no server, and no video leaves the phone or computer.

## Get it on your phone or computer

An installable web app needs one HTTPS address to install from. It doesn't have to be your website. Any of these works:

**Netlify Drop (no account setup, about a minute)**
1. Go to https://app.netlify.com/drop
2. Drag this whole `punch-lab-app` folder onto the page.
3. Open the address it gives you (something like `random-name.netlify.app`).

**Vercel, as its own project (separate from your website)**
1. Put this folder in a new GitHub repo, for example `punch-lab`.
2. In Vercel, click Add New → Project, import that repo, and deploy with the default settings (no build step).
3. You get a separate address like `punch-lab.vercel.app`.

Then install it:
- **Android / Chrome / Edge:** tap the "Install app" button in the header, or use the browser menu → Install app.
- **iPhone / iPad:** open the address in Safari → Share → Add to Home Screen.
- **Mac / Windows (Chrome or Edge):** click the install icon in the address bar.

## First launch

The pose model (Lite and Full) ships inside the app in `mediapipe/`, so it no longer depends on Google's download server. That server being blocked is what stopped the earlier version. The pose engine still downloads once from jsDelivr, and the app keeps it on the device, so after the first launch it opens and tracks offline.

The Heavy model (about 30 MB) isn't bundled. Picking it downloads it from Google; if that's blocked, the app shows a "Load model file" button.

## Video files

Video analysis pauses on every frame while the tracker works on it, so no frame is skipped, however slow the device. A slow device just takes longer. Phone slow-mo clips give the most accurate speeds; set "Video plays as" to match the clip.

## Try it on a computer without deploying

From inside this folder, run a local web server, for example `npx serve` or `python3 -m http.server 8000`, then open the `http://localhost` address it prints. Cameras are allowed on localhost. Opening `index.html` by double-clicking won't work, because browsers block the downloads for local files.

## Files

- `index.html`: the whole app (UI, punch detection engine, charts)
- `manifest.webmanifest`, `icons/`: what makes it installable
- `sw.js`: offline support (caches the app, engine and model)
- `mediapipe/`: the bundled pose models
