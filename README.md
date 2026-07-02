# Tennis Thermometer

Un proyecto de **Data Engineering y Machine Learning End-to-End** diseñado para predecir la tensión y el atractivo de los partidos de tenis (ATP/WTA) basándose en datos históricos. 

Este proyecto implementa un *Modern Data Stack* completo, desde la ingesta automatizada hasta el despliegue del modelo mediante una API REST.

## Arquitectura del Proyecto (Modern Data Stack)

El flujo de datos sigue un patrón ELT (Extract, Load, Transform) clásico:

1. **Extracción y Orquestación:** `Apache Airflow` programa la descarga de datos estadísticos históricos de tenis.
2. **Almacenamiento (Data Warehouse):** `Google BigQuery` actúa como el repositorio central en la nube.
3. **Transformación (Analytics Engineering):** `dbt (Data Build Tool)` limpia, normaliza y genera métricas avanzadas (ej. fatiga, rendimiento bajo presión) mediante SQL y Jinja.
4. **Machine Learning:** `XGBoost` consume los datos transformados para predecir el "Clutch Factor"
5. **Despliegue:** `FastAPI` sirve las predicciones del modelo en tiempo real.

## Estructura del Repositorio (src layout)

```text
tennis-clutch-predictor/
├── airflow/                # Orquestador (DAGs de ingesta y plugins)
├── dbt_project/            # Transformaciones SQL, macros y tests de calidad de datos
├── notebooks/              # Jupyter Notebooks para Análisis Exploratorio de Datos (EDA)
├── data/                   # Almacenamiento local temporal (ignorado en git)
└── src/                    # Código fuente principal de la aplicación
    ├── api/                # Endpoints de FastAPI y lógica del servidor web
    ├── ml/                 # Scripts de entrenamiento, experimentación y modelos serializados
    └── common/             # Funciones de utilidad compartidas, configuraciones y logs