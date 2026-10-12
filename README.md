# Ciutadella & Dragons · Atlas

Sitio estático en modo oscuro (verde/rosa pastel) dividido en varias páginas ligeras: `index.html` (inicio), `resources.html`, `guide.html`, `stats.html`, `weapons.html`, `razas.html` y `clases/index.html`.

## Cómo usar
- Abre `index.html` en local o publícalo en GitHub Pages; el menú enlaza al resto de secciones.
- `razas.html` incluye el bestiario completo; el resto de páginas están separadas para cargar más rápido.

## Datos y generación
- Los datos de armas parten de `weapons.csv`.
- Los datos canónicos de las razas están en `razas/index.json` y en los JSON individuales de `razas/`.
- `razas/index.json` tiene dos listas: `variantes` y `razas`. El orden de los archivos dentro de cada lista define el orden editorial de `razas.html`.
- Cada JSON contiene los datos de una raza y la ruta de su imagen. Las capacidades, atributos, idiomas y demás colecciones usan arrays para conservar su orden y evitar perder valores repetidos.
- `_config.yml` configura `razas/` como directorio de datos de Jekyll. GitHub Pages procesa `razas.html` con Liquid durante la compilación y genera todas las fichas desde esos JSON, sin JavaScript en el navegador.
- `razas.html` no contiene datos de razas hardcodeados. Para cambiar una ficha se edita su JSON; para añadir, retirar o reordenar fichas se edita `razas/index.json`.
- Al abrir directamente el archivo fuente `razas.html` no se ejecuta Liquid. Para previsualizar esta página en local hay que servir el proyecto con Jekyll; GitHub Pages realiza esta compilación automáticamente al publicar.
- Enlaces externos (fichas, clases, items, conjuros, guía) apuntan al material original de C&D.

## Filtros y buscador de razas
- Al principio de `razas.html` hay un panel con filtros por atributo (Fuerza, Destreza, Constitución, Inteligencia, Sabiduría, Carisma). Funciona sin JavaScript: son casillas `checkbox` y reglas CSS con `:has()`. El botón «Limpiar» es un `<button type="reset">` nativo del formulario.
- Al compilar, `_includes/race-card.html` añade a cada ficha clases `attr-fue`, `attr-des`, `attr-con`, `attr-int`, `attr-sab` y `attr-car` según sus atributos con bonificación no negativa. Una bonificación negativa (p. ej. Fuerza -2) no cuenta.
- Los nombres se reconocen por fragmento, sin distinguir mayúsculas: `fue`, `des`, `cons`, `int`, `sab`, `car`. Por eso valen variantes como `INT`, `Sabiduria` o `Fuerza o Destreza`.
- Los atributos que no son una característica concreta («A elegir», «🔷», «Selección de Propósito»…) marcan la ficha como `attr-any`. Esas razas aparecen en cualquier filtro mientras esté marcada la casilla «Incluir razas con atributo a elegir».
- Si se marcan varios atributos se muestran las razas que bonifican todos ellos.
- La lista de atributos de los filtros está definida una sola vez (`filter_attrs`, en el bloque `<style>` de `razas.html`) y genera tanto las reglas CSS como las casillas.
- El «buscador» es un índice alfabético desplegable generado desde los JSON que enlaza a cada ficha (`#clave-de-raza`). Un filtrado mientras se escribe no es posible sin JavaScript; para buscar texto libre se recomienda Ctrl+F.
- Una ficha enlazada desde el índice (`:target`) siempre se muestra, aunque los filtros activos la oculten.

## Origen en los JSON de razas
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
