# Actividad 04 — Clustering: Modelos Lineales y No Lineales con Métricas de Validación

Implementación y comparación de tres algoritmos de clustering aplicados sobre datasets reales y sintéticos. Se evalúa el rendimiento de cada modelo usando métricas de validación externa e interna para determinar cuál se adapta mejor a cada tipo de estructura de datos.

## Descripción

El clustering es una técnica de aprendizaje no supervisado que agrupa datos sin etiquetas en conjuntos homogéneos. En esta actividad se analiza cómo la naturaleza lineal o no lineal de cada algoritmo afecta su capacidad para detectar correctamente los grupos, dependiendo de la geometría de los datos.

## Datasets utilizados

| Dataset | Tipo | Clusters | Descripción |
|---|---|---|---|
| **Iris** | Real | 3 | 150 muestras, 4 características (sépalo y pétalo). Clusters casi linealmente separables |
| **Moons** | Sintético | 2 | Dos medias lunas entrelazadas. Estructura curva no lineal |
| **Circles** | Sintético | 2 | Dos círculos concéntricos. El caso más desafiante para modelos lineales |

## Modelos entrenados

### K-Means — Modelo Lineal
Agrupa datos minimizando la distancia al centroide de cada cluster. Sus fronteras de decisión son hiperplanos (lineales), por lo que asume clusters convexos y esféricos. Funciona bien en Iris pero falla completamente en Moons y Circles.

**Hiperparámetros críticos:**
- `n_clusters` — el más importante; se determina con el Método del Codo
- `n_init` — número de inicializaciones aleatorias (≥10 recomendado)
- `random_state` — reproducibilidad

### DBSCAN — Modelo No Lineal
Agrupa por densidad: un punto pertenece a un cluster si hay suficientes vecinos dentro de un radio definido. No requiere especificar el número de clusters y detecta outliers automáticamente (etiqueta -1).

**Hiperparámetros críticos:**
- `eps` — radio de vecindad; muy sensible: pequeño genera ruido excesivo, grande fusiona clusters
- `min_samples` — mínimo de puntos para formar un núcleo de cluster

### Spectral Clustering — Modelo No Lineal
Construye un grafo de similitud entre puntos, calcula los vectores propios del Laplaciano del grafo y aplica K-Means en ese espacio transformado. Captura estructuras no convexas que serían imposibles de separar linealmente.

**Hiperparámetros críticos:**
- `n_clusters` — número de grupos esperados
- `affinity` — tipo de grafo (`nearest_neighbors` para datos no lineales)
- `gamma` — ancho de banda del kernel si se usa `affinity='rbf'`

## Métricas de validación

### Externas (requieren etiquetas reales)
| Métrica | Rango | Mejor valor | Descripción |
|---|---|---|---|
| Adjusted Rand Index (ARI) | -1 a 1 | 1.0 | Compara etiquetas reales vs predichas, corregido por azar |
| V-Measure | 0 a 1 | 1.0 | Media armónica de Homogeneidad y Completitud |

### Internas (no requieren etiquetas)
| Métrica | Mejor valor | Descripción |
|---|---|---|
| Silhouette Score | Cerca de 1 | Mide qué tan bien separado está cada punto de su cluster |
| Davies-Bouldin Index | Cerca de 0 | Mide similitud promedio entre clusters |
| Elbow Method | — | Determina el k óptimo para K-Means graficando la inercia |

## Resultados resumidos

| Dataset | Mejor modelo | ARI aprox. | Por qué |
|---|---|---|---|
| Iris | Spectral / K-Means | ~0.75 | Datos casi linealmente separables |
| Moons | Spectral / DBSCAN | ~0.99 | Forma curva no lineal |
| Circles | Spectral Clustering | ~1.00 | Círculos concéntricos separables en espacio espectral |

## Archivos del repositorio

| Archivo | Dataset |
|---|---|
| `clustering_dataset_Iris.ipynb` | Iris |
| `moonsModeloMetricas.ipynb` | Moons |
| `clustering_dataset_circle.ipynb` | Circles |
| `Informe_Actividad04_Clustering.docx` | Informe completo |

## Tecnologías

Python · scikit-learn · matplotlib · numpy · pandas · Google Colab
