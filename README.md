# Ghostwave

Send and receive links and photos through sound (ggwave). Created by Ayush Vaitage.

## Build the APK on GitHub
1. Create a new GitHub repository and upload everything in this folder
   (keep the `.github/workflows/build-apk.yml` file and the `resources` folder).
2. Open the **Actions** tab and run **Build APK** (it also runs on every push).
3. When it turns green, open the run and download **Ghostwave-APK** from **Artifacts**.
4. Unzip it and install `Ghostwave.apk` on your phone.

Every build is signed with the same key (`resources/debug.keystore`), so a new APK
installs over the old one without uninstalling.

## Change the app name or logo
- Name: edit `appName` in `capacitor.config.json` (and the title in `www/index.html`).
- Logo: replace the PNG files inside `resources/android-res/`.

## Control the app from far away (no new APK needed)
The app downloads `remote-config.json` from this GitHub repo every time it opens.
Edit that file on github.com (pencil icon, then **Commit changes**) and every phone
shows the change the next time the app is opened. Editing it does **not** rebuild the APK.

**First time only:** open `www/index.html`, find `REMOTE_CONFIG_URL` and make sure the
repository name in it matches your repo (`savdragon786-sudo/Ghost-Wave`). Then build the APK once.

What you can change from `remote-config.json`:
- `notice` : a popup (or a top banner with `"display": "banner"`) with a title, message and an optional button.
  Set `"enabled": true`. Change `id` to show a new notice again to everyone.
- `links` : buttons shown in About and at the bottom of the app. Put your Telegram channel link in `url`
  (empty `url` = button hidden). You can add more links, up to 8.
- `update` : set `latestVersion` and the APK download `url` to show "New version available".
  `"force": true` or a higher `minVersion` blocks old versions until they update.
- `maintenance` : `"enabled": true` shows a message and pauses the app for everyone.
- `about.extraText` : extra text inside the About window.
- `flags` : your own on/off switches for future options (read in the app as `GW.flags.name`).

Only `http`, `https` and `tg://` links are accepted. When you build a new APK, change
`APP_VERSION` in `www/index.html` and `version` in `package.json` together.
