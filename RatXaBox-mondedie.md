## Auto installation de ruTorrent avec rTorrent
*Version "Seedbox-Manager Workflow"*

Salut à tous,

Voici un "fork" (une copie) du célèbre script Bonobox de notre ami @Ex_Rat, par plaisir j’y ai ajouté de nouvelles fonctionnalités:

* TARDIStart  
* SickRage multi-users
* CouchPotato  multi-users
* Plex  ou emby + icône dans ruTorrent
* Filebot
* Openvpn
* eZ Server Monitor
* Thème QuickBox-Dark par défaut
* Un sous-domain *****.ratxabox.ovh (sur demande)

## Installation des prérequis 

* [Bien lire le tuto de Ex_Rat](https://mondedie.fr/d/5399 "Titre") (juste le lire, ne pas exécuter script de ex_rat)
* [Dépot RatXaBox](https://github.com/xavier84/RatXaBox "Titre")



[b]2) Installation :[/b]

Mise a jours + installation de Git
[code]apt-get update && apt-get upgrade -y
apt-get install git-core -y
[/code]
on clone est lance le script
[code]cd /tmp
git clone https://github.com/xavier84/RatXaBox ratxabox
cd ratxabox
chmod a+x bonobox.sh && ./bonobox.sh[/code]

il vous suffira de suivre les indications affichées.

[b]3) Les Options :[/b]

Pour installé les options:
 après le redémarrage du serveur relancé le script et prendre le choix numéro : 10

[b]4) Les liens :[/b]

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



PS: si vous avez des bugs ou autres problèmes n'hésitez pas à me contacter !



La discussion se passe la https://mondedie.fr/d/8717-Discussion-RatXaBox-ruTorrent-avec-rTorrent-Version-Workflow

cordialement
Xavier