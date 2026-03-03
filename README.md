# Ciutadella & Dragons · Atlas

Sitio estático en modo oscuro (verde/rosa pastel) dividido en varias páginas ligeras: `index.html` (inicio), `resources.html`, `guide.html`, `casino.html`, `razas.html`.

## Cómo usar
- Abre `index.html` o súbelo a GitHub Pages; el menú enlaza al resto de secciones.
- `razas.html` incluye el bestiario (52 fichas con imágenes y barras de tamaño); el resto de páginas están separadas para cargar más rápido.

## Datos y regeneración
- Datos base en `razas_data.json`; rutas de imágenes en `razas.csv` (columna `image`).
- Si cambian los datos, vuelve a ejecutar el script Python usado en esta entrega para reconstruir las páginas.
- Enlaces externos (fichas, clases, items, conjuros, guía) apuntan al material original de C&D.



## Origen en razas.csv
- Se completo la columna `origen` con planos/escenarios (p. ej., Feywild, Plano Astral, Planos Elementales, Ravnica, Eberron).
- Marcadas como origen variable o desconocido: SELLADOS (variable por raza original), SHURA, Sonares, Dol-Haras, Efteros, Throthogas.
- Owlers se asigno a Arcavios (Strixhaven) y Foxfolks a Feywild segun el lore publico; ajustable si tu canon difiere.

## Fondo en carrusel
- El fondo comun usa `shared-background.css` sin JavaScript y cambia por orientacion de pantalla.
- Horizontal: usa las imagenes numeradas existentes en `carrusel/horizontal/`.
- Vertical: usa las imagenes numeradas existentes en `carrusel/vertical/`.
- Al terminar la ultima imagen, el carrusel vuelve a empezar automaticamente y se mantiene en bucle continuo.
- Si falta una imagen (por ejemplo `17.png`), se omite automaticamente en la secuencia.

## Clases
- `clases/index.html` detecta automaticamente las carpetas dentro de `clases/` y sus PDF al compilar en GitHub Pages (Liquid/Jekyll, sin JavaScript en cliente).
