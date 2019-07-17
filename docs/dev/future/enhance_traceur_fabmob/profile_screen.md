# Complete Profile Screen
---
**Issue**: https://github.com/fabmob/e-mission-phone-fabmob/issues/29

## Monitoring user geolocation status

After some investigation, we found that it is possible to use Wi-Fi, network triangulation and bluetooth to enhance the tracking. To retrieve Wi-Fi, Location and network statuses, we are using the cordova plugin: [cordova.plugins.diagnostic](https://www.npmjs.com/package/cordova.plugins.diagnostic). By using this plugin, we are able to check on Android if the geolocation parameters of the device is set to low-accuracy (only network triangulation and Wi-Fi network IDs also know as battery saving) or high-accuracy (network, wi-fi and GPS hardware). However, it only works with Android because in iOS we cannot change the location accuracy and the system will use everything it can as long as it is enabled.

#### Android: getLocationMode()

In Android, we can use `getLocationMode()` to retrieve the location mode of the device. The differents modes are:

- *High Accuracy*: GPS hardware, Wi-Fi networks IDs and network triangulation,
- *Battery saving*: only Wi-Fi networks IDs and network triangulation,
- *Device only*: only GPS hardware,
- *Location off*: location disabled.

```js
cordova.plugins.diagnostic.getLocationMode(function(locationMode){
    switch(locationMode){
        case cordova.plugins.diagnostic.locationMode.HIGH_ACCURACY:
            console.log("High accuracy");
            break;
        case cordova.plugins.diagnostic.locationMode.BATTERY_SAVING:
            console.log("Battery saving");
            break;
        case cordova.plugins.diagnostic.locationMode.DEVICE_ONLY:
            console.log("Device only");
            break;
        case cordova.plugins.diagnostic.locationMode.LOCATION_OFF:
            console.log("Location off");
            break;
    }
},function(error){
    console.error("The following error occurred: "+error);
});
```