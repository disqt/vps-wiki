---
icon: cube
---

# Minecraft

Le serveur minecraft est accessible à l'adresse `disqt.com:25565`. Toutefois, comme les clients minecraft se connectent toujours au même port, il est possible de se connecter via `disqt.com` directement.

La configuration du serveur minecraft se situe ici `/home/minecraft`.

Le serveur Minecraft est configuré en `offline` mode, ce qui veut dire que les clients non authentifiés avec Mojang peuvent se connecter.

Pour intéragir avec le serveur, il est possible d'utiliser l'alias `pmc`, qui est un alias redirigeant vers `/home/minecraft/pmcserver`. Par exemple, `pmc restart` va redémarrer le serveur.

```bash
minecraft@vps-d7cc07ce ➜  ~ pmc help
Error! Unknown command: /home/minecraft/pmcserver help
Usage: /home/minecraft/pmcserver [option]

LinuxGSM - PaperMC - Version v24.3.0
https://linuxgsm.com/pmcserver

Commands
start         st   | Start the server.
stop          sp   | Stop the server.
restart       r    | Restart the server.
monitor       m    | Check server status and restart if crashed.
test-alert    ta   | Send a test alert.
details       dt   | Display server information.
postdetails   pd   | Post details to termbin.com (removing passwords).
skeleton      sk   | Create a skeleton directory.
update-lgsm   ul   | Check and apply any LinuxGSM updates.
update        u    | Check and apply any server updates.
check-update  cu   | Check if a gameserver update is available
backup        b    | Create backup archives of the server.
console       c    | Access server console.
debug         d    | Start server directly in your terminal.
send          sd   | Send command to game server console.
install       i    | Install the server.
auto-install  ai   | Install the server without prompts.
developer     dev  | Enable developer Mode.
sponsor       s    | Sponsorship options.
```

## Configuration

La configuration du serveur se trouve ici `/home/minecraft/lgsm/config-lgsm/pmcserver`.

Elle s'applique par ordre d'importance :

`_default.cfg < common.cfg < pmcserver.cfg`. Par exemple dans le cas suivant :&#x20;

```
# _default.cfg
mcversion="1.0"

# common.cfg
mcversion="1.1"

# pmcserver.cfg
mcversion="1.2"
```

Alors la variable `mcversion`du serveur `pmcserver` sera `1.2`, puisque la configuration de `pmcserver.cfg` prend précédence.

## Tâches automatisées

Le serveur dispose d'un certain nombre de tâches automatisées via des crontabs.

Ces crontabs sont accessibles via la commande `crontab -e`. Le 30/09/2024, ces crontabs sont

```bash
*/5 * * * * source /home/minecraft/.zshrc; /home/minecraft/pmcserver monitor >> /home/minecraft/log/monitor.log 2>&1
0 4 * * 6 source /home/minecraft/.zshrc; /home/minecraft/pmcserver update >> /home/minecraft/log/update.log 2>&1
0 5 * * 6 source /home/minecraft/.zshrc; /home/minecraft/pmcserver update-lgsm >> /home/minecraft/log/update-lgsm.log 2>&1
0 6 * * * /home/minecraft/backup.sh >> /home/minecraft/log/backup.log 2>&1
```

{% hint style="info" %}
Il est important de spécifier `source /home/minecraft/.zshrc` avant de planifier une commande lgsm via crontab. Autrement, les scripts risquent de s'effectuer avec la mauvaise version de Java.

Ceci n'est pas nécessaire pour les scripts `*.sh`, à condition que le script effectue un `source ~/.zshrc` lui-même.
{% endhint %}

### Monitor

Le serveur effectue une commande monitor toutes les 5min. Cette commande permet au serveur de redémarrer si un problème est survenu et qu'il a crash.

### Mises-à-jour

Le serveur se met à jour automatiquement le dimanche à 4h et 5h du matin.

Il effectue d'abord une update de minecraft lui-même, si elle est disponible.

Puis une update de lgsm, si il y en a de disponibles.

### Sauvegardes

Le serveur se sauvegarde tous les jours à 6h du matin. Le backup s'effectue via LinuxGSM, qui crée une archive `.tar.gz` du serveur, puis cette sauvegarde est transférée vers un autre cloud via `rclone`.

Le script de sauvegarde est accessible ici `/home/minecraft/backup.sh`.

Des logs de ce script sont accessibles ici `/home/minecraft/log/backup.log`.

## Alertes

Le serveur envoie des alertes lorsqu'il crash, reboot de façon inattendue, effectue une sauvegarde, ou se met à jour.

Ces alertes sont envoyées sur le serveur Discord de la Disquette, sur le salon `alert-minecraft`, reservé à la modération.
