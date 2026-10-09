# Cale Consulting — Sitio web

Sitio corporativo de **Cale Consulting** (consultoría tecnológica y de IA para pymes) para el dominio **caleconsulting.net**.

- **Tipo:** sitio estático (un solo archivo HTML con estilos y código incluidos). No necesita servidor, base de datos ni instalación.
- **Idiomas:** inglés (principal), español y portugués, con selector en el menú.
- **Estado:** diseño y contenido listos. Falta conectar el formulario y publicar (ver [Pendientes](#pendientes)).

---

## Estructura del proyecto

```
Cale Consulting/
├── README.md              ← este archivo: qué es y cómo se modifica
├── CLAUDE.md              ← contexto para Claude (decisiones y reglas del proyecto)
├── DESIGN.md              ← guía de estilo visual (colores, tipografía, componentes)
├── docs/
│   └── BITACORA.md        ← historial de todo lo que se ha hecho, por fecha
├── .claude/launch.json    ← configuración del servidor local de vista previa
└── web/                   ← ESTO es lo que se publica en internet
    ├── index.html         ← la página completa (HTML + CSS + JS + textos en 3 idiomas)
    └── assets/
        ├── logo-mark.svg  ← símbolo solo (la "C" con punto naranja)
        ├── logo.svg       ← logo horizontal "Cale Consulting"
        └── favicon.svg    ← ícono de la pestaña del navegador
```

---

## Cómo ver la página en tu computadora

**Opción fácil:** doble clic en `web/index.html` (se abre en el navegador).

**Opción completa (igual que publicada):** pídele a Claude *"activa el server de Cale"*. Usa la configuración `cale-web` y abre `http://localhost:5500`.

O manualmente, en una terminal dentro de la carpeta del proyecto:

```bash
python -m http.server 5500 --directory web
```

y abre http://localhost:5500 en el navegador.

---

## Cómo modificar cosas

Todo está en `web/index.html`. El archivo tiene tres partes, en este orden:

1. **`<style>`**: el diseño (colores, tamaños, animaciones).
2. **El HTML**: las secciones de la página.
3. **`<script>`**: los textos en los 3 idiomas (`const I18N`) y las animaciones.

### Cambiar un texto

Los textos **no se cambian en el HTML**, sino en el diccionario `I18N` al final del archivo. Cada texto tiene una clave:

```html
<h2 data-i="sv.title">Technology that pays for itself.</h2>
```

Busca `'sv.title'` en el archivo y verás las 3 versiones (en, es, pt). Cambia las tres.

> El texto en inglés del HTML es solo un respaldo por si falla JavaScript; si cambias un texto, conviene actualizarlo también ahí.

**Mapa de claves por sección:**

| Prefijo | Sección |
|---|---|
| `meta.*` | Título de la pestaña y descripción para Google |
| `nav.*` | Menú superior |
| `hero.*` | Portada (titular, subtítulo, botones) |
| `term.*` | Terminal animada de la portada |
| `marquee` | Franja de capacidades que se desplaza |
| `sv.*` | Servicios (`sv.1` = IA, `sv.2` = Automatización, `sv.3` = Transformación digital, `sv.4` = Consultoría) |
| `ap.*` | Cómo trabajamos (4 pasos) |
| `why.*` | Por qué Cale (tarjeta clara) |
| `ab.*`, `orb.*` | Nosotros y la órbita de partners |
| `faq.*` | Preguntas frecuentes |
| `ct.*` | Bloque de contacto |
| `f.*` | Formulario |
| `ft.*` | Pie de página |

### Cambiar colores

Al inicio del `<style>`, en `:root`, están las variables. Por ejemplo `--orange: #ee6018;` es el color de acento. Cambiarlo ahí lo cambia en toda la página.

### Agregar un idioma

1. Copia el bloque `es: { ... }` dentro de `I18N`, renómbralo (por ejemplo `fr`) y traduce los textos.
2. Agrega un botón en el menú: `<button type="button" data-lang="fr" aria-pressed="false">FR</button>`.

### Agregar o quitar un servicio

Copia/borra un bloque `<article class="card">` en la sección `#services`, agrega sus claves `sv.5.*` en los 3 idiomas y ajusta `.cards { grid-template-columns: repeat(4, 1fr) }` al nuevo número.

---

## Formulario de contacto

- El correo de la empresa **no aparece en la página**. Los visitantes llenan el formulario de "solicitar consulta".
- El formulario usa **[Web3Forms](https://web3forms.com)** (gratis hasta 250 envíos al mes), que reenvía cada solicitud al correo de Cale.
- **Estado:** activo. La *Access Key* ya está en `web/index.html` (campo oculto `access_key`). Para cambiar el correo de destino, se genera una clave nueva en web3forms.com con el otro correo y se reemplaza ahí.
- La clave es pública por diseño. Solo permite enviar mensajes a ese correo, así que es seguro que esté en la página.

---

## Publicación (pendiente)

Plan elegido: **GitHub Pages**. El archivo `.github/workflows/publicar.yml` publica la carpeta `web/` automáticamente cada vez que se suben cambios a la rama `main`. El dominio se conecta con registros A (`@`) y CNAME (`www`) en el DNS actual, sin mover los nameservers. Los pasos detallados están en `docs/PUBLICAR.md`.

**Importante:** al cambiar el DNS del dominio solo se tocan los registros de la web (A/CNAME). **Nunca los registros MX**, porque son los del correo de Google Workspace.

---

## Pendientes

Ver la lista actualizada en [CLAUDE.md](CLAUDE.md#pendiente) y el historial en [docs/BITACORA.md](docs/BITACORA.md).
