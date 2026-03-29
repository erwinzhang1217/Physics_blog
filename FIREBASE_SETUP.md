# Firebase setup for Physics blog (cloud sync)

Posts sync across all devices via **Firebase Realtime Database**. Follow these steps once.

## 1. Create a Firebase project

1. Open [Firebase Console](https://console.firebase.google.com/) and create a project (Spark/free is enough).
2. In the sidebar: **Build → Realtime Database** → **Create database**.
3. Choose a region, start in **test mode** or set rules manually (see below).

## 2. Security rules (personal blog)

In **Realtime Database → Rules**, you can use open read/write for a small personal site:

```json
{
  "rules": {
    ".read": true,
    ".write": true
  }
}
```

**Warning:** Anyone with your database URL can read/write. For stronger security later, add Firebase Authentication and tighten rules.

## 3. Register a web app and copy config

1. **Project settings (gear) → General → Your apps** → Web app (`</>`).
2. Copy the `firebaseConfig` object values.

## 4. Put config in `index.html`

In [index.html](index.html), find **`FIREBASE_CONFIG`** in the `<script>` block and replace placeholders with your values:

- `apiKey`
- `authDomain` (e.g. `your-project.firebaseapp.com`)
- `databaseURL` — copy the exact **Realtime Database URL** from the Firebase console (e.g. `https://your-project-default-rtdb.firebaseio.com` or a regional `*.firebasedatabase.app` URL)
- `projectId`

Save, commit, and push. GitHub Pages will load the same data for every browser.

## Offline / no Firebase

If `apiKey` is still `REPLACE_ME`, the site falls back to **localStorage** (per device only), same as before.
