---
description: Notre super reverse-proxy
icon: chart-network
---

# Nginx

Le serveur utilise [Nginx comme reverse-proxy](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/).

Cela nous permet de contrôler les requêtes qui de clients qui proviennent d'en dehors du réseau local du serveur. C'est-à-dire que tous les clients qui effectuent une requête vers le serveur, par exemple `GET disqt.com/servers`, vont passer via Nginx, qui va proxy les requêtes vers le port local qui est configuré.

La configuration se trouve ici `/etc/nginx`.

Pour configurer une nouvelle adresse, il faut se rendre ici `/etc/nginx/available-sites/disqt.com`.

