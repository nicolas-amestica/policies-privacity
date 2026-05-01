# Despliegue

Este proyecto es **100 % estático**: solo necesita servir `index.html` y la carpeta `assets/` en la misma jerarquía relativa.

## Archivos que deben publicarse

- `index.html` (raíz del sitio)
- `assets/gi-logo.png` (y cualquier otro recurso añadido bajo `assets/`)

No es necesario compilar ni instalar dependencias para producción.

## URL recomendada

Mantenga una URL estable (por ejemplo `policiesprivacy.info.girasindomito.cl` o la convención que use la empresa) y configure redirecciones HTTP → HTTPS.

## Opciones de hosting

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
