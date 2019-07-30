# Installing prerequisites
___

It is possible to use the functionnalities of the **e-mission-server** without having to use the phone app provided by **e-mission**. However, there is some prerequisites.

## Installing and configuring the Cordova environment

Currently, to use **e-mission** Cordova plugins, you must use the version **8.1.2** of [Cordova](https://cordova.apache.org/). You can install it using [npm](https://www.npmjs.com/) by typing the following command in your terminal:

```bash
$ npm install -g cordova@8.1.2
```

After a succesful installation, you will need to create a Cordova project. You can now do it in your terminal with the command below:

```bash
$ cordova create <folder name> <package> <app name>
```

When you will be in your new project folder, you will now be able to add platforms (iOS or/and Android) and plugins to your Cordova project. You can add the platforms by either adding the following lines in your `config.xml` file (between the `<widget>` tag) or typing the command `cordova platforms add`.

```xml
    <engine name="ios" spec="^4.5.5" />
    <engine name="android" spec="^6.4.0" />
```

!!! warning
    For now, it is mandatory to use the 6.4.0 for Android and 4.5.5 for iOS. You can specify them when
    using the command line by adding `@^<version number>` right after the platform.

## Installing e-mission Cordova plugins

There are a total of 11 mandatory plugins to use a phone app in par with an **e-mission** server. The plugins are the following:

- [cordova-plugin-customurlscheme](https://github.com/EddyVerbruggen/Custom-URL-scheme),
- [cordova-plugin-inappbrowser](https://github.com/shankari/cordova-plugin-inappbrowser.git),
- [de.appplant.cordova.plugin.local-notification-ios9-fix](https://github.com/shankari/cordova-plugin-local-notifications.git),
- [edu.berkeley.eecs.emission.cordova.auth](https://github.com/e-mission/cordova-jwt-auth),
- [edu.berkeley.eecs.emission.cordova.comm](https://github.com/e-mission/cordova-server-communication),
- [edu.berkeley.eecs.emission.cordova.datacollection](https://github.com/e-mission/e-mission-data-collection),
- [edu.berkeley.eecs.emission.cordova.serversync](https://github.com/e-mission/cordova-server-sync),
- [edu.berkeley.eecs.emission.cordova.settings](https://github.com/e-mission/cordova-connection-settings),
- [edu.berkeley.eecs.emission.cordova.transitionnotify](https://github.com/e-mission/e-mission-transition-notify),
- [edu.berkeley.eecs.emission.cordova.unifiedlogger](https://github.com/e-mission/cordova-unified-logger),
- [edu.berkeley.eecs.emission.cordova.usercache](https://github.com/e-mission/cordova-usercache).
  
You can find most of them on the GitHub of **e-mission**: https://github.com/e-mission and install them by either typing `cordova plugin add <url of the plugin>` or by adding the following lines in the `config.xml`:

```xml
<plugin name="cordova-plugin-customurlscheme" spec="~4.3.0">
    <variable name="URL_SCHEME" value="emission" />
</plugin>
<plugin name="cordova-plugin-inappbrowser" spec="https://github.com/shankari/cordova-plugin-inappbrowser.git" />
<plugin name="de.appplant.cordova.plugin.local-notification-ios9-fix" spec="https://github.com/shankari/cordova-plugin-local-notifications.git" />
<plugin name="edu.berkeley.eecs.emission.cordova.auth" spec="https://github.com/e-mission/cordova-jwt-auth.git#v1.5.0" />
<plugin name="edu.berkeley.eecs.emission.cordova.comm" spec="https://github.com/e-mission/cordova-server-communication.git#v1.2.1" />
<plugin name="edu.berkeley.eecs.emission.cordova.datacollection" spec="https://github.com/e-mission/e-mission-data-collection.git#v1.3.3">
    <variable name="LOCATION_VERSION" value="11.0.1" />
</plugin>
<plugin name="edu.berkeley.eecs.emission.cordova.serversync" spec="https://github.com/e-mission/cordova-server-sync.git#v1.1.2" />
<plugin name="edu.berkeley.eecs.emission.cordova.settings" spec="https://github.com/e-mission/cordova-connection-settings.git#v1.2.0" />
<plugin name="edu.berkeley.eecs.emission.cordova.transitionnotify" spec="https://github.com/e-mission/e-mission-transition-notify.git#v1.2.0" />
<plugin name="edu.berkeley.eecs.emission.cordova.unifiedlogger" spec="https://github.com/e-mission/cordova-unified-logger.git#v1.3.1" />
<plugin name="edu.berkeley.eecs.emission.cordova.usercache" spec="https://github.com/e-mission/cordova-usercache.git#v1.1.0" />
```

## Connecting your Cordova application to the server

!!! note
    You can find the supported authentication modes in [Configuring authentication](../../../install/configuring_authentication.md) and configuration exemples can be found [there](https://github.com/fabmob/e-mission-phone-fabmob/tree/master/www/json).

To connect to the server, you will need to set the settings by using the function `setSettings(connectionConfig)`of the plugin ConnectionSettings where `connectionConfig` is a JSON object. To achieve that, you can add the following line into the `onDeviceReady` function:

```js
onDeviceReady: function () {
    this.receivedEvent('deviceready');
    window.cordova.plugins.BEMConnectionSettings.setSettings(connectionConfig);
}
```

You can now create a login function and add the following lines to connect your phone app users to the server. 

```js
function login() {
    window.cordova.plugins.BEMJWTAuth.signIn().then(function (userEmail) {
        window.cordova.plugins.BEMServerComm.getUserPersonalData("/profile/create", function (success) {

        }, function (errorResult) {
            alert(errorResult);
        });
    }, function (error) {
        alert(error);
    });
}
```

!!! note
    `/profile/create` will create a user profile only if the email address is not already in the database.