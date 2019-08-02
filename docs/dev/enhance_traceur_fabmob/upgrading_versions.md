# Upgrading versions
___

We are currently using [Cordova 8.1.2](https://cordova.apache.org/news/2018/10/07/cordova-cli-8.1.2.html) with `cordova-android 6.4.0` and `cordova-ios 4.5.5`. In November 2019, if we want to update the app, we will be forced to pass the target API to level 28+ ([Meet Google Play's target API level requirement](https://developer.android.com/distribute/best-practices/develop/target-sdk)). However, if we want to keep using `Cordova 8.1.2`, we will not be able to use the latest Android SDK since the version 8.1.2 only support `cordova-android` up to 7.X.X which only support Android API-Levels from 19 to 27 ([Android - Requirements and Support](https://cordova.apache.org/docs/en/9.x/guide/platforms/android/index.html)).

## Upgrading Android 

One of the main issue that we will encounter when we are going to upgrade our Android version is the structure changes. Cordova had to adapt the new structure used by Android Studio. The sources will now be into the directory `app/src/main/java`. So it will be necessary to refractor each `platforms/android/src` by `platforms/android/app/src/main/java` (same for `assets/` and `res/`).

Moreover, as we are using a Foreground service (with the plugin `e-mission-data-collection`), we also have to add a new permission: `android.permission.FOREGROUND_SERVICE` to the Android Manifest ([Behavior changes: apps targeting API level 28+](https://developer.android.com/about/versions/pie/android-9.0-changes-28)).

## iOS - Sign in with Apple

There is no Cordova plugin which provides **Sign In with Apple** right now. However, as we are using a WebView, we can use the [**Sign In with Apple JS framework**](https://developer.apple.com/documentation/signinwithapplejs) but there are some UI guidelines to respect: [Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/sign-in-with-apple/overview/). Apple also "asked" to make **Sign In with Apple** the first option when we offer different authentication options. 