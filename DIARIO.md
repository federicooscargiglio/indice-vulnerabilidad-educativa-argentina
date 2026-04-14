# Diario de trabajo — Índice de Vulnerabilidad Educativa — Argentina

---

## Sesión 2026-04-09

**Estado:** Semana 4 — Reestructuración del proyecto  
**Último hito:** EDA Parte I completa (5 visualizaciones sobre abandono y matrícula)  
**Próximo paso:** Exploración inicial de las 3 bases nuevas del Relevamiento Anual 2024

**Notas:**
- Repo reorganizado: raw/ ahora tiene subcarpetas por año
- Descargadas Base 2 (Matrícula), Base 3 (Trayectoria) y Base 5 (Características) del RA 2024
- Duplicado de 2024 Matrícula eliminado de raw/
- Archivos de tasas de abandono histórico movidos a raw/abandono_historico/
- Tema del proyecto actualizado de "bullying/apuestas" a "trayectorias educativas"
- Estrategia definida: modelo ML con datos 2024, tendencia visual con 2022-2024

---

## Sesión 2026-04-09 (continuación)

**Estado:** Semana 4 — Reestructuración completa del proyecto  
**Último hito:** 01_carga_datos.ipynb actualizado y funcionando con las 3 bases nuevas  
**Próximo paso:** Reestructurar 02_limpieza_datos.ipynb y 03_eda.ipynb

**Notas:**
- Base 3 (Trayectoria) confirmada: variable target identificada = `ssp_*` (salidos sin pase)
- 1.209 escuelas con datos de abandono por grado (ssp_1 a ssp_12)
- Fórmula del target definida: tasa_abandono = ssp_total / inicial_total × 100
- Todas las rutas del notebook corregidas después de reorganización de raw/
- Notebook corre limpio de principio a fin sin errores

## Sesión 2026-04-10

**Estado:** Semana 4 — Limpieza de datos completada  
**Último hito:** 02_limpieza_datos.ipynb reestructurado y corriendo limpio (19 celdas)  
**Próximo paso:** Reestructurar 03_eda.ipynb y agregar EDA sobre bases RA 2024

**Notas:**
- Rutas corregidas de absolutas a relativas — notebook ahora es reproducible en cualquier máquina
- Función limpiar_columnas() mejorada con normalize("NFKD") — reemplaza método frágil de mojibake manual
- Bases RA 2024 (Base 2, 3 y 5) cargadas y limpias — cero nulos en las tres
- Unidad de análisis confirmada: segmento (provincia × departamento × sector × ámbito), no por escuela
- Pregunta de investigación actualizada en README y contexto_sesion.md
- tasa_abandono calculada sobre Base 3 — rango 0% a 43.33%, media 0.86%, 1 NaN estructural
- 11 datasets exportados a data/clean/ — 8 existentes + base2, base3, base5
- Decisión registrada: datos del Ministerio no tienen granularidad por escuela — se trabaja con agregados

## Sesión 2026-04-13
**Estado:** Semana 4 — EDA en curso
**Último hito:** 03_eda.ipynb reestructurado — ruta relativa corregida, base3 y base5 agregadas a la carga
**Próximo paso:** Agregar Parte II del EDA — análisis de tasa_abandono por segmento RA 2024
**Notas:**
- Proyecto renombrado a "Índice de Vulnerabilidad Educativa — Argentina"
- Carpeta local y repositorio GitHub renombrados
- README actualizado con nuevo nombre y descripción
- contexto_sesion.md pendiente de actualizar (fuera del repo)

## Sesión 14/04/2026

### Objetivos de la sesión
- Completar EDA Parte II: análisis de tasa_abandono por segmento sobre base3_trayectoria

### Lo que se hizo
- Verificación del archivo base3_trayectoria.csv: separador coma (no punto y coma),
  tasa_abandono ya calculada, 1.209 segmentos, 1 NaN estructural
- Identificado segmento con máximo abandono: Catamarca — Valle Viejo — Estatal — Rural (43.33%)
- Análisis 6: distribución de tasa_abandono — distribución sesgada a la derecha,
  mediana 0.39%, media 0.86%, mayoría de segmentos entre 0% y 2%
- Análisis 7: abandono por provincia — Misiones, Entre Ríos y Formosa lideran (>1.5%),
  Buenos Aires y Mendoza en los valores más bajos
- Análisis 8: abandono por sector — estatales con mediana 5 veces mayor que privados (0.57% vs 0.11%)
- Análisis 9: abandono por ámbito — rurales con mediana más del doble que urbanos (0.64% vs 0.29%)
- Análisis 10: cruce sector × ámbito — Privado Rural lidera por tamaño de muestra pequeño (n=39),
  Privado Urbano es el grupo de menor riesgo (0.09%)
- Corregido warning de matplotlib: labels → tick_labels en boxplot de sector

### Outputs generados
- outputs/06_distribucion_tasa_abandono.png
- outputs/07_abandono_por_provincia_segmento.png
- outputs/08_abandono_por_sector.png
- outputs/09_abandono_por_ambito.png
- outputs/10_abandono_sector_ambito.png

### Hallazgos clave
- La distribución de tasa_abandono está fuertemente sesgada: el 75% de los segmentos
  tiene menos de 1.20% de abandono
- La brecha más pronunciada es entre Privado Urbano y todos los demás grupos
- Privado Rural (n=39) requiere interpretación cautelosa — perfil atípico
- El desbalance de clases será una consideración clave al definir el target binario para ML

### Próximo paso
- Feature engineering: definir features del modelo, target binario y unir bases 2, 3 y 5