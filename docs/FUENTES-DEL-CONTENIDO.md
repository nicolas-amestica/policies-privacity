# Fuentes del contenido (alineación con el portal)

Este documento enlaza los **apartados de la política** publicada en [`index.html`](../index.html) con **módulos del portal administrativo** `portal_admin_ng_dev_pri_usw2`. Sirve para auditorías internas; no forma parte del texto legal mostrado al público.

> Nota: Las rutas siguientes son relativas al repositorio del portal, no a este repo.

## Autenticación y sesión

- **Google Identity Services**, JWT, menú IAM, renovación de sesión: `src/app/app-auth/services/auth.service.ts`, stores `fn-login.ts`, `fn-google-login.ts`, `fn-renew-token.ts`.
- **Perfil usuario** (nombre, teléfono, contraseña): `src/app/app-admin-portal/profile/`.
- **`localStorage` / `sessionStorage`**: `src/app/app-auth/stores/`, `src/app/shared/constants/client-home-notice-session.const.ts`, `src/app/shared/stores/theme/theme.store.ts`.

## Programas, contratos y notificaciones

- Modelo de programa, representantes, institución, pagos contractuales: `src/app/app-admin-portal/program/interfaces/program.interface.ts`.
- Contratos y envío por correo (adjuntos S3 / base64): `src/app/app-admin-portal/program/interfaces/contract-request.interface.ts`, `program/services/contract.service.ts`.

## Pasajeros y fichas médicas

- Datos de pasajeros y metadatos de ficha en S3: `src/app/app-admin-portal/passenger/interfaces/passenger.interface.ts`, `passenger/services/passenger.service.ts`.

## Pagos

- Webpay / Transbank (crear, confirmar, cancelar cuotas): `src/app/app-admin-portal/payment/services/payment.ts`, interfaces en `payment/interfaces/`.

## Contabilidad y SII

- Ingresos, gastos, comprobantes en S3: `src/app/app-admin-portal/accounting/interfaces/`.
- DTE (validar, emitir, estado): `src/app/app-admin-portal/accounting/services/dte.service.ts`.

## WhatsApp, inbox y adjuntos

- Conversaciones, mensajes (cliente / equipo / agente IA), adjuntos prefirmados: `src/app/app-admin-portal/inbox/services/inbox.service.ts`, `inbox/interfaces/inbox.interface.ts`.
- WebSocket (opcional para tiempo real): `src/app/app-admin-portal/inbox/services/inbox-ws.service.ts`, `src/app/core/services/portal-ws.service.ts`.

## Reuniones

- Google Calendar / Meet vía API propia: `src/app/app-admin-portal/meet/services/meet.service.ts`, `meet/interfaces/meet.interface.ts`.

## Infraestructura y entorno

- API Gateway, WebSocket, buckets S3, URL de assets públicos: `src/environments/environment*.ts`.

## Analytics del portal

El módulo **analytics** del SPA consume **API propia** (`/v1/analytics`); no equivale a Google Analytics en el código revisado. La política puede mencionar tratamientos agregados de negocio solo si el backend los implementa así.

---

Cuando incorpore un **nuevo módulo** o proveedor en el portal, actualice primero la práctica real y luego refleje el cambio en `index.html` y en esta tabla si facilita el trabajo del equipo legal.
