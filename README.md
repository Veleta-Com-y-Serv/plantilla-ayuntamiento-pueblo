# Plantilla NoExpertise · Ayuntamiento y pueblo

Web institucional a todo color para ayuntamientos y pueblos: trámites, bandos, agenda, qué ver y servicios.
Bandas a todo el ancho en verde institucional, piedra y rojo rodeno, foto del pueblo a sangre y titulares en serif.

- Sectores: ayuntamiento, pueblo, turismo-local, oficina-turismo, mancomunidad. Estilo: institucional. Plan mínimo: presencia.
- Secciones: hero (con accesos rápidos), noticias, tramites, agenda, pueblo, que-ver, servicios, horario, preguntas, contacto; `texto` para apartados nuevos.
- Listas propias: `agenda.eventos` {fecha, titulo, lugar, hora, categoria}, `que-ver.lugares` {nombre, texto, imagen}; `noticias` con `categoria` e `imagen`; `hero.items` y `tramites.items` con `url`.
- Ejemplo: Ayuntamiento de Peñarrubia, municipio ficticio de la Sierra de Albarracín (Teruel); teléfonos y datos de muestra.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD (`GovernmentOffice`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos a generar en `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.
