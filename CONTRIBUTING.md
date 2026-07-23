# Contribuir a Subastapp

¡Gracias por pasar! Subastapp es un proyecto chico y autocontenido, así que
contribuir es simple. No hay build ni dependencias: todo vive en `index.html`.

## Antes de arrancar

Leé la sección **Seguridad y límites** del [README](README.md). Esta versión es
un demo cliente-only y hay cosas que, por diseño, no se pueden resolver sin un
backend (integridad de pujas, concurrencia real, identidad). Si tu idea depende
de eso, abrí primero un issue para charlarlo antes de escribir código.

## Cómo proponer un cambio

1. Hacé un fork y creá una rama descriptiva: `git checkout -b fix/puja-minima`.
2. Editá `index.html`. Todo el HTML, CSS y JS está inline en ese archivo.
3. Probalo en local sirviendo la carpeta:
   ```bash
   python -m http.server 8080
   ```
   y abrí `http://localhost:8080/`.
4. Verificá que la Content-Security-Policy no rompa (mirá la consola del
   navegador: no debería haber violaciones de CSP).
5. Abrí un Pull Request explicando el qué y el porqué.

## Pautas

- **No agregues dependencias externas.** El proyecto es un único archivo sin
  build; mantengámoslo así. Nada de CDNs de scripts ni `connect-src` a dominios
  nuevos.
- **Cuidá la seguridad.** Todo input del usuario se escapa o valida antes de
  tocar el DOM. Si agregás un punto de inyección nuevo, escapalo.
- **Mantené el estilo.** Seguí las convenciones de nombres y el formato que ya
  hay en el archivo.
- **Un cambio por PR.** Más fácil de revisar, más fácil de mergear.

## Reportar un bug o pedir una feature

Usá las plantillas de issue (bug o feature). Cuanto más contexto, mejor:
navegador, pasos para reproducir y qué esperabas que pasara.
