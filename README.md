# 📊 Retail Pro - Modelo de Datos Relacional y Medidas Core en DAX

Este repositorio contiene la entrega del **Checkpoint 2** del módulo de Power BI para el proyecto analítico de **TechStore / Retail Pro**.

En esta etapa se transformó el conjunto de datos limpio del proceso ETL previo en un **Modelo Dimensional en Estrella (Star Schema)** funcional, con tabla de calendario propia, inteligencia de tiempo y un contenedor con las medidas métricas clave de negocio (DAX).

---
## 📌 Objetivos del Proyecto

1. **Modelado relacional en estrella:** Crear y validar relaciones activas $1:N$ con dirección de filtro único.
2. **Tabla de dimensión temporal:** Generar una tabla `Dim_Fechas` mediante DAX, configurada oficialmente como tabla de fechas.
3. **Contenedor de métricas:** Organizar una tabla dedicada exclusivamente a almacenar la librería de medidas.
4. **Cálculos en DAX:** Desarrollar los 5 KPIs fundamentales para el análisis del negocio (agregación, filtros, inteligencia de tiempo y optimización con variables).
5. **Validación visual:** Verificar la consistencia de los indicadores en una vista matricial por año y mes.

---

## 🛠️ Estructura del Modelo de Datos

El modelo sigue un esquema en estrella con las siguientes tablas y relaciones:

- **`Dim_Clientes`** (`id_cliente`) $\rightarrow$ **`Fact_Ventas`** (`id_cliente`) `[1:N]`
- **`Dim_Productos`** (`id_producto`) $\rightarrow$ **`Fact_Ventas`** (`id_producto`) `[1:N]`
- **`Dim_Categorias`** (`id_categoria`) $\rightarrow$ **`Dim_Productos`** (`id_categoria`) `[1:N]`
- **`Dim_Fechas`** (`Date`) $\rightarrow$ **`Fact_Ventas`** (`fecha_venta`) `[1:N]`

---

## 📊 Librería de Medidas DAX (`_Medidas`)

| Medida | Tipo de Cálculo | Fórmula / Concepto |
| :--- | :--- | :--- |
| **`Total Ventas`** | Agregación básica | `SUM(Fact_Ventas[total_venta])` |
| **`Ventas OnLine`** | Filtro con `CALCULATE` | Segmentación de ventas para el canal "OnLine" |
| **`Ventas YTD`** | Inteligencia de Tiempo | `TOTALYTD([Total Ventas], Dim_Fechas[Date])` |
| **`Ventas LY`** | Comparativa año anterior | `CALCULATE([Total Ventas], SAMEPERIODLASTYEAR(Dim_Fechas[Date]))` |
| **`% Crecimiento Anual`** | Optimización con `VAR` | Cálculo seguro de variación porcentual usando `DIVIDE()` y variables |

---

## 📁 Archivos en el Repositorio

- **`Castro_Rocio_Checkpoint2.pbix`**: Archivo principal de Power BI con el modelo completo, relaciones y medidas creadas.
