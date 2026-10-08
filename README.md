# Meku Arts — Landing Page

Sitio web oficial de **Meku Arts**: papelería creativa, cake toppers, agendas, invitaciones y detallitos hechos a mano en Maracaibo, Venezuela.

🌐 [mekuarts.com](https://mekuarts.com)
📷 [@mekuarts](https://instagram.com/mekuarts)
💬 +58 414 068 7853

## Stack

Next.js (App Router) + Tailwind CSS 4, exportado como sitio estático (`output: "export"`).
Este repositorio guarda **solo el resultado del build** (lo que sirve GitHub Pages).
El código fuente vive en el proyecto `web-builder/site`.

Para actualizar la página:

1. En `web-builder`: `npm run build --prefix site`
2. Copiar el contenido de `site/out/` a este repo (sin borrar `CNAME`).
3. Commit y push a `main`.

La versión anterior de la página quedó en la rama `web-anterior`.

## Despliegue

Hosteado en **GitHub Pages** con dominio personalizado vía DNS (DonWeb). Ver `SETUP.md`.

Incluye el Meta Pixel (PageView + evento Contact en cada clic a WhatsApp).
