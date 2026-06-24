# Escáner Makana en GitHub Pages → scan.oncemillon.com

Página del escáner del bartender, con **cámara real**, hosteada gratis en GitHub Pages.
Escribe los canjes en la misma Google Sheet llamando al Apps Script vía JSONP (sin CORS).

## Antes de empezar
1. **Redeploy del Apps Script** (porque agregamos el endpoint `action=redeem`):
   En el editor de Apps Script → **Deploy → Manage deployments → ✏️ Edit → Version: New version → Deploy**.
   La URL `/exec` NO cambia.
2. Confirma que en `index.html` (bloque CONFIG) coincidan con el Apps Script:
   - `EXEC` = tu URL `/exec` (ya está puesta)
   - `TOKEN` = `mkscan_4Qp7Lh` (= `CONFIG.API_TOKEN`)
   - `PIN` = `4321` (= `CONFIG.SCANNER_PIN`)

## Paso 1 — Crear el repo
1. En la cuenta de GitHub de oncemillon: **New repository** → nombre p.ej. `makana-scan` → **Public** → Create.
   > Público es válido (el código no guarda secretos sensibles; el token solo evita llamadas casuales).
2. Sube el archivo **`index.html`** y el archivo **`CNAME`** de esta carpeta (botón *Add file → Upload files*).

## Paso 2 — Activar GitHub Pages
1. Repo → **Settings → Pages**.
2. En *Build and deployment* → **Source: Deploy from a branch** → Branch: `main` → carpeta `/ (root)` → **Save**.
3. A los ~1–2 min queda en `https://<usuario>.github.io/makana-scan/` (pruébalo ya; la cámara debe pedir permiso).

## Paso 3 — Subdominio scan.oncemillon.com
1. Donde administras el DNS de **oncemillon.com**, agrega un registro:
   ```
   Tipo: CNAME   |   Host/Nombre: scan   |   Valor/Destino: <usuario>.github.io
   ```
   (sin `https`, sin barra final).
2. En GitHub: **Settings → Pages → Custom domain** → escribe `scan.oncemillon.com` → Save.
   (El archivo `CNAME` del repo ya lo deja preconfigurado.)
3. Espera a que verifique el DNS (minutos a ~1 h) y marca **Enforce HTTPS**.

## Listo
- URL final del bartender: **https://scan.oncemillon.com**
- En la tablet/celular del bar: abre la URL → menú del navegador → **Agregar a pantalla de inicio** (queda como app).
- PIN: `4321` (cámbialo en ambos lados: `CONFIG.SCANNER_PIN` del Apps Script y `PIN` en `index.html`).

## Seguridad (opcional, endurecer luego)
- El token bloquea llamadas casuales. Para canjear hace falta un **código real** (que solo ve el cliente), así que el riesgo de abuso es bajo.
- Si quieres repo privado con Pages, requiere plan pago de GitHub. Para este caso, público está bien.
