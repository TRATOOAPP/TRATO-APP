# Trato · puesta en marcha (gratis)

Carpeta: `index.html` (la app), `schema.sql` (base de datos), `terminos.html` y `privacidad.html` (plantillas legales).

## 1. Base de datos (Supabase, plan gratis)
1. Crea cuenta en supabase.com y un proyecto nuevo (región UE).
2. **SQL Editor** → pega todo `schema.sql` → **Run**.
3. **Authentication → Providers → Email**: déjalo activado. Para probar rápido puedes desactivar "Confirm email"; en producción mantenlo activado.
4. **Project Settings → API**: copia *Project URL* y la clave *anon public*.
5. Abre `index.html` y rellena arriba del script: `const SB={url:"https://TU-PROYECTO.supabase.co",key:"TU_CLAVE_ANON"}`.
   La clave anon es pública por diseño; la protegen las reglas de seguridad (RLS) del paso 2. **Nunca** pongas la clave `service_role`.
6. **Authentication → URL Configuration**: pon la dirección final de tu web en *Site URL*.

## 2. Publicar la web (gratis)
Cloudflare Pages → *Create project* → *Direct Upload* → sube esta carpeta. (GitHub Pages y Netlify también valen.)

## 3. Antes de abrir al público
- Rellena los [corchetes] de `terminos.html` y `privacidad.html` y que los revise un abogado.
- Los pagos siguen **simulados**: no cobres dinero real así. Para pagos reales hace falta Stripe Connect (o Mangopay) con la lógica de pagos en el servidor (Supabase Edge Functions), porque ahora el navegador podría alterar el estado de un pago.
- El plan gratis de Supabase se pausa tras 1 semana sin uso.
- Los archivos del chat van dentro de la base de datos (límite 600 KB cada uno): para volumen real, pásalos a Supabase Storage.
- Si dos personas escriben a la vez en el mismo contrato, prevalece el último guardado: para volumen real, mueve los mensajes a su propia tabla.
