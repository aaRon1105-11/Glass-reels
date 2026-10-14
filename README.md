# GlassReels
Requirements
Minimum SDK: Android 6.0 (API Level 23)
Target SDK: Android 15 (API Level 35)
Compile SDK: API Level 35
Build System: Gradle 8.2+ with Android Gradle Plugin 8.1+
JDK: Java 17
GlassReels is an ultra-lightweight, high-performance local video viewer and gallery application for Android. Designed to mimic modern short-form video feeds, it delivers smooth vertical scrolling and gesture-driven media exploration with a total APK footprint of under 35 KB.

Built entirely using pure Java and standard Android Framework APIs, the project deliberately avoids external dependencies, AndroidX, and Jetpack libraries.

---

## Key Highlights

* **Microscopic Binary Size:** Full debug APK weighs approximately 32.6 KB.
* **Zero Dependencies:** Pure Android SDK implementation. No AndroidX, no Jetpack, and no third-party libraries.
* **Low Memory Footprint:** Custom lifecycle handling actively pauses and releases off-screen media instances to prevent memory accumulation.
* **Hardware-Accelerated Playback:** Custom matrix calculations ensure proper aspect-ratio fitting and cropping on TextureView without distortion.

---

## Features

* **Physics-Based Vertical Pager:** A custom-built ViewGroup using Android's native `Scroller` and `VelocityTracker` for authentic, tactile vertical snapping.
* **Media Explorer Grid:** A dense 4-column edge-to-edge media explorer with asynchronous background thumbnail loading.
* **Hidden Gesture Navigation:**
  * **Swipe Right:** Launches the system Storage Access Framework (SAF) folder picker (`ACTION_OPEN_DOCUMENT_TREE`) to scope playback to any chosen folder.
  * **Swipe Left:** Reveals a translucent metadata overlay displaying exact file creation date, time, and resolution.
* **Playback Controls:** Minimalist, translucent control bar with centered vector play/pause indicators inspired by native video players.
* **Local Video Ranking:** Built-in star ranking backed by SharedPreferences (`RankStore`), allowing real-time sorting by highest rating, creation date, or random shuffle.

---

## Technical Architecture

* **Custom ViewGroup (`VerticalVideoPager`):** Manages touch interception, touch slop thresholds, velocity tracking, and smooth scroll animations without relying on `ViewPager` or `RecyclerView`.
* **Video Presentation (`VideoPageView`):** Integrates `TextureView` and `MediaPlayer` with dynamic matrix transformation for zero-distortion video scaling across various screen aspect ratios.
* **Storage Access Framework & MediaStore:** Queries local media asynchronously via `ContentResolver` with strict MIME-type filtering (`video/*`) and SAF tree document parsing.
* **Memory Management:** Immediate cleanup of off-screen surfaces and players to guarantee smooth 60 FPS performance on resource-constrained devices.

---

## Project Structure

```text
GlassReels/
├── app/
│   ├── src/
│   │   └── main/
│   │       ├── AndroidManifest.xml
│   │       ├── java/com/glassreels/
│   │       │   ├── MainActivity.java
│   │       │   ├── MediaStoreRepository.java
│   │       │   ├── RankStore.java
│   │       │   ├── VerticalVideoPager.java
│   │       │   ├── VideoItem.java
│   │       │   └── VideoPageView.java
│   │       └── res/
│   │           ├── drawable/
│   │           ├── layout/
│   │           └── values/
│   └── build.gradle
├── gradle/
│   └── wrapper/
├── build.gradle
└── settings.gradle
