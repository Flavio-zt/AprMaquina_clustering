# Actividad 04 — Clustering: Modelos Lineales y No Lineales

Comparación de algoritmos de clustering (K-Means, DBSCAN, Spectral Clustering) sobre tres datasets, con métricas de validación externa e interna.

## Datasets utilizados

- **Iris** — dataset clásico con 3 clases y 4 características
- **Moons** — dataset sintético con dos medias lunas entrelazadas
- **Circles** — dataset sintético con dos círculos concéntricos

## Modelos entrenados

| Modelo | Naturaleza | Observación |
|---|---|---|
| K-Means | Lineal | Funciona bien en datos convexos (Iris), falla en formas curvas |
| DBSCAN | No lineal | Basado en densidad, detecta outliers automáticamente |
| Spectral Clustering | No lineal | Mejor rendimiento general en los 3 datasets |

## Métricas aplicadas

**Externas** (requieren etiquetas reales): Adjusted Rand Index (ARI), V-Measure

**Internas** (no requieren etiquetas): Silhouette Score, Davies-Bouldin Index, Elbow Method

## Archivos

| Archivo | Dataset |
|---|---|
| `clustering_dataset_Iris.ipynb` | Iris |
| `moonsModeloMetricas.ipynb` | Moons |
| `clustering_dataset_circle.ipynb` | Circles |

## Tecnologías

Python · scikit-learn · matplotlib · numpy · pandas
