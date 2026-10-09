# Cale Consulting — sitio web

Sitio corporativo de Cale Consulting para `caleconsulting.net` (dominio en Google Workspace).
**Empieza leyendo:** [README.md](README.md) (estructura y cómo editar) y [docs/BITACORA.md](docs/BITACORA.md) (qué se ha hecho).

## Contexto del negocio

- Consultoría tecnológica para **pymes**: Adopción de IA, Automatización de procesos, Transformación digital, Consultoría tecnológica.
- Empresa **nueva**. El fundador tiene +20 años en tecnología y una red de partners especialistas.
- **No hay clientes, casos, testimonios ni cifras de resultados reales. No inventarlos.** Cualquier número ilustrativo debe ir marcado como ejemplo.
- Nombre y foto del fundador: aún no proporcionados.

## Reglas del proyecto

- El nombre **"Cale Consulting" debe leerse claro y completo** (menú, portada, pie). No abreviar a "Cale" en la marca.
- El **correo no se muestra** en la página; el contacto es solo por formulario.
- Contenido en **inglés** (principal) + **español** + **portugués**. Todo texto nuevo va en las 3 versiones del diccionario `I18N`.
- Estilo: [DESIGN.md](DESIGN.md), más el "brillo" y las animaciones que pidió el cliente. Respetar siempre `prefers-reduced-motion`.
- Al cambiar DNS: **nunca tocar los registros MX** (correo de Workspace).
- El usuario prefiere: español, guía paso a paso, documentar todo. El usuario maneja sus cuentas y contraseñas; Claude no.
- Después de cada cambio: verificar en escritorio y celular (360px), agregar una entrada en `docs/BITACORA.md` y hacer commit.

## Decisiones tomadas

| Fecha | Decisión | Motivo |
|---|---|---|
| 2026-10-08 | Sitio estático a la medida, **no** Google Sites | Sites no reproduce la guía de estilo. |
| 2026-10-08 | Hosting: **GitHub Pages** vía GitHub Actions (`.github/workflows/publicar.yml` publica `web/`) | $0 y HTTPS automático. El dominio se conecta con registros A/CNAME sin mover los nameservers, así que el correo de Workspace no corre riesgo (Cloudflare Pages exigía mover los nameservers para usar el dominio raíz). |
| 2026-10-08 | Un solo `index.html` con CSS/JS/textos incluidos | Simple de mantener y publicar; sin dependencias ni compilación. |
| 2026-10-08 | Traducción por JS (`I18N`), con detección del idioma del navegador y memoria en `localStorage` | Pedido EN/ES/PT. Limitación: Google solo indexa la versión en inglés. |
| 2026-10-08 | Formulario → Web3Forms | Gratis, sin servidor, oculta el correo. |
| 2026-10-08 | Imágenes generadas con código (canvas/SVG), sin fotos de stock | Encajan con el estilo y no tienen problemas de licencia. |
| 2026-10-08 | Logo: "C" abierta + punto naranja | No existía logo. |

## Dónde encontrar qué

| Qué | Dónde |
|---|---|
| Página completa | [web/index.html](web/index.html) |
| Textos (3 idiomas) | `const I18N` al final de `web/index.html` |
| Colores / variables | `:root` al inicio del `<style>` |
| Logo y favicon | [web/assets/](web/assets/) |
| Guía de estilo | [DESIGN.md](DESIGN.md) |
| Historial | [docs/BITACORA.md](docs/BITACORA.md) |
| Repositorio en GitHub | https://github.com/Wag-Claude/caleconsulting-web |
| DNS (respaldo y registros de la web) | [docs/DNS.md](docs/DNS.md) |
| Guía de publicación paso a paso | [docs/PUBLICAR.md](docs/PUBLICAR.md) |
| Vista previa | config `cale-web` en `C:\Users\wwpch\.claude\launch.json` (la que lee el navegador integrado) y en `.claude/launch.json` → http://localhost:5500 |

## Pendiente

- [x] Formulario conectado a Web3Forms y probado: el envío de prueba llegó al correo (2026-10-09).
- [ ] Confirmar los textos que implican compromisos: "respondemos en 1 día hábil", "atendemos en EN/ES/PT", plazos del método (semanas 1–2 / 3 / 4–8).
- [ ] Nombre y foto del fundador para "About".
- [ ] LinkedIn de la empresa.
- [ ] Logo con el texto convertido a trazos (hoy `logo.svg` depende de la fuente Geist) y PNG para redes.
- [ ] Imagen para compartir en redes (`og:image`, 1200×630).
- [ ] Publicar en GitHub Pages y conectar el dominio, siguiendo [docs/PUBLICAR.md](docs/PUBLICAR.md) (solo registros web, no MX).
- [ ] Google Analytics + Search Console.
- [ ] (Opcional) Páginas `/es/` y `/pt/` para SEO multilingüe.
- [ ] (Opcional) Política de privacidad, recomendable al recoger datos con el formulario.
