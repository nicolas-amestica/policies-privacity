# Caché del navegador y del hosting

Si después de subir por FTP sigues viendo una **versión antigua** de la política, lo más probable es que **no sea el servidor**, sino una **copia en caché**.

## Comprobación rápida

Abre la misma URL en **una ventana privada/incógnito** o fuerza recarga sin caché:

- **Windows / Linux:** `Ctrl + Shift + R` o `Ctrl + F5`
- **Mac:** `Cmd + Shift + R`

Si ahí ves la versión nueva, el origen era la caché del navegador.

## Lo que está configurando tu hosting

El sitio público puede enviar cabeceras como:

```http
cache-control: max-age=604800, must-revalidate
```

Eso permite al navegador **guardar la página hasta una semana**. `must-revalidate` obliga a revalidar cuando expira el periodo, pero mientras tanto puedes seguir viendo HTML viejo.

## Soluciones

### 1. Tú (visitante)

- Recarga forzada o modo incógnito (arriba).
- Borrar datos de navegación del sitio para `policiesprivacy.info.girasindomito.cl`.

### 2. Panel del hosting

Si usas **LiteSpeed Cache**, **cPanel → Optimize Website**, **Cloudflare** delante del dominio, etc., usa **“Purge cache” / “Limpiar caché”** para ese subdominio o todo el dominio tras cada cambio importante.

### 3. Servidor Apache (FTP)

Sube junto con `index.html` el archivo **[`.htaccess`](../.htaccess)** incluido en este repo (requiere que el hosting permita `mod_headers`; si algo falla, renómalo o elimínalo y contacta al soporte).

Ese archivo intenta que **`index.html`** no se cachee agresivamente, para que los cambios legales se vean enseguida tras subirlos.

### 4. Truco rápido al compartir

Puedes enlazar con un parámetro que cambie cuando publiques:

`https://policiesprivacy.info.girasindomito.cl/?v=20260501`

No sustituye arreglar caché del servidor, pero ayuda a quien abre el enlace desde un correo antiguo.
