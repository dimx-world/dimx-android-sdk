# dimx-android-sdk

[![](https://jitpack.io/v/dimx-world/dimx-android-sdk.svg)](https://jitpack.io/#dimx-world/dimx-android-sdk)

Android SDK for integrating with the **DimensionX**.

---

## 🔧 Installation

### Step 1. Add the JitPack repository to your settings.gradle

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        google()
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}
```

### Step 2. Add the dependency to your app-level build.gradle

```gradle
dependencies {
    implementation 'com.github.dimx-world:dimx-android-sdk:Tag'
}
```

> 💡 Replace **Tag** with the latest release version.  
> You can check the latest version badge above or visit [JitPack.io](https://jitpack.io/#dimx-world/dimx-android-sdk).

## When a build must update

Every connection the SDK opens begins by telling the platform what this
build is - app, version, version code and the protocol it speaks - and the
platform answers with its verdict on the build, if it has one. Nothing is
sent about the holder, and this happens whether or not telemetry is on.
Nothing waits for it either; the verdict arrives at the one handler the app sets:

```java
Context.inst().setClientUpdateHandler(update -> {
    if (update.isRequired()) { /* stop and say so */ }
    else if (update.shouldPrompt()) { /* a nudge, at your own pace */ update.markPrompted(); }
});
```

`required` is a rare case: the platform has moved past this build. The SDK
refuses every request from then on (`E1003`), and `showARScreen` opens
nothing - it runs the handler set with
`Context.inst().setUpdateRequiredHandler(...)` when the app set one, and
shows its own dialog with the store link when it did not.
`Context.updateStatus()` says where the build stands at any time - `Unknown`
until the platform has answered on this run (offline, or not yet connected),
`None`, `Advisory`, `Required` - `Context.clientUpdate()` is the verdict
itself, or null, and `Context.requireCurrentBuild()` throws
`ClientUpdate.UpdateRequiredException` for code that would rather catch.

## Telemetry

The engine can report to the DimensionX platform: a marker when a session
ends in a crash, its errors, session and frame-rate records - and, when the
platform's operators switch one install to verbose for a while, its full log
stream, ending on its own. It is off unless the app turns it on:

```java
AppConfig config = new AppConfig();
config.setTelemetryEnabled(true, "android-sdk");
Context.initializeWithConfig(getApplicationContext(), config);
```

What is sent is tied to an install id the SDK mints (never a device
identifier) and the signed-in DimensionX account. Nothing is sent while it
is off; the app's own crash reporter is unaffected.

## The Live View cover

While the camera starts - a second or two on some phones - the AR screen
shows the engine's Live View cover, the DimensionX animation on white, in
place of a black surface, and the screen that opened Live View cross-fades
into it. The cover fades away with the camera's first frame. Nothing to
configure: the cover ships with the engine.
