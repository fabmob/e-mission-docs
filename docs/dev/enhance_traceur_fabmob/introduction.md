# Contributing to the traceur FabMob e-mission app

Traceur Fabmob is a fork of e-mission, we enhance or add features to the software.  
The current list of enhancements planned is described in [this issue list](https://github.com/fabmob/e-mission-phone-fabmob/issues).  
[This report (in French)](https://drive.google.com/file/d/1h7PWoA6sJBYYeRoO2OgSiibv1ZJH8VLZ/view) of the developments done by Loïc Mayol from June to August 2019 is particularly for understanding the details of the limesurvey, internationalisation and Profile+Dashboard screens enhancements.

## GIT process
In each of our repo, there at least 2 branches, the **master branch** and the **e-mission-contrib branch** (e.g. for e-mission-translate, e-mission-docs):

- the updates specific to our FabMob app (and thus do not concern Berkeley's e-mission) are merged on the master branch (e.g. for the page you are reading now which is a file in the e-mission-docs repo);

-the corrections or enhancements proposed as contributions to the e-mission project should be pushed on the e-mission-contrib branche. We then make a pull request to Shankari, who will validate and eventually updated e-mission master branche with the contrib. We can then pull the updates of e-mission master to our fabmob master branch.


## Enhancement "studies"
Among these enhancement, some are not immediate to implement so they are [tagged as "studies"](https://github.com/fabmob/e-mission-phone-fabmob/issues?utf8=%E2%9C%93&q=label%3Astudy+), 
we begin to look for a technical solution before trying to implement.

We publish here the results of the enhancement studies (one page for each study), when all goes smoothly, the page describes the solution found and the expected implementation difficulty,
and in a second step if we decide to implement, the general documentation will be updated too.
