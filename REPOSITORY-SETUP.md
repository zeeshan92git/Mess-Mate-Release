# Distribution repository setup

Repository: **zeeshan92git/Mess-Mate-Release** (public downloads/documentation only).
The MessMate source repository remains private. Never copy its Git history, `.env`,
keystore, credentials, source tree or student backups into this repository.

Suggested GitHub About description:

> Android releases for MessMate, an independent offline-first mess tracker for University of the Punjab hostel residents. Downloads, update notes and privacy information.

Suggested topics: `android`, `messmate`, `student-utility`, `hostel`, `meal-tracker`,
`offline-first`, `university-of-the-punjab`, `android-apk`.

## Initial repository

The repository was anonymously reachable as public during preparation, with no
latest stable release. No creation or visibility change is needed. If setting up
a replacement manually, create only the intended public distribution repository;
do not make the source repository public. Upload this documentation and actual
reviewed screenshots only. Configure About/topics manually; they were not changed.
Complete privacy/contact placeholders before inviting students.

## First APK

Build/test the app from its private source checkout after explicit approval.
Preserve `com.messmate.app`, the original signing key and a higher versionCode.
Inspect actual APK versionName/code/minimum Android API/architectures and signing
certificate. Never infer these from file size. A universal APK must actually
contain the supported architectures. Verify an in-place upgrade on a phone without
uninstalling or clearing storage.

Use a unique stable tag `v<APK versionName>` and filename
`MessMate-<APK versionName>-<actual versionCode>-universal.apk`.
For example, **only if** the resulting APK is version 1.0.2/code 5, use
`v1.0.2` and `MessMate-1.0.2-5-universal.apk`. Never reuse a published tag for a
different binary. Keep APKs in release Assets, not Git commits.

## Upload and metadata

Use GitHub Releases → Draft a new release → choose/create the version tag →
attach the inspected APK. Complete RELEASE-TEMPLATE.md using the APK facts.
The exact eventual asset URL must be:

`https://github.com/zeeshan92git/Mess-Mate-Release/releases/download/v<VERSION>/MessMate-<VERSION>-<CODE>-universal.apk`

No spaces, query parameters, alternate hosts or alternate filenames are accepted.
The app reads exactly one `messmate-release` JSON fence in the release body.
The adjacent JSON template has the same fields; by itself it is not a release.
`minimumSupportedVersionCode` is a genuine support-policy minimum, not a prompt
to block every older app. An ordinary first release need not be mandatory.

After reviewing the draft and physical upgrade tests, publish a non-prerelease
release and explicitly mark it latest. A public-beta label in the title is fine;
the app's stable latest checker intentionally ignores GitHub prereleases/drafts.

## Obtain the exact public URL and verify without login

These commands are read-only after a release has actually been published:

```powershell
$repo = 'zeeshan92git/Mess-Mate-Release'
$release = Invoke-RestMethod -Uri "https://api.github.com/repos/$repo/releases/latest"
$release | Select-Object tag_name,draft,prerelease,published_at,html_url
$apks = @($release.assets | Where-Object { $_.name -like 'MessMate-*-universal.apk' -and $_.state -eq 'uploaded' })
if ($apks.Count -ne 1) { throw 'Expected exactly one published universal APK' }
$apkUrl = $apks[0].browser_download_url
if ($apkUrl -notmatch '^https://github\.com/zeeshan92git/Mess-Mate-Release/releases/download/v[0-9]+\.[0-9]+\.[0-9]+/MessMate-[0-9]+\.[0-9]+\.[0-9]+-[0-9]+-universal\.apk$') { throw 'Unexpected APK URL' }
$apkUrl
Invoke-WebRequest -Method Head -Uri $apkUrl
```

Copy the returned URL, not a signed redirect URL from the browser. Confirm it
matches the tag, filename and metadata exactly. The app checks those equalities
strictly, then verifies the asset is still publicly reachable before opening the
canonical release page. Test that page and APK in a private/incognito browser
without a GitHub login. Do not use an authenticated API success as proof of public
access. No update notice should appear until a verified newer compatible APK exists.

The latest API returning 404 before the first stable release is expected. It must
not be displayed as “You're up to date” after a failed check.
