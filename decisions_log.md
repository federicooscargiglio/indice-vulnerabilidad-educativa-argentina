# Decisions Log — Índice de Vulnerabilidad Educativa — Argentina

Registro de decisiones analíticas tomadas durante el desarrollo del proyecto.
Cada entrada documenta qué se encontró, qué se decidió y el criterio utilizado.

---

## Carga de datos

**DEC-001 — Parámetros de lectura para CSVs de matrícula**
- Datasets: df_mat_2022, df_mat_2023, df_mat_2024, df_edad_2022, df_edad_2023, df_edad_2024
- Decisión: usar `sep=";"` y `encoding="latin-1"`
- Criterio: los archivos del Ministerio de Educación usan punto y coma como separador
  y codificación latin-1 por compatibilidad con sistemas legacy del Estado argentino.

**DEC-002 — Parámetros de lectura para Excel de abandono**
- Datasets: abandono_reciente, abandono_historico
- Decisión: usar `skiprows=10`
- Criterio: los archivos tienen 10 filas de encabezado institucional antes de los datos reales.
  Saltar esas filas evita que pandas las interprete como datos.

---

## Normalización de columnas

**DEC-003 — Rename manual en df_mat_2024**
- Problema: el archivo 2024 usaba "Departamento" y "Localizacion" en lugar de
  "departamento" y "localizacion" (mayúscula inicial vs minúscula).
- Decisión: rename explícito de esas dos columnas para alinear con 2022 y 2023.
- Criterio: consistencia entre años es necesaria para poder concatenar los datasets más adelante.

**DEC-004 — Función limpiar_columnas() para matrícula por edad**
- Problema: columnas con tildes y ñ (ej. "Año", "Región").
- Decisión: función que convierte a minúsculas, elimina tildes y reemplaza espacios por guión bajo.
- Criterio: nombres de columna sin caracteres especiales evitan errores en operaciones
  posteriores y son compatibles con cualquier sistema.

**DEC-005 — Rename explícito de 17 columnas en abandono_reciente y abandono_historico**
- Problema: columnas sin nombres descriptivos que no indicaban nivel educativo ni año.
- Decisión: prefijos `prim_` (primaria) y `sec_` (secundaria), con `sec_cb_` para
  ciclo básico y `sec_co_` para ciclo orientado.
- Criterio: nomenclatura que refleja la estructura real del sistema educativo argentino
  y facilita la lectura del código en análisis futuros.

---

## Limpieza estructural

**DEC-006 — Eliminación de filas de sub-encabezado en abandono_historico**
- Problema: filas 0 y 1 contenían sub-encabezados del Excel original, no datos.
- Decisión: `drop(index=[0,1])` seguido de `reset_index(drop=True)`.
- Criterio: esas filas no representan observaciones reales y distorsionarían cualquier análisis.

**DEC-007 — Eliminación de filas basura en abandono_reciente**
- Problema: filas del pie de página del Excel (definición metodológica, fuente, fecha,
  filas vacías de separación) quedaron cargadas como filas del DataFrame.
- Decisión: `dropna(subset=cols_numericas, how='all')` — eliminar filas donde todas
  las columnas numéricas son NaN.
- Criterio: el criterio es conservador (solo elimina si *todas* las numéricas son NaN),
  lo que evita borrar filas con datos parciales legítimos.
- Shape final: (27, 17)

**DEC-008 — Eliminación de filas basura en abandono_historico**
- Problema: idéntico a DEC-007. Pie de página del Excel con definición, fuente y fecha.
- Decisión: mismo criterio — `dropna(subset=cols_numericas, how='all')`.
- Shape final: (27, 17)

---

## Conversión de tipos

**DEC-009 — Conversión de columnas de abandono a float64**
- Datasets: abandono_reciente, abandono_historico
- Problema: columnas cargadas como `object` por mezcla de texto y números en el Excel.
- Decisión: `pd.to_numeric(errors='coerce')` sobre todas las columnas numéricas.
- Criterio: `errors='coerce'` convierte lo que no puede parsear a NaN en lugar de
  lanzar un error, lo que permite identificar después qué valores no eran numéricos.

---

## Valores nulos

**DEC-010 — NaN estructurales en prim_7 y sec_7 de abandono_reciente**
- Problema: nulos en columnas prim_7 y sec_7 para ciertas provincias.
- Decisión: no intervenir — estos NaN se conservan tal cual.
- Criterio: corresponden a diferencias estructurales del sistema educativo argentino.
  Provincias con estructura 6-6 no tienen 7° de primaria; provincias con estructura
  7-5 no tienen 7° de secundaria. El NaN es el dato correcto.


---


  ## Comparacion entre periodos
  
**DEC-011: Visualización III — comparación entre períodos superpuestos.
Se eligió comparar promedios de ambos datasets sabiendo que 2012–2016
aparece en los dos. La nota metodológica en el markdown del notebook
documenta esta limitación explícitamente.

---


## Cambios en ranking provincial entre períodos

**DEC-012 — Visualización IV — ranking provincial período histórico (2003–2016)**
- Decisión: replicar la estructura visual de Visualización II para permitir comparación directa entre períodos.
- Criterio: misma paleta, misma lógica de colores por promedio nacional, mismo tipo de gráfico.
- Hallazgo: San Juan (1°) y Formosa (2°) lideraban en 2003–2016. Chaco escala del puesto 9 al 1 en 2012–2024. San Juan cae del puesto 1 al 12. La Rioja es consistentemente la provincia con menor abandono en ambos períodos.


## Visualización V — matrícula secundaria vs. abandono por provincia

## DEC-013
**Fecha:** 2025-03-27
**Decisión:** Visualización V — matrícula secundaria vs. abandono por provincia
**Contexto:** Cierre de EDA I. Se calculó matrícula secundaria total por provincia
sumando columnas _7 a _12 del dataset matricula_total_2024.csv. Las columnas _1–_6
corresponden a primaria y _7–_12 a secundaria (confirmado por totales coherentes
con cifras nacionales ~4.25M alumnos secundarios).
**Alternativas descartadas:** Columnas _sec1–_sec12 descartadas — representan
secciones/divisiones, no alumnos.
**Hallazgo:** No existe relación lineal entre tamaño del sistema educativo provincial
y tasa de abandono. El abandono responde a factores estructurales propios de cada
provincia. Buenos Aires (1.6M alumnos, 6.7% abandono) y Chaco (122k alumnos,
14.3% abandono) ilustran el punto.
**Impacto:** Output guardado como 05_matricula_vs_abandono.png.


---


---

## Reestructuración del proyecto

**DEC-014 — Pivoteo de tema y redefinición del alcance**
- Fecha: 2026-04-09
- Decisión: cambio de tema de "Bullying escolar y apuestas online" a 
  "Trayectorias Educativas en Argentina con foco en riesgo de abandono escolar".
- Criterio: los datos disponibles públicamente (Relevamiento Anual, tasas de abandono)
  son sólidos y accionables. No existen microdatos públicos de calidad sobre bullying
  en Argentina. El nuevo enfoque permite construir un producto concreto — un índice de
  riesgo por escuela — y apuntar a organizaciones reales como Argentinos por la 
  Educación y UNICEF Argentina.
- Impacto: repo renombrado a trayectorias-educativas-argentina. Las decisiones 
  DEC-001 a DEC-013 se mantienen — el trabajo de limpieza sobre datos de abandono
  y matrícula es válido en el nuevo contexto.
- Fuente principal redefinida: Relevamiento Anual 2024 — Ministerio de Educación
  (Bases 2, 3 y 5 por establecimiento educativo).
- Pregunta principal: ¿Qué variables predicen tasas críticas de abandono por segmento geografico
  y es posible construir un índice de riesgo operacionalmente útil?


## DEC-015 — Unidad de análisis: segmento en lugar de establecimiento
**Fecha:** 10/04/2026
**Contexto:** Las bases del Relevamiento Anual 2024 descargadas son versiones agregadas
(sufijo `agregada(in).csv`). No existe CUEANEXO ni identificador de establecimiento individual.
La combinación provincia × departamento × sector × ámbito es única en las tres bases
y opera como clave de identificación.
**Decisión:** La unidad de análisis del modelo pasa de establecimiento a segmento educativo.
**Impacto:** Pregunta de investigación, README y foco del proyecto actualizados.
El índice de riesgo se construye por segmento, no por escuela.
**Alternativa descartada:** Buscar bases desagregadas por escuela en el sitio del Ministerio.
Se descartó porque no existen archivos con esa granularidad disponibles públicamente.

## DEC-016 — Inclusión de grados 1314 y 20 en el cálculo de tasa_abandono
**Fecha:** 10/04/2026
**Contexto:** Base 3 incluye columnas ssp_1314 y ssp_20 además de ssp_1 a ssp_12.
**Decisión:** Se incluyen en el cálculo de ssp_total e inicial_total.
**Justificación:** El Ministerio los reporta con el mismo prefijo que los grados estándar,
lo que indica que pertenecen al flujo de trayectoria del segmento. Excluirlos sin
justificación metodológica sería arbitrario.

## DEC-017 — Conversión de limpiar_columnas() a método NFKD
**Fecha:** 10/04/2026
**Contexto:** La versión anterior reemplazaba caracteres mojibake manualmente
(Ã¡ → a, Ã© → e, etc.). Ese método es frágil y dependiente del encoding del archivo.
**Decisión:** Se reemplaza por normalize("NFKD") + encode("ascii", errors="ignore"),
que descompone cualquier carácter acentuado correctamente sin depender del encoding fuente.
**Impacto:** limpiar_columnas() en 02_limpieza_datos.ipynb actualizada.

## DEC-018 — Renombrado del proyecto
**Fecha:** 13/04/2026
**Decisión:** El proyecto se renombra de "Trayectorias Educativas en Argentina" a
"Índice de Vulnerabilidad Educativa — Argentina".
**Criterio:** El nombre anterior describía el proceso de análisis. El nuevo nombre
describe el producto final — el índice — y comunica mejor el valor concreto del
proyecto para tomadores de decisión y reclutadores.
**Impacto:** Carpeta local, repositorio GitHub, README, DIARIO y encabezados de
notebooks actualizados.

### DEC-019 — Base5 sin variables de accesibilidad física
- Fecha: 14/04/2026
- Decisión: Base5 no contiene variables de caminos, transporte o distancia a la escuela. La variable `ambito` (Rural/Urbano) actúa como proxy indirecto.
- Motivo: El Relevamiento Anual releva características del establecimiento, no del entorno.
- Mejora futura: Cruzar con datos viales o censales del INDEC.

### DEC-020 — prop_multigrado descartada
- Fecha: 14/04/2026
- Decisión: Se descarta la feature `prop_multigrado` del modelo.
- Motivo: Las columnas `multi_ini`, `multi_pri`, `multi_sec` cuentan secciones multigrado, no escuelas. La proporción secciones/escuelas supera 1.0 en 300 segmentos (máximo 4.44), lo que invalida su uso como proporción.

### DEC-021 — Base 3 excluida como fuente de features (data leakage)
- Fecha: 14/04/2026
- Decisión: De Base 3 solo se usa `tasa_abandono` para construir el target binario. Ninguna otra columna de Base 3 entra como feature.
- Motivo: Las variables de flujo (promovidos, salidos, entrados, inicial) participan directamente en el cálculo de `tasa_abandono`. Usarlas como features generaría data leakage — el modelo tendría precisión artificial alta pero sería inútil para predicción real.

### DEC-022 — Umbral del target binario: percentil 75 (1.2%)
- Fecha: 14/04/2026
- Decisión: `abandono_alto = 1` si `tasa_abandono > 1.2%`, `0` si no.
- Resultado: 301 segmentos alto riesgo (24.9%), 906 bajo riesgo (75.1%).
- Justificación: Cuartil superior (criterio estándar), suficientes casos positivos para entrenar, volumen gestionable para priorización de intervenciones, consistente con quiebre natural observado en el EDA.

### DEC-023 — NaN en ratio_alumnos_seccion rellenados con mediana
- Fecha: 14/04/2026
- Decisión: 3 segmentos con 0 secciones registradas (Buenos Aires-Castelli, Chaco-General Belgrano, Santa Cruz) tenían NaN en `ratio_alumnos_seccion`. Se rellenaron con la mediana (21.77).
- Motivo: Probable error de registro en la fuente. Los 3 segmentos tienen datos válidos en todas las demás columnas, no se justifica eliminarlos.