# Firebase Setup — PDI Snag Tracker

Takes about 5 minutes. You'll need a Google account.

## 1. Create Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **Add project** → name it `pdi-snag-tracker` → disable Google Analytics (not needed) → Create
3. Wait for project creation

## 2. Enable Authentication

1. In the left sidebar, click **Build → Authentication**
2. Click **Get started**
3. Under Sign-in method, enable **Email/Password**
4. Go to the **Users** tab → **Add user**
5. Enter your email and a password — this is your login for the app

## 3. Create Firestore Database

1. In the left sidebar, click **Build → Firestore Database**
2. Click **Create database**
3. Choose **Start in production mode**
4. Pick a location close to you (e.g. `asia-south1` for India)
5. Once created, go to the **Rules** tab and replace the rules with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /snags/{snagId} {
      allow read, write: if request.auth != null;
    }
    match /media/{docId} {
      allow read, write: if request.auth != null;
    }
    match /meta/{docId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

6. Click **Publish**

## 4. Get Your Firebase Config

1. Click the **gear icon** (top left) → **Project settings**
2. Scroll down to **Your apps** → click the **Web** icon (`</>`)
3. Register app with nickname `pdi-tracker` (no Firebase Hosting checkbox needed)
4. You'll see a config block like this:

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "pdi-snag-tracker-xxxxx.firebaseapp.com",
  projectId: "pdi-snag-tracker-xxxxx",
  storageBucket: "pdi-snag-tracker-xxxxx.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcdef123456"
};
```

5. Copy this entire block

## 5. Add Config to the App

1. Open `index.html`
2. Find the line `const firebaseConfig = { /* PASTE YOUR CONFIG HERE */ };`
3. Replace it with your config block from step 5
4. Save

## 6. Deploy

### Option A: Firebase Hosting (recommended)

```bash
npm install -g firebase-tools
firebase login
firebase init hosting
# Select your project, set public directory to "." , single-page app: No
firebase deploy
```

### Option B: Any static hosting

Push to GitHub Pages, Netlify, Vercel, or Cloudflare Pages — same as before.
The Firebase backend works regardless of where the HTML is hosted.

## 7. First Login

1. Open the site
2. Log in with the email/password from step 2
3. The app will auto-seed all 91 snags on first login
4. Open on another device, log in → everything syncs
