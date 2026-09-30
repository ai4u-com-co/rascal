# CLAUDE.md — rascal

## Qué es
Sitio web de una sola página (landing) de RASCAL E-BIKE, marca de bicicletas eléctricas de Medellín
(contenido en español, `lang="es"`). Next.js App Router con secciones de marca y contacto.
Repo PÚBLICO: documentación y PRs sin secretos ni datos internos de clientes.
Producción (según la metadata del repo en GitHub): https://rascal-ai4u.vercel.app

## Stack
Next.js 16.0.10, React 19.2.1, TypeScript 5, Tailwind CSS v4 (`@tailwindcss/postcss`), framer-motion 12,
`clsx` + `tailwind-merge` (helper `cn` en `lib/utils.ts`). Alias de imports `@/`. CI usa Node 22.
No hay tests ni type-check como script.

## Comandos (package.json)
- `npm install` / `npm ci`
- `npm run dev` (next dev, puerto 3000 por defecto)
- `npm run build`
- `npm run start`
- `npm run lint` (eslint)

## Estructura
- `app/`: `layout.tsx` (fuentes locales, metadata/OpenGraph, Navbar + Footer + WhatsAppWidget), `page.tsx`
  (compone las secciones), `globals.css`.
- `components/sections/`: Hero, Manifesto, Values, WordsWorks, ProductShowcase, Lifestyle, Contact.
- `components/ui/`: piezas reutilizables (Heading, MonoText, RascalButton, StatusBadge, Marquee, BackgroundSlider).
- `components/`: Navbar, Footer, WhatsAppWidget.
- `public/`: assets servidos (fuentes en `public/fonts`, imágenes en `public/images`).
- `design_assets/`: guidelines de marca fuente (.ai, PDF, logos, fuentes). Pesado; no se sirve.

## Convenciones y trampas
- Las fuentes (Core Sans, Silka Mono) se cargan con `next/font/local` desde `public/fonts/`: si se renombra
  o mueve un archivo, el build falla.
- Paleta/tipografía vienen de la guía de marca en `design_assets/`; no improvisar colores ni logos.
- Los datos de contacto (teléfono, correo, Instagram, número y mensaje de WhatsApp) están escritos
  directamente en `components/sections/Contact.tsx` y `components/WhatsAppWidget.tsx`. Por confirmar si
  deben moverse a variables de entorno o configuración.
- Se deja `ESLint` como única verificación automática además del build; correr ambos antes de abrir PR.
- No es un sistema multitenant ni toca SAP. No hay backend ni rutas API en el repo.
- Mobile first (375px) sin scroll horizontal; revisar visualmente cambios de layout.

## Variables de entorno
Ninguna requerida según el código visto (no hay `.env.example`; `.env*` está en `.gitignore`).

## Despliegue y ramas
- Rama default: `master`. El CI (`.github/workflows/ci.yml`) corre `npm ci`, `lint` y `build` en push a
  main/master y en PRs.
- Despliegue en Vercel (hay `.vercel` en `.gitignore` y URL en el repo); por confirmar el nombre del
  proyecto, si hay integración Git automática y el dominio definitivo.
- El repo incluye plantillas de Issue/PR en `.github/`.
- Por confirmar: el `README.md` es el de `create-next-app` sin personalizar; no describe el proyecto.
