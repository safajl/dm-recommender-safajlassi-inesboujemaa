# 🎬 dm-recommender — Système de Recommandation MovieLens

Projet de Fouille de Données — Master FAVD  
**Approches** : Clustering (K-Means) + Fouille de graphes (networkx + Louvain)  
**Dataset** : [MovieLens Small](https://grouplens.org/datasets/movielens/latest/) (~100k ratings, 610 users, 9724 films)

---

## Structure du projet

```
dm-recommender-nom1-nom2/
├── data/                  # Dataset MovieLens (téléchargé automatiquement)
├── notebooks/
│   └── dm_recommender.ipynb   # Notebook principal (Phases 0-1-2)
├── results/               # CSV et images générés
├── report/
│   └── rapport.pdf        # Rapport écrit (5 pages)
├── requirements.txt
└── README.md
```

---

## Installation et exécution

### Option 1 — Google Colab (recommandé)

1. Ouvrir [Google Colab](https://colab.research.google.com/)
2. Importer le fichier `notebooks/dm_recommender.ipynb`
3. Exécuter toutes les cellules (`Runtime > Run all`)
4. Le dataset est téléchargé automatiquement à la première exécution

### Option 2 — Local (VS Code / Jupyter)

```bash
git clone https://github.com/votre-compte/dm-recommender-safajlassi-inesboujemaa.git
cd dm-recommender-safajlassi-inesboujemaa
pip install -r requirements.txt
jupyter notebook notebooks/dm_recommender.ipynb
```

---

## Dépendances

```
pandas
numpy
scikit-learn
networkx
matplotlib
seaborn
python-louvain
scipy
```

---

## Description des phases

| Phase | Contenu |
|-------|---------|
| **Phase 0** | Chargement, nettoyage, fusion, EDA, matrice utilisateurs × films |
| **Phase 1** | K-Means clustering, méthode Elbow + Silhouette, recommandation par cluster |
| **Phase 2** | Graphe biparti networkx, centralité, PageRank, Louvain, recommandation par graphe |
| **Phase 3** | Comparaison des deux approches — voir `report/rapport.pdf` |

---

## Résultats clés

- **k optimal** (K-Means) : déterminé par score de silhouette maximal
- **Communautés détectées** (Louvain) : voir `results/communautes.csv`
- **Films hubs** : voir `results/film_centralite.csv`
- **Exemple de recommandations** : disponibles dans le notebook (cellules Phase 1.4 et Phase 2.5)

---

## Auteurs

- Nom 1 — Jlassi safa
- Nom 2 — Boujemaa ines

Encadrant :Mr Mezni Haythem
Année universitaire : 2025-2026
