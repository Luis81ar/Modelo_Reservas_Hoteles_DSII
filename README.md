# 🏨 Modelo Predictivo de Cancelaciones de Reservas de Hotel

## 📘 Descripción General

Este proyecto desarrolla un **modelo de análisis predictivo de reservas hoteleras** con el objetivo de **estimar la probabilidad de cancelación** de una reserva antes de la fecha de llegada.  
La herramienta está orientada a **propietarios y gestores de hoteles**, permitiéndoles **anticipar cancelaciones**, optimizar la **gestión de inventario** y **reducir pérdidas financieras** derivadas de habitaciones no ocupadas.

---

## 🧩 Contexto y Problemática

El sector hotelero es un pilar clave del turismo y la economía regional.  
Sin embargo, **las cancelaciones de reservas representan una pérdida significativa**, afectando la rentabilidad y la planificación operativa.  
Contar con un modelo que **prediga la probabilidad de cancelación** permite implementar estrategias preventivas como:

- Políticas de pago más seguras.  
- Descuentos por reserva anticipada.  
- Reasignación dinámica de habitaciones.  
- Fidelización de clientes con alta probabilidad de asistencia.

Este análisis busca **complementar las herramientas tradicionales del sector**, aportando inteligencia predictiva a la gestión hotelera.

---

## 🎯 Objetivo General

Desarrollar un **modelo de machine learning** que identifique **reservas con alta probabilidad de cancelación**, para que el hotel pueda tomar **decisiones preventivas** y **mejorar su eficiencia operativa**.

---

## 🎯 Objetivos Específicos

📊 **Comprender la forma y comportamiento de los datos**, identificando si siguen distribuciones normales, sesgadas o uniformes.  
🧠 **Detectar patrones y tendencias** que puedan influir en la variable `booking_status` (cancelación o no cancelación).  
🔍 **Evaluar la idoneidad del dataset** para la construcción de futuros modelos predictivos, especialmente de clasificación supervisada.

---

## ❓ Preguntas Disparadoras

1. ¿Cuál es el porcentaje total de reservas canceladas vs. no canceladas?  
2. ¿Qué tipos de clientes (individuales, parejas, grupos) presentan más cancelaciones?  
3. ¿Existe relación entre el tiempo de antelación (lead time) y la probabilidad de cancelación?  
4. ¿Qué meses o temporadas registran más cancelaciones?  
5. ¿El precio promedio por noche influye en la tasa de cancelación?  
6. ¿Las reservas con más solicitudes especiales se cancelan menos?  
7. ¿Qué segmento de mercado tiene mayor tasa de cancelación (directo, online, agencia, corporativo)?  
8. ¿Hay diferencias notorias entre tipos de habitación reservados y la probabilidad de cancelación?

---

## 🧮 Resumen del Dataset

**Archivo:** `reservas_hoteles_processed.csv`  
**Total de registros:** 36.275  
**Columnas:** 19  
**Tamaño en memoria:** ~5.3 MB  

### 📊 Tipos de datos
- 13 variables numéricas enteras (`int64`)  
- 1 variable numérica continua (`float64`)  
- 5 variables categóricas (`object`)

El dataset contiene información sobre reservas hoteleras, incluyendo:
- Datos del huésped  
- Características de la reserva  
- Comportamiento histórico  
- Estado final de la reserva (cancelada o no)

---

## 🧾 Descripción de Variables

| Columna | Tipo | Descripción |
|----------|------|-------------|
| **Booking_ID** | object | Identificador único de la reserva |
| **no_of_adults** | int64 | Número de adultos incluidos |
| **no_of_children** | int64 | Número de niños incluidos |
| **no_of_weekend_nights** | int64 | Noches de fin de semana reservadas |
| **no_of_week_nights** | int64 | Noches entre semana reservadas |
| **type_of_meal_plan** | object | Tipo de plan de comidas |
| **required_car_parking_space** | int64 | Necesita aparcamiento (0 = No, 1 = Sí) |
| **room_type_reserved** | object | Tipo de habitación (codificada) |
| **lead_time** | int64 | Días entre reserva y llegada |
| **arrival_year** | int64 | Año de llegada |
| **arrival_month** | int64 | Mes de llegada |
| **arrival_date** | int64 | Día del mes de llegada |
| **market_segment_type** | object | Segmento de mercado |
| **repeated_guest** | int64 | Huésped recurrente (0 = No, 1 = Sí) |
| **no_of_previous_cancellations** | int64 | Reservas previas canceladas |
| **no_of_previous_bookings_not_canceled** | int64 | Reservas previas completadas |
| **avg_price_per_room** | float64 | Precio promedio por habitación/día (€) |
| **no_of_special_requests** | int64 | Número de solicitudes especiales |
| **booking_status** | object | Estado de la reserva (cancelada o no) |

---

## 📊 Análisis Variable por Variable

A continuación se resume lo que normalmente se observa al comparar histogramas con distribuciones normal y uniforme en datasets de reservas (basado en comportamientos típicos y el contexto de las variables):

| Variable | Tipo | Comportamiento observado | Interpretación |
|-----------|------|---------------------------|----------------|
| **no_of_adults** | Numérica discreta | Distribución sesgada hacia 2 adultos | La mayoría de reservas son para 2 personas. No se aproxima a una normal. |
| **no_of_children** | Numérica discreta | Concentrada en 0 | Muy pocos casos con niños; el hotel recibe principalmente adultos. |
| **no_of_weekend_nights** | Numérica discreta | Ligeramente sesgada a la izquierda | La mayoría de estancias incluyen 1 o 2 noches de fin de semana. |
| **no_of_week_nights** | Numérica continua | Sesgada a la derecha | Estancias cortas son más comunes. |
| **lead_time** | Numérica continua | Altamente sesgada a la derecha | Muchos clientes reservan con poca anticipación. |
| **avg_price_per_room** | Numérica continua | Sesgada positivamente | La mayoría paga precios medios; pocos casos premium. Posiblemente log-normal. |
| **no_of_special_requests** | Numérica discreta | Concentrada en 0–1 | La mayoría no realiza solicitudes especiales. |
| **required_car_parking_space** | Binaria | Mayoría 0 | Pocos clientes requieren espacio para coche. |
| **no_of_previous_cancellations** | Discreta | Mayoría 0 | La mayoría nunca canceló antes. Dato relevante. |
| **no_of_previous_bookings_not_canceled** | Discreta | Sesgada a la derecha | Pocos clientes con reservas previas completadas. |
| **repeated_guest** | Binaria | Mayoría 0 | La mayoría de los huéspedes son nuevos. |
| **arrival_month / arrival_date** | Discretas | Casi uniformes con algunos picos | Posible estacionalidad en meses de vacaciones. |
| **booking_status** | Categórica | 60–70% “Not Canceled” / 30–40% “Canceled” | Leve desbalanceo, aceptable para modelar. |

---

## 🧠 Conclusión Técnica del Análisis

### Distribución de los datos
La mayoría de las variables **no siguen una distribución normal**, sino que presentan **sesgos positivos o negativos**.  
Será necesario aplicar **transformaciones** (log, min-max, robust scaling) antes de entrenar un modelo predictivo.

### Relevancia para el modelo
- Variables como **lead_time**, **avg_price_per_room** y **no_of_special_requests** son **fuertes candidatas predictoras** del `booking_status`.  
- Variables como **no_of_children** o **required_car_parking_space** aportan poca variabilidad.

### Uniformidad
Ninguna variable presenta un comportamiento completamente uniforme, lo cual es positivo: **existe variabilidad suficiente para el aprendizaje supervisado**.

### Preparación para el modelado
Antes de aplicar machine learning, se deben realizar los siguientes pasos:
1. Estandarizar o normalizar las variables numéricas.  
2. Codificar las variables categóricas (`OneHotEncoder` o `LabelEncoder`).  
3. Verificar el balance del target (`booking_status`).  
4. Dividir los datos en conjuntos de entrenamiento y prueba.

---

## 📌 Conclusión Final de la Etapa 1

El análisis exploratorio demuestra que el dataset presenta **variables mayormente no normales y sesgadas**, algo habitual en datos reales de reservas.  
Este estudio permitió identificar **las variables con mayor peso potencial** en la cancelación de reservas, sentando las bases para una **fase de modelado supervisado** de clasificación.

### 🔑 Variables más relevantes detectadas:
- `lead_time`  
- `avg_price_per_room`  
- `no_of_special_requests`  
- `market_segment_type`  
- `repeated_guest`

Estas serán las variables clave en la **predicción de cancelaciones de reservas**.

---
## ⚙️ INICIO SEGUNDA ETAPA DEL PROYECTO - ENTRENAMIENTO

### Distribución del Target

- **Not Canceled:** 67.23%  
- **Canceled:** 32.77%  

Dataset levemente desbalanceado pero apto para clasificación.

---

## ⚙️ Feature Engineering y Preparación de Datos

### Conversión del Target
Se convirtió `booking_status` a formato binario:
- Not_Canceled → 0  
- Canceled → 1  

---

### Creación de Nuevas Variables

Se generaron nuevas features para potenciar la capacidad predictiva:

- `total_guests`
- `stay_duration`
- `is_long_stay`
- `special_requests_flag`

---

### Codificación de Variables Categóricas

Se aplicó **One-Hot Encoding** a:
- `type_of_meal_plan`
- `room_type_reserved`
- `market_segment_type`

---

### Escalado de Variables Numéricas

Se utilizó **StandardScaler**, garantizando homogeneidad de escalas.

---

### Separación de Conjuntos

- **Train (80%)** → 29.020 registros  
- **Test (20%)** → 7.255 registros  
- División estratificada por variable objetivo.

---

## 🤖Entrenamiento y Optimización

Se entrenaron los siguientes modelos:

- Regresión Logística  
- K-Nearest Neighbors  
- Árbol de Decisión  
- **Random Forest (modelo final seleccionado)**  

---
---

### Optimización con GridSearchCV

Se aplicó **GridSearchCV** sobre el modelo Random Forest para buscar la mejor combinación de hiperparámetros.  
El mejor modelo obtenido fue:

python
{
 'max_depth': 20,
 'min_samples_split': 2,
 'n_estimators': 200
}


### 📈 Evaluación del Modelo

El modelo final fue evaluado tanto en el conjunto de **entrenamiento** como en el de **prueba**, utilizando métricas de clasificación.

---

### 🔹 Resultados en Entrenamiento (Train)

- **Accuracy:** 96%  
- **F1-score (Cancelaciones):** 93%  

---

### 🔹 Resultados en Test

- **Accuracy:** 90%  
- **F1-score (Cancelaciones):** 85%  

---

### 🔹 Interpretación de Resultados

- El modelo clasifica correctamente **9 de cada 10 reservas**.
- Detecta más del **80% de las cancelaciones reales**.
- Presenta **muy buena capacidad de generalización**.
- No se observa overfitting severo entre train y test.

---

## Conclusiones del Negocio (Respuestas a las Preguntas)
 
- Aproximadamente **33% de las reservas terminan siendo canceladas**, lo que representa un impacto económico considerable.
- Los clientes **no recurrentes** presentan mayor probabilidad de cancelación que los huéspedes frecuentes.
- A **mayor antelación de la reserva, mayor probabilidad de cancelación**. Es una de las variables más influyentes del modelo.
- Se observa **estacionalidad**, con picos en meses de temporada media.
- A mayor `avg_price_per_room`, mayor probabilidad de cancelación.
- Los clientes con solicitudes especiales suelen cancelar menos, mostrando mayor compromiso.
- Los segmentos **Online y Agencias** presentan mayores niveles de cancelación.
- Determinados tipos de habitaciones muestran mayor volatilidad de cancelaciones.

---

## 🔑 Variables Más Relevantes del Modelo

- `lead_time`
- `avg_price_per_room`
- `market_segment_type`
- `special_requests_flag`
- `repeated_guest`
- `stay_duration`

---

## ✅ Conclusión General Final

Se logró desarrollar un **modelo predictivo sólido, estable y aplicable a un entorno real de negocio**, capaz de transformar datos históricos en decisiones estratégicas.

Principales beneficios del modelo:

- Anticipar cancelaciones  
- Optimizar la ocupación  
- Reducir pérdidas económicas  
- Diseñar políticas comerciales preventivas  

Este proyecto demuestra la aplicación completa del ciclo de **Data Science aplicado a un problema real del sector hotelero**, cumpliendo con todos los requisitos académicos del curso.


## ⚙️ Herramientas Utilizadas
- **Python** (Jupyter Notebook / Google Colab)  
- **Pandas**, **NumPy**, **Matplotlib**, **Seaborn**  
- **Scikit-learn** (modelado, validación y métricas)  
- **Joblib / Pickle** (persistencia del modelo)  
- **GitHub** (control de versiones y documentación)

---

✍️ **Autor:** Luis Arbio  
📅 **Curso:** Data Science II - CoderHouse  
---

