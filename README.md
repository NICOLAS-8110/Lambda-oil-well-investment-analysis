<img width="1280" height="640" alt="WhatsApp Image 2026-11-17 at 3 00 46 PM (10)" src="https://github.com/user-attachments/assets/8aaf67d7-734b-464f-8aa0-23d48a90ef27" />

# 🛢️ Λ Proyecto Lambda | Optimización de Inversiones Petroleras (OilyGiant)

## 📋 Descripción
**OilyGiant** es una compañía de exploración y extracción de petróleo que busca expandir sus operaciones mediante el desarrollo de nuevos pozos petroleros. La empresa dispone de información geológica proveniente de tres regiones potenciales de exploración, y el objetivo de este proyecto consiste en identificar la región que ofrece la mejor combinación entre **rentabilidad esperada** y **bajo riesgo financiero**, respaldando la decisión de inversión mediante análisis cuantitativos.

Para lograrlo, se construyeron modelos de **Regresión Lineal** capaces de estimar las reservas de petróleo de nuevos pozos y posteriormente se evaluó el riesgo de inversión mediante simulaciones con la técnica de **Bootstrapping**.

## 🎯 Objetivos
- ✅ Analizar y preparar los datos geológicos de tres regiones potenciales.
- ✅ Construir modelos de Regresión Lineal para estimar el volumen de reservas de petróleo.
- ✅ Evaluar el desempeño predictivo de los modelos mediante la métrica **RMSE**.
- ✅ Seleccionar los 200 pozos con mayor potencial de producción en cada región.
- ✅ Estimar las ganancias potenciales bajo condiciones de negocio.
- ✅ Implementar simulaciones de incertidumbre mediante **Bootstrapping** (1,000 iteraciones).
- ✅ Calcular beneficios promedio, intervalos de confianza al 95% y probabilidad de riesgo de pérdidas.
- ✅ Seleccionar la región óptima cumpliendo el límite máximo de riesgo permitido ($< 2.5\%$).

## 🛠️ Herramientas y Habilidades Utilizadas
* **Lenguaje:** Python
* **Librerías:** Pandas, NumPy y Scikit-Learn
* **Entorno:** Jupyter Notebook
* **Técnicas:** Regresión Lineal, Evaluación de errores (RMSE), Simulación Monte Carlo / Bootstrapping, Análisis de riesgo financiero e Intervalos de confianza.

## 📊 Fuente de Datos y Variables
El proyecto utiliza información geológica de tres regiones distintas:
* **Archivos utilizados:** `geo_data_0.csv`, `geo_data_1.csv`, `geo_data_2.csv`
* **Variables disponibles:**
  * `id`: Identificador único del pozo (eliminado antes del modelado).
  * `f0`, `f1`, `f2`: Características geológicas de los puntos de exploración.
  * `product`: Volumen de reservas de petróleo (en miles de barriles).

## ⚙️ Metodología
1. **Exploración y limpieza:** Verificación de tipos de datos, ausencia de valores nulos y eliminación de la columna `id`.
2. **Modelado predictivo:** División de datos en **75% Entrenamiento y 25% Validación** para entrenar un modelo independiente de Regresión Lineal por región.
3. **Evaluación financiera inicial:** Cálculo de ganancias potenciales seleccionando los 200 mejores pozos (considerando una inversión total de **$100M USD**, ingreso de **$4,500 USD** por unidad de producto y un punto de equilibrio de **111.1 mil barriles** por pozo).
4. **Análisis de riesgo (Bootstrapping):** Ejecución de **1,000 simulaciones** seleccionando muestras aleatorias de 500 pozos para elegir los 200 más rentables, construyendo la distribución empírica de beneficios y evaluando el riesgo real de pérdida.

## 💡 Evaluación de Modelos y Ganancias Iniciales
| Región | Reservas Promedio Estimadas | Error Predictivo (RMSE) | Ganancia Potencial (Top 200) |
| :--- | :---: | :---: | :---: |
| **Región 0** | 92.59 | 37.58 | **$33.21M USD** |
| **Región 1** | 68.73 | **0.89** | $24.15M USD |
| **Región 2** | 94.97 | 40.03 | $27.10M USD |

*Aunque a primera vista la **Región 0** parecía ofrecer la mayor ganancia potencial, su alto error de predicción introducía una fuerte incertidumbre financiera.*

## 🧪 Resultados Finales (Simulación Bootstrapping)
| Región | Ganancia Promedio | Intervalo de Confianza (95%) | Riesgo de Pérdidas | Estado frente a Regla de Negocio ($< 2.5\%$) |
| :--- | :---: | :---: | :---: | :---: |
| **Región 0** | $3.96M USD | `[-$1.11M ; $9.09M]` | 6.9% | ❌ Rechazada |
| **Región 1** | **$4.56M USD** | **`[$0.34M ; $8.52M]`** | **1.5%** | ✅ **Seleccionada** |
| **Región 2** | $4.04M USD | `[-$1.63M ; $9.50M]` | 7.6% | ❌ Rechazada |

## 📈 Principales Hallazgos
* **Precisión predictiva:** La **Región 1** presentó el modelo más exacto con un $\text{RMSE} = 0.89$, reduciendo drásticamente la incertidumbre sobre las reservas reales.
* **Evaluación del riesgo:** Las regiones 0 y 2 presentaron probabilidades de pérdida del **6.9%** y **7.6%** respectivamente, superando el umbral máximo tolerable por la compañía ($2.5\%$).
* **Rentabilidad ajustada al riesgo:** La **Región 1** no solo fue la única en cumplir con el criterio de seguridad financiera (**1.5%** de riesgo), sino que también alcanzó la **mayor ganancia promedio esperada ($4.56M USD)** tras incorporar la variabilidad del muestreo.

## 📂 Archivos Principales
* `lambda_oil_well_investment_analysis.ipynb` (o `Λ_Lambda_oil_well_investment_analysis_ipynb.ipynb`)
* `geo_data_0.csv`
* `geo_data_1.csv`
* `geo_data_2.csv`

## 🏁 Conclusión
El análisis cuantitativo permitió determinar la ubicación óptima para invertir **$100 millones de dólares** en el desarrollo de nuevos pozos petroleros. Aunque la Región 0 aparentaba liderar en un escenario determinista, el análisis de incertidumbre mediante **Bootstrapping** demostró un riesgo financiero inaceptable. Por el contrario, la **Región 1** ofrece el equilibrio ideal entre precisión predictiva, rentabilidad promedio (**$4.56M USD**) y seguridad financiera (**1.5% de riesgo de pérdidas**), siendo la recomendación definitiva para la expansión operativa de **OilyGiant**.
