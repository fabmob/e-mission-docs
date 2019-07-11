# Adding LimeSurvey Support
---

In addition to the normal survey support, it is possible to configure a LimeSurvey support to use with the Survey screen. 

## Dependencies

- Python **LimeSurvey RC2 API**, you can found it on GitHub by following this link :
https://github.com/lindsay-stevens/limesurveyrc2api,
- [LimeSurvey](https://www.limesurvey.org/).
  
## Configuring LimeSurvey 

Before configuring `e-mission-server`, it is needed to configure a bit your LimeSurvey server.

On your LimeSurvey admin interface :

1. Go to *Configuration -> Global settings*,
2. In the *Interfaces* tab, activate **JSON-RPC** by clicking on it,
3. Optionally, modify the RemoteControl URL which will be used by **e-mission-server**.

## Configuring e-mission-server

1. Go to `e-mission-server/bin/conf/net/ext_service`,
2. Add a `limesurvey.json` by copying `limesurvey.json.sample` and adapting it according to your server.

```json
{
    "url": "RemoteControl API URL", 
    "username": "Admin account of limesurvey",
    "password": "password",
    "url_surveys": "URL of the surveys"
}
```

The `url_surveys` will be used to build an URL to be send when the user will retrieve his surveys with the phone app.

## Preparing a LimeSurvey survey

For each new survey you will want to send, it will be necessary to quickly configure it. 

1. After clicking on *Create a new survey*, go to the *Participant settings* tab,
2. Change the default token length to 32 instead of 15 (by passing the length to 32, this will allow us to create an invitation token based on the `uuid` of the user),
3. Activate *Enable token-base response persistence*,
4. Optionally, if you want to allow the user to change his response you can enable *Allow multiple responses or update responses with one tokens*,
5. After the creation of the survey, into the settings of the survey go into *Survey menu -> Survey participants* and click on "Initialise participant table".

## Sending the LimeSurvey survey

After customising your survey, you can now send it to the user ! To send a survey, you can check [Pushing Surveys from the Server to the Phone](pushing_surveys_from_the_server_to_the_phone.md). However, use `limesurvey.sample` into the `emission/net/ext_service/push/sample.specs/push` as example. The *survey id* (`sid`) can be found either at the end of the survey url or in the LimeSurvey interface into *Survey settings -> Overview*. 
The uuidElementId is used by other external surveys, but not by LImeSurvey, you can pu any content here.

```json
{
    "alert_type": "survey",
    "title": "Did you share rides ?",
    "message": "3 questions - Approx. 1 min",
    "image": "icon",
    "force-start": 1,
    "spec": {
      "url": "https://fabmob.limequery.com/964722",
      "uuidElementId": "answer886519X3X3",
      "type": "limesurvey",
      "sid": "964722"
    }
}
```
> **WARNING**: Before sending the notification to users, do not forget to **Activate** the survey by clicking on `Activate this survey`.

We recommend to check everything before actually sending the survey :

0) create the survey spec and query as explained in [Pushing Surveys from the Server to the Phone](pushing_surveys_from_the_server_to_the_phone.md)

1a) use option -n for testing the query without sending the survey

```
cd directory_e-mission-server
conda activate emission
./e-mission-py.bash bin/push/send_survey.py -q /var/emission/e-mission-server/emission/net/ext_service/push/sample.specs/query/tripbike.json -n -s /var/emission/e-mission-server/emission/net/ext_service/push/sample.specs/push/bikesurvey.server.sample
```
This will the participant list (resulting from the query) in limesurvey for that survey.

1b) send the survey to you to check it is Ok (without -n)
```
./e-mission-py.bash bin/push/send_survey.py -e myaddress@mail.com -s /var/emission/e-mission-server/emission/net/ext_service/push/sample.specs/push/bikesurvey.server.sample
```
2a) now send the survey for real (sans le -n)
```
./e-mission-py.bash bin/push/send_survey.py -q /var/emission/e-mission-server/emission/net/ext_service/push/sample.specs/query/tripbike.json -n -s /var/emission/e-mission-server/emission/net/ext_service/push/sample.specs/push/bikesurvey.server.sample
```
2b) if necessary, add a user manually
```
./e-mission-py.bash bin/push/send_survey.py -e address_to_add@mail.com -s /var/emission/e-mission-server/emission/net/ext_service/push/sample.specs/push/bikesurvey.server.sample
```

