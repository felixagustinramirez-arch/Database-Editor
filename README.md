# Editor de Base de Datos — Manager de Fútbol

App web (PWA) para armar y editar ligas, equipos y jugadores para tu manager de fútbol: posiciones, estadísticas, contrato, salario, valor de mercado, presupuestos de club y más. Se puede usar desde el navegador o instalarse como app en el celular, y funciona sin internet una vez abierta al menos una vez.

## Estructura de archivos

```
├── DATABASE.html       → la app (todo el código vive acá)
├── manifest.json        → metadatos de instalación (nombre, ícono, colores)
├── sw.js                 → service worker (cachea la app para que ande offline)
├── icons/                → íconos de la app (Android/escritorio/favicon)
└── splash/               → pantallas de carga para iPhone (evitan el flash blanco al abrir)
```

Todos los archivos deben quedar juntos, respetando esta misma estructura de carpetas — el HTML los referencia con rutas relativas (`./manifest.json`, `icons/...`, `splash/...`).

## ⚠️ Requisito importante

Para que la instalación y el modo offline funcionen, la app necesita servirse por **http o https** — **no alcanza con abrir el archivo con doble clic** (eso es `file://`, y ahí los navegadores bloquean el service worker y el manifest por seguridad).

## Cómo probarlo en tu compu (rápido)

```bash
python3 -m http.server 8000
```

Y abrí `http://localhost:8000/DATABASE.html`.

## Cómo tenerlo instalado de verdad (hosting gratis)

### Opción A — GitHub Pages
1. Subí esta carpeta completa a un repositorio de GitHub, manteniendo la estructura de arriba.
2. Andá a **Settings → Pages**, elegí la rama y la carpeta raíz, guardá.
3. Te da una URL tipo `https://tu-usuario.github.io/tu-repo/DATABASE.html`.
   *(Tip opcional: subí también una copia renombrada a `index.html` para que la URL corta abra la app directo.)*

### Opción B — Netlify Drop
Entrá a [app.netlify.com/drop](https://app.netlify.com/drop) y arrastrá la carpeta completa. Te da un link público al toque, sin cuenta.

Cualquier otro hosting estático (Vercel, Cloudflare Pages, etc.) también sirve.

## Instalar en el celular

- **iPhone (Safari):** entrá a la URL → botón **Compartir** → **Agregar a pantalla de inicio**.
- **Android (Chrome):** entrá a la URL → menú (⋮) → **Instalar app** / **Agregar a pantalla de inicio**.

Una vez instalada abre en pantalla completa, sin la barra del navegador, con su propio ícono y splash screen.

## Tus datos

Las ligas, equipos y jugadores se guardan en el **almacenamiento local del navegador** (`localStorage`) del dominio donde esté hosteada la app. Cosas a tener en cuenta:

- Los datos **no se comparten entre navegadores ni dominios distintos** (si la movés de Netlify a GitHub Pages, por ejemplo, no se trasladan solos).
- Usá el botón de **exportar / importar** dentro de la app para hacer respaldos o mover tu base de datos de un lado a otro.
- Si navegás en modo privado/incógnito, los datos se pierden al cerrar esa ventana — es una limitación del navegador, no de la app.

## Actualizar la app más adelante

El service worker (`sw.js`) cachea todo para que funcione offline, pero por eso mismo puede tardar en notar cambios nuevos que subas. Si actualizás `DATABASE.html` y no ves el cambio reflejado:

1. Abrí `sw.js` y subí el número de versión en la primera línea:
   ```js
   const CACHE_NAME = "db-futbol-v1"; // cambiar a v2, v3, etc.
   ```
2. Volvé a subir los archivos actualizados a tu hosting.
3. Cerrá y volvé a abrir la app (o recargá con el navegador un par de veces) para que tome la versión nueva.
