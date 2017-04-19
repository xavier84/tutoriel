## Auto installation de ruTorrent avec rTorrent
*Version "Seedbox-Manager Workflow"*

![Google logo](https://cloud.llamasweet.tech/index.php/apps/files_sharing/ajax/publicpreview.php?x=1920&y=543&a=true&file=ratxabox.jpg&t=0SRd82hfO9PMWe7&scalingup=0 "google logo")

Salut à tous,

Voici un "fork" (une copie) du célèbre script [Bonobox](https://mondedie.fr/d/5399-Script-Installation-automatique-ruTorrent-nginx "Titre") de notre ami @Ex_Rat, par plaisir j’y ai ajouté de nouvelles fonctionnalités:

* TARDIStart  
* SickRage multi-users
* CouchPotato  multi-users
* Plex  ou emby + icône dans ruTorrent
* Filebot
* Openvpn
* eZ Server Monitor
* Thème QuickBox-Dark par défaut
* Un sous-domain *****.ratxabox.ovh (sur demande)

**Détail du tutoriel:**

1. ## Préambule
2. ## Installation
* git-core
* cloner et lancer le script
3. ## Les options
4. ## Liens utiles
## 1. Préambule

* [Bien lire le tuto de Ex_Rat](https://mondedie.fr/d/5399 "Titre") (juste le lire, ne pas exécuter script de ex_rat)
* [Dépot RatXaBox](https://github.com/xavier84/RatXaBox "Titre")

## 2.  Installation

*Mise a jours + installation de Git:*
```{r}
apt-get update && apt-get upgrade -y
apt-get install git-core -y
```

*On clone et on lance le script:*
```{r}
cd /tmp
git clone https://github.com/xavier84/RatXaBox ratxabox
cd ratxabox
chmod a+x bonobox.sh && ./bonobox.sh
```
*Il vous suffira de suivre les indications affichées:*

![Google logo](https://cloud.llamasweet.tech/index.php/apps/files_sharing/ajax/publicpreview.php?x=1920&y=543&a=true&file=ratxaboxlin.jpg&t=EWJJRRVDeKBnP7I&scalingup=0 "google logo")

## 3.  Les options

Pour installer les options: après le redémarrage du serveur, relancer le script et choisir le numéro **10**
![Google logo](https://cloud.llamasweet.tech/index.php/apps/files_sharing/ajax/publicpreview.php?x=1920&y=543&a=true&file=options.jpg&t=QoqdE9ywmV4DzX8&scalingup=0 "google logo")

*Voici les options disponibles:*
![Google logo](https://cloud.llamasweet.tech/index.php/apps/files_sharing/ajax/publicpreview.php?x=1920&y=543&a=true&file=options%25C3%25A9tendues.jpg&t=GAKD2pGwgBIkhB9&scalingup=0 "google logo")


## 4. Liens utiles

*Voici les liens pour vous connecter à l'interface de vos services*

* TARDIStart :
IPserveur/tardistart

* SickRage :
IPserveur/sickrage

* CouchPotato :
IPserveur/couchpotato

* Plex :
IPserveur:32400/web

* Emby :
IPserveur:8096

* Esm :
IPserveur/esm


*Partie technique:*

- TARDIStart
Administraion des liens TARDIStart :
IPserveur/tardistart/admin

> Si vous rencontrez un bug ou tout autre problème, n'hésitez pas à me contacter !

[La discussion se passe ici](https://mondedie.fr/d/8717-Discussion-RatXaBox-ruTorrent-avec-rTorrent-Version-Workflow "Titre")

Cordialement:
@Xavier