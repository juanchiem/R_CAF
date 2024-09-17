# R_CAF Mini curso de epidemio

1.  Análisis temporal de epidemias

  -   Área bajo la curva del progreso de la enfermedad

  -   Ajuste de modelos

2.  Predicción de enfermedades según variable meteorológicas

  -   Creación de variables

  -   Modelo logístico

  -   Validación de modelo ajustado


Abrir R Studio y correr el siguiente codigo en la consola

```         
usethis::use_course("https://bit.ly/4eph38o", destdir = getwd())
```

## Recursos

- https://r4pde.net/
- https://www.open-pde.info/index.html
- https://www.nature.com/articles/s41598-023-44338-6#Sec7
- https://repositorio.inta.gob.ar/xmlui/bitstream/handle/20.500.12123/17630/INTA_CR_LaPampa
- https://ohioline.osu.edu/factsheet/plpath-cer-03
- https://link.springer.com/content/pdf/10.1007/s13313-019-00655-x.pdf 
- https://apsjournals.apsnet.org/doi/10.1094/PHYTO-10-22-0362-KD


## Algunos conceptos importantes

**Sensibilidad** y **especificidad** son dos conceptos clave en la evaluación de la precisión de pruebas diagnósticas o modelos predictivos, particularmente en epidemiología y otras ciencias de la salud. A continuación explicamos cada uno:

### 1. **Sensibilidad**:
La sensibilidad mide la capacidad de un modelo para identificar correctamente a los **verdaderos positivos** (es decir, cultivos que realmente tienen la enfermedad). Es la proporción de verdaderos positivos entre todos los lotes que en realidad están enfermos.

- **Fórmula**:
  
  $\text{Sensibilidad} = \frac{\text{Verdaderos positivos}}{\text{Verdaderos positivos} + \text{Falsos negativos}}$
  

- **Interpretación**:
  
  - Una **alta sensibilidad** significa que el modelo es eficaz para detectar la presencia de la enfermedad o la condicion. Es útil cuando es importante minimizar los **falsos negativos** (casos que tienen la enfermedad o condicion favorable para desarrollarla, pero la prueba no la detecta).
  
  - Ejemplo: En la protección de cultivos, un modelo con alta sensibilidad detectaría la mayoría de las infecciones reales, incluso si algunas veces da falsas alarmas.
  (ej: fusariosis de la espiga en cereales de invierno)

### 2. **Especificidad**:

La especificidad mide la capacidad un modelo para identificar correctamente a los **verdaderos negativos** (es decir, los cultivos que realmente no tienen la enfermedad). Es la proporción de verdaderos negativos entre todos los lotes que no están enfermos.

- **Fórmula**:
  \[
  \text{Especificidad} = \frac{\text{Verdaderos negativos}}{\text{Verdaderos negativos} + \text{Falsos positivos}}
  \]

- **Interpretación**:

  - Una **alta especificidad** significa que la prueba o modelo es eficaz para detectar la ausencia de la enfermedad. Es útil cuando es importante minimizar los **falsos positivos** (casos donde se diagnostica la enfermedad, pero en realidad no está presente). 

  - Ejemplo: En la protección de cultivos, un modelo con alta especificidad evitaría falsas alarmas, prediciendo correctamente que no habrá una epidemia de enfermedad en condiciones normales.
  (ej: enfermedades fisiologicas en cebada variedad Montoya)

### Relación entre Sensibilidad y Especificidad:
- Generalmente, hay un **compromiso** entre sensibilidad y especificidad. Aumentar la sensibilidad puede disminuir la especificidad y viceversa.
- Un modelo ideal tendría tanto alta sensibilidad como alta especificidad, lo que significa que sería capaz de detectar todas las enfermedades verdaderas y evitar falsos diagnósticos.

### Ejemplo práctico:

En un sistema de alerta para una enfermedad de cultivo:

- **Alta sensibilidad**: Detecta cualquier condicion favorable para una enfermedad en cuestión, asegurando que no se pierdan epidemias, pero puede generar falsas alarmas.

- **Alta especificidad**: Solo genera alertas cuando hay un riesgo real, pero podría pasar por alto pequeños brotes epidémicos.

El **AUC de la curva ROC** es una medida utilizada para evaluar el rendimiento de un modelo de clasificación, especialmente en sistemas de diagnóstico o predicción, como en epidemiología o en modelos de manejo de enfermedades de cultivos. Vamos a desglosarlo:

### 3. **Curva ROC (Receiver Operating Characteristic)**:
La **curva ROC** es un gráfico que muestra la relación entre la **tasa de verdaderos positivos (sensibilidad)** y la **tasa de falsos positivos (1 - especificidad)** a medida que varía el umbral de decisión del modelo.

- **Eje Y**: Representa la **sensibilidad** o la tasa de verdaderos positivos (True Positive Rate, TPR).
- **Eje X**: Representa la **tasa de falsos positivos** (False Positive Rate, FPR), que es 1 - especificidad.

A medida que el umbral cambia, la curva ROC muestra cómo el modelo compromete entre detectar verdaderos positivos y evitar falsos positivos.

### 4. **AUC (Área Bajo la Curva)**:
El **AUC (Area Under the Curve)** de la curva ROC es el área total bajo esa curva y proporciona una métrica de qué tan bien el modelo distingue entre clases (por ejemplo, enfermo/no enfermo o infectado/no infectado). Es un valor numérico entre 0 y 1.

- **AUC = 1**: Indica que el modelo tiene un rendimiento perfecto, separando completamente los verdaderos positivos de los negativos.

- **AUC = 0.5**: Indica que el modelo no tiene poder predictivo, equivalente a una decisión aleatoria.

- **AUC < 0.5**: El modelo está clasificando incorrectamente, peor que el azar.

### Interpretación del AUC:

- **AUC cercano a 1**: El modelo tiene un excelente desempeño, siendo capaz de distinguir muy bien entre las dos clases (por ejemplo, plantas infectadas y no infectadas).

- **AUC entre 0.7 y 0.9**: El modelo tiene un buen desempeño, pero no es perfecto.

- **AUC entre 0.5 y 0.7**: El modelo tiene un desempeño moderado.

- **AUC = 0.5**: El modelo no tiene capacidad predictiva útil.

### Aplicación en epidemiología y manejo de cultivos:
En modelos de predicción de enfermedades de cultivos, un **AUC alto** significa que el sistema de predicción es eficaz para distinguir entre condiciones que conducirán a una epidemia y aquellas que no. Por ejemplo:

- Un AUC alto para un modelo de predicción de enfermedades en un cultivo indicaría que el modelo es capaz de predecir correctamente cuándo se presentarán las condiciones favorables para el brote epidemico.

### Ejemplo:

Supón que un modelo de predicción tiene un **AUC = 0.85**. Esto significa que en el 85% de los casos, el modelo clasificará correctamente una planta enferma frente a una sana, lo cual es una buena precisión.


