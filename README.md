# Proyecto UNICEF Argentina — Bullying Escolar y Apuestas Online

> **English summary:** Data analysis and machine learning project on school bullying and online gambling among Argentine adolescents. Built with Python, pandas, scikit-learn and Looker Studio. Data sources: UNICEF Argentina, Ministry of Education, INDEC. Currently in progress — Week 3 of 8 completed.

---

## ¿De qué trata este proyecto?

Este proyecto analiza dos problemáticas que afectan a los adolescentes argentinos: el **bullying escolar** y las **apuestas online**. A través de datos públicos de UNICEF Argentina, el Ministerio de Educación e INDEC, se construye un análisis completo que va desde la exploración de los datos hasta un modelo de Machine Learning para identificar perfiles de riesgo.

El objetivo final es presentar los hallazgos como propuesta de colaboración a **UNICEF Argentina**.

---

## Estado actual

| Semana | Fase | Estado |
|--------|------|--------|
| Semana 1 | Fundamentos y entorno | ✅ Completada |
| Semana 2 | Limpieza y auditoría de datos | ✅ Completada |
| Semana 3 | Análisis exploratorio I | ✅ Completada |
| Semana 4 | Análisis exploratorio II | ⏳ Pendiente |
| Semana 5 | Feature Engineering | ⏳ Pendiente |
| Semana 6 | Machine Learning I | ⏳ Pendiente |
| Semana 7 | Machine Learning II | ⏳ Pendiente |
| Semana 8 | Dashboard y propuesta final | ⏳ Pendiente |

---

## Hallazgos clave — EDA I (Semana 3)

- **sec_12 tiene ~20% de abandono**: el pico más alto de toda la trayectoria escolar
- **Chaco (14.3%), Salta (12.1%) y Misiones (12.0%)** lideran el abandono secundario provincial
- **Promedio nacional**: 8.0% (período reciente) vs 9.3% (período histórico) — tendencia positiva
- **Sin relación lineal** entre tamaño del sistema educativo y tasa de abandono provincial

---

## Fuentes de datos

| Fuente | Descripción |
|--------|-------------|
| [UNICEF Argentina — Encuesta Rápida 2020–2024](https://www.unicef.org/argentina/informes) | Bullying, bienestar y conductas de riesgo en adolescentes |
| [Ministerio de Educación](https://www.argentina.gob.ar/educacion/planeamiento/siteal) | Matrícula, deserción y repitencia por provincia |
| [INDEC — EPH](https://www.indec.gob.ar) | Nivel socioeconómico y condiciones habitacionales |
| [SITAN UNICEF Argentina 2024](https://www.unicef.org/argentina/informes/sitan) | Situación de la infancia y adolescencia |
| [SENAF](https://www.argentina.gob.ar/senaf) | Protección de niñez y vulnerabilidad |

---

## Stack tecnológico

- **Lenguaje:** Python 3.11
- **Análisis de datos:** pandas, numpy
- **Visualización:** matplotlib, seaborn
- **Machine Learning:** scikit-learn
- **Dashboard:** Google Looker Studio
- **Entorno:** Jupyter Notebooks / VS Code

---

## Estructura del proyecto

```
PROYECTO UNICEF/
│
├── data/
│   ├── raw/          # Datos originales sin modificar
│   ├── clean/        # Datos procesados y limpios (8 datasets)
│   └── ml/           # Datasets preparados para ML
│
├── notebooks/
│   ├── 00_test_entorno.ipynb        # Verificación de entorno
│   ├── 01_carga_datos.ipynb         # Carga de los 8 datasets
│   ├── 02_limpieza_datos.ipynb      # Limpieza y auditoría
│   └── 03_eda.ipynb                 # EDA I — 5 visualizaciones
│
├── outputs/          # Visualizaciones generadas
│   ├── 01_abandono_por_grado.png
│   ├── 02_abandono_por_provincia.png
│   ├── 03_abandono_por_periodo.png
│   ├── 04_abandono_historico_por_provincia.png
│   └── 05_matricula_vs_abandono.png
│
├── decisions_log.md  # Registro de decisiones técnicas (DEC-001 a DEC-013)
└── README.md
```

---

## Autor

**Federico Oscar Giglio**
Diplomado en Ciencias de Datos — UTN
[LinkedIn](https://www.linkedin.com/in/federico-claudio-sait-oscar-giglio/) · [GitHub](https://github.com/federicooscargiglio)

---

## Licencia

Este proyecto está bajo la licencia [MIT](LICENSE).