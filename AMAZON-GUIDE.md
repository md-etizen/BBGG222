# BillBubbles for the Amazon Appstore

Amazon's Appstore now only serves Fire tablets and Fire TV (it closed on regular Android phones on August 20, 2025).
Amazon wants an Android app file (`.apk`). This project builds one from the same BillBubbles page you already have, so it has
every feature (bills, calendar, repeats, tips, insights, themes, reminders banner, privacy policy).

I could not build or run this on my side (no Android tools here), so the first cloud build is the real test.

## Step 1: Put it on GitHub
1. Make a new **public** repository (for example `billbubbles-android`) so it does not mix with your iPhone project.
2. Upload everything from this folder (drag the contents in, keep the folders). The hidden `.github` folder must come too.
   If dragging skips it: Add file > Create new file, type `.github/workflows/android.yml`, and paste that file's text.
3. Your app ID is `io.github.mdetizen.billbubbles`. It can never change after you publish. To use another, edit `APP_ORG`
   near the top of `.github/workflows/android.yml` before the first build.

## Step 2: Signing key (before Amazon)
Use the four secrets from `ANDROID-SIGNING-SECRETS.txt` that I gave you earlier (Settings > Secrets and variables >
Actions > New repository secret): `ANDROID_KEYSTORE_PASSWORD`, `ANDROID_KEY_PASSWORD`, `ANDROID_KEY_ALIAS`,
`ANDROID_KEYSTORE_BASE64`. Without them the build still works but uses a throwaway test key, which is fine for trying it out
but not for publishing.

## Step 3: Build
1. Open the **Actions** tab, choose **Build Android app for Amazon Appstore**, and wait for the green check
   (about 5 minutes). If it is red, open the run, click **build**, expand the red step and send me the text.
2. At the bottom of the run page, download **BillBubbles-android-apk**. Unzip it: `app-release.apk` is your file.
3. Every build raises the version number automatically, which Amazon requires for each new upload.

## Step 4: Try it
Copy the `.apk` to a phone or Fire tablet and open it to test (you may need to allow installs from your files app).
Check: add a bill, tap a bill's delete X and confirm, add tips, Backup > Save backup file, Style > Bill reminders.

## Step 5: Amazon Appstore
1. Sign up at **developer.amazon.com** and open the Appstore section (check there for any fee and the current rules).
2. Add a new app for Android / Fire tablets and upload `app-release.apk`.
3. Fill in the listing from `STORE-LISTING-AMAZON.md`. Icons are in `store/`, screenshots in `store/screenshots/`
   (1280 x 800; if the console wants a different size, tell me which).
4. Privacy policy: put `docs/privacy-policy.html` online (GitHub repo > Settings > Pages > main branch, /docs folder), fill in your
   name and email at its bottom first, and paste the link into the console.
5. Answer the content questions: no ads, no purchases, no sign-in, no special permissions, all content-rating answers No.
6. Submit for review.

## Good to know
- The app asks for no Android permissions. Reminders show as a banner at the top of the page when the app is open
  (Android notifications while the app is closed are not in this version).
- The page is bundled inside the app, so it works with no internet.
- When BillBubbles gains features, I update `app/src/main/assets/index.html`, you upload it, and run the build again.
