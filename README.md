# Dhairya GPT for Android

The Android app for [Dhairya GPT](https://dhairyagpt.vercel.app).

It is a Trusted Web Activity (TWA) generated with [PWABuilder](https://www.pwabuilder.com). The app opens the live website, so there is no web code in this repository. The website and its API live in a separate repo:

**Web app:** https://github.com/Dhairys/dhairyagpt

Any change to the website shows up in the Android app automatically. You only need to rebuild the Android app to change its name, icon, version or package settings.

## Contents

```text
dhairyagpt-android/
├── app/                      # Android project from PWABuilder
├── .well-known/
│   └── assetlinks.json       # copy of the file to host on the website
├── .gitignore
└── README.md
```

## Build

1. Open https://www.pwabuilder.com and enter `https://dhairyagpt.vercel.app`.
2. Choose **Package for stores → Android**.
3. Set the package ID (for example `app.vercel.dhairyagpt`), name and version.
4. Generate a new signing key and download the zip.
5. Unzip it into this repository (keep the signing key out of git).

## Install

Download the latest `.apk` from the **Releases** page and open it on your phone. Allow "install unknown apps" if Android asks.

## Hide the browser address bar

Android hides the address bar only if the website proves it belongs to this app:

1. Put the `assetlinks.json` file from the PWABuilder zip in the **web** repo at `.well-known/assetlinks.json`.
2. Deploy the website.
3. Reinstall the app.

## Security

Never commit the signing key (`.keystore`, `.jks`) or its password. Losing it means you cannot update the app under the same identity. Store a backup somewhere private, like a password manager.

## Disclaimer

Dhairya GPT is a personal AI project. AI responses can contain mistakes, so verify important information. See the [Terms & Conditions](https://dhairyagpt.vercel.app/terms.html).

## Author

Built by Dhairya.
