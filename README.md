# Saudi VAT Invoice Reader

Updated Flutter source for a Saudi e-invoice QR reader.

## What this version includes

- Safer TLV Base64 decoder with length checks.
- Required ZATCA QR tags validation for tags 1 to 5.
- Phase 1 / Phase 2 display based on tags 6 to 9.
- English / Arabic manual language switch.
- RTL support through Flutter localization.
- Copy all invoice details.
- Share invoice details.
- Device scan history using `shared_preferences`.
- Swipe-to-delete history item and clear all history.
- Camera guidance message.
- AdMob banner integration using Google test IDs.
- Clear disclaimer: the app reads QR data only and does not verify invoice authenticity with ZATCA.

## Important release note

This app reads invoice QR data. It does not cryptographically verify the Phase 2 invoice hash, signature, public key, or ZATCA stamp. Do not market it as a ZATCA verification app unless you add full signature validation and official compliance checks.

Recommended app name:

```text
Saudi VAT Invoice Reader
```

Recommended short description:

```text
Read Saudi e-invoice QR details in Arabic and English.
```

## How to use this source in a full Flutter project

If this ZIP does not include `android/` and `ios/` folders, create a new Flutter project first:

```bash
flutter create saudi_vat_scanner
cd saudi_vat_scanner
```

Then copy these files/folders into the new project:

```bash
# From this updated ZIP source folder
cp pubspec.yaml /path/to/saudi_vat_scanner/pubspec.yaml
cp l10n.yaml /path/to/saudi_vat_scanner/l10n.yaml
cp -r lib /path/to/saudi_vat_scanner/lib
```

Then run:

```bash
flutter clean
flutter pub get
flutter gen-l10n
flutter run
```

## Android permissions and AdMob setup

Add camera permission inside `android/app/src/main/AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.CAMERA" />
```

Inside the `<application>` tag, add your real AdMob app ID before release:

```xml
<meta-data
    android:name="com.google.android.gms.ads.APPLICATION_ID"
    android:value="ca-app-pub-XXXXXXXXXXXXXXXX~YYYYYYYYYY" />
```

A sample manifest snippet is included in `config_snippets/android/AndroidManifest_snippet.xml`.

## iOS permissions and AdMob setup

Add this to `ios/Runner/Info.plist`:

```xml
<key>NSCameraUsageDescription</key>
<string>Camera access is required to scan invoice QR codes.</string>
<key>GADApplicationIdentifier</key>
<string>ca-app-pub-XXXXXXXXXXXXXXXX~YYYYYYYYYY</string>
```

A sample plist snippet is included in `config_snippets/ios/InfoPlist_snippet.xml`.

## Replace AdMob test IDs before release

In `lib/main.dart`, replace:

```dart
ca-app-pub-3940256099942544/6300978111
ca-app-pub-3940256099942544/2934735716
```

with your real Android and iOS banner ad unit IDs.

## Suggested next improvements

- Add app icon and splash screen.
- Add privacy policy URL in Play Console.
- Add invoice export to PDF or Excel.
- Add VAT number format warning.
- Add optional Pro version without ads.
- Add full Phase 2 cryptographic validation only if you are ready to implement and maintain compliance logic.
