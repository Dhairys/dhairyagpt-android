# Dhairya GPT for Android

The Android app for [Dhairya GPT](https://dhairyagpt.pages.dev), a free AI chat assistant.

It is a **Trusted Web Activity (TWA)** generated with [PWABuilder](https://www.pwabuilder.com). The app simply opens the live website in a full-screen Chrome window, so there is no web code in this repository. The website and its server code live in a separate repo:

**Web app:** https://github.com/Dhairys/dhairyagpt

Any change to the website shows up in the Android app automatically. You only rebuild the Android app to change its name, icon, version or package settings, or if the website's address changes.

| | |
| --- | --- |
| **Site loaded by the app** | https://dhairyagpt.pages.dev |
| **Package ID** | The one you chose in PWABuilder. Keep it identical for every update |
| **Needs** | Android with Chrome installed, and an internet connection |

## Repository contents

```text
dhairyagpt-android/
├── app/                      # Android project from PWABuilder
├── .well-known/
│   └── assetlinks.json       # copy of the file hosted on the website
├── .gitignore                # blocks signing keys and build files
└── README.md
```

Signed `.apk` files go on the **Releases** page, not in the repo.

## Install (for users)

1. Open the **Releases** page and download `dhairyagpt.apk`.
2. Open the file on your phone.
3. If Android asks, allow **Install unknown apps** for your browser or file manager.
4. If Play Protect shows a warning, tap **Install anyway**. This appears because the app is not from the Play Store.

No download needed: you can also open https://dhairyagpt.pages.dev in Chrome on Android, tap the **⋮** menu, and choose **Install app**.

## Build (for the maintainer)

1. Make sure the website is live and its PWABuilder score has no red errors. The site needs `manifest.json`, a service worker, and the icons `icons/icon-192.png` and `icons/icon-512.png`.
2. Go to https://www.pwabuilder.com, enter `https://dhairyagpt.pages.dev`, and click **Start**.
3. Click **Package For Stores → Android**.
4. Fill in the package ID, app name and version. Use **Create new** for the signing key and enter:

   | Field | Value |
   | --- | --- |
   | Key alias | `dhairyagpt` |
   | Key full name | `Dhairya` |
   | Key organization | `Dhairya GPT` |
   | Key organizational unit | `Personal` |
   | Key country code | `IN` |

5. Download the zip. It contains the signed `.apk`, an `.aab` for Google Play, `signing.keystore`, and `signing-key-info.txt`.
6. Unzip the project into this repo's folder, then upload the `.apk` as a GitHub Release.

> **Download Test Package** gives an *unsigned* APK that will not install. Use **Package For Stores** to get a signed one, or sign the test file with [uber-apk-signer](https://github.com/patrickfav/uber-apk-signer):
> ```bash
> java -jar uber-apk-signer.jar --apks app-release-unsigned.apk
> ```
> Install the file ending in `-aligned-debugSigned.apk`.

## Hide the browser address bar (fullscreen)

Android shows an address bar unless the website proves it belongs to this app:

1. Take `assetlinks.json` from the PWABuilder zip (it holds the package ID and the public fingerprint of your signing key).
2. Put it in the **web repo** at `.well-known/assetlinks.json` and let the site redeploy.
3. Confirm https://dhairyagpt.pages.dev/.well-known/assetlinks.json opens and shows the JSON.
4. Uninstall the app, reinstall the signed APK, and open it with internet on.

The file is public by design. The fingerprint in it must belong to the exact key that signed the APK on your phone, and the package name must match exactly.

## Publish a release

On GitHub open **Releases → Draft a new release**, then:

- **Tag:** type `v1.0.0` and click **Create new tag: v1.0.0 on publish** (typing alone is not enough)
- **Title:** `Dhairya GPT for Android v1.0.0`
- **Attach** the signed `.apk` (rename it `dhairyagpt.apk`)
- **Publish release**

Use `v1.0.1`, `v1.1.0` and so on for later versions. Before building an update, raise the version in PWABuilder, and sign it with the **same** keystore.

## Google Play (optional)

- A Google Play developer account costs a one-time $25.
- Upload the `.aab` file, not the `.apk`.
- Use https://dhairyagpt.pages.dev/privacy.html as the privacy policy URL.
- If you add ads, check AdSense's policy for apps. Google lists Trusted Web Activities among its allowed integration options, but confirm the current rules yourself.

## If the website address changes

The app is tied to the address it was built from. If you move the site (for example from `vercel.app` to `pages.dev`, or to a custom domain):

1. Update the website's `manifest.json`, `sitemap.xml`, `robots.txt` and `.well-known/assetlinks.json`.
2. Rebuild the APK in PWABuilder with the new address, using the **same signing key**.
3. Publish a new release with a higher version number.

A custom domain you own avoids this problem for good.

## Security

**Never commit** the signing key (`.keystore`, `.jks`), `signing-key-info.txt` or its passwords. Anyone who has them can publish apps as you, and losing them means you can't update the app under the same identity. Keep a private backup, such as a password manager or your own cloud drive. The included `.gitignore` blocks these files, but run `git status` before every commit.

## Privacy and terms

- Privacy Policy: https://dhairyagpt.pages.dev/privacy.html
- Terms & Conditions: https://dhairyagpt.pages.dev/terms.html

## Disclaimer

Dhairya GPT is a personal AI project. AI responses can be wrong or biased, so verify anything important.

## Author

Built by Dhairya.
