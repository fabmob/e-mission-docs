# FAQ page in French for end-users  

(some of this FAQ will be contributed back to the [English e-mission docs](https://github.com/e-mission/e-mission-docs)

Pensez à lire [la notice de présentation de l'application](https://docs.google.com/document/d/1X_FwiXjmWEFCLNhEXNa3-cD0FCjOURlLClCUiUoQ6PM/) et au besoin regarder [les autres livrables du projet traceur Fabmob](https://oultim.frama.site/livrables).  

- le tracking est-il activé?

L'application doit avoir été lancée (avec un utilisateur connecté), même si elle n'est plus ouverte et tourne en tâche de fond.
La localisation doit être autorisée sur le téléphone (de préférence acceptez la localisation améliorée proposée par Google qui prend en compte aussi les antennes Wifi).
En revanche l'application peut fonctionner même si il n'y a pas de réseau (wifi ou GSM) mais il est **fortement recommandé d'activer le wifi et la data** sur le téléphone, sinon la détection de début (et fin) de trajet fonctionera mal.

- le déplacement en cours est-il terminé?

Il peut arriver que le déplacement soit considéré encore cours, que l'appli n'ait pas détecté sa fin. Dans l'écran Diary, le déplacement s'affiche alors comme encore en cours. On peut si besoin, dans Profile, forcer la fin du "trip". Cela permet de recommencer le tracking des prochains déplacements.

- le traçage ne fonctionne pas: l'appli est-elle autoriséee à fonctionner en tâche de fond ? (vous avez un téléphone Huawei?)

 un [paramètre spécifique à Huawei](https://android.stackexchange.com/questions/152649/what-is-protected-apps-in-huawei-phones#152662) ferme par défaut les applications quand l'écran s'éteint, [ajouter l'app traceur comme "appli protégée"](https://support.mypacer.com/hc/en-us/articles/115004919668-My-Huawei-phone-stops-counting-steps-What-should-I-do) dans paramètres avancés / gestion de la batterie, pour que l'app continue à fonctionner en tâche de fond quand l'écran s'éteint... Ce problème concerne peut être d'autres marques de smartphone, mais pas à notre connaissance.
Attention, il faut reparamétrer le traceur comme appli protégée si on la désinstalle et réinstalle.

- notification d'une "erreur 6" ?
Cela signifie que le GPS n'est pas activé dans vos paramètres de téléphone. Cela empêche le tracking. 
