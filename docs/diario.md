## 09/03/2026 — Semana 1, Día 1 

**Qué hicimos:**
- Creamos contexto_sesion.md con el template de inicio de sesión
- Confirmamos Python 3.11.9 ya instalado
- Instalamos todas las librerías: pandas, numpy, matplotlib, seaborn, scikit-learn, jupyter, openpyxl, requests
- Verificamos entorno con python -c "import pandas" — funcionando

**Problemas / decisiones:**
- WARNING de PATH en la instalación — no afecta el proyecto
- Notice de pip desactualizado — ignorar por ahora

**Mañana:**
- Instalar extensiones Python y Jupyter en VS Code
- Crear primer notebook de prueba
- Arrancar con los datasets de UNICEF

---

## 10/03/2026 — Semana 1, Día 2

**Qué hicimos:**
- Instalamos extensiones VS Code: Jupyter, Pylance, Rainbow CSV
- Creamos y ejecutamos 00_test_entorno.ipynb — pandas 2.3.3, seaborn 0.13.2, sklearn 1.7.2, gráfico OK
- Descargamos 8 datasets reales del Ministerio de Educación y los guardamos en data/raw/
- Creamos 01_carga_datos.ipynb y cargamos todos los datasets con pandas
- Ejecutamos primer .info() y .describe() sobre matrícula y abandono interanual

**Problemas / decisiones:**
- FileNotFoundError al cargar CSVs — causa: faltaba extensión .csv en la ruta. Windows la oculta por defecto. Solución: activar "Extensiones de nombre de archivo" en Vista del Explorador
- Archivos CSV usan separador ";" y encoding "latin-1" — parámetros necesarios en pd.read_csv
- Excel de abandono tenía 10 filas de encabezado institucional — solucionado con skiprows=10
- Columnas de abandono con dtype object en vez de numérico — texto mezclado, se limpia en Semana 2

**Mañana:**
- Limpiar y reorganizar 01_carga_datos.ipynb (estructura, markdowns, orden lógico)
- Pendiente Semana 2-3: extraer datos de bullying/apuestas de PDFs de UNICEF y construirlos como dataset propio

----


## 13/03/2026 — Semana 1, Día 3

**Qué hicimos:**
- Reorganizamos 01_carga_datos.ipynb completo: de 18 celdas desordenadas a 9 celdas con estructura profesional
- Agregamos encabezado del proyecto con autor, fecha y descripción
- Separamos imports de carga de datos (buena práctica)
- Agregamos los 3 CSV de matrícula por edad que faltaban (df_edad_2022/23/24)
- Eliminamos todas las celdas de exploración/investigación que habían quedado del proceso de trabajo
- Documentamos la decisión de skiprows=10 en el markdown de la sección de abandono
- Notebook corre completo con Run All sin errores

**Problemas / decisiones:**
- Celda markdown ejecutada como código → SyntaxError: cambiar tipo de celda con tecla M
- NameError en abandono_reciente → causa: orden de ejecución; solución: Run All
- Celdas duplicadas (vieja + nueva) → eliminadas manualmente
- Carpeta del proyecto está directamente en Desktop\PROYECTO UNICEF\ sin subcarpeta adicional

**Próxima sesión:**
- Arrancar Semana 2: limpieza de datos
- Normalizar nombres de columnas, convertir dtypes, detectar nulos, crear decisions_log.md

## 16/03/2026 — Semana 2, Día 1

**Qué hicimos:**
- Creamos 02_limpieza_datos.ipynb como notebook dedicado a limpieza
- Eliminamos las celdas de diagnóstico que habíamos agregado en 01_carga_datos.ipynb
- Normalizamos columnas de los 8 datasets con tres estrategias distintas:
  - df_mat_2024: rename puntual de "Departamento" y "Localizacion" → snake_case
  - df_edad (2022/23/24): función limpiar_columnas() en bloque para eliminar tildes y ñ
  - abandono_reciente: rename explícito de 17 columnas con nomenclatura prim_/sec_
  - abandono_historico: rename explícito de 17 columnas + drop de filas 0 y 1 (eran sub-encabezados del Excel, no datos) + reset_index

**Problemas / decisiones:**
- FileNotFoundError al intentar cargar CSVs → causa: nombres de archivo inventados, no coincidían con los reales; solución: os.listdir() para ver los nombres exactos
- Los archivos están en data/raw/, no en la raíz del proyecto
- abandono_historico tenía encabezado multinivel de 3 niveles → pandas lo leyó como filas; se resolvió con drop(index=[0,1])
- Nomenclatura elegida para abandono: prim_ para primaria, sec_ para secundaria, sec_cb_ y sec_co_ para ciclo básico y orientado

**Próxima sesión:**
- Crear decisions_log.md documentando las decisiones de limpieza de hoy
- Convertir columnas de abandono de object a numérico
- Detectar y documentar valores nulos