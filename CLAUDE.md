# Plantilla «Ayuntamiento y pueblo» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **institucional**.
Para ayuntamientos, pueblos, oficinas de turismo y mancomunidades. Todo en castellano de España, frases cortas,
trato cercano y claro (de tú), sin jerga administrativa innecesaria.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y calcula el texto legible sobre cada color pleno (`--c-sobre-primario`, `--c-sobre-acento`, `--c-sobre-hondo`). Derivados en `src/styles/global.css`: `--c-hondo` (primario oscurecido, banda de «Qué ver» y pie) y `--c-piedra` (fondo con un toque de acento y de texto, bandas claras alternas).
- **Bandas**: clases `banda-primario`, `banda-hondo`, `banda-acento`, `banda-piedra` y `banda-fondo` de `global.css`. Cada sección es una banda a todo el ancho; el contenido va en `.contenedor` (máx. 90 rem, 16 px de margen en móvil).
- **Tipografías**: `--fuente-titulos` (serif clásica del sistema: Iowan, Palatino, Book Antiqua, Georgia) y `--fuente-texto` (system-ui). Antetítulos en versalitas espaciadas con una línea de acento delante. Sin fuentes externas.
- **Imágenes**: en `public/`. Fotos de ejemplo en `public/fotos/` (las genera el paso de fotos a partir de `fotos.json`); SVG de respaldo en `public/placeholders/` con el mismo nombre. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`).
- **Logo o escudo**: `site.yaml → logo` (ruta en `public/`); vacío = escudo de color de acento con la inicial del nombre (sin «Ayuntamiento de») y el nombre en serif.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (se oculta solo con `false`).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`. Todas pintan bien con listas y campos vacíos.
- `hero` → `hero.astro`: foto a sangre a casi toda la pantalla con velo, nombre del pueblo enorme, entradilla y dos botones; debajo, franja de **accesos rápidos** (`items`: titulo, texto, icono, url). La cabecera es transparente sobre la foto si la portada es la primera sección.
- `noticias` → `noticias.astro`: bandos, avisos y noticias (`noticias`: fecha, categoria, titulo, texto, imagen, url). La primera, grande con foto; el resto, en columna.
- `tramites` → `tramites.astro`: banda verde con rejilla de trámites a líneas finas (`items`: titulo, texto, icono, url) y botón a la sede (`cta`).
- `agenda` → `agenda.astro`: calendario de pared (`eventos`: fecha «15 nov 2026», titulo, lugar, hora, categoria). Si la fecha empieza por el día, el día va enorme.
- `pueblo` → `pueblo.astro`: fila 50/50 con foto a sangre y texto (párrafos separados por línea en blanco) y franja de datos de color acento (`items`: titulo = el dato, texto = qué es).
- `que-ver` → `que-ver.astro`: mosaico de lugares de borde a borde (`lugares`: nombre, texto, imagen), el primero grande.
- `servicios` → `servicios.astro`: servicios municipales en columnas con filete (`items`: titulo, texto, icono).
- `horario` → `horario.astro`: banda de acento con el horario de atención (`horario`: dia, horas), dirección y teléfono de `contacto` y botón de cita (`cta`). Sin `horario`, usa `contacto.horario`.
- `preguntas` → `preguntas.astro`: preguntas frecuentes en acordeón `details/summary` (sin preguntas no se pinta).
- `contacto` → `contacto.astro`: banda partida: datos de contacto sobre verde y formulario `mailto` sobre claro.
- `texto` → `texto.astro`: diseño genérico para apartados nuevos (`tipo: texto`).

Iconos disponibles (`icono`): los de `src/components/ui/Icono.astro` (documento, edificio, herramienta, euro, llave, mano, mensaje, maletin, calendario, megafono, estrella, montana, cruz, nino, libro, trofeo, gota, reciclaje, autobus, wifi, arbol, corazon, casa, mapa, reloj…).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Listas planas: nunca una lista dentro de un elemento de lista; máximo 24 elementos.
4. **Bando o noticia nueva**: añade un elemento al principio de `secciones.noticias.noticias` (el primero sale grande). **Evento nuevo**: añade a `secciones.agenda.eventos` en orden de fecha.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>` (la cabecera deja su hueco sola); enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: crea `src/components/secciones/<id>.astro` (copia la estructura de una existente: `seccion(id)`, una banda `banda-*`, `Titular`) y añade `secciones.<id>` en `site.yaml`. `src/pages/index.astro` la recoge sola.
7. **No tocar** `src/layouts/Base.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), sin JavaScript nuevo salvo necesidad real (solo hay el de la cabecera), 16 px de margen lateral del texto, fotos y bandas a sangre, sin scroll horizontal en móvil, botones de 44 px de alto como mínimo. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `hero.items[]`: accesos rápidos {titulo, texto, icono, url}; el primero va en color de acento.
- `noticias.noticias[]`: además de fecha, titulo, texto y url, `categoria` (Bando, Obras, Cultura…) e `imagen`.
- `agenda.eventos[]`: {fecha, titulo, lugar, hora, categoria}.
- `pueblo.items[]`: datos del pueblo {titulo, texto} en la franja de color.
- `que-ver.lugares[]`: {nombre, texto, imagen}.
- `horario.horario[]`: {dia, horas}; también lo usa el JSON-LD (`openingHours`) y el pie.

Fotos de partida en `public/fotos/` (generadas con IA a partir de `fotos.json`, sin derechos de terceros); los SVG de `public/placeholders/` siguen de respaldo.
