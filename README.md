# Predicción del Precio de la Leche

Descripción
-----------
Proyecto para analizar y predecir el precio promedio por litro de leche usando técnicas de series temporales y modelos de machine learning. El objetivo es preparar datos, generar variables exógenas y rezagos, entrenar modelos (ARIMAX, SARIMAX, Prophet, RandomForest, ElasticNet, XGBoost), evaluar su desempeño y comparar resultados.

Contenido del repositorio
-------------------------
- Data/  
  - base_con_dolar.csv  
  - base_con_dolar_gasolina.csv  

- notebooks/  
  - modelos_1.ipynb: exploración básica, RandomForest por escenarios, comparación de métricas y descomposición de la serie.  
  - modelo_2.ipynb: preparación avanzada de series, ARIMAX/SARIMAX/Prophet, rolling forecast, ElasticNet y XGBoost.

- Las demas carpetas y archivos son del procesamiento de los datos 

Estructura y flujo de trabajo
-----------------------------
1. Coloca los CSV en la carpeta `Data/`.
2. Revisa e instala dependencias como `statsmodels`, `prophet`, `xgboost`, `scikit-learn`, `matplotlib`, `pandas`, `seaborn`.
3. Abre los notebooks con Jupyter Lab/Notebook:
   - jupyter lab  (o jupyter notebook)
4. Ejecuta celdas en orden:
   - modelos_1.ipynb para exploración, RandomForest y descomposición.  
   - modelo_2.ipynb para pipelines de series temporales, SARIMAX/ARIMAX/Prophet, rolling forecasts y modelos ML.

Descripción técnica (resumen)
-----------------------------
- Preparación de datos:
  - Construcción de columna `FECHA` desde `año` y `mes`.
  - Renombrado a `LECHE`, `DOLAR`, `IPC` y variables de combustibles.
  - Agregación mensual, creación de rezagos (L1, L2), interpolación de NaNs.
- Modelos:
  - ARIMAX: SARIMAX sin estacionalidad con exógenas.
  - SARIMAX: SARIMAX con componente estacional (12 meses).
  - Prophet: con regresores exógenos.
  - RandomForest / ElasticNet / XGBoost: enfoque supervisado con train/test split (80/20, sin shuffle).
  - Rolling forecast SARIMAX: validación walk-forward por ventanas móviles.
- Métricas:
  - MAE, MSE, RMSE, R² y visualizaciones comparativas.
- Salidas y artefactos:
  - `resultados_modelos_leche.csv`, `metricas_modelos_E4.csv` (métricas por modelo).
  - Gráficas de validación y comparación.

# Configuración
## Linux y MacOS

Ejecute los siguientes comandos en el terminal:

```bash
python3 -m venv .venv
source .venv/bin/activate
source setup.sh
```
## Windows

Ejecute los siguientes comandos en el terminal:

```bash
python3 -m venv .venv
.venv\Scripts\activate
setup
```