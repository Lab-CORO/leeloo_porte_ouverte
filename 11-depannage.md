# 11. Dépannage

Chaque ligne suit le même schéma : **ce qu'on voit → pourquoi → quoi faire**. Commencer par la partie « opérateur » ; la partie « technicien » demande un terminal.

## Pour l'opérateur (sans terminal)

| Ce qu'on voit | Pourquoi | Quoi faire |
|---|---|---|
| La page web ne s'ouvre pas | Mauvaise adresse, tablette sur un autre réseau, Jetson pas démarré | Vérifier que la tablette est sur le réseau du robot, que le Jetson est allumé depuis 2 minutes, et l'adresse (voir le [chapitre 3](03-reseau.md)). |
| Un module est **Échec** | Le module n'a pas pu démarrer | Ouvrir le **Journal**, cliquer sur **Copier**, appeler le technicien. Ne pas redémarrer en boucle. |
| **Planificateur** reste « démarrage » | Le GPU se prépare : jusqu'à 2 minutes la première fois | Attendre. Après 2 minutes sans « Prêt » : Échec, voir ci-dessus. |
| Le planificateur devient **orange** avec « CUDA context corrupted » | Le calcul GPU a planté | **Arrêter puis redémarrer** le module Planificateur (mode Expert). |
| **Driver Doosan** en échec | Contrôleur éteint, pas en mode remote, câble réseau débranché | Vérifier le contrôleur et le teach pendant (mode **remote**), le câble réseau, puis redémarrer le module. |
| L'image d'une **caméra** est grise ou absente | Caméra débranchée ou module Caméras en échec | Vérifier le câble USB. Redémarrer le module « Caméras » (mode Expert). Si c'est une caméra rebranchée à chaud : voir plus bas (technicien). |
| « Casque VR » est refusé (mode de commande) | Bras en mouvement, ou un module nécessaire n'est pas prêt | Attendre l'arrêt complet, vérifier que **Planificateur**, **Pince et exécution**, **Driver Doosan** et **Casque VR** sont Prêts. |
| Le casque est refusé en mode Doosan | Le driver ou l'exécution n'est pas prêt | Vérifier les mêmes modules. |
| **« Observation seule »**, rien ne marche | Un autre poste pilote | Cliquer sur **« Piloter depuis ce poste »**. |
| Le visiteur appuie sur la gâchette, rien ne bouge | Mode ≠ « Casque VR », module VR arrêté, ou gâchette déjà enfoncée quand le mode a changé | Vérifier le mode, **relâcher puis réappuyer**. |
| Le bras ne suit plus quand le canard est saisi | cuRobo gêné par le canard | Passer en **Doosan** ([chapitre 10](10-curobo-doosan.md)). |
| « Arrêté : J4 près de 240° » | Limite de protection du Doosan | Relâcher la gâchette, repartir dans l'autre sens. |
| **Bandeau jaune** | Arrêt de protection du bras | **Continuer** ([chapitre 7](07-securite.md)). |
| **Bandeau rouge** | Panne du bras | **Couper le driver Doosan**, teach pendant, **Redémarrer** ([chapitre 7](07-securite.md)). |
| « Surveillance du bras perdue » | La page web ne reçoit plus l'état du bras | Le mode est repassé à « Aucun ». Vérifier le Driver Doosan, puis redonner la main. |
| Un module refuse de s'arrêter ou de redémarrer | Processus bloqués | Mode Expert → **Réinitialiser** (code PIN), puis **Tout démarrer**. |
| Le visiteur se sent mal | — | Casque retiré, mode « Aucun », pause. |

## Pour le technicien (avec un terminal sur le Jetson)

| Symptôme | Cause | Commande / action |
|---|---|---|
| Le conteneur ne tourne pas | Pas démarré ou planté | `docker compose ps`, puis `docker compose logs -f`. Le relancer : `docker compose up -d`. |
| Tout est « Prêt » mais le bras ne bouge pas | La cadence de commande ne correspond pas à celle de cuRobo (`command_period` et `interpolation_dt`) | Regarder les logs du module « Pince et exécution » : le message `Rejecting trajectory: incoming dt` indique ce défaut. |
| Message « failed to create domain » au lancement d'un nœud | Trop de processus ROS orphelins | Page web : **Réinitialiser** (PIN) ou, dans le conteneur, `ros2 run leeloo kill-ros-orphans`. |
| « No RealSense devices were found » après avoir rebranché la D405 | Le conteneur ne voit pas les nouveaux fichiers `/dev/video*` | Dans le conteneur, en root : `ros2 run leeloo sync-video-nodes`. La vraie cause : `/dev` doit être partagé avec le conteneur dans `docker-compose.yml` (voir le [chapitre 4](04-installer-jetson.md)). |
| Unity ne se connecte pas, erreur « port 10000 déjà utilisé » | Le module VR a été arrêté et relancé trop souvent en peu de temps | `docker compose restart`, puis tout redémarrer. |
| Unity ne se connecte pas | Mauvaise IP saisie, câble PC VR débranché, module « Casque VR » arrêté | Vérifier l'IP dans l'application, le câble, et que « Casque VR » est Prêt. |
| `set_source` refusé : `arm still moving` | Bras mesuré en mouvement | Attendre l'arrêt complet. |
| `set_source` refusé : `execute_trajectory action not available` | Planificateur arrêté | Démarrer le module « Planificateur de trajectoire ». |
| Le casque ne s'affiche pas / SteamVR rouge | Problème du Vive | Voir le chapitre [PC VR](05-installer-pc-vr.md) ; vérifier les stations de base. |

> Pour une analyse plus fine (topics ROS, état de `vr_bridge`), voir `leeloo_vr/README.md`, section *Troubleshooting*.

## Avant d'appeler le technicien

Noter :

1. **L'heure** et ce que le visiteur faisait.
2. **Le message** affiché sur la page (copie d'écran) et l'état des modules.
3. Le texte du **Journal** (bouton « Copier »).
4. Ce qui a déjà été essayé.
