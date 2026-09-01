# Programador de Logística — Constructora Dupla

Sistema web para programar y coordinar el uso de equipos pesados (minicargadores, telehandlers, retro palas, camiones, etc.) entre los distintos proyectos de **Grupo Dupla / Constructora Dupla**.

🔗 **App en producción:** https://programador-logistico.vercel.app

## Qué hace

- Cualquier persona con el link puede solicitar un equipo para un proyecto, eligiendo fecha, hora y duración.
- El sistema valida en el momento si el equipo está disponible, si choca con otra reserva, o si está fuera de servicio.
- Reglas de negocio automáticas:
  - Los equipos pesados (Minicargador / Telehandler) no se pueden reservar por más de 16 horas seguidas, salvo que la solicitud se marque como urgente.
  - Máximo 3 solicitudes urgentes por persona cada 7 días.
  - No se trabaja los domingos, ni los sábados después del mediodía.
- Al guardar una reserva, se abre WhatsApp automáticamente con el resumen ya escrito para avisar al coordinador.
- Modo administrador (protegido con código) para editar, aprobar urgencias, marcar equipos fuera de servicio, y generar reportes mensuales en Excel con el costo de cada asignación.
- Todo se sincroniza en vivo entre todos los que tengan la página abierta (Supabase Realtime), con una sincronización de respaldo cada 60 segundos.

## Tecnología

Es una aplicación de una sola página (**`index.html`**), sin proceso de build ni dependencias que instalar:

- HTML + CSS + JavaScript "vanilla" (sin framework).
- [Supabase](https://supabase.com) (Postgres) como base de datos y backend — se conecta directo desde el navegador con el cliente JS de Supabase.
- Las reglas de negocio más importantes también están reforzadas del lado del servidor (constraints y triggers en Postgres), no solo en el navegador.
- Se despliega automáticamente en [Vercel](https://vercel.com) con cada push a `main`.

## Desarrollo

No hay build ni instalación: basta con abrir `index.html` en un navegador, o servirlo con cualquier servidor estático (por ejemplo `python3 -m http.server`).

Un workflow de GitHub Actions (`.github/workflows/bump-version.yml`) sube automáticamente el número de versión ("SamKill X.X") en cada push a `main` que modifique `index.html`.

## Empresa

**Grupo Dupla** — Constructora Dupla, Porto Valencia · República Dominicana
[Instagram](https://www.instagram.com/grupodupla/) · [Facebook](https://www.facebook.com/grupodupla/) · [LinkedIn](https://www.linkedin.com/company/grupodupla)
