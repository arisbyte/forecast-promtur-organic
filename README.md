# Forecast de Canales GA4

Predicción de métricas de tráfico orgánico para 2026 usando Prophet de Facebook.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/arisbyte/forecast-promtur-organic/blob/main/notebooks/00_pipeline_completo.ipynb)

---

## Descripción

Sistema de forecasting automatizado que predice 4 métricas clave de Google Analytics 4 para cada canal de tráfico orgánico:

- **Sesiones**
- **Bounce Rate**
- **Vistas por sesión**
- **Duración promedio de sesión**

**Horizonte de predicción:** 12 meses (2026)  
**Modelo:** Prophet (Facebook) con intervalos de confianza del 95%

---

## Uso rápido

### Google Colab (recomendado)

1. Haz clic en el badge **"Open in Colab"** arriba
2. Ejecuta todas las celdas (Runtime → Run all)
3. Sube tu CSV de GA4 cuando se te pida
4. Descarga los resultados en ZIP al finalizar

## 📊 Formato del CSV

Tu archivo debe incluir estas columnas:

| Columna | Descripción |
|---------|-------------|
| `Year` | Año (2025) |
| `Month number` | Mes (1-12) |
| `Session Default Channel Group Custom (Recovery)` | Canal (Organic Search, Direct, etc.) |
| `Sessions - GA4` | Total de sesiones |
| `Bounces` | Total de rebotes |
| `Total session duration - GA4` | Duración total en segundos |
| `Views - GA4` | Total de vistas |

---

## Resultados generados

### Archivos CSV
- `dataset_clean.csv` - Datos procesados con métricas derivadas
- `forecasts_2026_all_channels.csv` - Predicciones mensuales 2026
- `canales_confiabilidad.csv` - Análisis de confiabilidad por canal

### Excel
- `tablas_resumen_2026.xlsx` - Una hoja por canal con:
  - Métricas en filas, meses en columnas
  - Duración en segundos Y formato HH:MM:SS

### Gráficos
- Comparativa histórico 2025 vs predicción 2026
- 4 gráficos por canal (sessions, bounce_rate, views_per_session, avg_session_duration)
- Intervalos de confianza visualizados
- Advertencias para canales poco confiables

---

## ⚠️ Confiabilidad de predicciones

El notebook clasifica cada canal en 3 niveles:

### 🟢 ALTA confiabilidad
- Volumen histórico > 1,000 sesiones/mes
- Sin valores negativos predichos
- **Recomendación:** Usar para planificación estratégica

### 🟡 MEDIA confiabilidad
- Volumen entre 100-1,000 sesiones/mes
- **Recomendación:** Usar considerando intervalos de confianza

### 🔴 BAJA confiabilidad
- Volumen < 100 sesiones/mes o valores negativos
- **Recomendación:** NO usar para decisiones estratégicas
- Señalizado con advertencias visuales

**¿Por qué baja confiabilidad?**
- Solo 11 meses de datos históricos (2025)
- Canales con poco volumen tienen alta variabilidad
- Prophet requiere más datos para predicciones robustas

---

## 🔮 Sobre el modelo

**Prophet** es un sistema de forecasting desarrollado por Facebook optimizado para:
- Series temporales con estacionalidad
- Datos faltantes y outliers
- Intervalos de confianza automáticos

**Configuración usada:**
- Sin estacionalidad anual (datos insuficientes)
- Intervalos de confianza: 95%
- Horizonte: 12 meses

**Limitaciones:**
- Bounce Rate puede predecir valores >100% (limitado automáticamente)
- Canales con bajo volumen generan predicciones poco confiables
- Tendencias pasadas se extrapolan al futuro

---

## Dependencias principales

- `prophet>=1.1.0` - Modelo de forecasting
- `pandas>=2.0.0` - Manipulación de datos
- `matplotlib>=3.7.0` - Visualizaciones
- `openpyxl>=3.1.0` - Exportación a Excel

Ver `requirements.txt` para lista completa.

---

## Recomendaciones

### Para uso en producción:
1. Validar predicciones vs datos reales de enero-febrero 2026
2. Ajustar modelos si MAPE > 30%
3. Considerar factores externos (campañas, estacionalidad)