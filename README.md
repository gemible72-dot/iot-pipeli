  # 🚀 Projet Connectivité IoT - Pipeline de Données Docker

Ce dépôt contient l'infrastructure complète pour la collecte, le traitement et la visualisation de données capteurs en temps réel en utilisant une architecture micro-services avec **Docker**.

## 🏗️ Architecture du Pipeline
- **Mosquitto** : Broker MQTT pour la réception des messages.
- **Node-RED** : Orchestration et transformation des données (ETL).
- **InfluxDB 2.7** : Base de données orientée séries temporelles pour le stockage.
- **Grafana** : Interface de visualisation et système d'alerte.

---

## 📝 Réponses aux Questions du TP

### A. Infrastructure & Docker
1. **Rôle de `depends_on`** : Définit l'ordre de démarrage. Node-RED attend que Mosquitto soit prêt pour éviter les erreurs de connexion au lancement.
2. **Volumes nommés** : Assurent la **persistance**. Sans eux, vos tableaux de bord Grafana et vos données InfluxDB seraient effacés à chaque arrêt du conteneur.
3. **`restart: unless-stopped`** : Permet au service de redémarrer automatiquement après un crash ou un reboot du PC, sauf si on l'arrête manuellement.
4. **Réseau Bridge vs Host** : Le mode *Bridge* crée un réseau virtuel isolé (sécurisé), tandis que le mode *Host* utilise directement l'adresse IP de l'ordinateur.

### B. Node-RED & Données
5. **Utilité du Topic** : Il permet d'identifier l'origine de la donnée (quel utilisateur et quel capteur) grâce au découpage de la chaîne de caractères.
6. **Measurement InfluxDB** : C'est le nom de la catégorie de donnée stockée (ex: "temperature").
7. **Tags vs Fields** : Les *Tags* sont indexés pour des recherches rapides (ex: ID du capteur), alors que les *Fields* contiennent les valeurs numériques réelles.

### C. Grafana & Supervision
8. **Alerte Grafana** : Contrairement à une alerte locale, elle permet d'analyser l'historique des données avant de déclencher une notification, évitant les faux positifs.
9. **`aggregateWindow`** : Cette fonction permet de regrouper les données par intervalles de temps pour rendre les graphiques plus fluides et lisibles.

---

## ⚙️ Installation et Lancement
1. Clonez ce dépôt.
2. Assurez-vous que le fichier `.env` contient vos identifiants InfluxDB.
3. Lancez l'infrastructure :
   ```bash
   docker compose up -d
   ```
4. Accédez aux interfaces :
   - Node-RED : `http://localhost:1880`
   - Grafana : `http://localhost:3000`
   - InfluxDB : `http://localhost:8086`

---
*Projet réalisé dans le cadre du TP Connectivité IoT - UFHB 2025.*
