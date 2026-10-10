# Bitácora del proyecto

Registro de todo lo realizado, del más reciente al más antiguo. Agregar una entrada nueva arriba cada vez que se haga un cambio.

---

## 2026-10-09 — Sesión 2

### 1. Formulario conectado
- Se instaló la *Access Key* de Web3Forms en `web/index.html`. Las solicitudes llegan al correo con el que se generó la clave, que no aparece en la página.
- Prueba de envío hecha desde la vista previa local: Web3Forms respondió con éxito y el usuario confirmó que el correo llegó.

### 2. Código subido a GitHub
- Repositorio: https://github.com/Wag-Claude/caleconsulting-web (público, rama `main`).
- La primera ejecución de "Publicar sitio" falló porque GitHub Pages aún no estaba activado (falta poner **Source = GitHub Actions** en Settings → Pages).

### 3. Página en línea (dirección temporal)
- El usuario activó Pages (Source = GitHub Actions) y ejecutó el flujo: terminó con éxito.
- En línea en https://wag-claude.github.io/caleconsulting-web/ : responde 200, el logo y el favicon cargan, y no hay errores en la consola.
- Siguiente: conectar el dominio caleconsulting.net (Pasos 1, 5, 6 y 7 de `docs/PUBLICAR.md`).

## 2026-10-10 — Sesión 3

### 4. Cambios pedidos por el cliente (v3)
- **Idioma:** la página siempre abre en **inglés**. Se quitó la detección del idioma del navegador y la memoria del idioma elegido.
- **Nombre más grande:** "Cale Consulting" en el menú pasó de 20px a 25px, con logo de 34px y barra de 76px. En celular pasó de 17px a 20px, y en el pie de página a 28px.
- **Nuevo posicionamiento** (no solo IA):
  - Titular: *"Technology that drives your business forward."* (ES: *"Tecnología que impulsa tu negocio."*, PT: *"Tecnologia que impulsiona o seu negócio."*).
  - 6 servicios en una cuadrícula de 3 columnas: Consultoría tecnológica, **Adopción de IA (tarjeta destacada con brillo naranja)**, Redes cableadas y Wi-Fi, Conectividad internacional, Automatización y Transformación digital. Hay íconos nuevos de Wi-Fi y de globo.
  - Actualizados en consecuencia: la terminal animada (sedes, Wi-Fi, horas manuales, IA), la marquesina, el paso 1 del método, el texto de partners (redes y telecomunicaciones), la órbita (Networks, Connectivity), el formulario (6 opciones), el pie, la nueva pregunta frecuente 5 (oficinas en varios países), el SEO y los datos estructurados.
  - Las claves de los servicios pasaron de `sv.1..4` a nombres: `sv.cons`, `sv.ai`, `sv.net`, `sv.intl`, `sv.auto`, `sv.dx`.
- **Logo:** 5 propuestas en `docs/logos/propuestas.html` (Señal, Red, Globo, Chispa, Terminal) más la actual, mostradas en grande, junto al nombre sobre fondo oscuro y claro, y en tamaño ícono. Pendiente: la elección del cliente.
- Verificado: todas las claves de texto existen en los 3 idiomas, la página abre en inglés aunque haya un idioma guardado, no hay errores en la consola, no hay desbordes en celular y la cuadrícula es de 3 columnas en escritorio.

### 3. 🚀 Sitio publicado en https://caleconsulting.net
- El usuario marcó **Enforce HTTPS** en GitHub.
- Comprobado: `https://caleconsulting.net` responde 200 con certificado válido. `http://` y `www` redirigen con 301 a `https://caleconsulting.net/`. Fuentes, idiomas y formulario cargan bien, sin errores en la consola y sin desbordes en celular.
- Se agregó en Squarespace el TXT de verificación de GitHub (`_github-pages-challenge-Wag-Claude`) y se confirmó que se ve públicamente con el valor correcto. El usuario hizo clic en **Verify** y GitHub marcó el dominio como **verificado**. ✅ Publicación terminada.

### 2. Suspensión levantada: el dominio ya abre la página
- El usuario cambió el correo de contacto en Squarespace por uno externo y lo verificó. RDAP ya no muestra "client hold".
- Comprobado: el MX del correo resuelve de nuevo. `http://caleconsulting.net` responde 200 con la página y `www` redirige con 301 al dominio sin www.
- HTTPS aún no responde porque GitHub está emitiendo el certificado. Falta marcar **Enforce HTTPS** en Settings → Pages.
- El TXT de verificación de GitHub (`_github-pages-challenge-wag-claude`) todavía no está agregado.

### 1. El dominio no resuelve: está en clientHold
- El usuario agregó los registros A/AAAA/CNAME en Squarespace y configuró el dominio personalizado en GitHub, pero GitHub mostró "DNS check unsuccessful" (InvalidDNSError).
- Diagnóstico: los DNS públicos responden NXDOMAIN para todo el dominio, incluido el MX. RDAP de Verisign: estado **client hold**. El problema no son los registros, sino que el registrador tiene el dominio suspendido. Detalle y solución en `docs/DNS.md`.
- Consecuencia: el correo @caleconsulting.net probablemente **no recibe mensajes desde fuera** mientras dure el hold.

## 2026-10-08 — Sesión 1: diseño y construcción inicial

### 5. Preparación para publicar
- Se eligió **GitHub Pages**: gratis y con HTTPS, y el dominio se conecta sin mover los nameservers, así que el correo de Workspace queda a salvo.
- Se agregó `.github/workflows/publicar.yml`, que publica la carpeta `web/` automáticamente con cada `git push` a `main`.
- Se escribió la guía paso a paso en `docs/PUBLICAR.md`: DNS, GitHub, verificación del dominio, HTTPS, pruebas y qué hacer si algo falla.

### 4. Nombre más visible + proyecto organizado
- Menú: el nombre aparece completo, **"Cale Consulting"**, en 20px ("Cale" en blanco, "Consulting" en gris claro) y también se ve en celular. El botón de menú del celular pasó a ser un ícono (☰) para dejarle espacio al nombre.
- Portada: la etiqueta superior ahora dice **"CALE CONSULTING / Technology & AI for SMBs"**.
- Pie de página: el nombre completo **"Cale Consulting"** en letras gigantes.
- `logo.svg` actualizado con el nombre completo.
- Se creó la estructura de proyecto: `README.md`, `docs/BITACORA.md`, `.claude/launch.json` y un repositorio git con el primer commit.
- Servidor local de vista previa: configuración `cale-web` (puerto 5500).

### 3. Versión 2 — contenido real del negocio, en 3 idiomas
Información del cliente:
- Servicios: consultoría tecnológica, adopción de IA, transformación digital, automatización de procesos y afines.
- Público: pequeñas y medianas empresas.
- Empresa nueva, **sin casos ni clientes todavía**. El fundador tiene más de 20 años en tecnología y una red de partners de distintas especialidades.
- Sin logo: se diseñó uno.
- El correo no debe mostrarse; el contacto es por un formulario de solicitud de cita.
- Pidió imágenes acordes al estilo, animación con "brillo", y contenido en inglés con opción a español y portugués.

Lo construido:
- **Logo:** una "C" abierta con un punto naranja de "señal en vivo" (`web/assets/`).
- **Secciones:** Portada → franja de capacidades → Servicios (4) → Cómo trabajamos (4 pasos) → Por qué Cale → Nosotros (órbita de partners) → Preguntas frecuentes → Contacto (formulario) → Pie.
- **Se quitaron las cifras y casos inventados** de la versión 1. La credibilidad se apoya en los +20 años de experiencia y la red de partners.
- **Animaciones:**
  - fondo de puntos que se ilumina y sigue al mouse (canvas);
  - resplandor naranja que "respira";
  - borde de luz giratorio en el panel;
  - terminal que simula un diagnóstico, con contadores (marcada "Illustrative example");
  - destello que recorre la palabra "AI" del titular;
  - foco de luz en las tarjetas de servicio;
  - íconos que se dibujan al pasar el cursor;
  - órbita de partners girando;
  - barra de progreso en los pasos;
  - textos que aparecen al hacer scroll;
  - marquesina continua.

  Todas se desactivan si el visitante tiene activado "reducir movimiento" en su sistema.
- **Idiomas:** diccionario `I18N` con EN/ES/PT. Detecta el idioma del navegador y recuerda la elección.
- **Formulario:** nombre, correo, empresa, tamaño, servicio de interés, fecha y horario preferidos, y mensaje. Envía vía Web3Forms (falta la clave), con antispam y validación.
- **SEO básico:** título y descripción por idioma, Open Graph y datos estructurados (schema.org `ProfessionalService`).
- Se revisó en escritorio (1440px) y en celular (360–375px): sin desbordes y sin errores en la consola.

### 2. Decisión de plataforma: sitio a la medida en vez de Google Sites
- El cliente compartió una guía de estilo (`DESIGN.md`, estética "Factory": fondo #101010, tarjetas #eeeeee, Geist 400).
- Google Sites no permite esa tipografía, el espaciado, las tarjetas ni los radios → el cliente eligió la **opción C**: HTML estático a la medida + hosting gratuito + su dominio.
- Versión 1 (maqueta) con textos y cifras de ejemplo.

### 1. Inicio
- Pedido original: página web de Cale Consulting en Google Sites con el dominio caleconsulting.net (Google Workspace).
- Se entregó el cuestionario de descubrimiento y la propuesta de estructura.
