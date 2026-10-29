# Utilitaires GCE Electronics

Ce dépôt réunit un ensemble d'**utilitaires freeware** pour les appareils de [GCE Electronics](https://www.gce-electronics.com) : **IPX800 (V1/V2/V3, V4, V5)**, **EcoDevices (ED3 et RT2)**, **X-Pool** et **X-Display V2**, ainsi que des outils réseau (scan, broker MQTT, passerelle Modbus, hub de navigation).

Ils ont été développés avec l'aide de l'IA **Claude Code**.

- **Licence** : MIT (voir [LICENSE](LICENSE))
- **Deux familles d'outils** :
  - **Outils web** : fichiers `.html` autonomes, sans installation, à ouvrir dans un navigateur
  - **Outils Java** : fichiers `.jar` avec interface graphique (Java requis)

---

## Sommaire

1. [Inventaire rapide](#inventaire-rapide)
2. [Outils Java (JAR)](#outils-java-jar)
3. [Testeurs d'API (API Deck)](#testeurs-dapi-api-deck)
4. [Tableaux de bord MQTT (MQTT Deck)](#tableaux-de-bord-mqtt-mqtt-deck)
5. [X-Display V2 : écran virtuel](#x-display-v2--écran-virtuel)
6. [Outils de création](#outils-de-création)
7. [Mini mode d'emploi](#mini-mode-demploi)
8. [Activer les WebSockets sur Mosquitto](#activer-les-websockets-sur-mosquitto)
9. [Dépannage](#dépannage)
10. [Licence](#licence)

---

## Inventaire rapide

| Fichier | Type | Cible | Rôle |
|---|---|---|---|
| `Gce-ScanDevice_v2.33.jar` | Java | Réseau local | Détecte les appareils GCE (scan UDP) |
| `GCE-Broker-Monitor-2_5_2.jar` | Java | MQTT | Broker MQTT local intégré + moniteur de trafic |
| `GCE-Modbus2Mqtt.jar` | Java | EcoDevices 3 | Passerelle Modbus (via API HTTP) vers MQTT |
| `GCE-Hub-1_0_7.jar` | Java | Tous | Hub de navigation : pages, appareils et outils |
| `GCE_IPX800V3_Api-Deck v1.html` | Web | IPX800 V1/V2/V3 | Testeur d'API M2M et API v1 |
| `GCE_IPX800V4_Api-Deck v4.html` | Web | IPX800 V4 | Testeur d'API (par catégories) |
| `GCE_IPX800V4_Api-Deck v5.html` | Web | IPX800 V4 | Testeur d'API (par groupes, avec panneau Élément) |
| `GCE_IPX800V5_Api-Deck v2.html` | Web | IPX800 V5 | Testeur d'API REST complet |
| `GCE_IPX800V5_Widget-Studio_v1.html` | Web | IPX800 V5 | Éditeur visuel de widgets de dashboard |
| `GCE_ED3_Api-Deck v2.1.html` | Web | EcoDevices 3 | Testeur d'API |
| `GCE_ED3_Mqtt-Deck v2.html` | Web | EcoDevices 3 | Tableau de bord MQTT |
| `GCE_ED3_Modbus-Generator v1.html` | Web | EcoDevices 3 | Générateur de configuration Modbus JSON |
| `GCE_EDRT2_Api-Deck v1.html` | Web | EcoDevices RT2 | Testeur d'API |
| `GCE_X-POOL_Mqtt-Deck v1.html` | Web | X-Pool | Tableau de bord MQTT |
| `GCE_X-DISPLAY-V2_Mqtt-Deck v1.html` | Web | X-Display V2 | Tableau de bord MQTT (API V3.2) |
| `GCE_X-DISPLAY-V2_Virtuel_v1.html` | Web | X-Display V2 | Écran virtuel (version du 24/05/2026) |
| `GCE_X-DISPLAY-V2_Virtuel_v1.1.html` | Web | X-Display V2 | Écran virtuel (version du 25/09/2026) |

---

## Outils Java (JAR)

Lancement : `java -jar NomDuFichier.jar` (ou double-clic). Interface graphique, **français / anglais**.

| JAR | Java minimum |
|---|---|
| `Gce-ScanDevice_v2.33.jar` | Java 8 |
| `GCE-Broker-Monitor-2_5_2.jar` | Java 8 |
| `GCE-Hub-1_0_7.jar` | Java 8 |
| `GCE-Modbus2Mqtt.jar` | **Java 11** |

### Gce-ScanDevice (v2.33)

Scanner réseau pour **détecter les appareils GCE** sur le réseau local (envois UDP).

- Tableau de résultats : adresse IP, nom d'hôte, adresse MAC, port, produit, informations complémentaires
- **Scan** du réseau local, **scan d'un sous-réseau** (IP de début / IP de fin), **scan d'une plage**
- **Scan automatique** de la plage `192.168.x.x`, avec arrêt possible à tout moment
- Bouton **Flash Device** pour l'accès à la mise à jour du firmware d'un appareil détecté
- Export des résultats
<img width="690" height="480" alt="image" src="https://github.com/user-attachments/assets/3f13b5d7-ab69-4b36-bf26-e09ff53e9a1b" />
<img width="693" height="753" alt="image" src="https://github.com/user-attachments/assets/b8ae837f-d612-4f3d-ab75-0ec5c0559184" />


### GCE-Broker-Monitor (v2.5.2)

**Broker MQTT local intégré** (basé sur Moquette) accompagné d'un **moniteur de trafic** en temps réel. Il évite d'installer Mosquitto pour faire des tests.

- Démarrage / arrêt du broker avec paramétrage du **port MQTT**, du **port WebSocket** (utile pour les MQTT Deck), du **SSL** (keystore / truststore) et de l'**authentification** (utilisateur / mot de passe)
- Affichage de tous les messages : topic, payload complet, QoS, flag *retained*
- **Filtres** par topic et par payload, filtres *Retained* / *QoS 2*, vue des **topics racine**
- Pause / reprise, auto-scroll, effacement, historisation
- **Scénarios** : moteur de règles pour réagir aux messages
- Copie du topic ou du payload, **export CSV**, statistiques (total, affichés, buffer)
<img width="690" height="341" alt="image" src="https://github.com/user-attachments/assets/9fa78df7-886a-4235-b2c2-62eb29b9ea46" />
<img width="886" height="641" alt="image" src="https://github.com/user-attachments/assets/812d15a7-e0a9-4afb-81db-c06a4b9d9c72" />
<img width="615" height="612" alt="image" src="https://github.com/user-attachments/assets/b8457034-baaf-4f2d-9022-f311875463d7" />


### GCE-Modbus2Mqtt

**Passerelle Modbus vers MQTT** pour l'EcoDevices 3 : elle interroge périodiquement l'API HTTP de l'appareil (lecture des registres Modbus) et publie les valeurs sur un broker MQTT.

- Connexion API : IP de l'appareil, URL de l'API, clé API, fréquence d'interrogation (avec fréquence dynamique)
- Connexion MQTT : broker, topic racine, Client ID, utilisateur / mot de passe, QoS, *Retain*
- Configuration Modbus : **chargement du fichier JSON** produit par `GCE_ED3_Modbus-Generator`, choix de l'appareil et de l'esclave
- Tableau des registres (commande, adresse, nombre, type, lecture/écriture, valeur, topic MQTT), bouton **Tester** pour voir la requête API, sauvegarde de la configuration
<img width="1086" height="693" alt="image" src="https://github.com/user-attachments/assets/730d74cb-e691-4d18-a0a2-df08ed3f260d" />
<img width="690" height="391" alt="image" src="https://github.com/user-attachments/assets/1acefbeb-c6f3-4c07-9d34-dbe7ad834d88" />
<img width="615" height="260" alt="image" src="https://github.com/user-attachments/assets/20d6974b-89bf-4a6d-b2d2-d11159c34583" />


### GCE-Hub (v1.0.7)

**Page d'accueil des outils GCE** : un arbre de pages classées en **Dashboards**, **Appareils** et **Outils**.

- Double-clic sur une page pour l'ouvrir dans le navigateur
- Ajout, modification, suppression, **import / export** de la liste de pages
- **Détection automatique des fichiers HTML** du dossier (bouton *Charger HTML*)
- Boutons de lancement des JAR voisins : **Scanner réseau**, **Broker MQTT**, **Pont Modbus↔MQTT (ED3)**
- Affiche l'IP locale de la machine

> Placez les JAR (`Gce-ScanDevice`, `GCE-Broker-Monitor`, `GCE-Modbus2mqtt`) **dans le même dossier** que `GCE-Hub` pour que les boutons de lancement les trouvent.
<img width="690" height="446" alt="image" src="https://github.com/user-attachments/assets/ef754d3d-c78e-4c0b-9d5f-365288046d5a" />

---

## Testeurs d'API (API Deck)

Équivalents d'un client de type Postman, préchargés avec les commandes de chaque appareil. Choix du protocole (HTTP / HTTPS), saisie de l'IP et de la clé API, bouton **Tester**, liste de commandes classées, zone de **réponse** copiable et **historique** des requêtes.

| Fichier | Appareil | Particularités |
|---|---|---|
| `GCE_IPX800V3_Api-Deck v1.html` | IPX800 V1 / V2 / V3 | Deux modes : **M2M** et **API v1**. Le M2M passe par un petit **serveur proxy Node.js** (HTTP vers socket TCP, port 9870), dont le guide d'installation et le code sont inclus dans l'outil |
| `GCE_IPX800V4_Api-Deck v4.html` | IPX800 V4 | Commandes `Get=` / `Set` (R, D, A, C, VI, VO, VA, PW, FP, SMS, X-010V, X-ENO, X-PWM, X-DMX, etc.), navigation par **catégories**, panneaux redimensionnables, réglages mémorisés dans le navigateur |
| `GCE_IPX800V4_Api-Deck v5.html` | IPX800 V4 | Mêmes commandes, présentées par **groupes** avec un panneau **Élément** pour détailler la commande sélectionnée |
| `GCE_IPX800V5_Api-Deck v2.html` | IPX800 V5 | API REST : méthodes GET / POST / PUT / DELETE, paramètres et corps JSON, **génération `curl` et `fetch`**, filtre par ID, gestion des **instances** (voir, créer, modifier, supprimer) avec rafraîchissement **Live**. Objets couverts : IPX, ANA, STR, calendriers, comparateurs, compteurs, fonctions, e-mails, MQTT, parseur JSON, watchdogs, planifications, thermostats, minuteries, Modbus, extensions X-xxx, météo, Hue, X-Pool, etc. |
| `GCE_ED3_Api-Deck v2.1.html` | EcoDevices 3 | Testeur avec méthodes GET / POST / PUT / DELETE. Catégories : état ED3 et plugins, relais (on / off / toggle), **logs et courbes** (Core Logger), **TIC / Linky**, **tarifs**, planning / calendrier. Lien vers la documentation officielle de l'API ED3 |
| `GCE_EDRT2_Api-Deck v1.html` | EcoDevices RT2 | Commandes `Get`, `Set`, `Clear` et `Toggle` (relais, sorties virtuelles, compteurs, fil pilote, actionneurs EnOcean, etc.) |
<img width="690" height="327" alt="image" src="https://github.com/user-attachments/assets/ab63d870-d29e-4596-82bf-55e43f1ea268" />
<img width="690" height="342" alt="image" src="https://github.com/user-attachments/assets/18a739e3-5efb-479e-adff-c1eb0d513542" />
<img width="690" height="327" alt="image" src="https://github.com/user-attachments/assets/4f96d896-25b2-490c-8674-e5c62260e42b" />
<img width="690" height="327" alt="image" src="https://github.com/user-attachments/assets/9be59311-0b28-4778-bc0f-d19c945fbf72" />
<img width="690" height="327" alt="image" src="https://github.com/user-attachments/assets/e90b8305-18bb-42de-b446-bf8bb936ba09" />
<img width="690" height="327" alt="image" src="https://github.com/user-attachments/assets/c5174513-166f-43a5-b8ef-8b846df9f0cf" />

---

## Tableaux de bord MQTT (MQTT Deck)

Clients MQTT **dans le navigateur** (via WebSocket). Ils s'abonnent aux topics de l'appareil (**SUB**), peuvent publier des commandes (**PUB**) et intègrent une **référence des topics** et le mode d'emploi pour activer les WebSockets sur Mosquitto.

| Fichier | Appareil | Contenu |
|---|---|---|
| `GCE_ED3_Mqtt-Deck v2.html` | EcoDevices 3 | TIC / Linky, relais embarqués, tores (puissance instantanée), impulsions, totaux instantanés, **index**, **prix** (cumuls en euros) et puissance par compteur, extensions X-8R, table de correspondance des 30 compteurs |
| `GCE_X-POOL_Mqtt-Deck v1.html` | X-Pool | Référence API V1.0 : commandes des sorties (PUB), états des sorties, mesures analogiques, notifications / alertes, entrées capteurs |
| `GCE_X-DISPLAY-V2_Mqtt-Deck v1.html` | X-Display V2 | Référence API V3.2 : configuration générale (extinction écran, verrouillage, etc.), gestion des écrans, types d'écrans, commandes par écran |

Champs de connexion : URL WebSocket du broker (`ws://IP:9001`), Client ID, utilisateur, mot de passe et identifiant de l'appareil (pour les topics de la forme `x-display_<ID>` ou `x-pool_<ID>`).

<img width="690" height="342" alt="image" src="https://github.com/user-attachments/assets/c555ede3-2d53-4098-9539-30c59574b505" />
<img width="690" height="327" alt="image" src="https://github.com/user-attachments/assets/0bd5c28e-fbc2-4163-84fc-9e0e26ebdf59" />
<img width="517" height="245" alt="image" src="https://github.com/user-attachments/assets/f29df1e5-7d4a-4c2e-8b69-42249cc803ec" />
<img width="517" height="245" alt="image" src="https://github.com/user-attachments/assets/e683001d-b88f-4eef-9314-a1afd8842ec8" />
<img width="517" height="245" alt="image" src="https://github.com/user-attachments/assets/d39b1650-7a01-4962-8685-d679b0a19702" />
<img width="517" height="245" alt="image" src="https://github.com/user-attachments/assets/9c8e3e47-05bb-494a-a6fd-677380814e53" />
<img width="323" height="323" alt="image" src="https://github.com/user-attachments/assets/9ebe5ce4-a6cd-4d1a-90cc-2b88cd4aa4d9" />


---

## X-Display V2 : écran virtuel

Simulateur du **X-Display V2** dans le navigateur, connecté au broker MQTT : il se comporte comme l'écran réel et permet de **concevoir et tester les écrans sans l'appareil**.

- Gestion des écrans avec **import / export JSON** et bouton **Déployer**
- État de l'écran (allumé / éteint), verrouillage, délai de veille (minutes)
- **Modes MQTT** : Normal (TX + RX), RX seul, Local (sans MQTT)
- Zone **Trafic MQTT** (écoute, copie, effacement), **historique** et **publication manuelle** (topic + payload)
- Référence des topics X-Display V2 intégrée

| Fichier | Version | Nouveautés |
|---|---|---|
| `GCE_X-DISPLAY-V2_Virtuel_v1.html` | v1 (24/05/2026) | Version initiale |
| `GCE_X-DISPLAY-V2_Virtuel_v1.1.html` | v1.1 (25/09/2026) | Ajoute l'**écran Message** (notification MQTT plein écran avec bouton de validation) et un panneau **Envoi MQTT** avec option *Retenu* |

---

## Outils de création

### GCE_IPX800V5_Widget-Studio_v1

Éditeur visuel pour fabriquer des **widgets HTML de dashboard** pour l'IPX800 V5.

- **Bibliothèque** de widgets filtrable (IPX800 V5 / autres) à placer sur un **canvas** (aimantation, zoom)
- Types disponibles : interrupteurs et boutons relais, impulsion, voyant LED, entrées TOR, jauges, barres, LCD, curseurs analogiques, graphiques, compteurs, sondes THL, thermomètre, CO2, pression, variateur, lumière Hue, fil pilote, thermostat, volet roulant, PWM, météo (actuelle et prévisions 7 jours), arc solaire, minuterie, chronomètre, GSM, texte live, et widgets pour les **extensions** (X-4FP, X-4VR, X-8R, X-24D, X-8D, X-Dimmer, X-THL, X-PWM, X-Display, X-8AI, X-Meter)
- Panneau de **propriétés** (libellé, couleurs, effet glow, rayon, police, ID IO / ANA GCE, unité, min / max)
- **Code du widget** éditable avec outils : décommenter, optimiser, compresser, purger les styles, copier
- **Sauvegarder / charger** un projet, **aperçu dashboard** (zoom 50 / 75 / 100 %), **export HTML**
- Tient compte des zones utiles de l'IPX800 V5 (150×150, 150×300, 300×300)
<img width="1920" height="910" alt="image" src="https://github.com/user-attachments/assets/f274d5f1-0881-4123-8c86-985f5b7528ce" />

### GCE_ED3_Modbus-Generator v1

Générateur de **fichier JSON de configuration Modbus** pour l'EcoDevices 3, à utiliser avec `GCE-Modbus2Mqtt`.

- Nom de la configuration (31 caractères max), numéro de périphérique (0 à 255)
- Type de conversion : aucune, complément à 2 ou IEEE float ; fréquence de lecture (ms)
- Jusqu'à **20 commandes** par objet Modbus (**32 objets** possibles) : nom, adresse (hex), nombre, direction, mode, type
- **Aperçu JSON** avec validation, boutons **Copier**, **Importer** et **Télécharger**
<img width="690" height="327" alt="image" src="https://github.com/user-attachments/assets/220b78e1-85a7-4b63-9f66-5a4410599253" />


---

## Mini mode d'emploi

### Outils web (`.html`)

1. **Télécharger** le fichier (GitHub : ouvrir le fichier, puis *Download raw file*) ou cloner le dépôt.
2. **Ouvrir** le fichier par double-clic : il s'affiche dans le navigateur.
3. **Renseigner l'appareil** :
   - *API Deck* : protocole, IP de l'appareil, clé API ;
   - *MQTT Deck* et *Écran virtuel* : URL WebSocket du broker, identifiants, ID de l'appareil, puis **Connecter**.
4. **Utiliser** : choisir une commande puis **Tester / Envoyer** (API Deck), ou observer et publier les topics (MQTT Deck).

> Pour l'IPX800 V1/V2/V3 en mode M2M, démarrez d'abord le proxy Node.js décrit dans l'outil.

### Outils Java (`.jar`)

1. Vérifier Java : `java -version` (Java 8 minimum, **Java 11** pour `GCE-Modbus2Mqtt`).
2. Lancer l'outil :
   ```bash
   java -jar Gce-ScanDevice_v2.33.jar
   ```
   (ou double-clic sur le fichier `.jar`)
3. Pour tout centraliser, lancer `GCE-Hub-1_0_7.jar` depuis le dossier contenant les autres JAR et les fichiers HTML.

### Scénarios courants

- **Retrouver l'IP d'un appareil** : `Gce-ScanDevice`, bouton *Scan*.
- **Tester un broker MQTT sans l'installer** : `GCE-Broker-Monitor`, bouton *Démarrer* (port WebSocket 9001 pour les MQTT Deck).
- **Publier les compteurs Modbus de l'ED3 sur MQTT** : créer le JSON avec `GCE_ED3_Modbus-Generator`, puis le charger dans `GCE-Modbus2Mqtt`.
- **Créer un widget pour l'IPX800 V5** : `GCE_IPX800V5_Widget-Studio_v1`, puis *Exporter HTML*.

---

## Activer les WebSockets sur Mosquitto

Les MQTT Deck et l'écran virtuel se connectent en **WebSocket**. Avec Mosquitto, ajoutez dans `mosquitto.conf` :

```
listener 1883
protocol mqtt

listener 9001
protocol websockets

allow_anonymous true
persistence true
persistence_location /mosquitto/data/
```

> `allow_anonymous true` est réservé aux tests : sécurisez ensuite votre broker avec une authentification.

Exemple avec Docker :

```bash
docker run -d --name mosquitto --restart unless-stopped \
  -p 1883:1883 -p 9001:9001 \
  -v ~/mosquitto/config:/mosquitto/config:ro \
  -v ~/mosquitto/data:/mosquitto/data \
  eclipse-mosquitto
```

Dans l'outil, saisir ensuite `ws://VOTRE_IP:9001`. Alternative plus simple : utiliser le broker intégré de `GCE-Broker-Monitor`.

---

## Dépannage

| Problème | Piste |
|---|---|
| L'appareil ne répond pas dans l'API Deck | Vérifier l'IP, le protocole, la clé API et que l'API est activée sur l'appareil |
| Requêtes bloquées par le navigateur (CORS / contenu mixte) | Essayer HTTP plutôt que HTTPS, ou un autre navigateur, depuis le même réseau |
| Le MQTT Deck ne se connecte pas | Vérifier le port **WebSocket** (9001) et les identifiants |
| Le `.jar` ne démarre pas | Vérifier la version de Java (11 pour `GCE-Modbus2Mqtt`) |
| Le Hub ne lance pas un outil | Placer les JAR dans le même dossier que `GCE-Hub` |
| Aucun appareil trouvé par ScanDevice | Vérifier que le PC est sur le même sous-réseau que les appareils |

---

## Licence

Distribué sous licence **MIT** : voir le fichier [LICENSE](LICENSE).

*Ces utilitaires sont indépendants et non officiels ; GCE Electronics n'est pas responsable de leur utilisation.*
