Reflexión sobre el proceso de refactorización asistida por agentes

Introducción



Durante este reto utilicé Claude Code como asistente para analizar y refactorizar progresivamente un proyecto Python existente.



El objetivo no fue permitir que el agente reescribiera el proyecto completo, sino utilizarlo dentro de un proceso controlado en el que cada cambio pudiera ser revisado y validado mediante tests.



Estrategias de prompting utilizadas



La estrategia que produjo mejores resultados fue proporcionar instrucciones específicas y limitar el alcance de cada tarea.



En lugar de solicitar una refactorización general, se trabajó con prompts que indicaban:



qué problema debía analizarse

qué archivo o función estaba involucrado

qué comportamiento debía mantenerse

qué cambios estaban permitidos

qué cambios estaban prohibidos

que los tests no debían modificarse



Esto permitió reducir cambios innecesarios y facilitó identificar el efecto de cada refactorización.



Uso incremental



Una de las principales lecciones fue la importancia de realizar una sola refactorización a la vez.



Después de cada cambio se ejecutó la suite de tests.



El flujo utilizado fue:



Analizar

&#x20;  ↓

Proponer solución

&#x20;  ↓

Aplicar un cambio

&#x20;  ↓

Revisar diff

&#x20;  ↓

Ejecutar tests

&#x20;  ↓

Documentar

&#x20;  ↓

Commit



Este enfoque permitió detectar rápidamente cualquier regresión.



Prompts que funcionaron mejor



Los prompts más efectivos fueron aquellos que establecieron restricciones claras.



Por ejemplo, indicar:



"No cambies la lógica, no modifiques los tests y realiza únicamente esta refactorización."



produjo resultados más controlables que solicitar simplemente:



"Mejora este código."



También fue útil pedir primero un análisis antes de permitir modificaciones.



Lo que funcionó bien



Claude Code fue especialmente útil para:



localizar code smells

explicar código existente

identificar funciones con demasiadas responsabilidades

sugerir nombres más claros

proponer extracción de funciones

identificar oportunidades para agregar type hints

revisar posibles mejoras en manejo de errores

Lo que requirió mayor supervisión



El agente no debe considerarse una autoridad sobre el comportamiento del programa.



Fue necesario revisar los cambios realizados y comprobar los tests después de cada modificación.



También fue importante evitar prompts demasiado generales, porque una solicitud amplia puede provocar múltiples cambios simultáneos y dificultar determinar cuál cambio provocó un problema.



Aprendizajes sobre prompt engineering



El principal aprendizaje fue que la calidad de la respuesta del agente depende en gran medida del contexto proporcionado.



Un prompt efectivo debe especificar:



contexto

objetivo

restricciones

alcance

criterio de aceptación



Una estructura que resultó útil fue:



Contexto

\+

Problema

\+

Objetivo

\+

Restricciones

\+

Validación esperada

Conclusión



La principal conclusión es que Claude Code resulta más efectivo cuando se utiliza como parte de un proceso de ingeniería controlado y no como sustituto de la revisión del desarrollador.



La combinación de prompts específicos, cambios pequeños, revisión del diff y ejecución frecuente de tests permitió mejorar la calidad del código manteniendo su comportamiento.



Para un proyecto real continuaría utilizando este enfoque incremental, complementándolo con revisión humana, tests automatizados y herramientas de análisis estático.

