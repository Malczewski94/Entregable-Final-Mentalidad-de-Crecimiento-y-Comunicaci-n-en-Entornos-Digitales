# Entregable-Final-Mentalidad-de-Crecimiento-y-Comunicaci-n-en-Entornos-Digitales
 Blog Técnico, Post-Mortem y Comunicación

Entregable Final: Blog Técnico, Post-Mortem y Comunicación

Entrada de Blog Técnico (Contenido Publicado)
A continuación se detalla el contenido exacto que publiqué en mi blog técnico, siguiendo las buenas prácticas de documentación para audiencias mixtas (técnicas y no técnicas).

Post-Mortem: Caída del Sistema durante la Generación de Reportes de Cierre de Mes
Contexto:
En mi rol actual, desarrollo una plataforma de gestión financiera corporativa. Uno de los módulos principales que tengo a mi cargo permite a los usuarios administradores generar un reporte consolidado al final de cada mes para analizar grandes volúmenes de datos. El entorno tecnológico está compuesto por una arquitectura en la nube con una base de datos relacional.
Problema:
El último día del mes pasado, a las 10:00 AM (hora pico de uso), la plataforma entera quedó inoperativa durante 45 minutos. Los usuarios no podían iniciar sesión ni registrar nuevas operaciones. Para explicarlo sin jerga técnica: el código que escribí intentó leer y procesar millones de registros anuales de una sola vez, sin usar ningún "índice" o atajo (como intentar buscar una palabra específica en una biblioteca leyendo cada libro página por página). Esto acaparó el 100% de la memoria del servidor de base de datos, bloqueando al resto de los usuarios que intentaban realizar tareas cotidianas sencillas.
Acciones (Post-Mortem Constructivo):
Fiel a la cultura SRE (Site Reliability Engineering), realicé un análisis retrospectivo libre de culpas (blameless post-mortem) enfocado en entender qué falló en mi proceso de desarrollo y cómo mejorarlo.

Fase
Contención Inmediata
Acción Tomada
Reinicié de emergencia el servicio de base de datos para liberar la memoria y restablecer el acceso a los usuarios afectados de forma inmediata.
Fase
Análisis de Causa Raíz
Acción Tomada
Identifiqué que la consulta (query) SQL que diseñé para el reporte no tenía límite de paginación y faltaba un índice de búsqueda clave en la columna de fechas.
Fase
Solución Permanente
Acción Tomada
Agregué un índice a la tabla de transacciones y refactoricé mi código para implementar paginación (procesamiento de datos por pequeños lotes en vez de cargar todo a la vez).

