# Iron Oxide — Nuxt site

Marketing site for Iron Oxide, built on Nuxt 3. Mirrors the design system in the
parent project (tokens, type, components, voice).

## Run locally

```bash
cd nuxt-site
npm install
npm run dev
```

Open http://localhost:3000.

## Pages

- `/` — landing (hero, features, architecture diagram, terminal, request-access form)
- `/architecture` — long-form walkthrough of the trust boundary
- `/docs` — install + quickstart
- `/changelog` — release log

## Structure

```
nuxt-site/
├─ app.vue                      # root, wires NuxtLayout + NuxtPage
├─ nuxt.config.ts               # head config, css imports, fonts
├─ assets/css/
│  ├─ tokens.css                # mirrors ../colors_and_type.css
│  └─ global.css                # body resets
├─ components/
│  ├─ SiteHeader.vue            # sticky nav + brand mark + CTA
│  └─ SiteFooter.vue            # © + links
├─ layouts/default.vue          # header + main + footer shell
├─ pages/
│  ├─ index.vue                 # landing
│  ├─ architecture.vue
│  ├─ docs.vue
│  └─ changelog.vue
└─ public/
   ├─ logo-mark.svg
   ├─ logo-lockup.svg
   └─ fonts/                    # Fira Code Nerd Font (4 weights)
```

## Build

```bash
npm run build      # SSR build
npm run generate   # static site
npm run preview    # preview the build
```

## Design tokens

`assets/css/tokens.css` is the source of truth for color, type, spacing, motion,
and radii. It mirrors `../colors_and_type.css` from the design system. If the
upstream tokens change, copy them across.
