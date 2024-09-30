---
icon: paper-plane
---

# PaperMC

Le serveur Minecraft est un serveur [PaperMC](https://papermc.io/). Il s'agit d'un serveur minecraft ultra optimisé, et très compatibles avec de nombreux plugins.

## Gérer les membres

Les membres sont gérés via la whitelist et les plugins LuckPerms et AuthMe.

Un nouveau membre doit d'abord être ajouté à la whitelist par un admin via la commande `/whitelist add <username>` en jeu.

Ensuite, lors de sa première connexion, un nouveau membre doit créer un mot de passe via le Plugin AuthMe. Pour se faire, iel doit run la commande `/register <mot de passe>` en jeu. Lorsque ce joueur se reconnectera, il faudra qu'iel run la commande `/login <mot de passe>`.

Cette sécurité est nécessaire puisque le serveur est en mode offline - autrement, il est possible pour n'importe qui de se connecter au serveur avec un pseudo qui est whitelisté. C'est arrivé le 12 Septembre 2024, où un hackeur russe s'est connecté avec le pseudo Termiduck et a pu grief le serveur via les commandes admin.

Après 120 jours d'inactivité, le mot de passe est réinitialisé.
