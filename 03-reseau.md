# 3. Réseau

## Principe

Tout le monde est branché au **routeur du robot**. Ce routeur attribue automatiquement une adresse (IP) à chaque appareil (**DHCP**). Pour que le robot fonctionne, trois choses doivent connaître la bonne adresse :

| Qui doit connaître quoi | Où c'est configuré |
|---|---|
| L'**application Unity** (PC VR) doit connaître l'IP du **Jetson** | Champ « IP » dans l'application Unity |
| Le **Jetson** doit connaître l'IP du **contrôleur Doosan** | Fichier `leeloo/launch/doosan.launch.py`, argument `host` (valeur actuelle : `192.168.50.100`) |
| La **tablette** doit connaître l'IP du **Jetson** | Adresse `http://<IP du Jetson>:8080` à saisir dans le navigateur |

## Adresses actuelles

| Appareil | Adresse | Rôle |
|---|---|---|
| Jetson | `192.168.50.12` | Robot (conteneur) |
| Contrôleur Doosan | `192.168.50.100` | Commande du bras |
| PC VR | `192.168.50.67` | Application Unity |
| Tablette de l'opérateur | _attribuée par le routeur_ | Page web |


Les adresses du Jetson et du contrôleur Doosan doivent **toujours être les mêmes** : dans l'interface du routeur, il faut **réserver** une adresse (« bail DHCP statique » ou « DHCP reservation ») pour chacune, associée à son adresse MAC.



## Ouvrir la page web depuis la tablette

Dans le navigateur, saisir :

```
http://192.168.50.12:8080
```

Remplacer `192.168.50.12` par l'IP du Jetson si elle a changé. Mettre l'adresse en **favori**.

## Si le routeur est remplacé (ou si une adresse change)

Un routeur neuf ou un autre réseau change les adresses. Procédure :

1. **Brancher** tout le matériel au nouveau routeur (Jetson, contrôleur Doosan, PC VR).
2. Dans l'interface du routeur, **noter** l'IP du Jetson et celle du contrôleur Doosan, puis **réserver** ces adresses (bail DHCP statique).
3. **Contrôleur Doosan** : Le doosan impose sont adresse comme static. il faut juste s'assurer qu'aucun autre materiel utilise cette adresse: `192.168.50.100`
4. **Unity** : sur le PC VR, ouvrir l'application et saisir la nouvelle IP du Jetson dans le champ « IP du bridge ».
5. **Tablette** : mettre à jour le favori avec la nouvelle IP.
6. Vérifier : voir la [check-list de démarrage](06-allumer-eteindre.md). Si la page web ne s'ouvre pas, voir le [dépannage](11-depannage.md).

> Le Jetson est lancé en mode « réseau de l'hôte » (`network_mode: host`) : le conteneur a donc **la même IP que le Jetson**, il n'y a pas d'adresse à configurer à part pour le conteneur.

## Ports utilisés

| Port | Sens | Utilité |
|---|---|---|
| `8080` | tablette → Jetson | Page web |
| `10000` | PC VR → Jetson | Connexion de l'application Unity |

Un pare-feu ou un réseau d'entreprise qui bloque ces ports empêche le fonctionnement : c'est pourquoi on utilise un routeur dédié, sans internet obligatoire (internet n'est nécessaire que pour télécharger l'image Docker).
