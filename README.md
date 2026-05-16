# 🎬 dm-recommender — Système de Recommandation de Films MovieLens

> **Projet de Fouille de Données — Master FAVD**  
> Année universitaire : 2025–2026  
> Encadrant : M. Mezni Haythem

---

## 📌 Description

Système de recommandation de films construit sur le dataset **MovieLens Small**, combinant deux approches complémentaires de fouille de données :

- **Fouille tabulaire** : clustering des utilisateurs par profil de notation (K-Means + Clustering Hiérarchique Agglomératif)
- **Fouille de graphes** : modélisation des interactions utilisateur-film sous forme de graphe biparti (centralité, PageRank, détection de communautés Louvain)

**Dataset** : [MovieLens Small](https://grouplens.org/datasets/movielens/latest/) — ~100 836 évaluations, 610 utilisateurs, 9 724 films

---

## 👩‍💻 Auteurs

| Nom | Prénom |
|-----|--------|
| DJlassi | Safa |
| Boujemaa | Ines |

---

## 🗂️ Structure du projet

```
dm-recommender-safajlassi-inesboujemaa/
├── data/                        # Dataset MovieLens (téléchargé automatiquement)
├── notebooks/
│   └── dm_recommender.ipynb     # Notebook principal (Phases 0 → 3)
├── results/                     # CSV exportés et images générées
│   ├── user_clusters_kmeans.csv
│   ├── user_clusters_hierarchique.csv
│   ├── film_centralite.csv
│   ├── film_pagerank.csv
│   └── communautes.csv
├── report/
│   └── rapport_fouille_donnees.pdf              # Rapport écrit (~13 pages)
├── requirements.txt
└── README.md
```

---

## ⚙️ Installation et exécution

### Option 1 — Google Colab (recommandé)

1. Ouvrir [Google Colab](https://colab.research.google.com/)
2. Importer le fichier `notebooks/dm_recommender.ipynb`
3. Exécuter toutes les cellules : `Exécution > Tout exécuter`
4. Le dataset est téléchargé automatiquement à la première exécution

### Option 2 — Local (VS Code / Jupyter)

```bash
git clone https://github.com/votre-compte/dm-recommender-safajlassi-inesboujemaa.git
cd dm-recommender-safajlassi-inesboujemaa
pip install -r requirements.txt
jupyter notebook notebooks/dm_recommender.ipynb
```

---

## 📦 Dépendances

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

> Installer toutes les dépendances en une commande : `pip install -r requirements.txt`

---

## 🔬 Description des phases

| Phase | Contenu |
|-------|---------|
| **Phase 0** | Chargement, nettoyage, fusion des fichiers CSV, EDA, construction de la matrice utilisateurs × films |
| **Phase 1** | Clustering K-Means (méthode Elbow + Silhouette, k=4) + Clustering Hiérarchique (Ward), comparaison des deux algorithmes, recommandation par cluster |
| **Phase 2** | Construction du graphe biparti (networkx), centralité de degré & betweenness, PageRank, détection de communautés (Louvain), recommandation par graphe |
| **Phase 3** | Comparaison globale Clustering vs Graphe — résultats détaillés dans `rapport/rapport.pdf` |

---

## 📊 Résultats clés

### Clustering

| Algorithme | Score Silhouette (k=4) | Temps d'exécution |
|---|---|---|
| **K-Means** ★ | **0.0725** | 0.30 s |
| Hiérarchique (Ward) | 0.0256 | 0.03 s |

- **k optimal retenu** : k = 4 (meilleur compromis silhouette / clusters informatifs)
- **k automatique** (silhouette max brute) : k = 2

### Fouille de graphes

- **Nœuds** : 7 286 (200 utilisateurs + 7 086 films)
- **Arêtes** : 47 886 (notes ≥ 3.5)
- **Communautés détectées (Louvain)** : 9 — modularité = 0.2714
- **Film le plus central** : *The Matrix* (1999) — degree centrality = 0.01894

### Exemple de recommandations — Utilisateur 1

| Approche | Top recommandation |
|---|---|
| K-Means | Paths of Glory (1957) — note moy. 4.90 |
| Hiérarchique | Paths of Glory (1957) — note moy. 4.83 |
| Graphe (Louvain + PageRank) | Pulp Fiction (1994) — PageRank 0.001066 |

> Les deux approches sont **complémentaires** : 0 film en commun entre clustering et graphe pour l'utilisateur 1.

---

## 🖼️ Visualisations générées

| Fichier image | Description |
|---|---|
| `eda_overview.png` | Distribution des notes, notes par utilisateur, top 20 films |
| `clustering_elbow_silhouette.png` | Méthode Elbow (inertie) + Score de Silhouette pour k=2 à 10 |
| `clustering_pca2d.png` | Visualisation PCA 2D des 4 clusters K-Means |
| `clustering_hierarchique_pca2d.png` | Visualisation PCA 2D des 4 clusters hiérarchiques |
| `dendrogramme.png` | Dendrogramme Ward (50 utilisateurs échantillonnés) |
| `comparaison_clustering.png` | Recommandations K-Means vs Hiérarchique côte à côte |
| `recommandations_cluster.png` | Top 8 recommandations K-Means pour l'utilisateur 1 |
| `graphe_centralite.png` | Top 15 films par Degree Centrality |
| `graphe_visualisation.png` | Sous-graphe biparti : hubs films et utilisateurs |

---

## 📁 Fichiers CSV exportés (`results/`)

| Fichier | Contenu |
|---|---|
| `user_clusters_kmeans.csv` | Assignation de chaque utilisateur à son cluster K-Means |
| `user_clusters_hierarchique.csv` | Assignation de chaque utilisateur au clustering hiérarchique |
| `film_centralite.csv` | Degree centrality et betweenness de chaque film |
| `film_pagerank.csv` | Score PageRank de chaque film |
| `communautes.csv` | Appartenance de chaque nœud à sa communauté Louvain |

---

## 📚 Références

1. Harper & Konstan. *The MovieLens Datasets: History and Context.* ACM TIIS, 2015. https://grouplens.org/datasets/movielens/
2. Pedregosa et al. *scikit-learn: Machine Learning in Python.* JMLR 12, 2011.
3. Hagberg et al. *NetworkX: Network Analysis in Python.* https://networkx.org
4. Aynaud. *python-louvain: Louvain Community Detection.* https://python-louvain.readthedocs.io
5. Blondel et al. *Fast unfolding of communities in large networks.* JSTAT, 2008.
6. Page et al. *The PageRank Citation Ranking.* Stanford InfoLab, 1999.
