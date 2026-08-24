# Pulso LinkedIn

Lead magnet de diagnóstico de perfiles de LinkedIn. Una sola página estática (`index.html`), sin dependencias ni build: el visitante deja nombre y correo, sube el `.xlsx` que exporta LinkedIn desde sus estadísticas, y recibe un score 0–100 sobre cuatro pilares (consistencia, alcance, engagement, crecimiento) con insights de mejora. Todo el procesamiento del archivo ocurre en el navegador del visitante — ningún dato de LinkedIn sale de su máquina.

**Producción:** https://brissia.github.io/pulso-linkedin/

## Captura de leads

El formulario de entrada envía cada registro (nombre, correo, fecha) vía [FormSubmit](https://formsubmit.co) a `brissia.benavente@gmail.com`.

- **Activación (una sola vez):** el primer envío dispara un correo de FormSubmit pidiendo confirmar la dirección. Hasta no confirmarlo, los leads no llegan.
- **Ocultar el correo del código fuente (recomendado):** tras activar, FormSubmit permite usar un alias aleatorio en lugar del correo. En https://formsubmit.co obtén tu *random-like string* y reemplaza en `index.html` la línea:
  ```
  const FORM_ENDPOINT = "https://formsubmit.co/ajax/brissia.benavente@gmail.com";
  ```
  por `https://formsubmit.co/ajax/<tu-alias>`.
- **Cambiar de proveedor:** cualquier endpoint que acepte un POST JSON funciona (Formspree, Tally, un webhook de Make/Zapier hacia tu CRM). Solo cambia `FORM_ENDPOINT`.
- Si el envío falla (sin conexión, endpoint caído), el visitante igual accede a la herramienta: la captura nunca bloquea la experiencia.

## Publicar cambios

```bash
git add -A && git commit -m "Describe el cambio" && git push
```

GitHub Pages redespliega solo (1–2 minutos).

## Calibrar el score

Los benchmarks viven en la función `analyze()` de `index.html`: cadencia objetivo (2.5 posts/semana), ER de referencia (5 % = máximo), crecimiento mensual (3 %), alcance sobre seguidores (4×) y share de audiencia con seniority (30 %). Los textos de los insights están en `buildInsights()`.
