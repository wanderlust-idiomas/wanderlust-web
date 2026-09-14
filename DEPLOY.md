# Wanderlust — Sitio web

Sitio one-page para Wanderlust (traductora pública + profesora, marca de Lau Willigs). HTML/CSS puro, sin frameworks ni build step — se sube tal cual a GitHub Pages.

## Estructura del proyecto

```
wanderlust/
├── index.html          ← el sitio completo (HTML + CSS inline)
├── img/                ← 6 fotos usadas en el sitio, ya optimizadas para web
├── logos/               ← logo en SVG (color y blanco)
└── DEPLOY.md            ← este archivo
```

Paleta de marca: `#132F57` (navy), `#1EABA3` (turquesa), `#EBDBC4` (beige), `#F7F4ED` (crema, fondo general), `#FF725E` (coral), `#1E1E1E` (texto). Tipografías: Plus Jakarta Sans (títulos) e Inter (texto), vía Google Fonts.

## Estado actual — qué falta para quedar 100% funcional

1. **Formularios sin conectar todavía.** Hay dos `<form>` en `index.html` (buscar `TU_FORM_ID_AQUI`, aparece 2 veces) que apuntan a Formspree pero con un ID placeholder. Sin esto, los formularios no van a enviar nada.
2. **El código nunca se subió a GitHub.** El repo `https://github.com/wanderlust-idiomas` existe como organización, pero no hay repositorio creado todavía.
3. **El dominio (en Cloudflare) no está apuntando a ningún lado todavía.**

## Instrucciones paso a paso

### 1. Conectar los formularios a info@wanderlust-idiomas.com
- Crear cuenta en https://formspree.io con el mail info@wanderlust-idiomas.com.
- Crear un formulario nuevo, copiar el ID que da (ej. `xzbqrwyz`).
- Reemplazar **las 2 apariciones** de `TU_FORM_ID_AQUI` en `index.html` por ese ID.
- **Importante:** el plan gratis de Formspree NO permite adjuntar archivos. El formulario de cotización (sección Traducciones) tiene un campo de subir documento — para que funcione hace falta el plan Personal (USD 10/mes). Avisar esto antes de dar por cerrado el proyecto, por si no estaba presupuestado.
- Formspree pide confirmar el primer envío por mail antes de que el formulario quede activo — hacerlo antes de avisarle a la clienta que el sitio ya está listo.

### 2. Crear el repositorio y subir el código
- Repo nuevo en la organización: `github.com/wanderlust-idiomas`, público (necesario para GitHub Pages gratis), nombre sugerido `wanderlust-web`.
- Desde la carpeta de este proyecto:
  ```
  git init
  git add .
  git commit -m "Primera versión del sitio Wanderlust"
  git branch -M main
  git remote add origin https://github.com/wanderlust-idiomas/wanderlust-web.git
  git push -u origin main
  ```
- En GitHub: **Settings → Pages** → rama `main`, carpeta `/ (root)` → Save. El sitio queda en `https://wanderlust-idiomas.github.io/wanderlust-web/`.

### 3. Conectar el dominio propio (Cloudflare)
- En **Settings → Pages → Custom domain** del repo, escribir el dominio final (ej. `wanderlust-idiomas.com`). Esto genera un archivo `CNAME` en el repo automáticamente.
- En Cloudflare → DNS del dominio, agregar:
  - 4 registros **A** en `@` apuntando a: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`
  - 1 registro **CNAME** en `www` apuntando a `wanderlust-idiomas.github.io`
- Si el certificado SSL de GitHub tarda en emitirse, probar con el proxy de Cloudflare (nube naranja) desactivado unos minutos.
- Activar "Enforce HTTPS" en GitHub Pages una vez que el dominio esté verificado (puede tardar horas en propagar).

### 4. Checklist final antes de avisarle a la clienta
- [ ] Los dos formularios envían y el mail llega a info@wanderlust-idiomas.com (probar en el sitio ya publicado, no en el archivo local)
- [ ] Todos los botones de navegación y CTA funcionan (Inicio, Nosotros, Traducciones, Contacto, "Solicitar experiencia", "Anotarme en la lista de espera")
- [ ] El acordeón "Conocé mi historia completa" abre y cierra bien
- [ ] El sitio se ve bien en mobile (falta una revisión más a fondo de esto — quedó pendiente)
- [ ] HTTPS activo y el dominio propio carga bien
