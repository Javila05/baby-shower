# Baby Shower — invitación web

Invitación de una sola página: sobre animado, datos del evento, ubicación con
botón a Google Maps y confirmación de asistencia por WhatsApp.

## Archivos

```
baby-shower/
  index.html      la página completa (estructura, estilos y animación)
  datos.js        los datos de la fiesta  ← lo único que necesitas editar
  assets/         las imágenes
  LEEME.md        este archivo
```

## Probarla

Doble clic en `index.html`. Se abre en el navegador y funciona tal cual, sin
instalar nada. Para ver cómo se verá en el celular: clic derecho → Inspeccionar
→ el iconito de teléfono (o F12 y luego Ctrl+Shift+M).

## Editar los datos

Abre `datos.js` con el Bloc de notas o VS Code y cambia los valores entre comillas.

| Campo | Qué poner |
|---|---|
| `whatsapp` | Código de país + número, sin `+`, sin espacios ni guiones. Guatemala: `502` + los 8 dígitos → `"50255551234"` |
| `diaSemana`, `fecha`, `hora` | Tal como quieres que se lean en pantalla |
| `salon`, `direccion` | Nombre y dirección del lugar |
| `lat`, `lng` | Coordenadas del salón para abrir el punto exacto en Google Maps |
| `mapsUrl` | Enlace obtenido con la opción “Compartir” de Google Maps |

### Cómo sacar las coordenadas

Abre Google Maps, mantén presionado sobre el punto exacto del salón. Aparecen dos
números, por ejemplo `14.599512, -90.513443`. El primero es `lat`, el segundo `lng`.
Van **sin comillas**, porque son números:

```js
lat: 14.599512,
lng: -90.513443,
```

## Cambiar las imágenes

Reemplaza los archivos dentro de `assets/` **conservando el mismo nombre**.

| Archivo | Qué es |
|---|---|
| `env_closed.webp` | El sobre cerrado de la pantalla inicial |
| `bear_hero.webp` | El osito en el globo que sube trayendo la invitación |
| `venue.webp` | La foto del salón |
| `osodurmiendo.png` | El osito dormido de la nube con la fecha |
| `oso.png` | El osito de la nube de confirmación |
| `PACHA.png` | La imagen de la nube de ubicación |
| `sonido.mp3` | Música que comienza al abrir el sobre y se repite automáticamente |
| `bear_sit.webp` | El osito sentado junto a "¡Te esperamos!" |
| `clouds.webp` | La banda de nubes del fondo |

Lo importante: que vengan **con fondo transparente** (PNG o WebP). Si tienen fondo
blanco se les nota un recuadro sobre el cielo de la página.

## Ajustar la animación

Está hecha con GSAP y vive al final de `index.html`, en la función `arrancar()`.
Es una línea de tiempo: cada paso lleva su duración en segundos y el momento en que
entra. Por ejemplo, para que el globo suba más rápido, baja el `2.7`:

```js
.to(riser, { y: 0, scale: 1, duration: 2.7, ease: "power2.out" }, .55)
```

Si cambias esa duración, ajusta también el `3.0` del `.add(mostrarSitio, 3.0)`
unas décimas más arriba, que es cuando aparece la página.

## Subirla a internet

La forma más rápida y gratis es **Netlify Drop**: entra a `app.netlify.com/drop`
y arrastra la carpeta `baby-shower` completa. En unos segundos te da un enlace
público listo para mandar por WhatsApp. Desde ahí puedes cambiarle el nombre al
sitio o conectarle un dominio propio.

También sirven GitHub Pages, Vercel o cualquier hosting normal: solo hay que subir
los archivos tal como están.

## Notas

- GSAP se carga desde internet. Si no hay conexión, la animación corre igual con
  una versión de respaldo en CSS; se ve un poco más simple pero nunca queda en blanco.
- El botón de WhatsApp no envía nada solo: abre la conversación con el mensaje ya
  escrito y la persona presiona enviar.
