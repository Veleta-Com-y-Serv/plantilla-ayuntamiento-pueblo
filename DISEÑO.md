# Ayuntamiento y pueblo: brief de diseño

Plantilla `ayuntamiento-pueblo` creada el 29/10/2026 a partir de `asociacion` con `php artisan plantillas:nueva` y
rediseñada entera (fila 26 del brief de la tanda «ancho completo»). Este fichero es lo que lee quien (persona o
agente) rediseñe la plantilla.

## Brief

- **Para quién**: ayuntamientos pequeños y medianos, pueblos, oficinas de turismo y mancomunidades. Quien entra es un
  vecino que quiere hacer un trámite, saber un horario o leer un bando, o un visitante que busca qué ver y qué hay en
  la agenda.
- **Qué tiene que conseguir la web**: que el vecino encuentre en dos toques el trámite o el horario (accesos rápidos
  bajo la portada, trámites en rejilla, horario en banda de color) y que el visitante se quede con ganas de ir
  (foto a sangre, mosaico de qué ver, agenda).
- **Tono y estilo** (`institucional`): serio, cercano y orgulloso del pueblo. Sí: los carteles de los paisajes
  protegidos y las webs municipales cuidadas de los pueblos bonitos. No: portal de administración gris con mil
  enlaces ni la «caja centrada con tarjetas blancas».
- **Paleta de ejemplo**: primario `#1e5b3f` (verde institucional), acento `#b5502e` (rojo rodeno, la arenisca de la
  Sierra de Albarracín), fondo `#fbf9f4` (blanco cal), texto `#1d2621`. Derivados: `--c-hondo` (verde oscurecido,
  banda de qué ver y pie) y `--c-piedra` (fondo con un toque de acento y de texto). El texto sobre cada color pleno
  se calcula en el build (`textoSobre`), así aguanta los colores del cliente.
- **Tipografía**: serif clásica del sistema para títulos (Iowan Old Style, Palatino, Book Antiqua, Georgia), 700,
  nombre del pueblo a 7 rem en escritorio y 2,75 rem en móvil; texto en system-ui; antetítulos, botones y menú en
  versalitas con interletrado amplio. Escudo de acento con la inicial como marca.
- **Ritmo de bandas** (todas a todo el ancho): portada con foto a sangre → franja de accesos (acento + verde) →
  actualidad (blanco cal) → trámites (verde) → agenda (piedra) → el pueblo (foto a sangre 50/50 + franja de datos
  rojo rodeno) → qué ver (verde hondo + mosaico de borde a borde) → servicios (blanco cal) → horario (rojo rodeno) →
  preguntas (piedra) → contacto partido (verde / blanco cal) → pie verde casi negro con franja de acento.
- **Forma**: rejillas con filetes finos en vez de tarjetas, esquinas rectas, iconos de línea, fechas de calendario
  de pared, capitular en el texto del pueblo.

## Apartados

1. `hero`: foto del pueblo a sangre (88 svh), velo, antetítulo con la comarca, nombre del pueblo enorme, entradilla,
   dos botones; franja de accesos rápidos `items` {titulo, texto, icono, url} en 2 columnas (móvil) o 4.
2. `noticias`: bandos y noticias `noticias` {fecha, categoria, titulo, texto, imagen, url}; la primera grande.
3. `tramites`: `items` {titulo, texto, icono, url} en rejilla 1-2-4 con líneas; filas compactas en móvil; `cta` a la sede.
4. `agenda`: `eventos` {fecha, titulo, lugar, hora, categoria}; titular fijo a la izquierda en escritorio.
5. `pueblo`: texto + foto a sangre 50/50; `items` como datos {titulo, texto} en franja de color.
6. `que-ver`: `lugares` {nombre, texto, imagen} en mosaico sin márgenes (el primero 2×2).
7. `servicios`: `items` {titulo, texto, icono} en columnas con filete (filas en móvil).
8. `horario`: `horario` {dia, horas} con horas en serif grande; dirección, teléfono y `cta` de cita.
9. `preguntas`: acordeón `details/summary` (4-6 en el ejemplo).
10. `contacto`: datos sobre verde + formulario `mailto`.

## Fotos

Pueblo de piedra rojiza y pinares de rodeno, luz cálida, sin gente, sin texto ni logotipos (detalle en `fotos.json`):
portada panorámica, calle empedrada (pueblo), tres de noticias (obra de la red de agua, rincón de reciclaje,
biblioteca) y seis lugares (casco antiguo, torre de iglesia, mirador, sendero de rodeno, fuente y lavadero, villa
medieval cercana).

## Qué no hacer

- Volver a la caja centrada estrecha con tarjetas blancas o al hero partido con collage de la base `asociacion`.
- Poner datos reales de un ayuntamiento existente: el ejemplo es un municipio ficticio.
- Hablar de la técnica en los textos de la web.
