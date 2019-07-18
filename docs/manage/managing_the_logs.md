# Managing the logs
___

**Issues**: https://github.com/fabmob/e-mission-phone-fabmob/issues/20, https://github.com/fabmob/e-mission-phone-fabmob/issues/19

## Actual configuration

Currently, logs are rotating daily at midnight using a [TimedRotatingFileHandler](https://docs.python.org/3/library/logging.handlers.html#timedrotatingfilehandler). Each day, at 7 o'clock, the server is executing a script which will merge the log files of the pipeline into a single file. Moreover, if there are errors, the server will also notify the administrator by sending them a push notification thanks to [notify.run](https://notify.run/). This script is currently only available locally on the server and can be found at `/var/emission/em-scripts/merge_intake_logs.py`. 

### Logs architecture

All the `e-mission` logs can be found into the folder `/var/log/emission`. It is possible to change that folder by editing some configuration files (see [Changing log configuration](#changing-log-configuration)). The current architecture is the following:

```
 var/log/emission/
            |__ pipeline/       # Contains all the logs linked to the pipeline
            |__ webserver/      # Contains all webserver logs
            |__ log_merger.log  # Contains information logged by the merge script
```

## Changing log configuration

Each logs configuration files can be found in the folder `e-mission-server/conf/log`. In those files, it is possible to change the [logging handlers](https://docs.python.org/3/library/logging.handlers.html) but also the [formatter](https://docs.python.org/3/library/logging.handlers.html). The log configuration file of the pipeline is `intake.conf` ; as for the `webserver`, it is `webserver.conf`. To have daily rotating logs, those files will be configured as below:

```json
{
    "handlers": {
        "errors": {
            "backupCount": 90,
            "when":"midnight",
            "level": "ERROR",
            "formatter": "detailed",
            "class": "logging.handlers.TimedRotatingFileHandler",
            "filename": "/var/log/emission/pipeline/intake-errors.log"
        },
        "console": {
            "class": "logging.StreamHandler",
            "level": "WARNING"
        },
        "file": {
            "backupCount": 90,
            "filename": "/var/log/emission/pipeline/intake.log",
            "when":"midnight",
            "formatter": "detailed",
            "class": "logging.handlers.TimedRotatingFileHandler"
        }
    },
    "version": 1,
    "root": {
        "handlers": [
            "console",
            "file",
            "errors"
        ],
        "level": "DEBUG"
    },
    "formatters": {
        "detailed": {
            "class": "logging.Formatter",
            "format": "%(asctime)s:%(levelname)s:%(thread)d:%(message)s"
        }
    }
}
```

## Notifying the administrator

**Current channel**: https://notify.run/gp4ekyBL51VAoNdi

To notify the administrator, we are currently using [notify.run](https://notify.run) public servers. 

!!! note 
    It is possible to [self-host a notify.run server](https://github.com/paulgb/notify.run/tree/master/server), but, as we are not sending any confidential data, it is not necessary. 

To use **notify.run** in a Python script, we can install it with `pip`.

```bash
$ pip install notify-run
```

After installing it, we have to configure it. To add a previously created channel, we will use `configure`.

```bash
$ notify-run configure <url>
```

Or, we can register a new channel with `register`.

```bash
$ notify-run register
```

!!! tip
    We can retrieve the currently configured channel into `~/.config/notify-run`.

Once configured, we can now add the following lines into our Python script: 

```python
from notify_run import Notify
notify = Notify()
notify.send('Error(s) in the pipeline, you should check intake_global-errors.log')
```

The administrator will just have to scan the QR code contained in the channel webpage and "Subscribe on this device" to receive a push notification on your phone. 
