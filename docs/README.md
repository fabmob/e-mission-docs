# Welcome to the Traceur FabMob e-mission Documentation!

[![Documentation Status](https://readthedocs.org/projects/fabmob/badge/?version=latest&style=flat-square)](https://fabmob.readthedocs.io/en/latest/?badge=latest)

**The documentation of Traceur Fabmob, a fork of e-mission, an open source phone-based personal mobility tracking software from UC Berkeley**. The doc is in English. (French docs are relative to end-user app manuel and evaluations and are to be found in the project site)

## Traceur Fabmob specific info:  

- [**projet Traceur web site**](https://oultim.frama.site) : presentation, evaluations, news...    
- [**CODE on GitHub**](https://github.com/fabmob)     

- **Docs**: the Traceur doc is [in the master branch](https://github.com/fabmob/e-mission-docs/tree/master) ; the doc pulled from e-mission is [in the e-mission-contrib branch](https://github.com/fabmob/e-mission-phone-fabmob/tree/e-mission-contrib), to be used when we want to contribute (PRs) to the e-mission docs  
- **Code** : similarly there is a traceur FabMob master branch for [e-mission-phone-fabmob](https://github.com/fabmob/e-mission-phone-fabmob/tree/master) and [e-mission-server-fabmob](https://github.com/fabmob/e-mission-server-fabmob/tree/master), as for [e-mission-translate](https://github.com/fabmob/e-mission-translate/tree/master), and an e-mission-contrib branch  
- **Issues** : [Specific issues of the Traceur FabMob project](https://github.com/fabmob/e-mission-phone-fabmob/issues) currently concern more the phone app. You can see how we are progressing by looking at the [Traceur PROJECT](https://github.com/fabmob/e-mission-phone-fabmob/projects/1)   

- [**Docs web site on ReadTheDocs**](https://fabmob.readthedocs.io/)


## General E-mission info:

The [e-mission-docs repo](https://github.com/e-mission/e-mission-docs) contains all the documentation for the project, except end-user documentation (which will be on the project web site) and [almost ALL THE ISSUES](https://github.com/e-mission/e-mission-docs/issues/).  

There are some specialized READMEs [in the individual repositories](https://github.com/e-mission), but they are gradually being moved in here. This means that if you have any questions, you should first search here and if you don't find any [existing issues](https://github.com/e-mission/e-mission-docs/issues/), you should [file an issue here](https://github.com/e-mission/e-missiond-docs/issue).
### [e-mission web site](https://e-mission.eecs.berkeley.edu/)   
### [LICENCE BSD-3](LICENSE.md)  

## What is e-mission
E-mission is an open source mobility platform developed at the [RISE](http://rise.cs.berkeley.edu/) and [BETS](https://bets.cs.berkeley.edu/) labs in the UC Berkeley EECS Department.  
E-mission includes a mobile application for Android and iOS, with user consent, automatically collects the user's travel patterns and sends them to the server so as to derive personal mobility information and analyses; depending on user consent for sharing his/her data, the data can also be used for aggregate mobility data studies. The application is also a tool for collecting information filled in by the user (such as incidents, ground truth information about his/her trip purpose and transportation mode, or answers to questions asked in external surveys).  
The server is a python web application, the data is stored in a mongoDB database; 
the client is a Cordova application for both Android and iOS.  
The application has been initially designed to be reused in research and academic projects either for conducting and as a good learning project for CS students. It is also freely reusable for any other user cases (LINK to list to be added here). 

## Overview
Read these papers for understand the context of the e-mission research project and concrete material for understanding the software.
- [TRB paper describing how to use e-mission functionality](https://people.eecs.berkeley.edu/~shankari/emission_trb_2017_paper.pdf)  
- [The in-review paper on the e-mission architecture, please do not distribute](https://people.eecs.berkeley.edu/~shankari/em-arch.pdf)  

## roadmap
The next features and enhancement can be guessed from the [ISSUES](https://github.com/e-mission/e-mission-docs/issues)  
Project organisation and funding (to be completed)  
The current are described in [Develop/Future](dev/future/overview.md)   

