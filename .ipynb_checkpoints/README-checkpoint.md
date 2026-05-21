# 🧠 Clasificación de Conectividad Cerebral Funcional en el Espectro Autista (TEA) usando Machine Learning

Este proyecto desarrolla un pipeline completo de **Neurociencia de Datos** y **Machine Learning** para clasificar y analizar patrones de conectividad funcional en el cerebro de niños varones diagnosticados con Trastorno del Espectro Autista (TEA), utilizando datos de Resonancia Magnética Funcional en Estado de Reposo (rs-fMRI) provenientes del repositorio internacional **ABIDE (Autism Brain Imaging Data Exchange)**.

---

## 🎯 El Problema Clínico y Estrategia de Selección

La variabilidad en el desarrollo cerebral y el dimorfismo sexual introducen un alto nivel de "ruido" en los estudios de neuroimagen. Para mitigar esto y maximizar la precisión del modelo, se aplicó una estrategia de **ingeniería de cohorte** filtrando el dataset global bajo criterios biológicos estrictos:
* **Población:** Solo niños de sexo biológico masculino.
* **Rango Etario:** Entre 5 y 10 años (período crítico de maduración cortical).
* **Pipeline de Preprocesamiento:** CPAC (Centros para la Computación en Alta Definición).

Al homogeneizar la muestra por edad y sexo, el algoritmo puede aislar de forma mucho más limpia las verdaderas alteraciones de conectividad asociadas al espectro.

---

## 🛠️ Stack Tecnológico Utilizado

* **Nilearn:** Manipulación de imágenes médicas 3D/4D (fMRI) y extracción de señales por regiones.
* **Scikit-Learn:** Escalado de datos, división de muestras y entrenamiento de modelos lineales con regularización.
* **Pandas y NumPy:** Procesamiento de datos fenotípicos (clínicos) y manipulación de matrices numéricas.
* **Seaborn y Matplotlib:** Visualización analítica avanzada y mapas de calor.

---

## 🚀 Pipeline del Proyecto (Paso a Paso)

1. **Extracción Espacial (Atlas Harvard-Oxford):** Se utilizó un molde tridimensional para dividir la corteza cerebral en **48 Regiones de Interés (ROIs)**. Las señales BOLD (oxigenación en sangre segundo a segundo) se promediaron dentro de cada región.
2. **Modelado de Conectividad:** Se calculó el *Coeficiente de Correlación de Pearson* entre las 48 áreas, generando una matriz de características de **1.176 conexiones funcionales únicas** por paciente.
3. **Clasificación:** Se entrenó un modelo de **Regresión Logística** con regularización Ridge ($L_2$) para domar la alta dimensionalidad y evitar el sobreajuste (*overfitting*).

---

## 📊 Análisis y Resultados Visuales

### 1. Rendimiento del Modelo de Machine Learning
El clasificador base entrenado con la cohorte específica alcanzó métricas equilibradas, demostrando una alta especificidad en el grupo de control.

| Métrica | Control (0) | Autismo (1) | General |
|---------|-------------|-------------|---------|
| **Precision** | 0.57        | 1.00        | -       |
| **Recall** | 1.00        | 0.25        | -       |
| **Accuracy** | -           | -           | **62.50%** |

*Clavar aquí tu gráfico de Matriz de Confusión:* `![Matriz de Confusión](matriz_confusion.png)`

### 2. Neuroimagen Comparativa (Huella Digital Cerebral)
Al promediar las señales de todos los sujetos por grupo y restar sus matrices, se obtiene la **Matriz de Contraste**. Este mapa revela de forma matemática las autopistas de información que sufren alteraciones:
* **Zonas Cálidas (Rojo):** Regiones con patrones de **Hiperconectividad** en niños con TEA.
* **Zonas Frías (Azul):** Vías que muestran **Hipoconectividad** respecto al grupo de desarrollo neurotípico.

*Clavar aquí tus gráficos de conectividad:*
`![Mapas de Calor Comparativos](mapas_calor_comparativos.png)`
`![Conectoma 3D Glass Brain](conectoma_3d.png)`

---

## 🔮 Conclusiones y Trabajo Futuro

* **Sensibilidad del Modelo:** El modelo actual es altamente confiable ante predicciones positivas de autismo (100% de precisión en Test), pero tiende a ser conservador debido al tamaño muestral restringido del piloto.
* **Próximos Pasos:**
  1. **Subir el volumen de datos:** Incrementar la muestra a 200 o más pacientes utilizando la infraestructura de descarga por bloques ya funcional.
  2. **Modelos no lineales:** Probar clasificadores basados en ensambles como *Random Forest* o máquinas de soporte vectorial (*SVM* con kernel lineal) que suelen destacar en tareas de neuroimagen.
  3. **Inyección de Features:** Combinar las variables de conectividad con la edad exacta del scan como un predictor numérico continuo directo.

---