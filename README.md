# Trail Ledger — Setup Guide (GitHub Pages + Firebase)

Two parts: connect a free database (5 min), then put the file on GitHub Pages (5 min).

## Part 1 — Free Firebase database

1. Go to https://console.firebase.google.com and sign in with any Google account.
2. Click **Add project** → name it anything (e.g. `trip-ledger`) → you can skip Google Analytics → **Create project**.
3. In the left sidebar, go to **Build → Realtime Database** → **Create Database**.
   - Pick any location.
   - Choose **Start in test mode** → **Enable**.
4. Click the **Rules** tab (still inside Realtime Database) and replace the contents with:
   ```json
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
   Click **Publish**. (Test mode alone expires after 30 days — this makes it permanent. Since there's no login on the app, anyone who has the config *and* knows what to do with it could read/write it, but in practice only people you share the link with will ever see it.)
5. Click the **gear icon (⚙) → Project settings**, scroll to **Your apps**, click the **`</>`** (web) icon.
   - Give it a nickname (e.g. `ledger`) → **Register app**.
   - You'll see a `firebaseConfig` object like:
     ```js
     const firebaseConfig = {
       apiKey: "AIza...",
       authDomain: "trip-ledger-xxxx.firebaseapp.com",
       databaseURL: "https://trip-ledger-xxxx-default-rtdb.firebaseio.com",
       projectId: "trip-ledger-xxxx",
       storageBucket: "trip-ledger-xxxx.appspot.com",
       appId: "1:...:web:..."
     };
     ```
   - Copy this whole object.

## Part 2 — Add it to the file

1. Open `trip-ledger-github.html` in any text editor.
2. Near the top, find the `firebaseConfig` block (search for `PASTE_YOUR`).
3. Replace it with the object you copied above.
4. Save the file.

## Part 3 — Put it on GitHub Pages

1. On GitHub, create a **new public repository** (e.g. `trip-ledger`).
2. Upload `trip-ledger-github.html`, but **rename it to `index.html`** when uploading.
3. Go to the repo's **Settings → Pages**.
4. Under **Source**, choose the `main` branch and `/ (root)` folder → **Save**.
5. Wait ~1 minute, then refresh that Pages settings tab — it'll show your live link:
   `https://yourusername.github.io/trip-ledger/`

That link is what you send your group. Everyone who opens it sees and edits the same live ledger in real time.

## Notes
- Anyone with the link can add/edit/delete expenses — there's no login.
- If you ever want to reset all data, go to Firebase → Realtime Database → find the `trip-ledger-data` node → delete it. The app will recreate it with the default 10 names on next load.
