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

## ⚠️ Problema detectado (2026-10-10): dominio en "clientHold"

- La consulta RDAP de Verisign (el registro de .net) muestra el estado **`client hold`** para caleconsulting.net. Con ese estado el dominio **no resuelve en internet**: ni la web, ni el correo (MX), ni nada. Los DNS públicos responden NXDOMAIN para todo.
- Datos: registrado el 2024-01-31, vence el 2027-01-31, último cambio el 2026-01-16. Registrador: Squarespace Domains II LLC. Nameservers: `ns-cloud-d1..d4.googledomains.com`.
- Causa más común: **no se verificó el correo del titular** (verificación de contacto exigida por ICANN). El registrador pone el dominio en *hold* si no se confirma en 15 días. Como el vencimiento es en 2027, no parece un problema de pago.
- Solución: en Squarespace → dominio → revisar avisos o "Información general" → reenviar el correo de verificación del contacto → hacer clic en el enlace. El *hold* se levanta en minutos u horas. Si no aparece ninguna opción, contactar al soporte de Squarespace Domains.
- Comprobar el estado: `https://rdap.verisign.com/net/v1/domain/caleconsulting.net` (el estado debe dejar de incluir "client hold").

## Recomendación pendiente

- Falta un registro **DMARC** (`TXT _dmarc`). No es urgente, pero mejora la entrega del correo y protege contra suplantación. Valor inicial sugerido: `v=DMARC1; p=none; rua=mailto:<correo-de-reportes>`.
