# Setup Guide — Gaming Tournament App

> A complete HTML + Firebase gaming tournament platform with user/admin front-ends, a giveaway module, and a 500+ theme switcher.

Made by **Sudais Alam**.

---

## Project Overview

The Gaming Tournament App is a static HTML application that runs entirely in the browser and uses **Firebase** as its backend (Realtime Database, Authentication, Firestore, and Hosting). It is designed to be deployed on any static host or wrapped into an Android app.

---

## Prerequisites

- A modern web browser (Chrome, Edge, Firefox, Safari).
- A text editor (VS Code recommended).
- A free **Firebase** account (https://console.firebase.google.com).
- (Optional) A static host such as **InfinityFree**, **Netlify**, or **Firebase Hosting**.
- (Optional) **HopWeb** if you want to package the app as an Android APK.

---

## Installation

1. **Extract the archive**

   ```bash
   unzip "Complete Gaming Tournament.zip" -d gaming-tournament
   cd gaming-tournament
   ```

2. **Configure Firebase**

   - Go to the [Firebase Console](https://console.firebase.google.com) and create a new project.
   - In **Build → Realtime Database**, create a database.
   - In **Build → Authentication**, enable Email/Password.
   - In **Build → Hosting**, set it up if you plan to host on Firebase.
   - In **Project Settings → General → Your apps**, add a **Web app** and copy the `firebaseConfig` snippet.

3. **Wire Firebase into the HTML**

   Open each HTML file (`user.html`, `admin 1.html`, `admin 2.html`, etc.) and locate:

   ```js
   const firebaseConfig = {
     apiKey: "YOUR_API_KEY_HERE",
     authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
     databaseURL: "https://YOUR_PROJECT_ID.firebaseio.com",
     projectId: "YOUR_PROJECT_ID",
     storageBucket: "YOUR_PROJECT_ID.appspot.com",
     messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
     appId: "YOUR_APP_ID"
   };
   ```

   Replace every placeholder with the values from your Firebase web app.

4. **Apply the security rules**

   - Open `firebase realtime rules.txt` from this project.
   - In Firebase Console → **Realtime Database → Rules**, paste the contents and click **Publish**.

---

## Running Locally

Because the app talks to Firebase over HTTPS, open it via a local server rather than `file://`:

```bash
# Python 3
python3 -m http.server 8080

# or Node
npx serve .
```

Then visit `http://localhost:8080/user.html` in your browser.

> Opening the HTML file directly (`file://`) can still work for basic UI preview, but Firebase Auth and some API calls require an http(s) origin.

---

## Project Structure

```
.
├── user.html                  # Main user-facing app
├── admin 1.html                # Admin dashboard (variant 1)
├── admin 2.html                # Admin dashboard (variant 2)
├── giveaway admin.html         # Giveaway management
├── giveaway user.html          # Giveaway entry page
├── only theme changer.html     # Live theme switcher
├── theme colour code.txt       # 500+ theme color palettes
├── firebase realtime rules.txt # Realtime Database security rules
├── instructions or support.txt # Original setup & deployment guide
├── README.md
└── preview/preview.png
```

---

## Deployment

### Option A — InfinityFree (free static host)
1. Create an account on https://www.infinityfree.com.
2. Open the File Manager.
3. Upload all HTML files and assets into the `htdocs` folder.
4. Your app goes live on a public URL.

### Option B — Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### Option C — Android App via HopWeb
1. Open HopWeb and create a new project.
2. Import the HTML file (set `user.html` as the homepage).
3. Preview, then Publish with your app details.
4. Tap the checkmark to finalize the APK.

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| **App loads but no data appears** | Realtime Database rules not published, or `firebaseConfig` still has placeholder values. |
| **Login fails** | Ensure Email/Password auth is enabled in Firebase Authentication. |
| **`firebase is not defined`** | Make sure the Firebase SDK `<script>` tags loaded (check network/CDN access). |
| **Rules rejected by validator** | Paste the exact contents of `firebase realtime rules.txt` without modification. |
| **White screen on `file://`** | Serve via `python3 -m http.server` instead of double-clicking the file. |
| **Theme switcher not persisting** | Browser blocked localStorage — allow storage for the origin. |
| **Images missing** | The `images/` folder referenced in HTML (e.g. `images/logoapp.png`) must exist alongside the HTML files. |

---

## Credits

Made by **Sudais Alam**.
