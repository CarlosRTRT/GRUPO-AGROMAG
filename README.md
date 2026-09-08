# GRUPO-AGROMAG

Sitio web de Agromag — clinica veterinaria y servicios de ganaderia.

## Stack

- [Astro](https://astro.build) 5 — sitio estatico
- Tailwind CSS 4 (via `@tailwindcss/vite`)
- Tabler Icons + Google Fonts (DM Sans / Space Grotesk)

## Levantar el proyecto

```bash
npm install
npm run dev      # http://localhost:4321
```

| Comando | Que hace |
|---|---|
| `npm run dev` | Servidor de desarrollo con recarga en caliente |
| `npm run build` | Build de produccion en `dist/` |
| `npm run preview` | Sirve el build ya compilado |

## Estructura

```
src/
  pages/index.astro    # landing completa
  styles/global.css    # Tailwind + variables de marca (--agromag-*)
public/                # assets estaticos (favicon, imagenes)
```

## Como trabajamos

Git Flow + Jira. **Antes de tocar codigo, lee [CONTRIBUTING.md](./CONTRIBUTING.md).**
Resumen: rama desde `develop`, PR a `develop`, lo mergea el lead.

## Herramientas de ayuda para ahorrar tokens 90%

- Repomix(Comprime todo el proyecto en md con estructuracion): https://github.com/yamadashy/repomix
- CloudConvert(Word a Markdown): https://cloudconvert.com/docx-to-md
