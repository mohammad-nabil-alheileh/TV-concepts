# Android TV Manifest Requirements

The `AndroidManifest.xml` file tells Android what your app is and what it needs. On TV, Google Play and the Android TV launcher read the manifest to decide whether your app is a TV app. They use it to decide whether to show it on the home screen and whether to list it for TV devices.

## The Key Pieces

| # | Requirement | Why it matters |
|---|---|---|
| 1 | Leanback launcher intent | Puts your app on the Android TV home screen. A mobile-only app doesn't have it, so it never appears. |
| 2 | Touchscreen not required | TVs have no touchscreen. If you don't say so, Play assumes you need one and hides your app from TV devices. |
| 3 | Leanback feature | Declares that the app supports the TV interface. |
| 4 | TV banner | The 320×180 image shown in the launcher row. Without it, your app can fail certification or show a blank tile. |
| 5 | Optional hardware features | Camera, microphone, GPS, telephony, and Bluetooth are often missing on TVs. If you require any of them, Play excludes your app from those devices. |

## 1. Leanback Launcher Intent

Add this to your main activity:

```xml
<activity android:name=".MainActivity" android:exported="true">
    <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LEANBACK_LAUNCHER" />
    </intent-filter>
</activity>
```

## 2. Touchscreen Not Required

```xml
<uses-feature android:name="android.hardware.touchscreen" android:required="false" />
```

## 3. Leanback Feature

```xml
<uses-feature android:name="android.software.leanback" android:required="false" />
```

- Use `android:required="true"` for a TV-only app.
- Use `android:required="false"` if the same APK also targets phones.

## 4. TV Banner

```xml
<application android:banner="@drawable/tv_banner" ...>
```

## 5. Optional Hardware Features

Set each one to `required="false"`:

```xml
<uses-feature android:name="android.hardware.camera" android:required="false" />
```

Apply the same pattern to microphone, GPS, telephony, and Bluetooth features.
