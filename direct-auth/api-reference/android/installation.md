# Installation

Torus Direct Web Sdk project uses [jitpack](https://jitpack.io/#org.torusresearch/torus-direct-android-sdk) for release management. This guide will cover some important topics for getting started with Android APIs and to make the most of Magic's features.

Typically your application should depend on release versions of torus-direct-android-sdk, but you may also use snapshot dependencies for early access to features and fixes, refer to the Snapshot Dependencies section.

Add the relevant dependency to your project:

```groovy
repositories {
        maven { url "https://jitpack.io" }
}
dependencies {
   implementation 'org.torusresearch:torus-direct-android-sdk:1.1.1'
}
```

### Import



