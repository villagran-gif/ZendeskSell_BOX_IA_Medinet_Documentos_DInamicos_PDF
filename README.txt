PATCH — Pendientes (Sección botones + Export Tampermonkey)

Qué agrega
1) Una sección de 4 botones (A/B/C/E) horizontal entre el header y la primera card (IA BOX).
2) Una sección al final del portal para:
   - cargar /api/deal-context por deal_id
   - mostrar links de Deal/Contacto
   - armar un JSON desde los campos del formulario
   - copiar al portapapeles (para pegar en Medinet vía Tampermonkey)

Archivos incluidos
- public/portal_nav_actions.css
- public/portal_nav_actions.js

Cómo instalar
1) Copia ambos archivos a tu carpeta:
   public/

2) Edita public/index.html y agrega:

  (A) en el <head> (después de style.css está bien):
      <link rel="stylesheet" href="/portal_nav_actions.css" />

  (B) antes de </body> (idealmente después de /app.js):
      <script src="/portal_nav_actions.js"></script>

Ejemplo al final del body:
    <script src="/app.js"></script>
    <script src="/portal_nav_actions.js"></script>
  </body>

Notas
- Los botones NO ejecutan acciones automáticamente: solo navegan y hacen foco.
- La sección Tampermonkey arma el JSON principalmente desde el formulario (IA BOX / Crear Contacto).
  El deal_id es opcional, sirve para traer links desde Sell.
