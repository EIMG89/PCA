# 📊 Post Campaign Analysis (PCA) - Cachantún Proyecto Infográfico

![Status](https://img.shields.io/badge/Status-Completed-success)
![Tools](https://img.shields.io/badge/Tools-Python%20|%20Adverity%20|%20DV360-blue)
![Stack](https://img.shields.io/badge/Platforms-Meta%20|%20TikTok%20|%20YouTube-red)

## 📖 Descripción del Proyecto

Este repositorio contiene el análisis ex-post de la campaña **"Proyecto Infográfico"** para la marca **Cachantún**, ejecutada entre el **27 de junio y el 08 de agosto de 2023**.

### 📄 Descripción del Proyecto

Este proyecto consolida el análisis de rendimiento de la campaña cross-media **"Proyecto Infográfico"** de **Cachantún**, ejecutada entre el 27 de junio y el 08 de agosto de 2023. La campaña tuvo como objetivo comunicar los beneficios y atributos naturales del producto bajo el concepto *"Únete al sabor de la Naturaleza"*.

El análisis integra datos de plataformas clave (**Meta, TikTok, YouTube**), gestionando una inversión total de **USD 70.360** con un mix de medios enfocado mayoritariamente en digital (57,3%). Para la extracción y normalización de métricas se utilizaron herramientas como **Adverity** y **DV360**.

**Puntos clave del análisis:**

* **Evaluación de KPIs:** Desglose detallado de métricas de eficiencia (CPM, CPV) y consumo (VTR, Alcance) comparadas contra benchmarks de la industria.
* **Performance por Plataforma:** Insights sobre el comportamiento de formatos específicos, destacando la eficiencia de costos y visualización en **TikTok** y el alcance incremental logrado en **YouTube**.
* **Brand Lift Study:** Resultados del experimento de incremento de marca en YouTube, midiendo el impacto real en el recuerdo del anuncio, logrando un **Lift absoluto del 4,66%**.
* **Análisis Creativo:** Matriz de rendimiento de los distintos activos publicitarios (anuncios) para identificar las *"Golden Rules"* y recomendaciones de optimización para futuras campañas.

La campaña tuvo como objetivo comunicar los beneficios de un producto natural directo de Coinco, bajo el concepto *"Únete al sabor de la Naturaleza"*. La estrategia de medios contó con un presupuesto de **USD 70.360**, con un mix de medios que destinó un **57,3% a Digital** y un 42,7% a TV Abierta.

### 🎯 Objetivos de Marketing
El análisis se centra en los siguientes KPIs definidos según la metodología iDDM de Heineken:

| Plataforma | Objetivo | KPIs Principales | Formato |
| :--- | :--- | :--- | :--- |
| **Meta (FB/IG)** | Reconocimiento (Awareness) | Alcance, Frecuencia, Ad Recall, VTR | Feed, Stories, Reels |
| **TikTok** | Visualización | CPV, VTR, Reproducción 100% | Video in Feed |
| **YouTube** | Consideración y Alcance | CPV, VTR, CPM | Instream |

---

## 🛠️ Stack Tecnológico y Flujo de Datos

Para la consolidación y análisis de los datos se utilizaron las siguientes herramientas:

1.  **Fuentes de Datos (Data Sources):** Extracción de métricas nativas desde **Meta Ads Manager**, **TikTok Ads** y **DV360/Google Ads** (para YouTube).
2.  **Orquestación (ETL):** Uso de **Adverity** para la ingesta y normalización de campos (naming convention) de las diferentes fuentes.
3.  **Procesamiento:** Python (Pandas/NumPy) para la limpieza de datos y cálculo de métricas compuestas.
4.  **Visualización:** Generación de gráficos de dispersión (Scatter Plots) para análisis de eficiencia creativa.

---

## 📊 Principales Hallazgos (Key Insights)

### 1. Performance General por Plataforma
* **Meta (Facebook/Instagram):** La campaña fue eficiente en costos. El **Ad Recall** tuvo un cumplimiento del 87% respecto al benchmark. Sin embargo, el **VTR** final (4,72%) estuvo levemente por debajo del benchmark (4,92%).
    * *Insight Demográfico:* El rango de **18 a 34 años** concentró el 59% del alcance pero mostró los resultados más bajos en rendimiento.
* **YouTube:** Se logró superar el alcance esperado en un **27%**. El costo fue eficiente, logrando un CPM un 10% más bajo que el pronóstico.
* **TikTok:** Fue la plataforma más eficiente en visualización. Superó el alcance benchmark en un **78%** y la frecuencia en un **68%**.

### 2. Análisis de Creatividades (Scatter Plot Analysis)
Se realizó un análisis de cuadrantes cruzando **Alcance vs. Frecuencia** y **VTR vs. Costo**:

* **Meta:** Solo 4 de 14 anuncios superaron el benchmark de VTR. Destacan los anuncios "Vertical-Horizontal" por su alta eficiencia.
* **TikTok:** 5 de 8 piezas superaron el VTR benchmark. Las piezas "Minerales Gato" y "Naturaleza" tuvieron la mayor inversión y un CPV 75% inferior al benchmark.

### 3. Brand Lift Study (YouTube)
Se ejecutó un experimento de **Brand Lift** comparando un grupo expuesto vs. grupo control.
* **Lift Absoluto:** +4.66% en recuerdo del anuncio.
* **Significancia:** Los resultados mostraron un lift positivo, siendo el segmento de **Hombres** el que mayor incremento tuvo (5.4%) versus el benchmark.

---

## 🧪 Metodología de Cálculo (Snippets)

El cálculo de KPIs sigue las definiciones del glosario oficial del proyecto:

$$VTR = \frac{\text{Reproducciones completas (o 3s)}}{\text{Impresiones}}$$

$$CPV = \frac{\text{Inversión Total}}{\text{Visualizaciones}}$$

*Ejemplo de código utilizado para el análisis de eficiencia:*

```python
import pandas as pd

def calcular_eficiencia(df):
    # Benchmark VTR promedio mercado
    benchmark_vtr = 0.0492 
    
    # Cálculo de VTR y Delta
    df['VTR'] = df['video_views'] / df['impressions']
    df['Delta_Benchmark'] = (df['VTR'] - benchmark_vtr) / benchmark_vtr
    
    # Clasificación de anuncios
    df['Performance'] = df.apply(
        lambda x: 'Efficient' if x['VTR'] > benchmark_vtr and x['cpm'] < x['target_cpm'] 
        else 'Review', axis=1
    )
    return df
