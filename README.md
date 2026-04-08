# AdCloser — Automatic Ad Skip for Android

AdCloser is a native Android app that uses the **Accessibility Service** to automatically detect and tap ad close/skip buttons (X, Close, Fermer, Skip, Passer, etc.) — no root required.

---

## How to get the APK (no Android Studio needed)

### Step 1 — Create a GitHub repository

1. Go to [github.com](https://github.com) and sign in
2. Click the **+** icon → **New repository**
3. Name it `AdCloser`, set it to **Public** or **Private**
4. Click **Create repository**

### Step 2 — Upload these files

1. On your new empty repository page, click **"uploading an existing file"**
2. Drag and drop the **entire `android-adcloser` folder** (or all its contents)
3. Make sure the folder structure is preserved — especially `.github/workflows/build.yml`
4. Click **Commit changes**

### Step 3 — Wait for the build (~5 minutes)

1. Go to the **Actions** tab in your repository
2. You'll see a workflow called **"Build AdCloser APK"** running
3. Wait for the green checkmark ✓

### Step 4 — Download your APK

1. Click on the completed workflow run
2. Scroll down to **Artifacts**
3. Download **AdCloser-debug-apk** — this is your APK file!

---

## Installing the APK on your Android phone

1. Transfer the `.apk` file to your phone (email, Google Drive, USB, etc.)
2. On your phone: **Settings → Security → Install unknown apps** → allow your file manager or browser
3. Open the APK file and tap **Install**
4. Open **AdCloser** from your app drawer

---

## Enabling the Accessibility Service

The auto-tap won't work until you activate the service:

1. Open **AdCloser**
2. Tap **"Enable Service →"**
3. Android will open **Accessibility Settings**
4. Find **"AdCloser – Auto Ad Skip"** in the list
5. Toggle it **ON** and confirm the permission dialog
6. Go back to AdCloser — the status should now say **"ACTIVE ✓"**

---

## Adding custom patterns

If the app doesn't close a specific ad, you can add its button text:

1. Open AdCloser → **Configure Patterns**
2. Type the button text you see (e.g. "Continuer", "Regarder")
3. Tap **ADD**
4. The new pattern is active immediately — no restart needed

To remove a custom pattern: **long-press** it in the list.

---

## How it works (technical)

- Listens for `TYPE_WINDOW_STATE_CHANGED` and `TYPE_WINDOW_CONTENT_CHANGED` events
- Traverses the full UI node tree of every active window
- Matches nodes by: **text**, **content description**, or **resource ID**
- Waits a **random 500–1500ms** before clicking (mimics human behavior)
- Taps at a **randomised position** within the button bounds
- **Debounce**: minimum 2 seconds between any two auto-clicks (prevents loops)
- Falls back to `dispatchGesture` for non-clickable nodes

---

## Supported ad SDKs (resource ID matching)

AdMob, IronSource, AppLovin/MAX, Unity Ads, Vungle, MoPub, and more — matched via their close-button view IDs.

---

## Built-in patterns

`x`, `×`, `close`, `fermer`, `skip`, `passer`, `ignorer`, `dismiss`, `skip ad`, `fermer pub`, `passer l'annonce`, and more.
