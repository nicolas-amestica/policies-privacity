# Políticas de privacidad — Giras Indómito

Sitio estático que publica la **Política de Privacidad** de Giras Indómito Ltda. El contenido legal vive en un único HTML autocontenido (estilos embebidos) para poder hospedarlo en cualquier CDN o bucket S3 sin paso de build.

## Estructura del repositorio

```
policies-privacy/
├── README.md                 # Este archivo
├── CONTRIBUTING.md           # Cómo proponer cambios al contenido
├── CHANGELOG.md             # Historial de cambios del repo (no sustituye el badge legal en index.html)
├── package.json             # Scripts opcionales de vista previa local
├── .gitignore
├── .editorconfig
├── .htaccess                # Opcional (Apache): menos caché en index.html tras FTP
├── index.html               # Política completa + CSS inline
├── assets/
│   ├── README.md            # Recursos estáticos
│   └── gi-logo.png          # Marca en cabecera
└── docs/
    ├── README.md            # Índice de documentación
    ├── DESPLIEGUE.md        # Opciones de publicación (S3, CDN, etc.)
    ├── MANTENIMIENTO.md           # Actualizar texto, fechas y revisiones
    ├── FUENTES-DEL-CONTENIDO.md   # Alineación con el portal administrativo
    └── CACHE-NAVEGADOR-Y-HOSTING.md  # Caché tras despliegue FTP
```

## Requisitos

Ninguno obligatorio: basta un navegador y un servidor HTTP estático para previsualizar con rutas correctas.

Opcional: Node.js solo si usa los scripts de `package.json`.

## Vista previa local

Desde la raíz del proyecto:

```bash
npm run serve
```

Abra `http://localhost:5173`. Alternativa sin npm:

```bash
python3 -m http.server 5173
```

## Relación con otros proyectos

El contenido de la política está alineado de forma orientativa con el portal Angular **`portal_admin_ng_dev_pri_usw2`** (autenticación, pasajeros, pagos, WhatsApp/inbox, S3, etc.). El detalle está en [`docs/FUENTES-DEL-CONTENIDO.md`](docs/FUENTES-DEL-CONTENIDO.md).

## Despliegue

Instrucciones en [`docs/DESPLIEGUE.md`](docs/DESPLIEGUE.md).

## Licencia del contenido legal

El texto de la política es propiedad de **Giras Indómito Ltda.** y no implica licencia de código abierto sobre ese contenido. La estructura de este repositorio (plantillas Markdown, scripts) puede adaptarse según la política interna de la empresa.

## Contacto

Consultas sobre privacidad (según la política publicada): **contacto@girasindomito.cl**
