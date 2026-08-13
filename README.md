# Task Manager (Android)

A phone-native take on Windows Task Manager: live RAM / storage / battery / CPU-core
stats up top, and a scrollable list of every installed app below, sorted by size or
name, with quick access to Force Stop and Uninstall for each.

## How to build it

1. Install **Android Studio** (free, from developer.android.com).
2. Choose **File → Open**, and select this `TaskManagerApp` folder.
3. Let Gradle sync (first time may take a few minutes — it downloads dependencies).
4. Plug in your phone via USB with **USB debugging** enabled (Settings → About
   Phone → tap "Build number" 7 times → Developer Options → USB debugging), or use
   an emulator.
5. Click the green **Run ▶** button. The app installs and launches on your device.

You can also build a signed APK yourself via **Build → Generate Signed Bundle / APK**
if you want an installable file to share or sideload.

## Why "Force Stop" and "Uninstall" work the way they do

Android intentionally does not let one ordinary app kill another app's process or
force-stop it directly — that capability was removed in Android 5.0 specifically to
stop apps from messing with each other. There's no permission a regular
(non-system) app can request to get it back.

So the app is honest about this instead of faking it:

- **Force Stop** jumps straight to that app's system "App info" screen, with the
  real Force Stop button one tap away.
- **Uninstall** triggers Android's real uninstall confirmation dialog — this one
  *does* work directly, no extra hop needed.

## About the "Usage Access" prompt on first launch

To show accurate per-app storage sizes (like Windows Task Manager's "Disk" column),
Android requires a special permission that can only be granted manually in
Settings — it can't be requested via a normal popup. The app will send you there
once on first launch. If you skip it, everything still works, just without size
numbers (they'll show as 0 MB).

## What's included

- `MainActivity.kt` — reads RAM/storage/battery/CPU stats and builds the app list
- `AppListAdapter.kt` — RecyclerView adapter for the app rows
- `AppInfo.kt` — simple data model per app
- Dark theme matching Task Manager's look, via `colors.xml` / `themes.xml`
