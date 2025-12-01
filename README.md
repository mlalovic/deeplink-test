# Deep Link Test Site

Quick setup to test HTTPS deep linking before full DevOps deployment.

## Quick Deploy to GitHub Pages (2 Minutes)

### Step 1: Create GitHub Repository

1. Go to https://github.com/new
2. Name: `diana-conforti-deeplink-test` (or any name)
3. Set to **Public** (required for free GitHub Pages)
4. Click "Create repository"

### Step 2: Push These Files

```bash
cd test-deep-link-site

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial deep link test setup"

# Add your GitHub repo as remote (replace YOUR_USERNAME)
git remote add origin https://github.com/YOUR_USERNAME/diana-conforti-deeplink-test.git

# Push
git branch -M main
git push -u origin main
```

### Step 3: Enable GitHub Pages

1. Go to your repo on GitHub
2. Click **Settings**
3. Click **Pages** (left sidebar)
4. Under "Source", select **main** branch
5. Click **Save**
6. Wait ~1 minute
7. You'll get a URL like: `https://YOUR_USERNAME.github.io/diana-conforti-deeplink-test/`

### Step 4: Update Mobile App Config

Once you have your GitHub Pages URL, you need to add it to the app:

**Edit these files:**

1. `android/app/src/main/AndroidManifest.xml` - Add:
```xml
<data
    android:scheme="https"
    android:host="YOUR_USERNAME.github.io"
    android:pathPrefix="/diana-conforti-deeplink-test/app"/>
```

2. `ios/Runner/Info.plist` - Add to associated domains array in Xcode:
```
applinks:YOUR_USERNAME.github.io
```

3. Rebuild app:
```bash
flutter run
```

### Step 5: Test!

1. Open the GitHub Pages URL on your mobile device
2. Tap one of the buttons
3. App should open and navigate to login with email pre-filled! 🎉

---

## Verification URLs

After deploying, verify files are accessible:

**AASA File (iOS):**
```
https://YOUR_USERNAME.github.io/diana-conforti-deeplink-test/.well-known/apple-app-site-association
```

**Asset Links (Android):**
```
https://YOUR_USERNAME.github.io/diana-conforti-deeplink-test/.well-known/assetlinks.json
```

Both should return JSON (not 404).

---

## Testing Notes

**iOS:**
- Long-press the link → Should show "Open in [App]"
- Tap normally → Opens app directly
- First time might need app reinstall to refresh AASA cache

**Android:**
- Tap link → Prompts "Open with [App]"
- Or opens app directly if already associated

---

## After Testing

Once this works, you know:
- ✅ Your SHA-256 fingerprints are correct
- ✅ Your Team ID is correct
- ✅ The app configuration is correct
- ✅ Deep linking works end-to-end

Then DevOps can deploy the same files to production domains!

---

## Cleanup

When done testing, you can:
- Delete the GitHub repository
- Remove the GitHub Pages domain from your app config
- Keep these files as reference for DevOps


