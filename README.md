# 🔨 Martillo

Subastas en vivo, sin vueltas. Creás un lote, compartís un código de 4
caracteres y la gente entra a pujar en tiempo real desde el navegador.
Todo en un único archivo HTML autocontenido, sin build ni dependencias.

## Correr en local

No necesita compilar nada. Serví la carpeta con cualquier servidor estático:

```bash
# Python
python -m http.server 8080

# o Node
npx serve .
```

Abrí `http://localhost:8080/` (o `http://localhost:8080/index.html`).

> Podés abrir el `.html` directo con doble clic, pero servirlo por HTTP es lo
> recomendado (algunas APIs del navegador se portan mejor bajo `http://`).

## Deploy

Es un sitio estático: subís la carpeta y listo.

- **GitHub Pages**: subí el repo, activá Pages sobre la rama `main`, y listo:
  como el archivo se llama `index.html`, la subasta carga en la raíz del sitio.
- **Netlify / Vercel**: arrastrá la carpeta (o conectá el repo). No hay comando
  de build; el output es la carpeta tal cual.

## Seguridad y límites (LEÉ ESTO)

Esta versión es un **demo cliente-only**. No tiene backend, y eso define lo que
puede y lo que **no** puede hacer.

**Lo que sí se endureció en esta versión:**

- **Content-Security-Policy** restrictiva (`default-src 'none'`, sin scripts ni
  conexiones externas más allá de las fuentes de Google).
- **XSS cerrado en todos los puntos de inyección**: título, descripción, nombres,
  moneda e imágenes se escapan o se validan antes de pintarse en el DOM. Las
  imágenes solo se aceptan si son `data:image/...` o `blob:` inertes.
- **Validación de entradas**: límites de longitud, montos finitos y acotados,
  duración y moneda restringidas a una lista blanca, código de sala limitado a
  `A–Z0–9`.
- **Fallback de almacenamiento**: si no existe el `window.storage` del entorno
  que la generó, usa `localStorage` para no romperse en un hosting normal.

**Lo que esta versión NO puede garantizar (y por qué):**

- **Integridad de las pujas.** No hay servidor que sea dueño de la verdad. Toda
  la validación (puja mínima, subasta cerrada) vive en el cliente, así que
  alguien con la consola abierta puede saltearla. El cliente **nunca** puede ser
  la autoridad de una subasta.
- **Concurrencia real.** Dos pujas simultáneas leen y reescriben el lote entero
  → gana la última y la otra se pierde (last-write-wins).
- **Identidad.** El nombre es texto libre; cualquiera puede pujar como cualquiera.
- **Compartir entre dispositivos con el fallback de `localStorage`.** Ese
  almacenamiento es por navegador: el código no viaja a otro celular. Compartir
  salas de verdad requiere almacenamiento del lado del servidor.

**Conclusión:** usalo para demos, juegos internos o pruebas de concepto. Para una
subasta con valor real hace falta un backend que valide las pujas, maneje
concurrencia de forma atómica y autentique a quién puja. Ese es el próximo paso
si algún día lo necesitás.

## Estructura

```
martillo/
  index.html      # la app completa (HTML + CSS + JS inline)
  README.md
  CONTRIBUTING.md
  LICENSE
  .gitignore
```
