# Projet — Segmentation et classification des clients

## Non supervisé

* **Clustering** : regrouper les clients selon leurs comportements sans avoir de target prédéfinie.
* **K-means** : crée `k` groupes autour de centroïdes.
* **DBSCAN** : regroupe les points selon leur densité et identifie le bruit (`-1`).
* **Silhouette Score** : mesure la qualité/séparation des clusters.
* **Inertie** : mesure la distance entre les points et leur centroïde.
* **Méthode du coude (Elbow)** : aide à choisir `k`.
* **PCA** : réduction de dimension avant le clustering.
* **Variance** : mesure la dispersion / les différences présentes dans les données.
* **Explained variance ratio** : proportion de variance capturée par chaque composante PCA.
* **Variance cumulée** : somme progressive des variances expliquées.

## Feature Story 1 — EDA

* Importation et exploration du dataset.
* Vérification des dimensions, types et valeurs.
* Recherche des valeurs manquantes et doublons.
* **Skewness** : mesure de l'asymétrie d'une distribution.
* **Histogramme + KDE** : visualisation des distributions.
* **Corrélation de Pearson** : relation linéaire entre deux variables.
* **Boxplot / IQR** : détection des outliers.

## Feature Story 2 — Prétraitement

```text
df
→ df_clean
→ df_prepare_clustering
→ log1p
→ StandardScaler
→ PCA
→ variance expliquée
→ variance cumulée
```

* `df_clean` : dataset propre de référence.
* `df_prepare_clustering` : copie dédiée au clustering.
* `log1p` : transformation logarithmique.
* `StandardScaler` : standardisation.
* `PCA` : réduction des dimensions.
* `explained_variance_ratio_` : variance capturée par chaque PC.
* `cumulative_variance` : variance cumulée.
* Seuil PCA : **80% de variance cumulée**.
* Garder le nombre minimal de composantes permettant de dépasser **80%**.

### PCA — À retenir

```text
7 features originales
        ↓
      PCA
        ↓
PC1 → plus grande variance
PC2 → deuxième plus grande variance
PC3 → troisième...
        ↓
Variance cumulée
        ↓
Nombre de PC retenues
```

## K-means
- Test de `2 à 5` composantes PCA.
- Test de `k = 2 à 7`.
- Calcul de l’inertie et du Silhouette Score.

## Résultat actuel
- Meilleure combinaison testée :
  - `PCA = 2`
  - `k = 3`
  - `Silhouette = 0.448719`
