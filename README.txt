CÓMO INSTALAR TU APP (PWA)
===========================

Esta carpeta contiene todo lo necesario:
- DATABASE.html   (la app)
- manifest.json   (metadatos de instalación)
- sw.js           (service worker, permite que funcione offline)
- icons/          (íconos de la app)

IMPORTANTE: para que "Instalar app" aparezca y funcione el modo offline,
el navegador necesita que estos archivos se sirvan por http(s), NO abriendo
el archivo DATABASE.html directamente con doble clic (protocolo file://).
Esa es una restricción de seguridad de todos los navegadores, no de la app.

OPCIÓN 1 — Probarlo en tu compu (rápido, local):
  1. Abrí una terminal en esta carpeta.
  2. Ejecutá:  python3 -m http.server 8000
  3. Abrí en el navegador:  http://localhost:8000/DATABASE.html
  4. Vas a ver la opción "Instalar app" en la barra de direcciones (Chrome/Edge)
     o "Agregar a pantalla de inicio" en el celular.

OPCIÓN 2 — Hostearlo gratis y accederlo desde cualquier dispositivo:
  - Netlify Drop: https://app.netlify.com/drop
    Arrastrá esta carpeta completa a la página y te da un link público al toque.
  - GitHub Pages: subí esta carpeta a un repositorio y activá Pages.
  - Cualquier hosting estático (Vercel, Cloudflare Pages, etc.)

  Una vez hosteado, entrá desde el celular a la URL que te dieron y elegí
  "Agregar a pantalla de inicio" (Android/Chrome) o "Compartir > Agregar a
  inicio" (iPhone/Safari). Va a quedar como un ícono más, abre en pantalla
  completa sin la barra del navegador, y funciona sin internet una vez
  que la abriste al menos una vez.

NOTA SOBRE TUS DATOS:
Tus ligas/equipos/jugadores se guardan en el almacenamiento local del
navegador (localStorage) de ese dominio específico. Si cambiás de hosting
o de navegador, no se transfieren solos — usá el botón de exportar/importar
de la app para llevarte tu base de datos de un lado a otro.
