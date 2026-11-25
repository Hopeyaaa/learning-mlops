# learning-mlops

Travaux pratiques du parcours MLOps (M2 Expert IT, Bases de données et Big Data — IRIS École).
Fil conducteur : prédire la durée des trajets des taxis jaunes de New York.

## Avancement

| TP | Contenu | Fichiers |
|---|---|---|
| 01 — Introduction | Cycle de vie ML, niveaux de maturité, réponses aux activités | `docs/01-intro-reponses.md` |
| 02 — Environnement | Dépôt GitHub, environnement Conda `mlops` (Python 3.12) | `environment.yml` |
| 03 — Docker local | Installation de Docker Desktop et vérification | — |
| 04 — Jupyter et Parquet | Lecture des données Yellow Taxi, lecture de plusieurs mois | `notebooks/04-read-parquet.ipynb` |

## Reproduire l'environnement

```bash
conda env create -f environment.yml
conda activate mlops
python -m ipykernel install --user --name mlops --display-name "Python (mlops)"
```

## Données

Les fichiers Parquet sont téléchargés par le notebook dans `data/`, qui est ignoré par Git.
Source : [NYC Taxi and Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page).
