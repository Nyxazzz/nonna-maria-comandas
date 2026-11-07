# Nonna Maria · Comandas

App web para tomar comandas, cobrar (con cálculo del cambio) y llevar los turnos de Nonna Maria.
Funciona en el navegador y se puede instalar en el móvil o la tablet como una app más.

## Instalarla en un dispositivo

- **iPhone / iPad (Safari):** abre el enlace, pulsa Compartir → *Añadir a pantalla de inicio*.
- **Android (Chrome):** abre el enlace, menú ⋮ → *Instalar aplicación* (o *Añadir a pantalla de inicio*).
- **Ordenador (Chrome / Edge):** icono de instalar en la barra de direcciones.

## Cómo llegan las actualizaciones

Cada vez que se publica un cambio en este repositorio, GitHub Pages lo sirve en un minuto o dos.
Al abrir la app (o volver a ella) se descarga la versión nueva. Si no hay ninguna comanda a medias
se recarga sola; si la hay, aparece el botón **Actualizar** para no perderla.

Al publicar un cambio, sube el número de versión en dos sitios:
`APP_VERSION` en `index.html` y `VERSION` en `sw.js`.

## Datos

Las comandas y los turnos se guardan en cada dispositivo (almacenamiento del navegador).
No se comparten entre dispositivos y se pierden si se borran los datos del navegador.
