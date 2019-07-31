# Retrieving users data
___

To communicate with **e-mission** REST API, we will use the plugin [cordova-server-communication](https://github.com/e-mission/cordova-server-communication) which will allow us to make authenticated calls to the server. You can find all the endpoints [there](https://github.com/e-mission/e-mission-server/blob/master/emission/net/api/cfc_webapp.py).

## How to extract trips information

There is two types of trips: unprocessed trips and processed trips. 

### Retrieving processed trips

To retrieve processed trips, we can use the endpoint `/timeline/getTrips/<date>`. The date format must be `YYYY-MM-DD`. This URI will return us a JSON containing the trips of the chosen day. To make an authenticated call to the server in order to retrieve the trips of the logged user, we will use the function `getUserPersonalData(uri, resolve, reject)`. 

```js
function getTimelineForDay (date){
    var dateString = date.toISOString().slice(0, 10);
    window.cordova.plugins.BEMServerComm.pushGetJSON('/timeline/getTrips/' + dateString, function (response){
        console.log(response);
    }, function (error) {
        console.log(error);
    });
}
```

### Retrieving unprocessed trips

Retrieving unprocessed trips is a bit more delicate than retrieving processed trips. Indeed, we will have to find the starting and ending transitions of each unprocessed trips into the local storage. As it is a bit thorough, you can find the method used by @Shankari into e-mission-phone [readUnprocessedTrips(day, tripListForDay)](https://github.com/e-mission/e-mission-phone/blob/b1e73b8e59ce3c674ac895dc94d26b3fabf83af0/www/js/diary/services.js#L871).

## How to retrieve metrics

If we want to display metrics, we can retrieve them at `/result/metrics/<timetype>`. However, you will have to enclose a JSON into the POST request to precise between which dates you want to do the request, the frequency and the metrics you want to retrieve (count, duration, median speed and/or distance).

### Query types

When you will try to call the `/result/metrics/`, you will have to precise the timetype. The timetype can be either `local_date` or `timestamp`. 

```js
function getMetrics(timeType, metrics_query) {
  return new Promise(function(resolve, reject) {
    var msgFiller = function(message) {
        for (var key in metrics_query) {
            message[key] = metrics_query[key]
        };
    };
    window.cordova.plugins.BEMServerComm.pushGetJSON("/result/metrics/"+timeType, msgFiller, resolve, reject);
  })
};

getMetrics("timestamp", metrics_query).then(function (result) {
	console.log(result)
});
```
#### timestamp

If you are using `timestamp`, the query will have an attribute `freq` which can take the following values: "D" (daily), "W" (weekly), "2W" (biweekly), "M" (monthly) or "A" (yearly). You will also have to precise the `start_time`, the `end_time` in `UNIXTIMESTAMP`, the metrics that you want to retrieve into an attribute `metric_list` which is an array and a boolean `is_return_aggregate` to tell if you want to retrieve only the user metrics or both user and aggregates metrics. 

```js
var metrics_query = {
    freq: "D",
    start_time: new Date(1970,01,01).getTime() / 1000,
    end_time: new Date().getTime() / 1000,
    metric_list: ["count","distance","duration", "medianspeed"],
    is_return_aggregate: false
}
```

!!! tips
    To convert a Date into a `UNIXTIMESTAMP`, you can either use the method above (`new Date().getTime()/1000`) 
    or use the [moment.js](https://momentjs.com/) library which provides a couple of useful functions
    to manipulate dates.

#### local_date

For the `local_date` the frequency can be either `DAILY`, `MONTHLY`or `YEARLY` but the biggest change is the format of the `start_time` and `end_time` which will be a JSON object now (`{year: <year>, month: <month>, day: <day>}`). The metrics query will then looks like that:

```js
var date = new Date();

var metrics_query = {
    freq: "DAILY",
    start_time: {year: 1970, month: 1, day: 1},
    end_time: {year: date.getFullYear(), month: date.getMonth() + 1, day: date.getDate()}
    metric_list: ["count","distance","duration", "medianspeed"],
    is_return_aggregate: false
}
```

## Getting and updating users information

### Getting users information

To retrieve the information of a user such as his user id, you can use the function `getUserPersonalData(uri, resolve, reject)` with the endpoint `/profile/get`.

```js
window.cordova.plugins.BEMServerComm.getUserPersonalData("/profile/get", function (success) {
    console.log(success)
});
```

### Updating user information

We can also update the information of a user to change his sync interval, platform or device token. It can be useful if you are using the [push notification](../../../../install/deploying_your_own_server_to_production#configuring-push) as you will need the FCM token of the user. 

```js
var updateDoc = {
    curr_platform: window.cordova.platformId
}

window.cordova.plugins.BEMServerComm.postUserPersonalData("/profile/update", "update_doc", updateDoc, function (success){
    console.log(success);
}, function (error){
    console.log(error);
});
```