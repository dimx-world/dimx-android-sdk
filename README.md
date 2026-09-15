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
