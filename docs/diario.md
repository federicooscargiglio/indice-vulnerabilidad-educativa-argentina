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

## 16/03/2026 — Semana 2, Día 1 (continuación)

**Qué hicimos:**
- Configuramos Git por primera vez (user.name y user.email)
- Creamos el repositorio público en GitHub: proyecto-unicef-argentina
- Conectamos la carpeta local con GitHub y subimos el proyecto completo
- Armamos README.md profesional con descripción bilingüe, tabla de estado semanal,
  fuentes de datos, stack tecnológico y estructura de carpetas

**Problemas / decisiones:**
- FileNotFoundError en push → causa: nombre de rama local era "master" en vez de "main"; solución: git branch -m master main
- Error 403 → causa: credenciales de otra cuenta de GitHub guardadas en Windows; solución: limpiar desde Administrador de credenciales
- Push rechazado → causa: GitHub tenía un commit con la licencia MIT que el local no tenía; solución: git pull --allow-unrelated-histories
- Editor vim abierto para confirmar merge → solución: :wq para guardar y salir
- Título "Licenciado en Ciencias de Datos" corregido a "Diplomado en Ciencias de Datos — UTN"
- Link de LinkedIn corregido con URL real del perfil

**Próxima sesión:**
- Crear decisions_log.md documentando las decisiones de limpieza
- Convertir columnas de abandono de object a numérico
- Detectar y documentar valores nulos