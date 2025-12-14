# Predicción del precio de la leche en Colombia usando modelos econométricos y de aprendizaje automático

## Resumen

El precio de la leche presenta una dinámica compleja influenciada por factores macroeconómicos, energéticos y estructurales. Este trabajo evalúa distintos modelos de predicción de series temporales —econométricos, híbridos y de aprendizaje automático— con el fin de identificar el enfoque más adecuado para distintos escenarios temporales. Se consideran cuatro escenarios (E1–E4), encontrándose que el modelo Prophet, aplicado al escenario E4 (Gasolina), ofrece el mejor desempeño predictivo.

---

## 1. Introducción

La predicción de precios agropecuarios es un problema central en economía aplicada, planeación sectorial y análisis de riesgos. En Colombia, el precio de la leche ha estado sujeto a choques estructurales derivados de la pandemia, variaciones en el precio de la energía, inflación y tipo de cambio.

Este trabajo propone un enfoque comparativo entre modelos clásicos de series temporales y modelos modernos de machine learning, evaluados bajo distintos escenarios económicos.

---

## 2. Datos y escenarios analizados

Se construyó una serie temporal mensual del precio promedio de la leche, junto con variables exógenas macroeconómicas y energéticas. Se definieron cuatro escenarios:

- **E1 – Completo:** Serie total disponible  
- **E2 – Pre-pandemia:** Hasta 2018  
- **E3 – Post-pandemia:** Desde 2019  
- **E4 – Gasolina:** Subperiodo reciente con fuerte influencia del precio de combustibles  

Todas las series fueron agregadas mensualmente usando el día 1 de cada mes y se incluyeron rezagos de variables exógenas.

---

## 3. Metodología

### 3.1 Modelos econométricos clásicos

#### ARIMAX

El modelo ARIMAX extiende el ARIMA tradicional incluyendo variables exógenas:

$$
y_t = \sum_{i=1}^p \phi_i y_{t-i} + \sum_{j=1}^q \theta_j \varepsilon_{t-j} + \beta X_t + \varepsilon_t
$$

Permite incorporar información externa, pero asume relaciones lineales y estabilidad estructural.

#### SARIMAX

SARIMAX añade componentes estacionales:

$$
ARIMA(p,d,q) \times (P,D,Q)_s
$$

Este modelo es adecuado para series con estacionalidad regular, aunque puede ser inestable ante quiebres estructurales.

---

### 3.2 Prophet (modelo seleccionado)

Prophet modela la serie como una suma de componentes estructurales:

$$
y(t) = g(t) + s(t) + h(t) + \varepsilon_t
$$

donde:

-  /[ g(t) ]/ : tendencia flexible (lineal o logística con *changepoints*)
-  s(t) : estacionalidad modelada mediante series de Fourier
-  h(t) : efectos de variables exógenas
-  /[ \varepsilon_t ]/: ruido

#### Tendencia con puntos de cambio

$$
g(t) = (k + a(t)^T \delta)t + (m + a(t)^T \gamma)
$$

Esto permite capturar cambios estructurales sin necesidad de redefinir el modelo.

#### Estacionalidad

$$
s(t) = \sum_{n=1}^{N} \left( a_n \cos \frac{2\pi nt}{P} + b_n \sin \frac{2\pi nt}{P} \right)
$$

Prophet es especialmente adecuado para series económicas con rupturas y cambios de régimen.

---

### 3.3 Modelos adicionales evaluados

#### Rolling SARIMAX

Se implementó un esquema de ventana móvil de 36 meses, recalibrando el modelo continuamente:

$$
\hat{y}_{t+1} = f(y_{t}, y_{t-1}, X_t, X_{t-1})
$$

Este enfoque simula un escenario operativo realista, aunque presenta alta varianza del error.

---

#### ElasticNet con rezagos

ElasticNet combina penalizaciones L1 y L2:

$$
\minimize_{\beta} \left\{ \|y - X\beta\|^2 + \lambda \left( \alpha \|\beta\|_1 + (1-\alpha)\|\beta\|_2^2 \right) \right\}
$$

Ventajoso por su interpretabilidad, pero limitado al asumir relaciones lineales.

---

#### XGBoost

XGBoost es un modelo de boosting basado en árboles:

$$
\mathcal{L} = \sum_i l(y_i, \hat{y}_i) + \sum_k \Omega(f_k)
$$

Capaz de capturar relaciones no lineales, pero requiere grandes volúmenes de datos y presenta menor interpretabilidad económica.

---

## 4. Resultados

### 4.1 Comparación por escenarios (modelos clásicos)

| Escenario | Modelo | MAE | RMSE | R² |
|----------|--------|-----|------|----|
| E4 Gasolina | Prophet | **31.10** | **43.87** | **0.62** |
| E4 Gasolina | ARIMAX | 152.99 | 178.13 | -5.24 |
| E4 Gasolina | SARIMAX | 614.55 | 652.65 | -82.78 |

---

### 4.2 Modelos adicionales – Escenario E4

| Modelo | MAE | RMSE | R² |
|------|------|------|----|
| Rolling SARIMAX | 89.93 | 113.98 | -11.56 |
| ElasticNet | 195.82 | 210.23 | -30.18 |
| XGBoost | 83.74 | 94.66 | -5.32 |
| **Prophet** | **31.10** | **43.87** | **0.62** |

---

## 5. Discusión

Los modelos de machine learning no superaron a Prophet debido a:

- Tamaño limitado de la muestra
- Alta presencia de quiebres estructurales
- Importancia de modelar explícitamente tendencia y estacionalidad

ElasticNet mostró el peor desempeño, evidenciando la no linealidad del problema. XGBoost y Rolling SARIMAX mejoran respecto a SARIMAX clásico, pero presentan inestabilidad y bajo poder explicativo.

Prophet logra el mejor equilibrio entre flexibilidad, estabilidad y capacidad predictiva.

---

## 6. Conclusiones

Prophet es el modelo más adecuado para la predicción del precio de la leche en el escenario E4. Su estructura aditiva y su manejo explícito de cambios estructurales lo hacen superior frente a enfoques puramente econométricos o de machine learning en contextos de series cortas y volátiles.

---
