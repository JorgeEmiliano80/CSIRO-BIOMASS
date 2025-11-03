### 🌱 Image2Biomass Prediction - Predicción de Biomasa de Pastizales

## 📋 Descripción del Proyecto

Sistema de prediccion de biomasa de pastizales usando vision por computadora y deep learning.

El proyecto predice 5 componentes de biomasa a partir de imagenes aereas de pastizales australianos.


## 🎯  Objetivos del Proyecto

### Variables a Predecir (Targets)

Variable | Descripción | Peso en Score |

Dry_Green_g | Vegetación verde seca (sin trébol) | 0.1 |
Dry_Dead_g | Material muerto seco | 0.1 |
Dry_Clover_g | Biomasa de trébol seco | 0.1 |
GDM_g | Materia seca verde (Green Dry Matter) | 0.2 |
Dry_Total_g | Biomasa seca total | 0.5 |


### Métrica de Evaluación

Weighted R² Score:

Score = 0.1 * R²(Dry_Green) + 0.1 * R²(Dry_Dead) + 0.1 * R²(Dry_Clover) 
        + 0.2 * R²(GDM) + 0.5 * R²(Dry_Total)


🚀 Pipeline Completo

1. Preparación de Datos

Cargar datos desde /mnt/project/
Dividir en train/validation/test
Normalizar características tabulares
Aplicar data augmentation a imágenes

2. Modelos a Implementar

a) Baseline Model

Regresión con features tabulares (NDVI, altura)
Establece score mínimo a superar

b) CNN Simple

Red convolucional básica desde cero
Combina features de imagen + tabulares

c) Transfer Learning (ResNet/EfficientNet)

Pre-entrenado en ImageNet
Fine-tuning en nuestros datos
Multi-output regression

d) Ensemble

Combina mejores modelos
Weighted averaging

3. Entrenamiento

K-Fold Cross-Validation
Early stopping
Learning rate scheduling
Model checkpointing

4. Evaluación

Calcular R² para cada target
Weighted R² score final
Análisis de errores por estado/especie
Visualizaciones de predicciones vs reales

5. Predicción Final

Generar predicciones para test set
Formato: sample_id, target
Validar restricciones matemáticas


🛠️ Tecnologías Utilizadas

Python 3.8+
PyTorch - Deep Learning
torchvision - Visión por computadora
timm - Transfer learning models
pandas - Manipulación de datos
numpy - Computación numérica
scikit-learn - Machine learning clásico
Pillow - Procesamiento de imágenes
matplotlib/seaborn - Visualización
tensorboard - Monitoreo de entrenamiento


📊 Datos del Proyecto

Imágenes de entrenamiento: 357 imágenes
Imágenes de prueba: ~800 imágenes
Periodo: Enero - Noviembre 2015
Ubicaciones: Tasmania, Victoria, NSW, Australia Occidental
Especies: 15 tipos diferentes de pastizales


🔑 Features Disponibles
Features de Imagen

Imágenes RGB de pastizales (vista cenital)
Resolución variable

Features Tabulares

Pre_GSHH_NDVI: Índice de vegetación normalizado (0.16 - 0.91)
Height_Ave_cm: Altura promedio del pastizal (1 - 70 cm)
Sampling_Date: Fecha de muestreo
State: Estado australiano
Species: Especies de pasto presentes.


💡 Insights del EDA

Relaciones matemáticas fuertes:

Dry_Total ≈ Dry_Green + Dry_Dead + Dry_Clover
GDM ≈ Dry_Green + Dry_Clover


Correlaciones importantes:

Altura → Biomasa verde (r=0.65)
NDVI → GDM (r=0.47)
GDM → Biomasa total (r=0.90)


Desbalance leve:

Tasmania tiene más muestras (138 imágenes)
Ryegrass_Clover es la especie dominante


📝 Notas Importantes

Las predicciones deben respetar las relaciones matemáticas entre targets
Dry_Total_g tiene el mayor peso (0.5) en la métrica final
Considerar stratified sampling por estado y especie
Data augmentation debe ser realista (rotaciones, flips, brightness).

👥 Equipo de Desarrollo

JORGE EMILIANO - DATA SCIENTIST Ssr.


🎓 Referencias

Competición: CSIRO - Image2Biomass Prediction
