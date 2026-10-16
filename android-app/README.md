# CJ Fabrications Android

This Android client opens the production CJ Fabrications web app at
https://parkzone.in/cjfabrication/ in a hardened WebView. The web application
remains the source of truth for the catalogue, customer RFQs, vendor login,
quotation handling and order workflows.

## Build locally

Requirements: JDK 17, Android SDK platform 35, Android Build Tools 35, and
Gradle 8.11.1 or compatible.

From this directory:

```bash
gradle --version
gradle --no-daemon :app:assembleDebug
```

APK output:
`app/build/outputs/apk/debug/app-debug.apk`

For a release build, configure signing through environment variables or a
private keystore outside the repository. Never commit signing material.

## Security model

- The app requires HTTPS and never ignores TLS certificate errors.
- Mixed content, file URL access and third-party cookies are disabled.
- Only parkzone.in HTTPS URLs remain inside the WebView; WhatsApp, tel, mailto
  and other external schemes are handed to Android.
- File selection is user initiated. Server-side upload validation and access
  control remain mandatory.
- The Android app does not contain database credentials, Supabase service-role
  keys or backend secrets.
- Anonymous RFQ access is enforced by the backend; a public ID alone must not
  grant access to sensitive data.

## Scope and limitation

This first Android build reuses the live web app instead of duplicating its
business logic in native Android. A network connection is required. The
availability of a feature in the app depends on the production web app and API.
Push notifications, offline RFQ submission, and native deep-link routing are
not included in this initial version.
