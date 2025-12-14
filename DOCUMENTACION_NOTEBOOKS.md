# Documentación de Notebooks

Este documento resume los notebooks (.ipynb) presentes en el proyecto y proporciona: propósito, entradas y salidas, dependencias principales y notas de ejecución. No se modifican las celdas de código en los notebooks al generar esta documentación.

---

**Resumen de notebooks**

- **modelos_1.ipynb**: [modelos_1.ipynb](modelos_1.ipynb#L1)
  - Propósito: Entrenar modelos RandomForest para predecir el precio promedio por litro de leche y comparar distintos escenarios (serie completa, pre-pandemia, post-pandemia, extensión con gasolina).
  - Entradas: `Data/base_con_dolar.csv`, `Data/base_con_dolar_gasolina.csv`.
  - Salidas: Visualizaciones (gráficos comparativos, importancia de variables) y un DataFrame `res_df` con métricas; no guarda CSV por defecto.
  - Dependencias: `pandas`, `numpy`, `matplotlib`, `seaborn`, `statsmodels`, `scikit-learn`.
  - Notas: Función `entrenar_modelo()` con RandomForest; descomposición de la serie temporal con `seasonal_decompose`.

- **modelo_2.ipynb**: [modelo_2.ipynb](modelo_2.ipynb#L1)
  - Propósito: Implementa un flujo de análisis avanzado y predicción de la serie (ARIMAX, SARIMAX, Prophet, ElasticNet, XGBoost, rolling SARIMAX) con evaluación y comparación por escenarios (E1/E2/E3/E4).
  - Entradas: `Data/base_con_dolar.csv`, `Data/base_con_dolar_gasolina.csv`.
  - Salidas: `Resultados/resultados_modelos_leche.csv`, `Resultados/metricas_modelos_E4.csv` (CSV exportados), gráficas comparativas.
  - Dependencias: `pandas`, `numpy`, `matplotlib`, `statsmodels`, `prophet`, `scikit-learn`, `xgboost`.
  - Notas: Contiene funciones de preparación de series (rezagos), funciones de entrenamiento para ARIMAX/SARIMAX/Prophet/ElasticNet/XGBoost y evaluación mediante MAE/MSE/RMSE/R².

- **exploracion/analisis.ipynb**: [exploracion/analisis.ipynb](exploracion/analisis.ipynb#L1)
  - Propósito: Exploración inicial de datos, visualizaciones de evolución temporal y correlaciones entre variables (precio leche, dólar, IPC, combustibles).
  - Entradas: `Data/base_con_dolar.csv`, `Data/base_con_dolar_gasolina.csv`.
  - Salidas: Visualizaciones (series temporales, heatmaps, scatter plots) y análisis de correlación.
  - Dependencias: `pandas`, `matplotlib`, `seaborn`.
  - Notas: Útil para entender relaciones entre variables y para selección previa de features.

- **exploracion/proyecto-prediccion-precio-leche-ipc.ipynb**: [exploracion/proyecto-prediccion-precio-leche-ipc.ipynb](exploracion/proyecto-prediccion-precio-leche-ipc.ipynb#L1)
  - Propósito: Explorar la serie `leche_yarumal_ipc_limpio.csv` (Yarumal) y analizar correlación entre IPC y precio de la leche.
  - Entradas: `Data/leche_yarumal_ipc_limpio.csv` (en el notebook se usa ruta de Kaggle, ejemplo: `/kaggle/input/yarumal-leche/leche_yarumal_ipc_limpio.csv`).
  - Salidas: Gráficas de evolución temporal y correlaciones.
  - Dependencias: `pandas`, `matplotlib`, `seaborn`.
  - Notas: Se usa dataset focalizado por municipio (Yarumal) para hacer visualizaciones y análisis local.

- **limpieza/unificacion.ipynb**: [limpieza/unificacion.ipynb](limpieza/unificacion.ipynb#L1)
  - Propósito: Unir datasets por año y mes y generar las bases finales usadas por los modelos.
  - Entradas: `Data/leche_yarumal_ipc_limpio.csv`, `Dolar/promedio_mensual_dolar.csv`, `Gasolina/promedios_mensuales_productos.csv`.
  - Salidas: `Data/base_con_dolar.csv`, `Data/base_con_dolar_gasolina.csv`.
  - Dependencias: `pandas`.
  - Notas: Realiza merges por año/mes y guarda los outputs en `Data/`.

- **limpieza/dolar_limpieza.ipynb**: [limpieza/dolar_limpieza.ipynb](limpieza/dolar_limpieza.ipynb#L1)
  - Propósito: Limpiar el archivo histórico del dólar y generar promedios mensuales.
  - Entradas: `Dolar/wilkinsonpc-dolar-historico-2010-01-03-al-2025-12-03.csv`.
  - Salidas: `Dolar/promedio_mensual_dolar.csv`.
  - Dependencias: `pandas`.
  - Notas: Agrupa por año/mes y obtiene promedio mensual de precio del dólar para que quede alineado con las series mensuales de leche.

- **limpieza/gasolina_limpieza.ipynb**: [limpieza/gasolina_limpieza.ipynb](limpieza/gasolina_limpieza.ipynb#L1)
  - Propósito: Procesar datos de EDS (ventas por estación/producto) y producir promedios mensuales por tipo de combustible (corriente, extra, biodiésel).
  - Entradas: `Gasolina/EDS.csv`.
  - Salidas: `Gasolina/promedios_mensuales_productos.csv`.
  - Dependencias: `pandas`.
  - Notas: Normaliza meses, limpia precios y genera pivote por producto.

- **limpieza/proyecto-prediccion-precio-leche-ipc-limpieza.ipynb**: [limpieza/proyecto-prediccion-precio-leche-ipc-limpieza.ipynb](limpieza/proyecto-prediccion-precio-leche-ipc-limpieza.ipynb#L1)
  - Propósito: Limpieza y estandarización de múltiples ficheros Excel de precios mayoristas de leche (2013–2024) y de IPC, generando datasets consolidados.
  - Entradas: varios archivos Excel por año y archivo de IPC (ej.: `/kaggle/input/leche/series-historicas-precios-mayoristas-leche-20xx.xlsx`, `/kaggle/input/indice-ipc/IPC_Indice_de_Precios_al_Consumidor_2013-2024`).
  - Salidas: `precio_leche_2013_2024.csv`, `ipc_2013_2024.csv`, `leche_yarumal_ipc_limpio.csv` (y luego se usa en `Data/` tras procesamiento).
  - Dependencias: `pandas`, `numpy`, `unicodedata`, `re`.
  - Notas: Implementa funciones avanzadas para limpiar encabezados inconsistentes, normalizar columnas y concatenar varias hojas por año.

---

**Dependencias generales (sugeridas)**

- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn
- statsmodels
- prophet
- xgboost

Puedes instalarlas (ejemplo) con:

```bash
pip install -r requirements.txt
```

---

**Cómo ejecutar los notebooks**

- Opción interactiva: Abrir con `jupyter lab` o `jupyter notebook` y ejecutar celdas manualmente.
- Opción por lotes (sin interactivo): ejecutar todos los notebooks con `nbconvert` (solo si las celdas deben ejecutarse sin intervención):

```bash
jupyter nbconvert --to notebook --execute modelos_1.ipynb --inplace
jupyter nbconvert --to notebook --execute modelo_2.ipynb --inplace
# etc.
```

- Recomendación para reproducibilidad: ejecutar primero los notebooks en `limpieza/` (limpieza y unificación), luego los de `exploracion/` y por último los de `modelo(s)`.

