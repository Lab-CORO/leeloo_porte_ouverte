# 2. Matériel et branchements

## Liste du matériel

| Matériel | Rôle | Branché où |
|---|---|---|
| **Bras Doosan M1013** et son **contrôleur** | Le robot qui bouge | Câble réseau vers le routeur |
| **Teach pendant** Doosan | Tablette de commande du bras, arrêt d'urgence | Câble au contrôleur |
| **Pince Robotiq 2F-85** | Saisit les objets | Sur le bras. **À COMPLÉTER** : câble de liaison vers le Jetson (USB-série ?) |
| **Jetson** | Cerveau du robot (conteneur Docker) | **Câble réseau** vers le routeur |
| **Caméra Kinect** | Voit la scène (fixe) | USB vers le Jetson |
| **Caméra RealSense D405** | Voit la pince (sur le poignet) | USB vers le Jetson |
| **Routeur du robot** | Réseau local, attribue les adresses (DHCP) | Alimenté, câbles aux machines |
| **PC VR** (Windows) | Exécute l'application Unity et SteamVR | **Câble réseau** vers le routeur |
| **Casque HTC Vive** + 2 manettes + stations de base | Casque du visiteur | Au PC VR (câble casque) |
| **Tablette ou PC de l'opérateur** | Affiche la page web de supervision | Wi-Fi du routeur ou câble |
| **Plastique « canard »** et **boîte** | Objets de la démonstration | Sur la table |

> La **base mobile Ridgeback** existe sur le robot mais **n'est pas utilisée** : ne pas la brancher ni la démarrer.

> **À COMPLÉTER** : alimentations, références des câbles, fixation précise des caméras.
> **Capture à ajouter** : schéma de câblage (routeur au centre, avec les 3 machines branchées en ethernet).

## Règles de branchement

1. Le **Jetson** et le **PC VR** doivent être branchés **en ethernet** (câble) au routeur du robot. Le Wi-Fi n'est pas fiable pour la VR : les pertes de paquets ajoutent de la latence avec les cameras et le control du robot.
2. Le **contrôleur Doosan** est lui aussi branché en ethernet au même routeur.
3. La **tablette de l'opérateur** peut être en Wi-Fi, mais sur le **réseau du routeur du robot**.
4. Les caméras sont branchées en **USB 3** au Jetson, **avant** de démarrer le Jetson.
5. Ne **jamais débrancher** une caméra pendant que le robot tourne. Si c'est arrivé : voir le [dépannage](11-depannage.md).
