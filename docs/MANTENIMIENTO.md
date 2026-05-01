# Mantenimiento de la política de privacidad

## Archivo fuente único

Todo el texto visible y los estilos están en [`index.html`](../index.html). No hay pipeline de CSS aparte.

## Checklist al actualizar contenido

1. **Badge de vigencia**  
   Actualice la fecha en el elemento `<span class="badge">` del encabezado para que coincida con la publicación jurídica.

2. **Tabla de contenidos**  
   Si agrega o elimina secciones, actualice el `<nav class="toc">` y los `id` de cada `<section>` para que los anclajes coincidan.

3. **Numeración**  
   Los recuadros `<span class="num">` deben mantener orden coherente con el índice (o redefinir criterio de numeración de forma consistente).

4. **Enlaces externos**  
   Compruebe que URLs a Meta, Google, SII o sitio corporativo sigan vigentes.

5. **Coherencia operativa**  
   Verifique que lo descrito coincida con el portal, backend y proveedores reales (véase [`FUENTES-DEL-CONTENIDO.md`](FUENTES-DEL-CONTENIDO.md)).

6. **Revisión legal**  
   Cambios en finalidades, bases legales, plazos, transferencias internacionales o derechos deben pasar por abogado.

7. **Pie de página**  
   Alinee el año del copyright (`©`) con la política de la empresa si aplica.

## Prueba local

```bash
npm run serve
```

Revise responsive (móvil) y lectura de tablas anchas.

## Versionado en Git

Use mensajes de commit descriptivos y, si la política cambia por normativa nueva, etiquete el repositorio o anote la versión en el cuerpo del commit.
