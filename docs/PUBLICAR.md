# Cómo publicar caleconsulting.net

**Hosting:** GitHub Pages (gratis, con HTTPS automático).
**Dominio:** se conecta agregando registros en el DNS actual. **No se mueven los nameservers y no se tocan los registros MX**, así que el correo de Google Workspace sigue funcionando igual.

Tiempo estimado: 30–45 minutos de trabajo, más la espera de propagación del DNS (de minutos a 24 h).

> Quién hace qué: el usuario entra a sus cuentas (Google Admin, registrador del dominio, GitHub) y hace los clics. Claude prepara los archivos, sube el código y verifica.

---

## Paso 0 — Antes de empezar (opcional, pero recomendado)

- **Clave del formulario:** entra a https://web3forms.com, escribe el correo donde quieres recibir las solicitudes y copia la *Access Key* que te llega. Pásasela a Claude para que la ponga en la página. Se puede publicar sin ella y agregarla después, pero mientras falte el formulario no envía.
- **Revisar los textos** con compromisos (ver *Pendiente* en `CLAUDE.md`).

---

## Paso 1 — Averiguar dónde se administra el DNS del dominio

1. Entra a **https://admin.google.com** con tu cuenta de administrador de Workspace.
2. Menú izquierdo → **Cuenta** → **Dominios** → **Administrar dominios**.
3. Busca `caleconsulting.net` y haz clic en **Ver detalles** o **Configuración avanzada de DNS**.
4. Fíjate qué empresa aparece como registrador:
   - **Squarespace**: es lo más común. Los dominios comprados con Google pasaron a Squarespace en 2023–2024. El DNS se administra en https://account.squarespace.com/domains.
   - **Otro** (GoDaddy, Namecheap, etc.): el DNS se administra en esa empresa. Los pasos son equivalentes.
5. Entra al panel de DNS de `caleconsulting.net` y **toma una captura de pantalla de todos los registros actuales** (es el respaldo por si algo sale mal).

---

## Paso 2 — Crear el repositorio en GitHub

1. Entra a **https://github.com** con tu cuenta (o crea una gratis).
2. Arriba a la derecha, botón **+** → **New repository**.
3. Completa:
   - **Repository name:** `caleconsulting-web`
   - **Visibility:** **Public**. GitHub Pages gratis requiere un repositorio público; el contenido es la misma página web, que de todos modos es pública.
   - **No** marques "Add a README", ".gitignore" ni "license": el repositorio debe quedar vacío.
4. Clic en **Create repository** y copia la dirección que aparece, por ejemplo `https://github.com/TU-USUARIO/caleconsulting-web.git`.
5. Pásale esa dirección a Claude.

---

## Paso 3 — Subir el código (lo hace Claude)

Claude ejecuta, desde la carpeta del proyecto:

```bash
git remote add origin https://github.com/TU-USUARIO/caleconsulting-web.git
git push -u origin main
```

La primera vez, Windows abre una ventana de **Git Credential Manager** para iniciar sesión en GitHub. **Ese inicio de sesión lo haces tú** en la ventana del navegador.

---

## Paso 4 — Activar GitHub Pages

1. En GitHub, dentro del repositorio → pestaña **Settings** → menú izquierdo **Pages**.
2. En **Build and deployment** → **Source**, elige **GitHub Actions**.
3. Ve a la pestaña **Actions** del repositorio: debe aparecer el flujo **"Publicar sitio"**. Si no corrió solo, ábrelo y haz clic en **Run workflow**.
4. Cuando termine con ✓ verde (1–2 minutos), la página ya está en línea en una dirección temporal: `https://TU-USUARIO.github.io/caleconsulting-web/`. Ábrela y revísala.

---

## Paso 5 — Verificar el dominio en GitHub (seguridad)

Esto evita que otra cuenta de GitHub pueda usar tu dominio.

1. En GitHub: tu foto (arriba a la derecha) → **Settings** → menú izquierdo **Pages**.
2. **Add a domain** → escribe `caleconsulting.net` → **Add domain**.
3. GitHub te muestra un registro **TXT** parecido a este:
   - Nombre/Host: `_github-pages-challenge-TU-USUARIO`
   - Valor: un código largo
4. Agrégalo en el panel DNS del Paso 1 (registro tipo **TXT**). En Squarespace: **DNS** → **Custom records** → **Add record**.
5. Vuelve a GitHub y clic en **Verify**. Si falla, espera 10–30 minutos y reintenta.

---

## Paso 6 — Apuntar el dominio a GitHub (registros DNS)

En el panel DNS de `caleconsulting.net`:

### 6.1 Revisar y limpiar solo lo que choca

- Si existe un registro **A** o **CNAME** con host `@` o `www` que apunta a otro lugar (por ejemplo el bloque **"Squarespace Defaults"** o una página de estacionamiento), hay que quitarlo. **Solo esos.**
- **NO borres nada** que diga **MX**, **Google Workspace**, `google-site-verification`, **SPF** (`v=spf1`), **DKIM** (`google._domainkey`) ni **DMARC**. Son los del correo.

### 6.2 Agregar estos registros

| Tipo | Host / Nombre | Valor |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |
| CNAME | `www` | `TU-USUARIO.github.io` |

Si el panel pide **TTL**, deja el valor por defecto (por ejemplo 1 hora). Los registros AAAA (IPv6) son recomendados; si el panel no los permite, basta con los A.

---

## Paso 7 — Conectar el dominio en el repositorio

1. Repositorio → **Settings** → **Pages** → **Custom domain** → escribe `caleconsulting.net` → **Save**.
2. GitHub revisa el DNS. Al principio puede decir que falla; es normal mientras se propaga el DNS (de minutos a 24 h).
3. Cuando aparezca **"DNS check successful"**, marca la casilla **Enforce HTTPS**. Si está gris, espera: GitHub está generando el certificado de seguridad (hasta 1 h después de que el DNS funcione).

---

## Paso 8 — Comprobar que todo funciona

- [ ] https://caleconsulting.net abre la página con el candado 🔒.
- [ ] https://www.caleconsulting.net redirige a la dirección sin www.
- [ ] Se ve bien en el celular.
- [ ] El selector EN / ES / PT funciona.
- [ ] El formulario envía una solicitud de prueba y llega al correo (si ya está la clave de Web3Forms).
- [ ] **El correo sigue funcionando:** envía un mensaje desde otro correo a tu dirección @caleconsulting.net y confirma que llega.

---

## Paso 9 — Después del lanzamiento (recomendado)

1. **Google Search Console** (https://search.google.com/search-console): agrega la propiedad `caleconsulting.net`. Como el dominio ya está verificado para Workspace, puede quedar verificado automáticamente. Envía el sitio para que Google lo indexe.
2. **Google Analytics**: crea una propiedad y pásale a Claude el ID (`G-XXXXXXX`) para agregarlo a la página.
3. **Perfil de Empresa de Google** (https://business.google.com): crea el perfil de Cale Consulting con el enlace a la web.
4. **LinkedIn**: agrega la URL en la página de empresa y en tu perfil.

---

## Cómo actualizar la página en el futuro

1. Pídele a Claude el cambio, por ejemplo: *"cambia el título de servicios"*.
2. Claude edita, verifica, registra el cambio en la bitácora y ejecuta `git push`.
3. GitHub publica solo en 1–2 minutos. Puedes seguir el progreso en la pestaña **Actions**.

## Si algo sale mal

| Síntoma | Qué hacer |
|---|---|
| El correo dejó de llegar | Compara el DNS con la captura del Paso 1 y restaura cualquier registro MX/TXT de Google que falte. |
| "Domain does not resolve" en GitHub | Espera la propagación (hasta 24 h). Revisa que los 4 registros A estén exactos. |
| "Enforce HTTPS" no se puede marcar | Espera hasta 1 h después de que el DNS funcione. Si sigue igual, borra el dominio personalizado en Pages, guarda y vuelve a ponerlo. |
| El flujo "Publicar sitio" falla | En **Settings** → **Pages**, revisa que **Source** sea **GitHub Actions**. |
| La página se ve sin estilos o vieja | Recarga forzada con **Ctrl + F5**. |
