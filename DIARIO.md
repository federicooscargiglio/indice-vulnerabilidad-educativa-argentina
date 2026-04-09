# Diario de trabajo — Trayectorias Educativas en Argentina

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