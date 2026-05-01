# Contribución y cambios al contenido legal

## Alcance

Este repositorio contiene texto con efectos jurídicos. Los cambios sustantivos deben ser revisados por **asesoría legal** y por **producto/operaciones** para asegurar que reflejan la práctica real de tratamiento de datos.

## Flujo recomendado

1. Abrir una rama desde `main` con un nombre descriptivo (`docs/actualiza-conservacion`, `legal/revision-mayo-2026`).
2. Editar únicamente [`index.html`](index.html) para el texto visible y la fecha del badge de vigencia en cabecera.
3. Actualizar [`docs/MANTENIMIENTO.md`](docs/MANTENIMIENTO.md) si incorpora nuevo proceso de revisión o checklist interno.
4. Si el cambio introduce nuevos tratamientos o proveedores, actualizar también [`docs/FUENTES-DEL-CONTENIDO.md`](docs/FUENTES-DEL-CONTENIDO.md).
5. Generar PR con descripción clara del motivo del cambio y referencias normativas si aplican.

## Commits

Seguir **Conventional Commits** en español cuando el equipo los use, por ejemplo:

- `docs: actualiza plazos de conservación en política de privacidad`
- `fix: corrige enlace externo en sección de pagos`

## Qué no hacer

- No incluir datos personales reales en commits, issues ni ejemplos en la documentación.
- No declarar tratamientos que el sistema no realiza sin confirmación explícita del negocio.
- No eliminar la nota de que la política no sustituye asesoría legal sin indicación contraria del área jurídica.
