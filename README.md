# Daily Weight Tracker — CS 360 Project Three

A complete, production-ready Android app in Java. Includes login/registration,
SQLite persistence, a RecyclerView grid of weight entries, full CRUD, and a
runtime SMS permission flow that sends a congratulatory text when the user
reaches their goal weight.

## Project structure

```
WeightTracker/
├── build.gradle
├── settings.gradle
├── gradle.properties
└── app/
    ├── build.gradle
    ├── proguard-rules.pro
    └── src/main/
        ├── AndroidManifest.xml
        ├── java/com/example/weighttracker/
        │   ├── data/DatabaseHelper.java
        │   ├── model/User.java
        │   ├── model/WeightEntry.java
        │   └── ui/
        │       ├── LoginActivity.java
        │       ├── MainActivity.java
        │       ├── SettingsActivity.java
        │       ├── WeightAdapter.java
        │       └── WeightEntryActivity.java
        └── res/
            ├── layout/
            │   ├── activity_login.xml
            │   ├── activity_main.xml
            │   ├── activity_settings.xml
            │   ├── activity_weight_entry.xml
            │   └── item_weight.xml
            ├── menu/menu_main.xml
            └── values/
                ├── colors.xml
                ├── strings.xml
                └── themes.xml
```

## How to run (step by step)

1. Open Android Studio (Hedgehog 2023.1.1 or newer recommended).
2. `File → Open…` and pick the `WeightTracker` folder.
3. When prompted, let Android Studio install the Gradle wrapper and SDKs
   (compileSdk 34, minSdk 24).
4. Wait for Gradle sync to finish. It will download AppCompat, Material,
   RecyclerView, CardView, and CoordinatorLayout automatically.
5. Create or start an emulator (API 24+) **or** plug in a physical device
   with USB debugging enabled.
6. Click the green ▶ Run button. The app installs and launches `LoginActivity`.

## Using the app

1. **Register** — enter a username + password (4+ chars) and tap
   *Create New Account*.
2. **Log in** — enter those credentials and tap *Log In*.
3. **Add entry** — tap the **+** FAB, enter a weight, pick a date, tap *Save*.
4. **Edit** — tap any card in the grid.
5. **Delete** — long-press any card, or open it and tap *Delete Entry*.
6. **Set goal** — menu (⋮) → *Set Goal*. Enter target weight.
7. **Goal reached** — when your newest logged weight ≤ goal, the app sends
   a celebratory SMS if permission was granted, otherwise shows an in-app
   message.
8. **Log out** — menu (⋮) → *Log Out*.

## SMS permission

- On first launch of `MainActivity` the app requests `SEND_SMS`.
- If **granted**, goal-reached notifications fire as an SMS (in the default
  emulator setup it sends to `5555215554` so you can see it in the emulator's
  other console — change this number in `MainActivity.notifyGoalReached` if
  you want to text a real phone).
- If **denied**, the app works fully; goal alerts just show as a Toast.

## Notes

- Database file: `weight_tracker.db` (managed by `DatabaseHelper`).
- Passwords are stored in plain text for simplicity — this is a classroom
  project. In production you would hash + salt them.
- The grid uses a 2-column `GridLayoutManager` on a `RecyclerView`.
