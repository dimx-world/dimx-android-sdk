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
