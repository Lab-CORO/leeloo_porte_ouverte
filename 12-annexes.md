# 12. Annexes

## A. Scénario de démonstration : « le canard dans la boîte »

**Objectif du visiteur** : saisir un canard en plastique et le placer dans une boîte.

**Préparation (opérateur)** : suivre la check-list du [chapitre 6](06-allumer-eteindre.md). Vérifier :

- tous les modules sont **Prêts** ;
- le mode de commande est **« Casque VR »** ;
- le contrôleur du casque est **cuRobo** (mode Expert : le bouton « cuRobo » est actif) ;
- sur l'écran du PC VR, le voyant indique **« ROS : Connecté »** ;
- le canard et la boîte sont posés à leur place, à portée du bras.

**Déroulé**

| Étape | Visiteur | Opérateur |
|---|---|---|
| 1 | Met le casque, fait le tutoriel (déplacement, téléportation) | Explique les règles ([chapitre 9](09-casque-vr.md)) |
| 2 | Se téléporte près du robot, **appuie sur la gâchette** : le bras suit sa main | Surveille le bras, main près du STOP |
| 3 | Amène la pince au-dessus du canard et la **ferme** pour le saisir | Surveille la pince |
| 4 | Soulève un peu le canard | Constate que le bras **ne suit plus** bien (cuRobo voit le canard comme un obstacle) |
| 5 | **Relâche la gâchette** | Attend l'arrêt complet, menu **Expert** → coche **« Mode expert »**, clique **« Doosan »** |
| 6 | **Reprend la gâchette**, amène le canard au-dessus de la boîte | **Regarde le bras** (aucun contrôle d'obstacles) |
| 7 | **Ouvre la pince** pour déposer | |
| 8 | Relâche la gâchette, retire le casque | Remet **cuRobo**, mode **« Aucun »** |

**Si une alarme apparaît** (par exemple près de 240° sur J4) : relâcher la gâchette, **STOP** si nécessaire, puis **Continuer** (jaune) ou la procédure du [chapitre 7](07-securite.md) (rouge).

**Durée** : prévoir 5 à 10 minutes par visiteur, plus le changement de visiteur.

> **À COMPLÉTER** : position de départ du canard et de la boîte (schéma coté), consigne si le canard tombe.

## B. Aide-mémoire

| Je veux… | Je fais… |
|---|---|
| Arrêter tout de suite | **STOP** ; danger : arrêt d'urgence physique |
| Reprendre après un arrêt | Mode **« Aucun »**, puis choisir de nouveau le mode, puis relâcher et réappuyer sur la gâchette |
| Passer en Doosan | Gâchette relâchée, bras arrêté, **Expert** → panneau Casque VR → **Doosan** |
| Revenir à cuRobo | Même chose avec **cuRobo** |
| Reprendre la main sur la page | **Piloter depuis ce poste** |
| Réinitialiser | Expert → **Réinitialiser…** (PIN) |
| Préparer le visiteur suivant | PC VR : **Maj + R**, puis remettre **cuRobo** |
| Le bras ne suit pas alors que tout est « Prêt » | PC VR : le voyant doit être « ROS : Connecté », et « Envoi actif » quand la gâchette est appuyée |

## C. Pour aller plus loin (développeurs)

Ces documents supposent de connaître ROS 2. Ils ne sont pas dans ce dépôt : ils se trouvent dans le workspace ROS du Jetson, sous `/home/ros2_ws/src/`.

| Document | Contenu |
|---|---|
| `leeloo_vr/README.md` | Passerelle VR : topics, services, modèle de sécurité, paramètres, dépannage |
| `leeloo/README.md` | Nœuds d'exécution, fichiers de lancement, URDF, profil DDS |
| `leeloo_web/config/stacks.yaml` | Liste des modules supervisés et leurs conditions de « Prêt » |
| `leeloo_vr/config/vr_bridge.yaml` | Paramètres de sécurité (zone de travail, vitesses, contrôleur par défaut) |

> Le fichier `vr_unity_ros_doosan/README.md` décrit une **ancienne version** du système (ROS Humble, Ubuntu 20.04) : ne pas le suivre pour installer.

## D. Points à contrôler dans le code ou sur le robot

À vérifier par le technicien avant de publier cette documentation :

1. **Contrôleur par défaut de la page web** : `controller_web` vaut encore `doosan`, ce qui grise la commande articulaire à la souris par défaut (voir le [chapitre 8](08-page-web.md)).
2. **`profile.xml`** : contient l'adresse d'un PC personnel (`192.168.50.65`) et celle de la base mobile (`192.168.50.163`), non utilisée. À nettoyer pour le dépôt public.
3. **`fake_vr_publisher`** : voir le TODO dans `leeloo_vr/README.md` (pose publiée sur un mauvais topic).
