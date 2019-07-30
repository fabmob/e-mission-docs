# How to add tracking to your app
___

The tracking strongly depends on the plugin [e-mission-data-collection](https://github.com/e-mission/e-mission-data-collection). This plugin needs a valid consent to work.

## Managing consent

```json
{
    "protocol_id": "2014-04-6267",
    "approval_date": "2016-07-14"
}
```
In **e-mission**, a Consent object has two fields: the approval date and the protocol ID. In order for the plugin to work in par with the app, we need to add the following line into the `config.xml`.

```xml
<preference name="emSensorDataCollectionProtocolApprovalDate" value="2016-07-14" />
```

If the user accepts your consent, to start tracking him, it will be necessary to use the function `markConsented(consent)` to notify the plugin that the user accepted the consent and that we can now track him. 

```js
var consentProtocol = {
    "protocol_id": "2014-04-6267",
    "approval_date": "2016-07-14"
};

window.cordova.plugins.BEMDataCollection.markConsented(consentProtocol).then(function (response) {
    alert("You are now tracked");
}, function (errorResult) {
    alert(errorResult);
});
```

When `markConsented`is called, the consent will be stored in the user local storage with the key `config/consent` the plugin will then check if the approval date is equals to the one specified into the `config.xml`, if it matches, the state will changed from `local.state.start` to `local.state.waiting_for_trip_start`. You can retrieve and display the current state with the function `getState()`of the same plugin. 

## Displaying and managing states


### Retrieving current state

As said before, it is possible to retrieve the state by using the function `getState()`. However, the states keys vary between iOS and Android, so you will need to check the platform to parse them and display a human readable value. 

```js
window.cordova.plugins.BEMDataCollection.getState().then(function (result) {
    console.log("State is " + result);
});
```
### Forcing a transition

It is also possible to force a transition in order to force start a trip or to force end it. To achieve that, we can use the `forceTransition(generalTransitionName)`. The general transition names are: `INITIALIZE`, `EXITED_GEOFENCE`, `STOPPED_MOVING`, `STOP_TRACKING` and `START_TRACKING`.  To force start a trip, we will use the transition `EXITED_GEOFENCE` and to force end a trip we will use `STOPPED_MOVING`.

```js
function forceStartTrip(){
    window.cordova.plugins.BEMDataCollection.forceTransition('EXITED_GEOFENCE').then(function (response) {
        console.log("User forced a start trip.")
    });
}

function forceEndTrip(){
    window.cordova.plugins.BEMDataCollection.forceTransition('STOPPED_MOVING').then(function (response) {
        console.log("User forced a end trip.")
    });
}
```

!!! note
    By using the same logic, it is possible to enable (`START_TRACKING`) and disable (`STOP_TRACKING`) the tracking of the app.