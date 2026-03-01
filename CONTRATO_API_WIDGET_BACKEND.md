# Contrato API — Widget Zendesk Sell (Repo A) ↔ Backend/Portal Render BOX-IA (Repo B)
**Versión:** 1.0.0  
**Estado:** Activo  
**Fecha:** 2026-03-01  
**Dueños:** Clinyco (Equipo CRM/Automatización)

---

## 0) Propósito
Este contrato define **cómo se integran**:
- **Repo A:** Widget en Zendesk Sell (UI/acciones del agente)
- **Repo B:** Backend/Portal en Render (BOX-IA) para Drive, templates y render de documentos

Objetivos clave:
1) Unificar **templates, carpetas Drive y lógica de creación** en el backend BOX-IA.
2) Asegurar **Accountability**: toda acción relevante queda asociada a un **Agente** y registrada.
3) Forzar **creación obligatoria de notas** en Zendesk Sell para acciones que generan valor.
4) Incluir en **todos los documentos** un header gris: `DEAL.ID + Agente email`.

---

## 1) Definiciones
- **Widget (A):** App en Zendesk Sell, se ejecuta en el contexto del usuario autenticado en Sell.
- **Backend/Portal (B):** Servicio en Render (BOX-IA), fuente de verdad de templates y Drive.
- **Actor (Agente):** Usuario autenticado en Sell o Portal (email @clinyco.cl).
- **Acción de valor:** cualquier acción asociada a incentivos/ingresos (crear docs, crear carpeta, crear contacto/deal, etc.).

---

## 2) Autenticación y Autorización

### 2.1 Widget (A) → Backend (B)
- Header obligatorio: `x-api-key: <API_KEY>`
- TLS obligatorio (HTTPS).
- El widget debe enviar un objeto `actor` en **todas** las acciones de valor.

**Regla de dominio:**
- El widget debe bloquear o degradar permisos si `actor.email` NO termina en `@clinyco.cl`.

### 2.2 Portal (B) — Login
- Login recomendado: Google OAuth/Workspace restringido a `@clinyco.cl`.
- Modo “Invitado” (transitorio):
  - Permitido: ver UI, navegar, demo.
  - NO permitido: generar documentos, crear carpetas Drive, crear/editar contactos/deals, escribir notas.

---

## 3) Identidad del Actor (Accountability)

### 3.1 Contrato del objeto `actor`
El widget debe enviar:

```json
{
  "actor": {
    "sell_user_id": 12345,
    "email": "agente@clinyco.cl",
    "name": "Nombre Apellido"
  },
  "source": "sell_widget"
}
