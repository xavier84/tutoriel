# CouchPotato multi-utilisateur

![Google logo](https://couchpota.to/media/images/full.png "google logo")

N'ayant pas trouvé de tuto sur internet pour installer & configurer Couchpotato en multi-utilisateur, en voici un expliquant sa mise en place.
À titre indicatif, nous choisissons ces deux utilisateurs: xavier & zarev. 

> Prenez soin de les remplacer par vos propres utilisateurs tout au long du tutoriel!  
                                                                                                                                                                                                                  
## Détail du tutoriel:

1. Installation des prérequis

* python-cheetah
* Couchpotato

2. Création du service


3. Configuration de l'utilisateur


## 1. Installation des prérequis

*Installation de python-cheetah*

```shell
apt-get install git-core python python-cheetah
```

*Installation de CouchPotato*
```shell
git clone https://github.com/CouchPotato/CouchPotatoServer.git /opt/couchpotato
cd /opt/couchpotato
```

## 2. Création du service

*On commence par*
```shell
nano /etc/init.d/couchpotato-xavier
```

*On copie dedans*
```shell
#!/bin/sh
#
# DON'T EDIT THIS FILE DIRECTLY!
#
# Instead, create your own configuration by setting any of the 7 variables
# listed below in /etc/default/couchpotato. For example: adding CP_USER=noob
# to /etc/default/couchpotato makes the service run under the 'noob' account,
# overruling the default value of 'couchpotato'.
#
# Accepted variables with default values -if any- in parentheses:
# CP_USER	# username to run couchpotato under (couchpotato)
# CP_HOME	# directory of CouchPotato.py (/opt/couchpotato)
# CP_DATA	# directory of couchpotato's db, cache and logs (/var/opt/couchpotato)
# CP_PIDFILE	# full path of couchpotato.pid (/var/run/couchpotato/couchpotato.pid)
# PYTHON_BIN	# full path of the python binary (/usr/bin/python)
# CP_OPTS	# extra cli options for couchpotato, see 'CouchPotato.py --help'
# SSD_OPTS	# extra options for start-stop-daemon, see 'man start-stop-daemon'

### BEGIN INIT INFO
# Provides:          xavier
# Required-Start:    $network $remote_fs
# Required-Stop:     $network $remote_fs
# Should-Start:      $named deluged network-manager nzbget qbittorrent-nox sabnzbdplus transmission-daemon
# Should-Stop:       $named deluged network-manager nzbget qbittorrent-nox sabnzbdplus transmission-daemon
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: CouchPotato PVR for Usenet and torrents
# Description:       starts instance of CouchPotato using start-stop-daemon
### END INIT INFO

DESC=CouchPotato
#CONFIG=/etc/default/couchpotato

# don't accept config vars from the shell environment
unset CP_USER CP_HOME CP_DATA CP_PIDFILE PYTHON_BIN CP_OPTS SSD_OPTS

# source lsb init functions
. /lib/lsb/init-functions

# try loading the configuration file
[ -r "$CONFIG" ] && . "$CONFIG" \
	|| log_action_msg "$DESC: $CONFIG unreadable, falling back to default settings"

# assorted settings and their defaults
: "${CP_USER:=xavier}"
: "${CP_HOME:=/opt/couchpotato}"
: "${CP_DATA:=/opt/couchpotato/data/xavier}"
: "${CP_PIDFILE:=/opt/couchpotato/data/xavier/couchpotato.pid}"
: "${PYTHON_BIN:=/usr/bin/python}"

# basic sanity checks
([ -x "$PYTHON_BIN" ] && [ -f "$CP_HOME/CouchPotato.py" ]) || {
	log_failure_msg "$DESC: init script setup failed basic sanity checks, aborting!";
	# exit zero since this condition may also occur after a user
	# uninstalled cp while leaving this script in place.
	exit 0;
}

start_cp() {
	# create directories with sensible ownership and permissions
	# (but refuse to touch any pre-existing ones)
	for D in "$(dirname "$CP_PIDFILE")" "$CP_DATA"; do
		[ ! -d "$D" ] && {
			install --directory --owner="$CP_USER" --group=root --mode=0750 "$D" || exit 1;
		}
	done

#	# for backwards compatibility create an empty pidfile so it
#	# can be in any pre-existing directory, even those unwritable
#	# for the $CP_USER. PEBCAK?
#	[ ! -e "$CP_PIDFILE" ] && {
#		touch "$CP_PIDFILE" && \
#		chmod 0600 "$CP_PIDFILE" && \
#		chown "$CP_USER" "$CP_PIDFILE" \
#		|| exit 1;
#	}

	log_daemon_msg "Starting $DESC"
	start-stop-daemon --start --quiet --pidfile "$CP_PIDFILE" --chdir "$CP_HOME" --chuid "$CP_USER" --oknodo --exec "$PYTHON_BIN" $SSD_OPTS -- \
		CouchPotato.py --daemon --quiet --pid_file="$CP_PIDFILE" --data_dir="$CP_DATA" $CP_OPTS
	log_end_msg $? || exit $?
}

stop_cp() {
	log_daemon_msg "Stopping $DESC"
	# for security reasons, require the process to be both:
	# 1) listed in the pidfile and 2) running as $CP_USER
	start-stop-daemon --stop --quiet --pidfile "$CP_PIDFILE" --user "$CP_USER" --retry 15 --oknodo
	log_end_msg $? || exit $?
}

case "$1" in
	start)
		start_cp;;
	stop)
		stop_cp;;
	restart|force-reload)
		stop_cp && start_cp;;
	status)
		status_of_proc -p "$CP_PIDFILE" "$PYTHON_BIN" "$DESC"
		exit $?;;
	*)
		echo "Usage: $0 {start|stop|restart|force-reload|status}" >&2
		exit 3;;
esac

exit 0

```
> On vérifie que les 4 xavier sont bien modifiés suivant vos besoins  

## Démarrage du service + attribution des droits
```shell
update-rc.d couchpotato-xavier defaults
/etc/init.d/couchpotato-xavier start
/etc/init.d/couchpotato-xavier stop
chmod -Rf 755  /opt/couchpotato/data/
```

## Configuration de l'utilisateur Couchpotato
```shell
nano /opt/couchpotato/data/xavier/settings.conf
```
## Rechercher & remplacer
```shell
username = xavier
port = 5051
url_base = /couchpotato
show_wizard = 0

#dans le bloc blockhole
[blackhole]
magnet_file = 0
enabled = True
manual = 0
directory = /home/xavier/watch/
create_subdir = 0
use_for = both
```

## Configuration de nginx
```shell
location ^~ /couchpotato {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $remote_addr;
                proxy_set_header Host $host;
                proxy_redirect off;
                if ($remote_user = "xavier") {
                        proxy_pass http://127.0.0.1:5051;
                        break;
                }
        }
```
## On démmare le tout
```shell
/etc/init.d/couchpotato-xavier start
service nginx restart
```
# Partie 2 ajout d'un utilisateur.


## On crée le service
```shell
nano /etc/init.d/couchpotato-zarev
```

## On copie dedans
```shell
#!/bin/sh
#
# DON'T EDIT THIS FILE DIRECTLY!
#
# Instead, create your own configuration by setting any of the 7 variables
# listed below in /etc/default/couchpotato. For example: adding CP_USER=noob
# to /etc/default/couchpotato makes the service run under the 'noob' account,
# overruling the default value of 'couchpotato'.
#
# Accepted variables with default values -if any- in parentheses:
# CP_USER	# username to run couchpotato under (couchpotato)
# CP_HOME	# directory of CouchPotato.py (/opt/couchpotato)
# CP_DATA	# directory of couchpotato's db, cache and logs (/var/opt/couchpotato)
# CP_PIDFILE	# full path of couchpotato.pid (/var/run/couchpotato/couchpotato.pid)
# PYTHON_BIN	# full path of the python binary (/usr/bin/python)
# CP_OPTS	# extra cli options for couchpotato, see 'CouchPotato.py --help'
# SSD_OPTS	# extra options for start-stop-daemon, see 'man start-stop-daemon'

### BEGIN INIT INFO
# Provides:          zarev
# Required-Start:    $network $remote_fs
# Required-Stop:     $network $remote_fs
# Should-Start:      $named deluged network-manager nzbget qbittorrent-nox sabnzbdplus transmission-daemon
# Should-Stop:       $named deluged network-manager nzbget qbittorrent-nox sabnzbdplus transmission-daemon
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: CouchPotato PVR for Usenet and torrents
# Description:       starts instance of CouchPotato using start-stop-daemon
### END INIT INFO

DESC=CouchPotato
#CONFIG=/etc/default/couchpotato

# don't accept config vars from the shell environment
unset CP_USER CP_HOME CP_DATA CP_PIDFILE PYTHON_BIN CP_OPTS SSD_OPTS

# source lsb init functions
. /lib/lsb/init-functions

# try loading the configuration file
[ -r "$CONFIG" ] && . "$CONFIG" \
	|| log_action_msg "$DESC: $CONFIG unreadable, falling back to default settings"

# assorted settings and their defaults
: "${CP_USER:=zarev}"
: "${CP_HOME:=/opt/couchpotato}"
: "${CP_DATA:=/opt/couchpotato/data/zarev}"
: "${CP_PIDFILE:=/opt/couchpotato/data/zarev/couchpotato.pid}"
: "${PYTHON_BIN:=/usr/bin/python}"

# basic sanity checks
([ -x "$PYTHON_BIN" ] && [ -f "$CP_HOME/CouchPotato.py" ]) || {
	log_failure_msg "$DESC: init script setup failed basic sanity checks, aborting!";
	# exit zero since this condition may also occur after a user
	# uninstalled cp while leaving this script in place.
	exit 0;
}

start_cp() {
	# create directories with sensible ownership and permissions
	# (but refuse to touch any pre-existing ones)
	for D in "$(dirname "$CP_PIDFILE")" "$CP_DATA"; do
		[ ! -d "$D" ] && {
			install --directory --owner="$CP_USER" --group=root --mode=0750 "$D" || exit 1;
		}
	done

#	# for backwards compatibility create an empty pidfile so it
#	# can be in any pre-existing directory, even those unwritable
#	# for the $CP_USER. PEBCAK?
#	[ ! -e "$CP_PIDFILE" ] && {
#		touch "$CP_PIDFILE" && \
#		chmod 0600 "$CP_PIDFILE" && \
#		chown "$CP_USER" "$CP_PIDFILE" \
#		|| exit 1;
#	}

	log_daemon_msg "Starting $DESC"
	start-stop-daemon --start --quiet --pidfile "$CP_PIDFILE" --chdir "$CP_HOME" --chuid "$CP_USER" --oknodo --exec "$PYTHON_BIN" $SSD_OPTS -- \
		CouchPotato.py --daemon --quiet --pid_file="$CP_PIDFILE" --data_dir="$CP_DATA" $CP_OPTS
	log_end_msg $? || exit $?
}

stop_cp() {
	log_daemon_msg "Stopping $DESC"
	# for security reasons, require the process to be both:
	# 1) listed in the pidfile and 2) running as $CP_USER
	start-stop-daemon --stop --quiet --pidfile "$CP_PIDFILE" --user "$CP_USER" --retry 15 --oknodo
	log_end_msg $? || exit $?
}

case "$1" in
	start)
		start_cp;;
	stop)
		stop_cp;;
	restart|force-reload)
		stop_cp && start_cp;;
	status)
		status_of_proc -p "$CP_PIDFILE" "$PYTHON_BIN" "$DESC"
		exit $?;;
	*)
		echo "Usage: $0 {start|stop|restart|force-reload|status}" >&2
		exit 3;;
esac

exit 0

```
tu as 4 zarev a modifié

## Démarrage du service + attribution des droits
```shell
update-rc.d couchpotato-zarev defaults
/etc/init.d/couchpotato-zarev start
/etc/init.d/couchpotato-zarev stop
```

## config de user couch
```shell
nano /opt/couchpotato/data/zarev/settings.conf
```
## recherche/remplacé
```shell
username = zarev
port = 5052
url_base = /couchpotato
show_wizard = 0

#dans le bloc blockhole
[blackhole]
magnet_file = 0
enabled = True
manual = 0
directory = /home/zarev/watch/
create_subdir = 0
use_for = both
```
## Configuration de nginx
```shell
location ^~ /couchpotato {
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $remote_addr;
                proxy_set_header Host $host;
                proxy_redirect off;
                if ($remote_user = "xavier") {
                        proxy_pass http://127.0.0.1:5051;
                        break;
                }
                if ($remote_user = "zarev") {
                        proxy_pass http://127.0.0.1:5052;
                        break;
                }
        }
```
## On démmare le tout
```shell
/etc/init.d/couchpotato-zarev start
service nginx restart
```
