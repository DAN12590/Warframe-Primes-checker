# Warframe Primes Tracker

Web para llevar la cuenta de qué piezas tienes de cada objeto Prime de Warframe: Warframes, armas, centinelas y archwings. Marcas las piezas que vas consiguiendo y ves el progreso de cada objeto y el total.

Web: https://warframe-checker.danapps.dev/

## Qué hace

- Pestañas por tipo de objeto y búsqueda por nombre
- Filtros por estado (completos, en progreso, sin empezar) y por categoría de arma
- Botones para marcar todas las piezas de un objeto o reiniciarlo
- Exportar e importar el progreso como archivo JSON

## Cómo usarlo

No necesita instalar nada: abre `index.html` en el navegador.

El progreso se guarda en el `localStorage` del navegador, con la clave `warframe_prime_tracker`. Por eso:

- si borras los datos del navegador, se pierde
- en otro navegador o en modo incógnito no aparece

Para pasarlo de un navegador a otro, usa **Exportar** y luego **Importar**.

## Cómo está hecho

HTML, CSS y JavaScript sin librerías.

- `data.js` tiene el catálogo de objetos. Las listas de piezas que se repiten (las de los Warframes, los rifles...) se definen una vez en `PARTS`.
- `app.js` tiene toda la lógica. El estado (pestaña, filtros, búsqueda y progreso) está en un objeto `state`, y cada vez que cambia algo se llama a `render()`, que vuelve a pintar las tarjetas a partir de ese estado.
- El progreso se guarda por índice de pieza (`{ "ash_prime": { "0": true } }`) y no por nombre, porque hay objetos con piezas repetidas, como dos "Blade".
- Las tarjetas se recrean en cada render, así que en vez de poner un listener en cada botón hay uno solo en la rejilla que mira en qué se ha hecho clic (delegación de eventos).
- La búsqueda espera 200 ms a que dejes de escribir antes de filtrar, para no repintar en cada tecla.
