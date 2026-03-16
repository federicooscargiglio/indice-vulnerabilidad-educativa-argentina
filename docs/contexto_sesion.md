# Contexto de Sesión — Proyecto UNICEF

CONTEXTO DEL PROYECTO — LEER ANTES DE RESPONDER

=== QUIÉN SOY ===
- Nombre: Federico Oscar Giglio
- Perfil: Recién graduado en Ciencias de Datos, nivel Python básico
- Objetivo: Colaborar o entrar a UNICEF Argentina
- OS: Windows | Editor: VS Code

=== EL PROYECTO ===
- Tema: Bullying escolar y apuestas online en adolescentes argentinos
- Fuentes: UNICEF Argentina, INDEC-EPH, Ministerio de Educación, SENAF
- Stack: Python, pandas, scikit-learn, matplotlib/seaborn, Looker Studio
- Drive: C:\Users\fedeo\Desktop\PROYECTO UNICEF\

=== DÓNDE ESTAMOS ===
- Semana: 2 de 8
- Fase: Limpieza y auditoría de datos
- Último hito completado: Normalización de columnas de los 8 datasets en 02_limpieza_datos.ipynb
- Estado del entorno: Funcionando

=== ARCHIVOS ACTUALES ===
- Datasets cargados (8 en total):
  - df_mat_2022, df_mat_2023, df_mat_2024 — matrícula total por departamento
  - df_edad_2022, df_edad_2023, df_edad_2024 — matrícula por edad
  - abandono_reciente — tasas 2012-2024 (38 filas, 17 columnas)
  - abandono_historico — tasas 2003-2016 (34 filas, 17 columnas — 2 filas de sub-encabezado eliminadas)
- Notebooks existentes:
  - 00_test_entorno.ipynb — entorno verificado, OK
  - 01_carga_datos.ipynb — limpio, 9 celdas, Run All sin errores
  - 01_carga_datos_backup.ipynb — backup de la versión anterior
  - 02_limpieza_datos.ipynb — EN PROGRESO (normalización de columnas completa)

=== ESTRUCTURA DE 02_limpieza_datos.ipynb ===
1. Título del notebook (markdown)
2. Imports, rutas y carga de datos (código)
3. Normalización — Matrícula total: rename de Departamento/Localizacion en 2024 (markdown + código)
4. Normalización — Matrícula por edad: función limpiar_columnas() elimina tildes y ñ (markdown + código)
5. Normalización — Abandono reciente: rename explícito de 17 columnas con prefijos prim_/sec_ (markdown + código)
6. Normalización — Abandono histórico: rename explícito + drop filas 0-1 + reset_index (markdown + código)

=== PRÓXIMO PASO ===
- Crear decisions_log.md documentando las decisiones de limpieza
- Convertir columnas de abandono de object a numérico
- Detectar y documentar valores nulos

=== PENDIENTES IMPORTANTES ===
- Semana 2-3: los datos de bullying y apuestas de UNICEF están solo en PDF.
  Hay que extraer los números clave manualmente y construirlos como dataset propio.
  Fuente: Encuesta Rápida UNICEF Argentina 2020-2024 (informes PDF públicos).

=== NOTAS TÉCNICAS ===
- Archivos CSV del Ministerio: separador ";" y encoding "latin-1"
- Archivos Excel de abandono: skiprows=10
- Los archivos están en data/raw/ dentro de la carpeta del proyecto
- Columnas de abandono tienen dtype object en vez de numérico — pendiente de conversión
- Nomenclatura elegida para abandono: prim_ (primaria), sec_ (secundaria),
  sec_cb_ (ciclo básico), sec_co_ (ciclo orientado)
- abandono_historico tenía 2 filas de sub-encabezados → eliminadas con drop(index=[0,1])
- Windows oculta extensiones por defecto — activar en Vista > Extensiones de nombre de archivo
- Siempre abrir VS Code desde la carpeta del proyecto para que la terminal arranque correctamente