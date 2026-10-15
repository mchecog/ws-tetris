---
name: verify-game
description: Verifica el Tetris en Chrome tras un cambio en game.js, index.html o style.css (sintaxis, consola sin errores y controles respondiendo). Úsala antes de dar un cambio por terminado.
---

Verifica el juego de verdad, no solo la sintaxis.

1. `node --check game.js` (en la raíz del repo). Si falla, corregir antes de seguir.
2. Arrancar `python3 -m http.server 8020` en segundo plano (`run_in_background`). Si el puerto está ocupado, usar otro.
3. Cargar las herramientas `mcp__claude-in-chrome__*` necesarias en **una sola** llamada a ToolSearch (`tabs_context_mcp`, `tabs_create_mcp`, `navigate`, `computer`, `read_console_messages`, `read_page`, `tabs_close_mcp`).
4. Crear una pestaña nueva y abrir `http://localhost:8020`.
5. Leer la consola con `read_console_messages` (`onlyErrors: true`): no debe haber errores.
6. Pulsar con `computer` (`key`): `ArrowLeft`, `ArrowRight`, `ArrowUp`, `ArrowDown`, `space` y `p` (dos veces para pausar y reanudar). Tras cada una, hacer una captura y comprobar que la pieza se mueve/rota/cae y que el overlay de pausa aparece y desaparece. Si el cambio toca puntuación, líneas o niveles, comprobar también que `SCORE`, `LINES` y `LEVEL` se actualizan.
7. Volver a leer la consola buscando errores.
8. Cerrar la pestaña con `tabs_close_mcp` y detener el servidor con `TaskStop`.

Informar qué pasó en cada paso y, si algo falló o no se pudo comprobar, decirlo claramente.
