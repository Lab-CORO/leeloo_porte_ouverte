# Leeloo : téléopération par casque VR et interface web

Ce guide explique comment **installer**, **allumer** et **piloter** le robot Leeloo (bras Doosan M1013 + pince Robotiq) avec un casque HTC Vive ou depuis une page web.

Il s'adresse à deux personnes :

- **le technicien du laboratoire** : il installe le matériel, le réseau et le logiciel (parties A) ;
- **l'opérateur** (un étudiant, le jour des portes ouvertes) : il allume le robot et accompagne le visiteur (parties B).

Aucune connaissance préalable de ROS ou de Linux n'est nécessaire : chaque commande est à copier-coller, avec ce qu'il faut voir après.

> **Première chose à lire : [la sécurité](07-securite.md).** À lire avant d'allumer le robot, même si vous êtes pressé.

## Sommaire

**A. Installation (technicien)**

1. [Vue d'ensemble et glossaire](01-vue-ensemble.md)
2. [Matériel et branchements](02-materiel.md)
3. [Réseau](03-reseau.md)
4. [Installer le Jetson](04-installer-jetson.md)
5. [Installer le PC VR](05-installer-pc-vr.md)

**B. Utilisation (opérateur)**

6. [Allumer et éteindre](06-allumer-eteindre.md)
7. [Sécurité](07-securite.md)
8. [La page web](08-page-web.md)
9. [Le casque VR](09-casque-vr.md)
10. [cuRobo ou Doosan : quel contrôleur et quand](10-curobo-doosan.md)
11. [Dépannage](11-depannage.md)

**C. Annexes**

12. [Scénario « le canard dans la boîte » et références](12-annexes.md)

## Informations encore à compléter

Les endroits marqués **À COMPLÉTER** dans le texte attendent ces informations :

| Information | Chapitre |
|---|---|
| Nom de l'image Docker | 4 |
| Contenu exact du fichier `docker-compose.yml` | 4 |
| Version de SteamVR et réglages de la zone de jeu | 5 |
| Nom exact et lieu de distribution du `.exe` Unity | 5 |
| Emplacement des arrêts d'urgence physiques | 7 |
| Emplacement et gestion du code PIN | 8 |
| Capture de la **page web sur le robot en marche** : modules « Prêt » et images des caméras. Les autres captures web sont faites (certaines en état simulé, signalé sous l'image). | 6 |
| Captures **depuis le casque** (celles des chapitres 5 et 9 viennent de l'éditeur Unity), fenêtre SteamVR | 5, 9 |
| Photos du matériel et schéma de câblage | 1, 2 |

Les captures Unity sont dans [img/](img/). Elles ont été prises dans l'éditeur, pas dans le casque.
