# Studio 54 Barbería — Sitio Web

Sitio web de una sola página para Studio 54 Barbería: catálogo de servicios, agenda con confirmación por WhatsApp, galería, video de presentación y contacto/ubicación.

100% HTML/CSS/JS estático — sin frameworks, sin build step, sin dependencias. Se puede editar y desplegar directamente.

## Estructura

```
index.html                  Página completa (marcado, estilos y lógica en un solo archivo)
site.webmanifest            Manifest para iconos de app / PWA básica
favicon.ico
assets/
  img/
    logo.png                 Logo a resolución media (secciones grandes)
    logo-nav.png              Logo pequeño (navbar / footer)
    favicon-16.png, favicon-32.png, android-chrome-192.png, android-chrome-512.png, apple-touch-icon.png
    og-image.jpg               Imagen para previsualización en redes sociales (WhatsApp, Facebook, etc.)
    video-poster.jpg           Fotograma de portada del video, se muestra antes de reproducir
  video/
    intro.mp4                  Video de introducción, comprimido para web (~4 MB, original en /originals)
originals/
  logo-original.png           Logo en máxima resolución entregado por el cliente
  video-introduccion-original.mp4   Video original sin comprimir
```

## Editar contenido del negocio

Casi todo el contenido variable (servicios, precios, horarios de agenda, WhatsApp, dirección, testimonios, galería) vive en un solo bloque `CONFIG` dentro de `index.html` — busca:

```js
const CONFIG = {
  business: { ... },
  services: [ ... ],
  ...
};
```

Edita esos valores y guarda; no hace falta tocar el resto del código.

Hay algunos datos de contacto duplicados como texto plano en el HTML (tarjeta de contacto, mapa decorativo y footer) porque no están conectados a `CONFIG` — si cambias dirección/horarios/teléfono, actualízalos también ahí (búscalos por el texto actual).

## Ver el sitio en local

No requiere instalación. Basta un servidor estático simple, por ejemplo:

```bash
python -m http.server 4173
```

y abrir `http://localhost:4173`.

(Abrir `index.html` con doble clic también funciona, pero algunos navegadores restringen la carga de video/imagen vía `file://`.)

## Pendientes antes de publicar

- [ ] **Dirección real** (tarjeta de contacto, mapa y footer)
- [ ] **Teléfono / WhatsApp** real y confirmado (`CONFIG.business.whatsapp`, formato `52XXXXXXXXXX` sin `+` ni espacios)
- [ ] **Horarios reales**
- [ ] **Catálogo y precios reales** (o confirmar que los actuales ya lo son)
- [ ] **Redes sociales**: los íconos de Instagram/Facebook/TikTok están deshabilitados (`href="#"`) hasta tener los enlaces reales
- [ ] **Testimonios**: los 3 actuales son de ejemplo (marcados con la etiqueta "Ejemplo" en la tarjeta) — sustitúyelos por reseñas reales de clientes
- [ ] **Galería**: las tarjetas actuales son marcadores de posición (etiqueta "Demo" al pasar el cursor) — sustituir por fotografía real del local
- [ ] **Dominio real**: actualizar las URLs `https://www.studio54barberia.com/` en las etiquetas `<meta>` Open Graph, `canonical` y el JSON-LD del `<head>`, una vez que se confirme el dominio definitivo

## Desplegar

Cualquier hosting de archivos estáticos sirve. Opciones típicas:

- **GitHub Pages**: Settings → Pages → Deploy from branch (`main`, carpeta `/`).
- **Netlify / Vercel**: conectar el repositorio, sin build command, publish directory `/`.
- **Hosting tradicional (cPanel, etc.)**: subir todo el contenido de este repositorio (excepto `/originals`, que es solo respaldo) a la carpeta pública del dominio vía FTP/SFTP o el administrador de archivos.

## Créditos

Video e imagen de logo proporcionados por el cliente. Video comprimido y logo optimizado (favicons, imagen Open Graph) para web.
