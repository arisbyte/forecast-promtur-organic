# Forecast de Canales GA4

Predicción de métricas de tráfico orgánico para 2026 usando Prophet de Facebook.

---

## Notebooks disponibles

Selecciona el notebook según tus datos:

### Forecast de métricas completas

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/arisbyte/forecast-promtur-organic/blob/main/notebooks/00_pipeline_session-scope_colab.ipynb)

**Métricas predichas:**
- Sesiones
- Bounce Rate
- Vistas por sesión
- Duración promedio de sesión

**Archivo CSV esperado:** `ga4_promtur_organic_2025.csv`

### Forecast de usuarios

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/arisbyte/forecast-promtur-organic/blob/main/notebooks/00_pipeline_user-scope_colab.ipynb)

**Métrica predicha:**
- Usuarios

**Archivo CSV esperado:** `ga4_promtur_organic_users_2025.csv`

---

## Descripción

Sistema de forecasting automatizado que predice métricas clave de Google Analytics 4 para cada canal de tráfico orgánico.

**Horizonte de predicción:** 12 meses (2026)  
**Modelo:** Prophet (Facebook) con intervalos de confianza del 95%

---

## Uso rápido

### Google Colab (recomendado)

1. Selecciona el notebook según tus datos (métricas completas o usuarios)
2. Haz clic en el badge **"Open in Colab"** correspondiente
3. Ejecuta todas las celdas (Runtime → Run all)
4. Sube tu CSV de GA4 cuando se te pida
5. Descarga los resultados en ZIP al finalizar

---

## Formato del CSV

### Para métricas completas

**Nombre de archivo:** `ga4_promtur_organic_2025.csv`

| Columna | Descripción |
|---------|-------------|
| `Year` | Año (2025) |
| `Month number` | Mes (1-12) |
| `Session Default Channel Group Custom (Recovery)` | Canal (Organic Search, Direct, etc.) |
| `Sessions - GA4` | Total de sesiones |
| `Bounces` | Total de rebotes |
| `Total session duration - GA4` | Duración total en segundos |
| `Views - GA4` | Total de vistas |

### Para usuarios

**Nombre de archivo:** `ga4_promtur_organic_users_2025.csv`

| Columna | Descripción |
|---------|-------------|
| `Year` | Año (2025) |
| `Month number` | Mes (1-12) |
| `Session Default Channel Group Custom (Recovery)` | Canal (Organic Search, Direct, etc.) |
| `Total Users - GA4` | Total de usuarios |

**Nota:** Al subir tu archivo en Colab, será renombrado automáticamente al nombre esperado.

---

## Resultados generados

### Métricas completas (Session Scope)

**Archivos CSV:**
- `dataset_clean.csv` - Datos procesados con métricas derivadas
- `forecasts_2026_all_channels.csv` - Predicciones mensuales 2026
- `canales_confiabilidad.csv` - Análisis de confiabilidad por canal

**Excel:**
- `tablas_resumen_2026.xlsx` - Una hoja por canal con:
  - Métricas en filas, meses en columnas
  - Duración en segundos Y formato HH:MM:SS

**Gráficos:**
- Comparativa histórico 2025 vs predicción 2026
- 4 gráficos por canal (sessions, bounce_rate, views_per_session, avg_session_duration)
- Intervalos de confianza visualizados
- Advertencias para canales poco confiables

### Usuarios (User Scope)

**Archivos CSV:**
- `dataset_users_clean.csv` - Datos procesados
- `forecasts_users_2026_all_channels.csv` - Predicciones mensuales 2026
- `canales_users_confiabilidad.csv` - Análisis de confiabilidad por canal

**Excel:**
- `tablas_resumen_users_2026.xlsx` - Una hoja por canal con predicciones mensuales

**Gráficos:**
- Comparativa histórico 2025 vs predicción 2026 de usuarios por canal
- Intervalos de confianza visualizados
- Advertencias para canales poco confiables

---

## Confiabilidad de predicciones

Ambos notebooks clasifican cada canal en 3 niveles:

### ALTA confiabilidad
- Volumen histórico mayor a 1,000 registros/mes
- Sin valores negativos predichos
- **Recomendación:** Usar para planificación estratégica

### MEDIA confiabilidad
- Volumen entre 100-1,000 registros/mes
- **Recomendación:** Usar considerando intervalos de confianza

### BAJA confiabilidad
- Volumen menor a 100 registros/mes o valores negativos
- **Recomendación:** NO usar para decisiones estratégicas
- Señalizado con advertencias visuales en gráficos

**Motivos de baja confiabilidad:**
- Solo 11 meses de datos históricos (2025)
- Canales con poco volumen tienen alta variabilidad
- Prophet requiere más datos para predicciones robustas

---

## Sobre el modelo

**Prophet** es un sistema de forecasting desarrollado por Facebook optimizado para:
- Series temporales con estacionalidad
- Datos faltantes y outliers
- Intervalos de confianza automáticos

**Configuración usada:**
- Sin estacionalidad anual (datos insuficientes)
- Intervalos de confianza: 95%
- Horizonte: 12 meses

**Limitaciones:**
- Bounce Rate puede predecir valores mayores a 100% (limitado automáticamente a 0-100%)
- Canales con bajo volumen generan predicciones poco confiables
- Tendencias pasadas se extrapolan al futuro

---

## Dependencias principales

- `prophet>=1.1.0` - Modelo de forecasting
- `pandas>=2.0.0` - Manipulación de datos
- `matplotlib>=3.7.0` - Visualizaciones
- `openpyxl>=3.1.0` - Exportación a Excel

Ver `requirements.txt` para lista completa.