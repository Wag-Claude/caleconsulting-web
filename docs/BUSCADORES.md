# Cómo lograr que Google y otros buscadores encuentren caleconsulting.net

## Lo técnico (ya hecho, 2026-10-11)

| Qué | Dónde | Para qué |
|---|---|---|
| `robots.txt` | `web/robots.txt` → https://caleconsulting.net/robots.txt | Permite a los buscadores recorrer la página e indica dónde está el sitemap. |
| `sitemap.xml` | `web/sitemap.xml` → https://caleconsulting.net/sitemap.xml | Lista las direcciones que se deben indexar. **Actualizar `<lastmod>`** cuando haya cambios importantes. |
| Dirección canónica | `<link rel="canonical">` en `index.html` | Le dice a Google que la dirección oficial es `https://caleconsulting.net/` y no la variante con www ni la de github.io. |
| Título, descripción y Open Graph | `<head>` de `index.html` y `meta.*` en `I18N` | Es lo que aparece en el resultado de Google y al compartir el enlace. |
| Datos estructurados | `<script type="application/ld+json">` | Le explica a Google que es una empresa de servicios profesionales. |

## Lo que hace el usuario (con su cuenta)

### 1. Google Search Console (lo más importante)
1. Entra a https://search.google.com/search-console con **admin@caleconsulting.net**.
2. **Agregar propiedad** → elige **Dominio** (la opción de la izquierda) → escribe `caleconsulting.net` → **Continuar**.
3. Si aparece "Propiedad verificada automáticamente", listo: ocurre porque el dominio ya está verificado en Google Workspace con esa misma cuenta.
4. Si pide un registro **TXT** (`google-site-verification=...`), agrégalo en Squarespace → DNS → Registros personalizados (tipo TXT, nombre `@`) y haz clic en **Verificar**. **No borres el TXT de SPF** que ya existe: son registros distintos y deben convivir.
5. Menú izquierdo → **Sitemaps** → escribe `sitemap.xml` → **Enviar**.
6. Barra superior → pega `https://caleconsulting.net/` → **Solicitar indexación**.

### 2. Bing Webmaster Tools (cubre Bing, Yahoo, DuckDuckGo, Ecosia y otros)
1. Entra a https://www.bing.com/webmasters.
2. Elige **Importar desde Google Search Console**: copia la propiedad y el sitemap sin verificar de nuevo.

### 3. Perfil de Empresa de Google (Google Business Profile)
1. Entra a https://business.google.com → **Agregar empresa**.
2. Nombre: **Cale Consulting**. Categoría: *Consultor de informática* o *Servicio de consultoría*.
3. Si no atiendes clientes en una dirección física, elige **"Empresa de servicios a domicilio / área de servicio"** y define las ciudades o países.
4. Agrega la web `https://caleconsulting.net`, la descripción, los servicios y el logo.
5. Google pide verificar el negocio, normalmente con un video corto o un código.

### 4. Enlaces desde otros sitios
- **Página de empresa en LinkedIn** con la web, y la web también en tu perfil personal.
- Directorios: Clutch, GoodFirms, el directorio de la cámara de comercio local y asociaciones del sector.
- Partners: que te enlacen desde sus webs si es posible.

## Qué esperar
- **Búsqueda por nombre** ("Cale Consulting"): suele aparecer en **días a 2 semanas** después de enviar el sitemap.
- **Búsquedas genéricas** ("consultoría IA pymes"): toma **meses** y depende de contenido y enlaces.
- Para comprobarlo, busca en Google: `site:caleconsulting.net`.

## Mejoras futuras recomendadas
- **Imagen para compartir** (`og:image`, 1200×630 PNG): mejora cómo se ve el enlace en LinkedIn y WhatsApp.
- **Páginas `/es/` y `/pt/`**: hoy Google solo indexa la versión en inglés, porque la traducción se hace con JavaScript.
- **Contenido**: artículos o casos (por ejemplo "Cómo elegir un proveedor de internet para varias sedes") que atraigan búsquedas genéricas.
- **Google Analytics**: para medir las visitas.
