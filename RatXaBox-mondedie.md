## Auto installation de ruTorrent avec rTorrent
*Version "Seedbox-Manager Workflow"*

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
Il vous suffira de suivre les indications affichées

## 3.  Les options

Pour installer les options: après le redémarrage du serveur, relancer le script et choisir le numéro **10**

Les liens

[list=*]
[*]TARDIStart :
IPserveur/tardistart[/*]
[/list]
[list=*]
[*]SickRage :
IPserveur/sickrage[/*]
[/list]
[list=*]
[*]CouchPotato :
IPserveur/couchpotato[/*]
[/list]
[list=*]
[*]Plex :
IPserveur:32400/web[/*]
[/list]
[list=*]
[*]Emby :
IPserveur:8096[/*]
[/list]
[list=*]
[*]Esm :
IPserveur/esm[/*]
[/list]

[b]5) Partie technique :[/b]

- TARDIStart
Administraion des liens :
[list=*]
[*]TARDIStart   IPserveur/tardistart/admin[/*]
[/list]

PS: si vous rencontrez un bug ou tout autre problème, n'hésitez pas à me contacter !

[La discussion se passe ici](https://mondedie.fr/d/8717-Discussion-RatXaBox-ruTorrent-avec-rTorrent-Version-Workflow "Titre")

Cordialement:
Xavier