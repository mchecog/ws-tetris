# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proyecto

Tetris en JavaScript vanilla + Canvas 2D (`index.html`, `style.css`, `game.js`). **Cero dependencias y sin build**: no crear `package.json` ni instalar paquetes; si hace falta una herramienta, usarla de forma puntual con `npx` o `python3`.

## Ejecutar

```bash
python3 -m http.server 8020   # puerto fijo: README y /verify-game usan el mismo
```

Abrir `http://localhost:8020`.

## Gotchas

- `COLS`, `ROWS` y `BLOCK` de `game.js` deben coincidir con `width`/`height` de `<canvas id="board">` en `index.html` (`COLS × BLOCK` por `ROWS × BLOCK`, hoy 300×600).
- Los controles viven en tres sitios: el handler `keydown` de `game.js`, la lista `CONTROLS` de `index.html` y la tabla de controles del `README.md`. Mantenerlos sincronizados.
- La velocidad (`dropInterval`) se fija a 1000 en `init()` y se recalcula en `clearLines()` con `Math.max(100, 1000 - (level - 1) * 90)`: si cambia la fórmula, tocar ambos sitios.
- El `README.md` documenta constantes, funciones (`collide`, `tryRotate`, `clearLines`, `ghostY`…), la tabla de puntuación y la fórmula de velocidad: actualizarlo si cambian.

## Plugins

`.claude/settings.json` declara el plugin [caveman](https://github.com/JuliusBrussee/caveman) (`caveman@caveman`, alcance de proyecto): respuestas telegráficas para gastar menos tokens. Es configuración de Claude Code, no una dependencia del juego. Al abrir el proyecto Claude Code pedirá confiar en el marketplace. Las respuestas siguen siendo en español. Para quitarlo: `claude plugin uninstall caveman@caveman --scope project`.

## Verificación

No hay tests ni linter. Tras cualquier cambio usar `/verify-game` (comprueba la sintaxis y prueba el juego en Chrome con la consola sin errores). Además, un hook `PostToolUse` (`.claude/settings.json`) ejecuta `node --check` sobre cada `.js` editado (requiere `jq` y `node`): si falla, corregir la sintaxis antes de seguir.

## Git

Una rama por cambio y PR a `main` con `gh`; no commitear directamente en `main`.
