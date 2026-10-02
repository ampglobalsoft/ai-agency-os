# Plantillas de entregable — la marca de la casa

Tres plantillas HTML con la estética del OS (monocromo, una página, lenguaje de dueño de negocio). Las usan los playbooks `/informe`, `/auditoria` y `/propuesta`, y cualquier skill que genere entregables (vía `tool-visual-explainer`).

**Cómo se usan**: copiar la plantilla, incrustar `base.css` dentro de `<style>`, sustituir TODOS los `{{...}}` (el gate de entregables detecta los que se queden sin rellenar), guardar en `clients/<cliente>/entregables/YYYY-MM-nombre.html`.

**Personalización de agencia**: el operador puede cambiar `base.css` (su color de acento, su logo en el footer) UNA vez y toda su producción sale con su marca.

**Marca AMP Global Soft (ya aplicada en `base.css`)**:
- **Logo**: la regla `header::before` incrusta el logo (data URI) en la cabecera de cualquier plantilla que lleve `<header>`. No hace falta añadir ninguna etiqueta `<img>`; basta con incrustar `base.css` como siempre. Para cambiar de marca, sustituir la URL de esa regla.
- **Colores**: `--ink` = `#353531` (gris carbón del logo) y `--accent` = `#F9C13C` (amarillo del logo). El amarillo se usa como acento (líneas, bordes, franjas), nunca como color de texto sobre blanco.
