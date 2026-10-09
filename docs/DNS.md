# DNS de caleconsulting.net

- **Registrador / panel DNS:** Squarespace Domains. Se entra desde admin.google.com → Cuenta → Dominios → Administrar dominios → *Manage domain (via Squarespace)*, con la cuenta Admin@caleconsulting.net.
- **Nameservers:** los de Squarespace (no se cambian).
- Ruta en Squarespace: **DNS → Configuración de DNS**.

## Respaldo: registros ANTES de publicar la web (2026-10-09)

Si el correo falla en algún momento, compara con esta tabla y restaura lo que falte.

**Ajustes predeterminados → "Conectar dominio de Squarespace"**

| Tipo | Nombre | Datos | TTL |
|---|---|---|---|
| CNAME | `_domainconnect` | `_domainconnect.domains.squarespace.com` | 1 h |

**Registros personalizados (correo de Google Workspace)**

| Tipo | Nombre | Prioridad | Datos | TTL |
|---|---|---|---|---|
| MX | `@` | 1 | `aspmx.l.google.com` | 4 h |
| MX | `@` | 5 | `alt1.aspmx.l.google.com` | 4 h |
| MX | `@` | 5 | `alt2.aspmx.l.google.com` | 4 h |
| MX | `@` | 10 | `alt3.aspmx.l.google.com` | 4 h |
| MX | `@` | 10 | `alt4.aspmx.l.google.com` | 4 h |
| TXT | `@` | — | `v=spf1 include:_spf.google.com ~all` | 4 h |
| TXT | `google._domainkey` | — | `v=DKIM1; k=rsa; p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ…` (clave DKIM completa en el panel de Google Admin → Gmail → Autenticar correo) | 4 h |

No había registros A/CNAME para `@` ni `www`, así que no se borró nada.

## Registros agregados para la web (GitHub Pages)

| Tipo | Nombre | Datos |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| AAAA | `@` | `2606:50c0:8000::153` |
| AAAA | `@` | `2606:50c0:8001::153` |
| AAAA | `@` | `2606:50c0:8002::153` |
| AAAA | `@` | `2606:50c0:8003::153` |
| CNAME | `www` | `wag-claude.github.io` |
| TXT | `_github-pages-challenge-wag-claude` | *(código de verificación que da GitHub)* |

## Recomendación pendiente

- Falta un registro **DMARC** (`TXT _dmarc`). No es urgente, pero mejora la entrega del correo y protege contra suplantación. Valor inicial sugerido: `v=DMARC1; p=none; rua=mailto:<correo-de-reportes>`.
