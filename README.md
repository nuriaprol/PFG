# Automatización del Procesamiento de Facturas REN

Este repositorio contiene el notebook desarrollado para la automatización del tratamiento de facturas semanales XML recibidas por Naturgy desde REN.

## Descripción

El código extrae automáticamente información clave de los archivos XML (Encargo de Regulación, Desvíos por Exceso/Defecto, Fechas, Sociedad, etc.), construye una base de datos estructurada y genera informes semanales en Excel para facilitar la conciliación de pagos.

## Requisitos

- Entorno de ejecución: AWS Glue Studio o PySpark local
- Acceso a bucket S3 de Naturgy
- Python 3.8+
- Librerías necesarias:
  - `boto3`
  - `xml.etree.ElementTree`
  - `pyspark`

## Instrucciones de uso

1. Subir los archivos XML al bucket de Amazon S3 mediante el siguiente comando:
   aws s3 sync [ruta_local] s3://[bucket]/[ruta_destino] --exclude "*" --include "*.xml"
   
2. Ejecutar el script en AWS Glue Studio.
   
3. La tabla tablafacts se actualizará automáticamente en la base de datos prevision_test_electricidad.

4. Conectar Excel a Athena mediante Power Query (ODBC) con la siguiente consulta:
  SELECT DISTINCT * FROM prevision_test_electricidad.tablafacts

5. Revisar el resumen semanal generado automáticamente en la hoja de Excel.


---

# Análisis y Modelado Predictivo del Cargo de Regulación (ERCBRP)

Este repositorio contiene también el código en Python desarrollado para analizar y predecir los encargos de regulación imputados por REN, usando técnicas de aprendizaje automático.

## Descripción

Incluye análisis exploratorio, tratamiento de outliers, visualización y entrenamiento de modelos de predicción (Random Forest y XGBoost) para anticipar los ERCBRP a partir de variables como generación renovable, precio del pool y desvíos.

## Requisitos

- Entorno de ejecución: Google Colab
- Python 3.10+
- Librerías necesarias:
  - `pandas`
  - `numpy`
  - `matplotlib`
  - `seaborn`
  - `xgboost`
  - `sklearn`
  - `statsmodels`
  - `plotly`

##  Instrucciones de uso

1. Subir los siguientes datasets:
   - Base horaria del BRP (precio pool, desvíos, cargo regulación, etc.)
   - Breakdown of Production (producción eléctrica por tecnología)
   
2. Ejecutar las celdas del notebook en orden:
   - Análisis exploratorio
   - Tratamiento de outliers
   - Matriz de correlación
   - Modelado con Random Forest y XGBoost
   - Evaluación con métricas (MAE, RMSE)

3. Consultar los gráficos generados para interpretar resultados.
