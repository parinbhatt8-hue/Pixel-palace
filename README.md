# Pixel Palace Murder (APK project)

A retro pixel-tile detective game packaged with Capacitor.

## Build the APK from your phone (GitHub Actions)
1. Create a new GitHub repo and open it in a Codespace.
2. Upload this zip in the Codespace Explorer, then run: `unzip -o pixel-palace-murder-apk.zip -d . && rm pixel-palace-murder-apk.zip`
   (if the files land in a subfolder, move them to the repo root so `package.json` sits next to `.github/`)
3. Commit and push to `main`.
4. Open the repo's **Actions** tab, pick **Build APK**, and wait for it to finish (it also runs on every push).
5. Open the finished run, download the **PixelPalaceMurder-apk** artifact, unzip it, and install `app-debug.apk`
   (allow "install unknown apps" when Android asks).

## Build locally (needs Node 20, JDK 17, Android SDK)
```
npm install
npx cap add android
npx cap sync android
cd android && ./gradlew assembleDebug
```
APK: `android/app/build/outputs/apk/debug/app-debug.apk`

## Notes
- Game files live in `www/`. Edit `www/index.html`, push, and the workflow rebuilds the APK.
- The AI levels (the AI picks each theme, look, and difficulty) and free-typed suspect chat appear only when `AI_ENDPOINT` is set. Without it, the APK plays the classic case with scripted answers.
- Suspects use scripted answers in the APK. To enable free-typed AI chat, set `window.AI_ENDPOINT` at the top of
  `www/index.html` to a small server of yours that accepts `POST {prompt}` and returns `{text}` (with CORS enabled).
  Keep API keys on that server, never in the app.
- This is a debug-signed APK, fine for installing on your own phone. A Play Store release needs a signed release build.
