# IDS impulsado por Deep Learning para Redes IoT en Hogares Inteligentes

## Acerca del Proyecto
La proliferación de dispositivos en hogares inteligentes ha incrementado las vulnerabilidades de red frente a ciberataques. Los Sistemas de Detección de Intrusiones (IDS) tradicionales enfrentan limitaciones críticas en escenarios de escasez de datos (*few-shot*) y generan bloqueos erróneos que afectan la disponibilidad del ecosistema. 

Este proyecto propone un IDS impulsado por aprendizaje profundo (*Deep Autoencoder*) basado estrictamente en el análisis de patrones de comportamiento benignos. El modelo actúa como un filtro primario implacable, y para abordar el desafío de los falsos positivos derivados de la sensibilidad algorítmica, integra un mecanismo sociotécnico (*human-in-the-loop*) que deriva clasificaciones ambiguas a validación humana, evitando una denegación de servicio autoinfligida.

## Características Principales
* **Enfoque No Supervisado:** Entrenado exclusivamente con tráfico normal, eliminando la necesidad de historiales masivos de ataques previos.
* **Reducción de Dimensionalidad:** Arquitectura de *Deep Autoencoder* que comprime 51 características de red en un "cuello de botella" de tan solo 8 neuronas.
* **Detección por Error Cuadrático Medio (MSE):** El límite de decisión (*Threshold*) se estableció dinámicamente en `6.00e-05` (percentil 80 de los datos de entrenamiento).
* **Supervisión Humana (*Human-in-the-loop*):** Las anomalías límite no bloquean la red automáticamente, sino que se categorizan como "Eventos" ambiguos derivados al usuario.

## 📂 Estructura del Repositorio
El repositorio contiene el código fuente para la extracción de características, entrenamiento y validación del modelo:

```text
IDS_AUTOENCODER_IOT_2026/
│
├── CSV_Output/                             # Contiene los datasets procesados tras la extracción (ej. benign_final.csv, bruteforce_final.csv)
|   ├── dataset_limpio.csv                      # Dataset consolidado final utilizado para el entrenamiento y evaluación
│
├── 01_extraccion_flujos_nfstream.ipynb     # Extracción de características (51 dimensiones) desde archivos crudos
├── 01_5_consolidacion_csv.ipynb            # Unificación y agrupación de los flujos de red extraídos
├── 02_preprocesamiento_limpieza.ipynb      # Aplicación de Min-Max Scaler y eliminación de datos atípicos
├── 03_autoencoder_entrenamiento.ipynb      # Definición de la arquitectura y entrenamiento del modelo con datos benignos
└── validacion.ipynb                        # Evaluación del conjunto de prueba mixto, generación de Matriz de Confusión y cálculo de métricas
```
(Nota: Los archivos crudos PCAP originales y la carpeta del entorno virtual venv han sido excluidos de este repositorio por motivos de capacidad y buenas prácticas de control de versiones).

## Resultados y Métricas del Modelo

El modelo fue evaluado en un entorno realista con un desbalance de clases significativo, arrojando resultados altamente competitivos frente al estado del arte:
Precisión (frente a ataques): 98.00%
F1-Score Global: 86.75%
Exactitud (Accuracy): 78.17%
Falsos Positivos Derivados (Eventos): 14.355 flujos legítimos derivados a validación humana.

## Conjunto de Datos Utilizado

La extracción de flujos para este experimento se basó en el conjunto de datos público CICIoT2023, el cual captura el comportamiento real de 105 dispositivos IoT comerciales interconectados bajo protocolos como Wi-Fi, Zigbee y Z-Wave.

## Autor
Sebastian David Torres Reyes
Proyecto de investigación académica (2026).
