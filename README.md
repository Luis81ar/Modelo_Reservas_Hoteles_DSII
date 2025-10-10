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
- Fidelización de clientes con alta probabilidad de asistir.

Este análisis busca **complementar las herramientas tradicionales del sector**, aportando inteligencia predictiva a la gestión hotelera.

---

## 🎯 Objetivo General

Desarrollar un **modelo de machine learning** que identifique **reservas con alta probabilidad de cancelación**, para que el hotel pueda tomar **decisiones preventivas** y **mejorar su eficiencia operativa**.

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

## 🔍 Análisis General

- El dataset **no presenta valores nulos**, lo que facilita el procesamiento.  
- Incluye **variables temporales, económicas y de comportamiento del cliente**.  
- La variable objetivo (**target**) es `booking_status`.  

### 🧠 Variables con mayor potencial predictivo:
- `lead_time` (tiempo de antelación de reserva)  
- `avg_price_per_room` (precio promedio)  
- `no_of_special_requests` (solicitudes especiales)  
- `market_segment_type` (segmento de mercado)  
- `repeated_guest` (reincidencia del huésped)

---

## ⚙️ Herramientas Utilizadas
- **Python** (Jupyter Notebook)  
- **Pandas**, **NumPy**, **Matplotlib**, **Seaborn**, **Scikit-learn**  
- **GitHub** (control de versiones y documentación)

---

✍️ **Autor:** Luis Arbio  
📅 **Curso:** Data Science II - CoderHouse  

