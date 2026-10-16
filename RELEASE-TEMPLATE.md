# MessMate VERSION — Android beta

## Changes

- Replace with the actual tested changes.

## Install / update

Download `MessMate-VERSION-CODE-universal.apk` from Assets. Install over the
existing MessMate app. **Do not uninstall or clear data.** Save a durable backup
before changing phones or testing upgrades. Android requirement: read the actual
minimum API from this APK. Record its signing certificate and SHA-256 before upload.

## Known limitations

- Replace with verified device limitations.
- Independent student utility; not an official University of the Punjab application.

## Release metadata

Fill every placeholder from the inspected signed APK and actual tested support
policy. Keep exactly one fenced block. The template is intentionally invalid until
completed; never publish code 0, guessed minimum API or a fake download URL.

```messmate-release
{
  "schemaVersion": 1,
  "platform": "android",
  "distribution": "public",
  "androidPackage": "com.messmate.app",
  "latestVersion": "REPLACE_WITH_APK_VERSION_NAME",
  "latestVersionCode": 0,
  "minimumSupportedVersionCode": 0,
  "releaseNotes": "REPLACE_WITH_TESTED_CHANGES",
  "downloadUrl": "REPLACE_WITH_PUBLISHED_ASSET_BROWSER_DOWNLOAD_URL",
  "mandatoryUpdate": false,
  "minimumAndroidApi": 0,
  "universalApk": true
}
```
