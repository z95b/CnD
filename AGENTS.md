# AGENTS.md · Ciutadella & Dragons · Atlas

Este sitio se publica en **GitHub Pages**. Todo cambio debe poder compilarse y servirse ahí tal cual, sin pasos manuales ni servicios externos. Ante la duda, elige siempre la opción más estática.

Puedes escribir en `README.md` todo lo que necesites para documentar el proyecto.

---

## 1. Qué es (y qué no es) GitHub Pages

GitHub Pages es **hosting estático**. Sirve los ficheros tal cual, o después de compilarlos una vez con **Jekyll** al publicar. **No ejecuta nada en el servidor** cuando alguien visita la página.

### Prohibido (no funciona en GitHub Pages)
- Lenguajes de servidor: **PHP, Python, Ruby, Node.js, ASP, Perl, CGI**, etc.
- Bases de datos (MySQL, SQLite, MongoDB…), sesiones, login o formularios que procesen datos en el servidor.
- Ficheros de configuración de servidor: `.htaccess`, `web.config`, `nginx.conf`, cabeceras HTTP personalizadas o redirecciones del lado del servidor.
- Plugins de Jekyll propios (carpeta `_plugins/`) o gems que no estén en la lista blanca de GitHub Pages. GitHub compila en *safe mode* y los ignora o falla.
- Pasos de build con npm, bundlers, preprocesadores no soportados, etc. Este repo se publica con el build clásico de Jekyll, sin GitHub Actions.
- Secretos, claves API o tokens en el repo. Todo lo publicado es público.

### Permitido
- **HTML, CSS** e imágenes, PDF, fuentes y demás ficheros estáticos.
- **Jekyll + Liquid**, que se ejecuta una sola vez al compilar, no en cada visita. Es la herramienta para generar contenido a partir de datos.
- Ficheros de datos **JSON / YAML / CSV / TSV** leídos por Liquid (aquí, `razas/` es el `data_dir`).
- Recursos externos por HTTPS (p. ej. Google Fonts).

## 2. Política de scripting del proyecto

> **No se usan lenguajes de scripting.** Todo debe resolverse con HTML, CSS y Liquid/Jekyll en tiempo de compilación.

- GitHub Pages técnicamente admite JavaScript en el navegador, pero **este proyecto ha decidido no depender de él**. No añadas `<script>`, atributos `on*=` ni enlaces `javascript:`.
- Las interacciones se hacen con HTML/CSS nativo: `<details>/<summary>`, `:target`, `:checked` con checkbox/radio ocultos, `@media`, animaciones CSS, `<object>/<iframe>` para PDF, etc.
- **Excepciones heredadas:** hoy existen dos scripts, la tirada de estadísticas en `stats.html` y el auto-scroll de `clases/index.html`. No amplíes su uso. Si tocas esas páginas, la página debe seguir funcionando sin JavaScript (con `<noscript>` o un comportamiento CSS equivalente).

## 3. Jekyll en GitHub Pages: restricciones concretas

Versiones fijadas por GitHub (ver <https://pages.github.com/versions/>): **Jekyll 3.10**, **Liquid 4.0.4**, **kramdown** como Markdown y **Rouge** para resaltado.

- **Es Jekyll 3, no 4.** No uses filtros exclusivos de Jekyll 4, como `find`, `find_exp` o `number_of_words` con modo `cjk`. Sí puedes usar `where`, `where_exp`, `group_by`, `group_by_exp`, `sort`, `sort_natural`, `map`, `uniq`, `relative_url`, `absolute_url`, `jsonify`, `slugify`, etc.
- **En HTML, Liquid solo se procesa en ficheros con front matter** (`---` al principio, aunque esté vacío). Sin front matter, el fichero se copia literalmente y las etiquetas de Liquid aparecen como texto.
- **Excepción: los `.md` se procesan con Liquid aunque no tengan front matter** (plugin `jekyll-optional-front-matter`, activo en GitHub Pages). Escribir una etiqueta de Liquid literal en un `.md` rompe toda la compilación. Este fichero está excluido en `_config.yml` por ese motivo. En otros `.md` publicados, envuelve los ejemplos en `{% raw %}…{% endraw %}`.
- **Ficheros y carpetas que empiezan por `_` o `.` no se publican** (salvo que se añadan a `include:` en `_config.yml`). `_includes/` y el `data_dir` se usan al compilar pero no se sirven como URL.
- **No añadas `.nojekyll`.** Desactivaría Jekyll y romperían `razas.html` y `clases/index.html`.
- Solo se pueden activar plugins de la lista blanca (p. ej. `jekyll-sitemap`, `jekyll-seo-tag`, `jekyll-feed`, `jekyll-redirect-from`, `jemoji`, `jekyll-relative-links`, `jekyll-optional-front-matter`…) declarándolos en `plugins:` de `_config.yml`.
- Para previsualizar en local hay que servir con Jekyll (`bundle exec jekyll serve` con la gem `github-pages`). Abrir el HTML fuente directamente no ejecuta Liquid.

## 4. Rutas y URLs

- El servidor es **Linux y distingue mayúsculas**: `Logo.png` ≠ `logo.png`. Windows no lo detecta, así que revisa siempre el nombre exacto.
- El sitio puede servirse bajo un subdirectorio (`usuario.github.io/CnD/`). Usa **rutas relativas** (`../shared-background.css`) o el filtro `relative_url` en Liquid. Nunca uses rutas absolutas que empiecen por `/` sin `relative_url`.
- Evita espacios y caracteres raros en nombres de fichero nuevos.
- No hay enlaces simbólicos: GitHub Pages no los sigue.
- Todos los recursos externos deben ir por **HTTPS** (el sitio se sirve por HTTPS y bloquea contenido mixto).
- Una página de error personalizada solo puede ser `404.html` en la raíz.

## 5. Límites de tamaño y uso

- Sitio publicado: **máx. 1 GB**. Repositorio: recomendado ≤ 1 GB.
- Ficheros individuales: GitHub **rechaza > 100 MB** y avisa a partir de 50 MB. Optimiza imágenes (WebP/JPG comprimido) y PDF antes de subirlos.
- Ancho de banda: límite blando de **100 GB/mes**.
- Builds: límite blando de **10 por hora** y **timeout de 10 minutos**. Evita bucles Liquid anidados innecesariamente costosos.
- No está permitido usar GitHub Pages para comercio, tienda online ni como servicio comercial.

## 6. Codificación y formato

- Todo en **UTF-8** (ver `.editorconfig`). Cada HTML lleva `<meta charset="UTF-8">`.
- Los datos de razas se editan en `razas/*.json`; el orden se controla en `razas/index.json`. No hardcodees datos de razas en `razas.html`.

## 7. Checklist antes de dar un cambio por terminado

- [ ] No hay código de servidor, `.htaccess`, `_plugins/` ni gems fuera de la lista blanca.
- [ ] No se ha añadido JavaScript nuevo (`<script>`, `on*=`, `javascript:`).
- [ ] Los ficheros con Liquid tienen front matter.
- [ ] Solo se usan filtros/etiquetas disponibles en Jekyll 3.10 / Liquid 4.0.4.
- [ ] Las rutas son relativas o usan `relative_url`, y coinciden exactamente en mayúsculas/minúsculas.
- [ ] Recursos externos por HTTPS.
- [ ] Ningún fichero > 50 MB; imágenes optimizadas.
- [ ] Texto guardado en UTF-8.

## Referencias

- Límites de GitHub Pages: <https://docs.github.com/en/pages/getting-started-with-github-pages/github-pages-limits>
- GitHub Pages y Jekyll: <https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/about-github-pages-and-jekyll>
- Versiones y plugins soportados: <https://pages.github.com/versions/>
- Gem `github-pages`: <https://github.com/github/pages-gem>
