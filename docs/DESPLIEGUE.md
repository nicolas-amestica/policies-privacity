# Despliegue

Este proyecto es **100 % estático**: solo necesita servir `index.html` y la carpeta `assets/` en la misma jerarquía relativa.

## Archivos que deben publicarse

- `index.html` (raíz del sitio)
- `assets/gi-logo.png` (y cualquier otro recurso añadido bajo `assets/`)

No es necesario compilar ni instalar dependencias para producción.

## URL recomendada

Mantenga una URL estable (por ejemplo `policiesprivacy.info.girasindomito.cl` o la convención que use la empresa) y configure redirecciones HTTP → HTTPS.

## Opciones de hosting

### Hosting compartido (FTP / cPanel)

Este sitio **no usa PHP ni base de datos**: solo son archivos estáticos. Lo habitual es que “no funcione” por **ubicación**, **nombre del índice** o **falta la carpeta `assets/`**.

#### 1. Dónde subir los archivos

En la mayoría de hostings la web pública es una de estas carpetas (conéctese por FTP y compruebe cuál existe):

| Carpeta típica | Uso |
| ---------------- | --- |
| `public_html/` | Raíz del dominio principal (`https://tudominio.cl/`) |
| `www/` | A veces es un acceso directo igual a `public_html` |
| `domains/tudominio.cl/public_html/` | Multidominio en algunos paneles |

Debe existir **exactamente** esta estructura **dentro** de esa carpeta (o dentro de una subcarpeta si publica solo la política, p. ej. `public_html/privacidad/`):

```text
public_html/
├── index.html
└── assets/
    └── gi-logo.png
```

**Importante:** si sube solo `index.html` y el logo lo deja suelto al lado sin carpeta `assets`, la imagen dará **404** y parecerá rota la cabecera. Use el cliente FTP en modo que **preserve carpetas** (no aplastar todo en un solo directorio).

#### 2. Documento índice del servidor

El servidor debe servir `index.html` cuando entras a la URL sin archivo (por ejemplo `https://tudominio.cl/`).

En **cPanel** → *Preferencias del índice* / *Indexes* o *DirectoryIndex*: incluya `index.html` primero (antes que `index.php` si hace falta).

Prueba directa en el navegador:

```text
https://tudominio.cl/index.html
```

Si esa URL **sí** muestra la política pero `https://tudominio.cl/` no, el problema es solo la configuración del índice.

#### 3. Sitio en una subcarpeta

Si los archivos están en `public_html/privacidad/`:

- La URL correcta es `https://tudominio.cl/privacidad/` o `https://tudominio.cl/privacidad/index.html`.
- Las rutas relativas del proyecto (`./assets/gi-logo.png`) siguen siendo válidas respecto a esa carpeta; no cambie el HTML solo por estar en subcarpeta.

#### 4. Modo de transferencia FTP

Use transferencia **binaria** (o automática) para `gi-logo.png`. En modo ASCII incorrecto la imagen puede corromperse.

#### 5. Permisos

Valores habituales: archivos **644**, carpetas **755**.

#### 6. Comprobación rápida

1. Abrir DevTools del navegador (F12) → pestaña **Red / Network**.
2. Recargar la página.
3. Si `gi-logo.png` sale en **404**, falta la ruta `assets/gi-logo.png` en el servidor o está mal escrita (mayúsculas/minúsculas: en Linux `Assets` ≠ `assets`).

#### 7. “Sigo viendo la versión antigua” tras subir archivos

Muchos hostings envían `Cache-Control` largo (por ejemplo **7 días**) para HTML. El archivo nuevo puede estar en el servidor, pero el navegador muestra una copia vieja.

- Prueba **recarga forzada** (`Ctrl+Shift+R` / `Cmd+Shift+R`) o **ventana privada**.
- Si el hosting tiene **caché** (LiteSpeed, Cloudflare, etc.), use **purga / limpiar caché**.
- Opcional: suba también el **[`.htaccess`](../.htaccess)** de la raíz del repo para intentar desactivar caché agresiva solo en `index.html` (Apache + `mod_headers`).

Detalle en [`CACHE-NAVEGADOR-Y-HOSTING.md`](CACHE-NAVEGADOR-Y-HOSTING.md).

### Amazon S3 + CloudFront

1. Cree un bucket configurado para hosting estático o sirva objetos detrás de **CloudFront**.
2. Suba `index.html` como objeto raíz (`/`).
3. Suba `assets/gi-logo.png` manteniendo el prefijo `assets/`.
4. Configure `index.html` como documento índice del bucket o comportamiento equivalente en CloudFront.
5. Active HTTPS en el distribuidor.

Ejemplo de sincronización con AWS CLI (ajuste bucket y perfil):

```bash
aws s3 sync . s3://SU-BUCKET-PRIVACY/ \
  --exclude '.git/*' \
  --exclude 'docs/*' \
  --exclude '*.md' \
  --exclude 'package.json' \
  --exclude '.editorconfig' \
  --exclude '.gitignore'
```

Revise los `--exclude` para no subir documentación si no la desea pública; si el bucket es solo para este sitio, puede sincronizar solo `index.html` y `assets/`.

### GitHub Pages

1. Publique la rama `main` desde la carpeta raíz del repo (site root `/`).
2. Asegúrese de que `assets/gi-logo.png` esté versionado.

### Netlify / Vercel / Render (sitio estático)

- **Publish directory**: raíz del repo (`/`).
- **Build command**: vacío.

### Servidor propio (Nginx)

Ejemplo mínimo de `location`:

```nginx
location / {
    root /var/www/policies-privacy;
    try_files $uri $uri/ /index.html;
}
```

Para un único `index.html` sin rutas adicionales, basta con servir el archivo en `/`.

## Cabeceras HTTP recomendadas

- `Content-Type: text/html; charset=utf-8` para `/index.html`.
- Política de seguridad razonable (`Content-Security-Policy`) si el equipo la define globalmente (la página usa fuentes de Google Fonts).

## Tras cada despliegue

Verifique en navegador privado:

1. Carga correcta del logo (`assets/gi-logo.png`).
2. Fecha de actualización en el badge superior.
3. Enlaces externos (WhatsApp, Google, girasindomito.cl) abren en nueva pestaña donde corresponda.
