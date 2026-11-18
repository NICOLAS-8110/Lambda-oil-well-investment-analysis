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
* **Entorno:** Jupyter Notebook (`lambda_oil_well_investment_analysis.ipynb`)
* **Técnicas:** Regresión Lineal, Evaluación de errores (RMSE), Simulación Monte Carlo / Bootstrapping, Análisis de riesgo financiero e Intervalos de confianza.

## 📊 Fuente de Datos y Variables
El proyecto utiliza información geológica de tres regiones distintas (100,000 registros por archivo):
* **Archivos utilizados:** `geo_data_0.csv` (Región 1), `geo_data_1.csv` (Región 2) y `geo_data_2.csv` (Región 3).
* **Variables disponibles:**
  * `id`: Identificador único del pozo (eliminado antes del modelado).
  * `f0`, `f1`, `f2`: Características geológicas de los puntos de exploración.
  * `product`: Volumen de reservas de petróleo (en miles de barriles).

## ⚙️ Metodología
1. **Exploración y limpieza:** Verificación de tipos de datos, ausencia de valores nulos y eliminación de la columna `id`.
2. **Modelado predictivo:** División de datos en **75% Entrenamiento y 25% Validación** (`random_state=12345`) para entrenar un modelo independiente de Regresión Lineal por región.
3. **Condiciones financieras:** Inversión total de **$100,000,000 USD** para desarrollar **200 pozos** ($500,000 USD por pozo), con un ingreso de **$4,500 USD** por unidad de producto, estableciendo un punto de equilibrio mínimo de **111.11 mil barriles** por pozo.
4. **Análisis de riesgo (Bootstrapping):** Ejecución de **1,000 simulaciones** seleccionando muestras aleatorias de 500 pozos con reemplazo para elegir los 200 más rentables, construyendo la distribución empírica de beneficios y evaluando el riesgo real de pérdida.

## 💡 Evaluación de Modelos Predictivos
| Región (Dataset) | Volumen Medio Predicho | Error Predictivo (RMSE) |
| :--- | :---: | :---: |
| **Región 1** (`geo_data_0.csv`) | 92.59 | 37.58 |
| **Región 2** (`geo_data_1.csv`) | 68.73 | **0.89** |
| **Región 3** (`geo_data_2.csv`) | 94.97 | 40.03 |

*Aunque la **Región 2** presenta un promedio general de reservas más bajo, la excepcional precisión de su modelo ($\text{RMSE} = 0.89$) reduce drásticamente la incertidumbre al identificar los pozos más productivos.*

## 🧪 Resultados Finales (Simulación Bootstrapping)
| Región (Dataset) | Ganancia Promedio | Intervalo de Confianza (95%) | Riesgo de Pérdidas | Estado frente a Regla de Negocio ($< 2.5\%$) |
| :--- | :---: | :---: | :---: | :---: |
| **Región 1** (`geo_data_0.csv`) | $6,007,352.44 USD | `[$129,483.31 ; $12,311,636.06]` | 2.0% | ⚠️ Cumple, menor retorno |
| **Región 2** (`geo_data_1.csv`) | **$6,652,410.58 USD** | **`[$1,579,884.81 ; $11,976,415.87]`** | **0.3%** | ✅ **Seleccionada** |
| **Región 3** (`geo_data_2.csv`) | $6,155,597.23 USD | `[-$122,184.95 ; $12,306,444.74]` | 3.0% | ❌ Rechazada ($> 2.5\%$) |

## 📈 Principales Hallazgos
* **Precisión determinante:** La **Región 2 (`geo_data_1.csv`)** obtuvo el error más bajo ($\text{RMSE} = 0.89$), permitiendo seleccionar con alta certeza los 200 pozos más rentables de cada muestra.
* **Descarte por riesgo:** La **Región 3** quedó descartada al registrar un riesgo de pérdida del **3.0%**, superando el límite máximo permitido por la compañía ($2.5\%$).
* **Máxima rentabilidad y seguridad:** La **Región 2** generó la mayor ganancia promedio (**$6,652,410.58 USD**) junto con el riesgo de pérdida más bajo de todo el estudio (**0.3%**), respaldado por un intervalo de confianza al 95% holgadamente positivo.

## 📂 Archivos Principales
* `lambda_oil_well_investment_analysis.ipynb`
* `geo_data_0.csv`
* `geo_data_1.csv`
* `geo_data_2.csv`

## 🏁 Conclusión
A partir de la evaluación de los modelos de regresión lineal y las simulaciones con **Bootstrapping**, se recomienda de manera categórica desarrollar los nuevos pozos petrolíferos en la **Región 2 (`geo_data_1.csv`)**. Esta alternativa ofrece el equilibrio óptimo para invertir los **$100 millones de dólares**, alcanzando el mayor beneficio promedio esperado (**$6.65M USD**) y un riesgo de pérdida mínimo de apenas **0.3%**, garantizando una inversión segura y alineada con los criterios corporativos de **OilyGiant**.
