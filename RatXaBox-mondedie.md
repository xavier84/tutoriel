[center][b]Auto installation de ruTorrent avec rTorrent. Version [color=red]"Seedbox-Manager Workflow"[/color][/b][/center]



Salut à tous,



Voici un "fork" (une copie) de notre ami [color=green]Ex_Rat[/color] du célèbre script Bonobox que par plaisir j’ai ajouté des fonctionnalités,


[list=*]
[*][color=#D2691E]TARDIStart[/color][/*]
[/list]
[list=*]
[*][color=#D2691E]SickRage multi-users[/color][/*]
[/list]
[list=*]
[*][color=#D2691E]CouchPotato  multi-users[/color][/*]
[/list]
[list=*]
[*][color=#D2691E]Plex  ou emby + icône dans ruTorrent[/color] "dans options"[/*]
[/list]
[list=*]
[*]*******[/*]
[/list]
[list=*]
[*]*******[/*]
[/list]
[list=*]
[*][color=#D2691E]Filebot[/color] "dans options"[/*]
[/list]
[list=*]
[*][color=#D2691E]Openvpn[/color] "dans options"[/*]
[/list]
[list=*]
[*][color=#D2691E]eZ Server Monitor[/color][/*]
[/list]
[list=*]
[*][color=#D2691E]Thème QuickBox-Dark par défaut [/color][/*]
[/list]
[list=*]
[*][color=#D2691E]Un sous-domain[/color] [color=#9932CC] *****.ratxabox.ovh [/color][color=#D2691E](sur demande)[/color][/*]
[/list]

[b]1) Préambule :[/b]

Bien lire le tuto de Ex_Rat : [url]https://mondedie.fr/d/5399[/url] (juste le lire, ne pas exécuter script de ex_rat)

Dépot RatXaBox : [url]https://github.com/xavier84/RatXaBox[/url]

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