# Trayectorias Educativas en Argentina — Análisis de Datos y Machine Learning

> **English summary:** Data analysis and machine learning project on school dropout risk 
> in Argentina. Built with Python, pandas, scikit-learn and Looker Studio. Data source: 
> Ministerio de Educación — Relevamiento Anual 2024. Goal: build a school-level dropout 
> risk index to support NGO intervention prioritization.

---

## ¿De qué trata este proyecto?

Este proyecto analiza las trayectorias educativas en Argentina (nivel primario y secundario)
con foco en la identificación de escuelas en riesgo de abandono escolar.

A través de datos públicos del Ministerio de Educación (Relevamiento Anual 2024), se 
construye un índice de riesgo de abandono por establecimiento educativo. El objetivo es 
que ese índice sea una herramienta concreta para que organizaciones como 
**Argentinos por la Educación** y **UNICEF Argentina** puedan priorizar intervenciones 
territoriales.

---

## Preguntas de investigación

**Principal**
> ¿Qué variables institucionales y de trayectoria escolar predicen que un establecimiento 
> presente tasas críticas de abandono, y es posible construir un índice de riesgo por 
> escuela operacionalmente útil?

**Secundarias**
1. ¿Cómo se distribuye el abandono, la repitencia y la sobreedad por provincia y nivel 
   educativo?
2. ¿En qué medida el nivel socioeconómico del hogar explica diferencias en rendimiento 
   que derivan en abandono?
3. ¿Es posible construir un índice compuesto de riesgo por escuela interpretable para 
   tomadores de decisión no técnicos?

---

## Estado actual

| Semana | Fase | Estado |
|--------|------|--------|
| Semana 1–2 | Setup, recolección y limpieza de datos | ✅ Completada |
| Semana 3 | EDA Parte I — abandono y matrícula | ✅ Completada |
| Semana 4 | EDA Parte II — repitencia, sobreedad, características | 🔄 En curso |
| Semana 5 | Feature engineering y preparación para ML | ⏳ Pendiente |
| Semana 6 | Modelado — clasificación y construcción del índice | ⏳ Pendiente |
| Semana 7 | Validación, interpretación y visualización | ⏳ Pendiente |
| Semana 8 | Informe final y presentación | ⏳ Pendiente |

---

## Hallazgos clave — EDA I (Semana 3)

- **Secundaria 12° año (~20% de abandono):** pico más alto de toda la trayectoria escolar
- **Chaco (14.3%), Salta (12.1%) y Misiones (12.0%)** lideran el abandono provincial
- **Promedio nacional:** 8.0% (período reciente) vs 9.3% (histórico) — tendencia positiva
- **Sin relación lineal** entre tamaño del sistema educativo y tasa de abandono provincial

---

## Fuentes de datos

| Dataset | Fuente | Cobertura |
|---------|--------|-----------|
| Base por Escuela — Relevamiento Anual 2024 | [datos.gob.ar](https://datos.gob.ar/dataset/educacion-base-datos-por-escuela-2024) | Matrícula, repitencia, sobreedad, trayectoria, características del establecimiento |
| Tasas de abandono interanual 2003–2024 | [datos.gob.ar](https://datos.gob.ar) | Serie histórica por provincia y nivel |
| Matrícula agregada 2022–2024 | [datos.gob.ar](https://datos.gob.ar) | Tendencia reciente por provincia |

> **Nota metodológica:** Los años 2020 y 2021 quedan fuera del modelo por la ruptura 
> estructural que generó la pandemia COVID-19 en las trayectorias escolares. Se mencionan 
> en el análisis descriptivo como contexto histórico.

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

trayectorias-educativas-argentina/
│
├── data/
│   ├── raw/
│   │   ├── 2022_relevamiento/     # Matrícula 2022
│   │   ├── 2023_relevamiento/     # Matrícula 2023
│   │   ├── 2024_relevamiento/     # Base 2 (matrícula), Base 3 (trayectoria),
│   │   │                          # Base 5 (características) — fuente principal
│   │   └── abandono_historico/    # Series 2003–2024
│   ├── clean/                     # Datos procesados listos para análisis
│   └── ml/                        # Datasets preparados para modelos
│
├── notebooks/
│   ├── 00_test_entorno.ipynb      # Verificación de entorno
│   ├── 01_carga_datos.ipynb       # Carga de datasets
│   ├── 02_limpieza_datos.ipynb    # Limpieza y auditoría
│   └── 03_eda.ipynb               # EDA I — abandono y matrícula
│
├── outputs/                       # Visualizaciones generadas
├── DIARIO.md                      # Bitácora de sesiones de trabajo
├── decisions_log.md               # Registro de decisiones técnicas
└── README.md

---

---

## Autor

**Federico Oscar Giglio**  
Diplomado en Ciencias de Datos — UTN  
[LinkedIn](https://www.linkedin.com/in/federico-claudio-sait-oscar-giglio/) · 
[GitHub](https://github.com/federicooscargiglio)

---

## Licencia

Este proyecto está bajo la licencia [MIT](LICENSE).