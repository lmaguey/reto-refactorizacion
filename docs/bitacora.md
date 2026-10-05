# Bitácora de refactorización

**Nombre:** Alejandro Maguey
**Matrícula:**
**Fecha:** 2026-10-04

Registra aquí **cada refactorización** que realices con Claude Code. Copia el
prompt tal cual lo escribiste (o un resumen fiel si fue una conversación larga),
describe el cambio que se aplicó al código y justifica por qué mejora la calidad.
Después de cada cambio ejecuta `pytest` y anota el resultado.

| #  | Prompt usado | Cambio realizado | Justificación | Tests OK |
|----|--------------|------------------|---------------|----------|
| 1  | "Quiero realizar únicamente la primera refactorización propuesta: Eliminar código muerto y comentarios obsoletos. Quitar `calcular_descuento_viejo`, el `exportar_txt` comentado, `reporteViejoCSV`, `MODO_DEBUG`, `import os` en reportes.py y los comentarios que solo repiten el código." | **Eliminación de código muerto + comentarios obsoletos.** `gestor.py`: se eliminan `calcular_descuento_viejo`, el bloque comentado `exportar_txt`, la variable `MODO_DEBUG` y los comentarios `# calculo del subtotal` y `# descontar del inventario`. `reportes.py`: se eliminan `reporteViejoCSV` y el `import os` sin uso. `almacen.py`: se elimina el comentario `# checa si ya existe el archivo de datos`. | Antes de borrar se confirmó con `grep` que ninguno de esos elementos se usaba en `src/` ni en `tests/`. El código muerto confunde (por ejemplo, una fórmula de descuento obsoleta junto a la vigente) y el historial de git ya lo conserva. Los comentarios eliminados solo repetían lo que dice el código; se conservaron los que aportan contexto de negocio (descuentos por volumen y regla VIP). `ruff check src` pasa de 20 a 17 errores (desaparecen F401, N802 y SIM115). | ✅ 20/20 |
| 2  | "Quiero realizar únicamente la #2, el manejo de archivos y errores en almacen.py" | **Manejo de errores (+ simplificación de condicionales).** `almacen.py`: `guardar_datos` y `cargar_datos` abren el archivo con `with` en lugar de `open()`/`close()` manual; `cargar_datos` captura `(json.JSONDecodeError, UnicodeDecodeError)` en lugar de `except Exception` y se quita el modo `"r"` redundante; `hayArchivo` regresa `os.path.exists(ruta)` directamente en lugar de un `if/else` con `True`/`False`. | Con `with`, el archivo se cierra aunque `json.dump`/`json.load` lancen una excepción (antes `guardar_datos` dejaba el archivo abierto si fallaba). Capturar excepciones específicas evita ocultar errores inesperados: un JSON mal formado o un archivo con UTF-8 inválido siguen regresando `False` con `"archivo corrupto"`, pero otros fallos ya no se silencian. Como el caso del archivo corrupto no está cubierto por los tests, se verificó con un script manual antes y después del cambio (JSON inválido, UTF-8 inválido, archivo vacío, archivo inexistente y hash del JSON guardado): la salida fue idéntica. `ruff check src` pasa de 17 a 13 errores (desaparecen SIM115 ×2, UP015 y SIM103). | ✅ 20/20 |
| 3  |              |                  |               |          |
| 4  |              |                  |               |          |
| 5  |              |                  |               |          |

> Agrega más filas si realizas más de 5 refactorizaciones.

## Reflexión final (10-15 líneas)

Responde: ¿Qué tan útil fue Claude Code para detectar y corregir los problemas?
¿Qué propuso la IA que tú no habías notado? ¿En qué casos tuviste que corregir
o rechazar sus sugerencias? ¿Qué aprendiste sobre refactorizar con apoyo de IA?

*(Escribe aquí tu reflexión)*
