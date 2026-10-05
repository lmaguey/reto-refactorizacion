CLAUDE.md

Descripción del proyecto



Este proyecto es una aplicación Python utilizada para el reto de refactorización asistida por agentes.



El objetivo principal es mejorar la calidad, legibilidad y mantenibilidad del código sin modificar su comportamiento funcional.



Reglas generales

Mantener la funcionalidad existente.

No modificar los tests para hacerlos pasar.

Realizar cambios pequeños e incrementales.

Ejecutar los tests después de cada refactorización.

No realizar varias refactorizaciones independientes en un mismo cambio.

Mantener las APIs públicas existentes salvo que exista una razón justificada.

Evitar cambios innecesarios fuera del alcance de la refactorización.

Estilo de código

Seguir PEP 8.

Utilizar nombres descriptivos para variables, funciones y clases.

Preferir funciones pequeñas con una responsabilidad clara.

Evitar código duplicado.

Utilizar type hints en funciones nuevas o modificadas cuando sea apropiado.

Evitar comentarios que simplemente repitan lo que hace el código.

Mantener los comentarios únicamente cuando aporten contexto útil.

Manejo de errores

No ocultar excepciones silenciosamente.

Capturar excepciones específicas en lugar de utilizar except Exception cuando sea posible.

Los mensajes de error deben ser claros y útiles.

No modificar el comportamiento esperado de las excepciones existentes sin verificar los tests.

Testing



Antes de comenzar cualquier refactorización:



pytest



Después de cada refactorización:



pytest



Todos los tests existentes deben continuar pasando.



Linting



Antes de finalizar el trabajo ejecutar la herramienta de linting configurada por el proyecto.



Si existe configuración específica en pyproject.toml, respetarla.



Estrategia de refactorización



Para cada cambio:



Analizar primero el código.

Explicar el problema encontrado.

Proponer una solución.

Aplicar un cambio pequeño.

Ejecutar los tests.

Corregir cualquier regresión.

Documentar el cambio en docs/bitacora.md.

Crear un commit cuando el cambio esté validado.

Restricciones

No eliminar funcionalidad.

No modificar tests salvo que el instructor indique expresamente lo contrario.

No introducir dependencias nuevas sin justificación.

No hacer una reescritura completa del proyecto.

Priorizar cambios pequeños, comprensibles y verificables.

