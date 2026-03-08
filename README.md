# Ciutadella & Dragons · Atlas

Sitio estático en modo oscuro (verde/rosa pastel) dividido en varias páginas ligeras: `index.html` (inicio), `resources.html`, `guide.html`, `stats.html`, `weapons.html`, `razas.html` y `clases/index.html`.

## Cómo usar
- Abre `index.html` en local o publícalo en GitHub Pages; el menú enlaza al resto de secciones.
- `razas.html` incluye el bestiario completo; el resto de páginas están separadas para cargar más rápido.

## Datos y regeneración
- Los datos de armas y razas parten de `weapons.csv` y `razas.csv`.
- Si cambian los datos, regenera las páginas estáticas antes de publicar.
- Enlaces externos (fichas, clases, items, conjuros, guía) apuntan al material original de C&D.

## Origen en `razas.csv`
- Se completó la columna `origen` con planos/escenarios (por ejemplo: Feywild, Plano Astral, Planos Elementales, Ravnica, Eberron).
- Marcadas como origen variable o desconocido: SELLADOS (variable por raza original), SHURA, Sonares, Dol-Haras, Efteros y Throthogas.
- Owlers se asignó a Arcavios (Strixhaven) y Foxfolks a Feywild según el lore público (ajustable según canon de mesa).

## Fondo en carrusel
- El fondo común usa `shared-background.css` sin JavaScript y cambia por orientación de pantalla.
- Horizontal: usa las imágenes numeradas en `carrusel/horizontal/`.
- Vertical: usa las imágenes numeradas en `carrusel/vertical/`.
- Al terminar la última imagen, el carrusel reinicia automáticamente en bucle continuo.
- Si falta una imagen (por ejemplo `17.png`), se omite automáticamente.

## Clases
- `clases/index.html` detecta automáticamente carpetas y PDF al compilar en GitHub Pages (Liquid/Jekyll, sin JavaScript en cliente).

## Codificación
- Todo el contenido textual debe guardarse en UTF-8.
- Las páginas HTML incluyen `<meta charset="UTF-8">` (o equivalente en minúsculas).
- Se añadió `.editorconfig` para forzar UTF-8 y evitar mojibake en GitHub Pages.
