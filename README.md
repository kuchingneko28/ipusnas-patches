# 👋🧩 iPusnas Patches

Morphe patches for the **iPusnas** digital library app
(`mam.reader.ipusnas`, v2.1.4).

## ❓ About

A set of patches that improve privacy and add a "Save to Downloads" feature
to the iPusnas e-reader app. These patches are applied with
[Morphe](https://morphe.software) and are based on the manual smali modding
pipeline documented in `research/docs/modifications.md`.

## 🩹 Patches list

<!-- PATCHES_START EXPANDED -->

- **Save book to Downloads** — Adds a "Simpan ke Unduhan" entry to the book
  detail overflow menu. Tapping it runs the app's own download + decrypt flow
  and copies the readable PDF/EPUB into the public Downloads folder via
  MediaStore (works on Android 10+ scoped storage, no permissions needed).
- **Remove screenshot restriction** — Disables the `FLAG_SECURE` window flag in
  the PDF (Radaee `PDFViewAct`) and EPUB (FolioReader `FolioActivity`) readers,
  so screenshots and screen recordings of books work normally.

- **Disable Firebase Analytics and FCM** — Removes Firebase Analytics
  collection and Firebase Cloud Messaging (push notification) components from
  the manifest, and neutralizes the in-app FCM token registration.
- **Neuter Telegram security breach reporter** — Stops the app from reporting
  security breaches or APK integrity failures to the developers' Telegram
  channel.
- **Remove certificate pinning** — Removes the hard-coded OkHttp certificate
  pins and the SSL pinning interceptor so the app trusts system and user CAs.

<!-- PATCHES_END -->

## 🚀 Getting development started

1. [Setup](https://github.com/MorpheApp/morphe-documentation/blob/main/docs/morphe-development/README.md)
   your development environment, including a GitHub PAT with `read:packages`
   scope (used to resolve the `app.morphe.patches` Gradle plugin). Add it to
   `~/.gradle/gradle.properties` as `gpr.user` / `gpr.key` or export
   `GITHUB_ACTOR` / `GITHUB_TOKEN`. An Android SDK is also required
   (`local.properties` with `sdk.dir=...`).
2. Build the patch bundle:
   ```bash
   ./gradlew buildAndroid
   # Output: patches/build/libs/patches-*.mpp
   ```
3. Apply it with [Morphe-Desktop](https://github.com/MorpheApp/morphe-desktop)
   like any other patch bundle.

### 🛠️ Verifying against a real APK

A small harness applies every patch to a real APK and reports whether each
fingerprint matched:

```bash
./gradlew :patches:verifyPatches --args="path/to/base.apk build/verify-output"
```

## 📜 License

GPLv3 — see [LICENSE](LICENSE).
