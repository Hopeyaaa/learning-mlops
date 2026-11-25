# Introduction au MLOps — réponses aux activités

## Le cycle MLOps retenu

Le cours réunit les cycles de Google Cloud et de Microsoft en sept étapes :

1. Cadrer le besoin et les critères de réussite
2. Collecter et comprendre les données
3. Préparer les données
4. Entraîner et expérimenter
5. Évaluer et valider (le modèle doit battre une référence)
6. Déployer
7. Surveiller et améliorer, puis reprendre le cycle

À ce stade du cours, mon travail se situe au **niveau 0 de maturité** (notebooks et opérations manuelles). Les prochains TP visent le niveau 2 (entraînement automatisé et suivi des expériences).

## Question de départ

> Avec un excellent score sur des données historiques, que manque-t-il pour décider d'utiliser le modèle ?

- **Problème de données** : les variables utilisées doivent être disponibles au moment de la prédiction. La durée réelle, ou la distance réellement parcourue, n'existe pas avant le départ : si le modèle les utilise, son score est trompeur (fuite de données). Les données récentes peuvent aussi être différentes des données historiques.
- **Problème technique** : un fichier de modèle n'est pas un service. Il faut une API, la validation des entrées, une version identifiée, des journaux et un comportement défini en cas d'erreur.
- **Problème d'usage** : il faut savoir qui utilise la prédiction, à quel moment, et quelle erreur est acceptable. Une erreur moyenne faible peut cacher de gros retards sur certains trajets.

## Activité A — comprendre « modele_final_v3.joblib, l'erreur est de 3 »

| Question | Preuve associée |
|---|---|
| Quelle métrique vaut 3, dans quelle unité, et par rapport à quelle référence ? | Critère métier et règle de référence |
| Sur quelles données le modèle a-t-il été entraîné ? D'où viennent-elles ? | Schéma, provenance, empreinte du fichier |
| Avec quel code, quels paramètres et quelles versions de bibliothèques ? | Code, paramètres, versions et journal |
| L'erreur est-elle mesurée sur des données non vues à l'entraînement ? Comment ont-elles été séparées ? | Séparation documentée et métriques |
| Ce fichier est-il bien la version testée et utilisée ? Fonctionne-t-il encore aujourd'hui ? | Identifiant d'artefact, tests, mesures et alertes |

## Activité B — environnement

- **Image et conteneur** : l'image est le modèle figé (fichiers et dépendances) ; le conteneur est une instance de cette image en cours d'exécution. Plusieurs conteneurs peuvent partir de la même image.
- **Pourquoi installer une bibliothèque sur sa machine ne l'installe pas dans le conteneur** : le conteneur a son propre système de fichiers et son propre Python, construits à partir de l'image. Une bibliothèque doit être déclarée dans l'image (Dockerfile) pour y être disponible.
- **Mon environnement** : Anaconda sur macOS, environnement `mlops` (Python 3.12) déclaré dans `environment.yml`. Ses dépendances sont versionnées dans le dépôt pour pouvoir le recréer.

## Ce qu'il faut conserver pour reproduire une expérience

1. Le code exécuté et sa version
2. Les données utilisées et leur découpage
3. Les paramètres et les graines aléatoires
4. Les versions de Python et des dépendances

Reproduire un résultat montre que l'expérience est stable. Cela ne prouve pas que le modèle fonctionnera sur d'autres données ou une autre période.
