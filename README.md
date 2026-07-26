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

Aprendizajes:
Validación en entornos realistas: Comprendí que no puedo asumir que si una función es rápida en mi entorno local de desarrollo (con pocos datos de prueba), lo será en producción. Es imperativo utilizar bases de datos con volúmenes masivos simulados para estas pruebas.
Autoevaluación y Revisiones: Ningún código de impacto estructural debe ser subido sin revisión. Actualicé mi propio flujo de trabajo para incluir un checklist personal antes de cada Pull Request, evaluando rigurosamente el impacto en el rendimiento.

Evidencia de Flujo de Trabajo y Control de Versiones
Gestioné este trabajo siguiendo el modelo de control de versiones con ramas separadas y redacté mensajes de commit descriptivos para asegurar la trazabilidad de mis cambios.
Captura de pantalla de los Commits / Pull Request en GitHub:

<img width="2555" height="1386" alt="Captura de pantalla 2026-07-26 172127" src="https://github.com/user-attachments/assets/8043b240-d3be-4f9c-ad21-a253294f03e9" />

Ejemplo de los commits que realicé en mi repositorio:
commit 7f656b3
feat: implemento paginacion por lotes para la generacion de reportes

commit 42ef8bf
fix: agrego indice en columna fecha para optimizar tiempo de respuesta

commit 8afd3f8
docs: publico entrada de blog con post-mortem constructivo del


Reflexión sobre Feedback Radicalmente Sincero
Durante la resolución de este incidente, recibí una sesión de feedback radicalmente sincero por parte de mi líder técnico que marcó un punto de inflexión en mi manera de enfocar el desarrollo. Aplicando el modelo de Kim Scott, su retroalimentación fue directa, constructiva y empática.
Me comunicó lo siguiente: "Entiendo perfectamente que querías entregar la funcionalidad del reporte antes del cierre de mes y valoro enormemente tu esfuerzo individual para cumplir con los tiempos (Care Personally). Sin embargo, el haber omitido las pruebas de estrés en la base de datos y acelerar tu proceso de revisión de código provocó la caída del sistema, afectando a los usuarios en producción (Challenge Directly)."
Al principio fue un impacto escucharlo, pero al separar el problema de mi persona, entendí que el objetivo no era juzgarme, sino salvaguardar la calidad técnica y enseñarme a prever riesgos. Esto me ayudó a adoptar una mentalidad de crecimiento genuina: comprendí que mi "agilidad" para entregar tareas no debe significar saltarme las medidas de seguridad. Gracias a esa conversación sincera, hoy soy mucho más riguroso con mis pruebas de carga. Entendí que el feedback claro, brindado sin ambigüedades pero con respeto humano, es la herramienta más poderosa para potenciar mi aprendizaje y construir confianza profesional.

URL pública del blog (GitHub Pages): https://malczewski94.github.io/Entregable-Final-Mentalidad-de-Crecimiento-y-Comunicaci-n-en-Entornos-Digitales/
