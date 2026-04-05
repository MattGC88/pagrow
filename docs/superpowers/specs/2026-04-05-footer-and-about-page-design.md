# Footer Fix & Sobre Nosotros Page — Design Spec

**Date:** 2026-04-05  
**Status:** Approved

---

## Overview

Fix the mock footer so all links are real and functional, and create a standalone `sobre-nosotros.html` page. The site is a static single-page catalog (`index.html`) with one CSS file and two JS files (`data.js`, `app.js`).

---

## 1. Footer — Productos Section

Replace the 4 current placeholder `#` links with real category anchors.

| Label | href |
|---|---|
| Bioestimulantes | `index.html#bioestimulantes` |
| Biología del suelo | `index.html#suelo` |
| Correctores nutricionales | `index.html#correctores` |
| Microorganismos | `index.html#micro` |

**Hash routing behavior (new JS in `app.js`):**  
On `DOMContentLoaded`, read `window.location.hash`. If it matches a category id (`bioestimulantes`, `suelo`, `correctores`, `micro`), activate the corresponding tab chip, set `activeCategory`, call `renderCatalog()`, then scroll `#catalogBody` into view. This must work both when landing directly on `index.html#suelo` and when navigating back from `sobre-nosotros.html`.

---

## 2. Footer — Empresa Section

Remove all placeholder links (Investigación, Distribuidores, Blog). Keep only:

| Label | href |
|---|---|
| Sobre Pagrow | `sobre-nosotros.html` |

Privacy policy page is skipped — the site has no forms, no cookies, and no user data collection.

---

## 3. Footer — Contacto Section

Replace all placeholder links with real contact data:

| Label | href | Notes |
|---|---|---|
| @pagrow_ec | `https://www.instagram.com/pagrow_ec/` | Opens in new tab |
| Administracion@pagrow.co | `mailto:Administracion@pagrow.co` | — |
| WhatsApp | `https://wa.me/593999406826?text=...` | Same encoded message as modal |

WhatsApp message text: `Hola, me gustaría obtener más información sobre los productos Pagrow.`

---

## 4. `sobre-nosotros.html`

Standalone HTML page. Shares `assets/css/styles.css`. Has its own `<header>` and `<footer>` (same markup as `index.html` — no JS dependency on `data.js`/`app.js`).

### Sections

**Hero**
- Heading: `Sobre Pagrow`
- Subheading: `Ciencia agrícola que transforma cultivos`
- Reuses `.hero` and `.hero-content` classes from existing styles

**Misión**
- Section label: `Nuestra misión`
- Body: the Instagram mission text verbatim:
  > En Pagrow trabajamos con un propósito claro: proporcionar soluciones innovadoras y sostenibles que eleven la productividad y calidad de los cultivos de exportación, siempre respetando el medio ambiente. Nuestro compromiso es impulsar una agricultura responsable, rentable y alineada con el futuro del planeta.

**Lo que hacemos**
- Section label: `Nuestras líneas de producto`
- Four cards/items — one per category — with name and one-sentence description pulled from `data.js` category `description` fields (hardcoded in HTML, not JS-rendered):
  1. **Bioestimulantes** — Formulaciones para potenciar el desarrollo radicular y las defensas naturales de la planta.
  2. **Biología del suelo** — Desbloqueo y establecimiento de microorganismos benéficos para suelos sanos y productivos.
  3. **Correctores nutricionales** — Soluciones foliares de alta asimilación para corregir deficiencias y equilibrar la nutrición.
  4. **Microorganismos** — Hongos y bacterias benéficas para el control biológico y la salud del cultivo.

**CTA**
- Button: `Explorar catálogo` → `index.html`
- Styled with existing `.btn-download` or similar CTA button class

### SEO & Meta
- `<title>Sobre Pagrow – Ciencia Agrícola para tus Cultivos</title>`
- `<meta name="description">` — one sentence from the mission
- `<link rel="canonical" href="https://pagrow.es/sobre-nosotros.html">`
- Same favicon, same CSP meta

---

## Out of Scope

- Privacy policy page
- Blog, distribuidores, investigación links (removed)
- Any backend, form, or analytics integration
- Mobile nav / hamburger menu functionality (not currently implemented)
