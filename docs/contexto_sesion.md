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
- Repositorio GitHub: https://github.com/federicooscargiglio/proyecto-unicef-argentina

=== DÓNDE ESTAMOS ===
- Semana: 2 de 8
- Fase: Limpieza y auditoría de datos
- Último hito completado: Conversión a numérico + detección de nulos + limpieza filas basura en abandono_reciente + markdowns profesionales en 02_limpieza_datos.ipynb
- Estado del entorno: Funcionando

=== ARCHIVOS ACTUALES ===
- Datasets cargados (8 en total):
  - df_mat_2022, df_mat_2023, df_mat_2024 — matrícula total por departamento
  - df_edad_2022, df_edad_2023, df_edad_2024 — matrícula por edad
  - abandono_reciente — tasas 2012-2024 (27 filas, 17 columnas — filas basura eliminadas)
  - abandono_historico — tasas 2003-2016 (34 filas, 17 columnas — 2 filas de sub-encabezado eliminadas)
- Notebooks existentes:
  - 00_test_entorno.ipynb — entorno verificado, OK
  - 01_carga_datos.ipynb — limpio, 9 celdas, Run All sin errores
  - 01_carga_datos_backup.ipynb — backup de la versión anterior
  - 02_limpieza_datos.ipynb — EN PROGRESO (18 celdas, Run All sin errores)

=== ESTRUCTURA DE 02_limpieza_datos.ipynb ===
1. Título del notebook (markdown)
2. Imports, rutas y carga de datos (código)
3. Normalización — Matrícula total: rename de Departamento/Localizacion en 2024 (markdown + código)
4. Normalización — Matrícula por edad: función limpiar_columnas() elimina tildes y ñ (markdown + código)
5. Normalización — Abandono reciente: rename explícito de 17 columnas con prefijos prim_/sec_ (markdown + código)
6. Normalización — Abandono histórico: rename explícito + drop filas 0-1 + reset_index (markdown + código)
7. Conversión a numérico — columnas de abandono a float64 (markdown + código)
8. Detección de nulos — auditoría de los 8 datasets (markdown + código)
9. Inspección de nulos — abandono_reciente: identificación de nulos estructurales y filas basura (markdown + código)
10. Eliminación de filas basura — abandono_reciente: shape final (27, 17) (markdown + código)

=== CIERRE DE SESIÓN — HACER SIEMPRE ===
Al final de cada sesión de trabajo, antes de cerrar VS Code:
1. Guardar todos los archivos (Ctrl+S)
2. Actualizar diario.md y contexto_sesion.md
3. Subir cambios a GitHub:
   git add .
   git commit -m "descripción breve de lo que hiciste"
   git push

=== PRÓXIMO PASO ===
- Revisar nulos de abandono_historico (inspección pendiente)
- Crear decisions_log.md documentando todas las decisiones de limpieza

=== PENDIENTES IMPORTANTES ===
- Semana 2-3: los datos de bullying y apuestas de UNICEF están solo en PDF.
  Hay que extraer los números clave manualmente y construirlos como dataset propio.
  Fuente: Encuesta Rápida UNICEF Argentina 2020-2024 (informes PDF públicos).

=== NOTAS TÉCNICAS ===
- Archivos CSV del Ministerio: separador ";" y encoding "latin-1"
- Archivos Excel de abandono: skiprows=10
- Los archivos están en data/raw/ dentro de la carpeta del proyecto
- Columnas de abandono convertidas a float64 con pd.to_numeric(errors='coerce')
- Nomenclatura elegida para abandono: prim_ (primaria), sec_ (secundaria),
  sec_cb_ (ciclo básico), sec_co_ (ciclo orientado)
- abandono_historico tenía 2 filas de sub-encabezados → eliminadas con drop(index=[0,1])
- abandono_reciente tenía filas basura (pie de página Excel) → eliminadas con dropna(how='all') sobre columnas numéricas
- NaN estructurales esperados en abandono_reciente: prim_7 en provincias 6-6, sec_7 en provincias 7-5
- Windows oculta extensiones por defecto — activar en Vista > Extensiones de nombre de archivo
- Siempre abrir VS Code desde la carpeta del proyecto para que la terminal arranque correctamente