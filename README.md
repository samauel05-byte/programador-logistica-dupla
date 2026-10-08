# Programador de Logística — Constructora Dupla

Sistema web para programar y coordinar el uso de equipos pesados (minicargadores, telehandlers, retro palas, camiones, etc.) entre los distintos proyectos de **Grupo Dupla / Constructora Dupla**.

🔗 **App en producción:** https://programador-logistico.vercel.app

## Qué hace

- Cualquier persona con el link puede solicitar un equipo para un proyecto, eligiendo fecha, hora y duración.
- El sistema valida en el momento si el equipo está disponible, si choca con otra reserva, o si está fuera de servicio.
- Reglas de negocio automáticas:
  - Los equipos pesados (Minicargador / Telehandler) no se pueden reservar por más de 16 horas seguidas, salvo que la solicitud se marque como urgente.
  - Los Minicargadores además requieren 2 días de margen entre solicitudes del mismo proyecto (los Telehandler no tienen esa restricción).
  - Máximo 3 solicitudes urgentes por persona cada 7 días.
  - No se trabaja los domingos, ni los sábados después del mediodía.
- Al guardar una reserva, se abre WhatsApp automáticamente con el resumen ya escrito para avisar al coordinador (con protección anti-bloqueo de ventanas emergentes).
- **Solicitud de Renta de Equipo**: formulario aparte para pedir equipo que la empresa no posee (alquiler a un proveedor externo). Quien solicita debe indicar cuánto tiempo necesita el equipo (texto libre: "8 horas", "2 días", "1 semana", etc.). Queda pendiente de aprobación; al aprobar, el administrador debe indicar fecha y duración; al rechazar, el administrador está obligado a escribir el motivo del rechazo (se valida también en el servidor), el cual queda visible en la solicitud. Se oculta del panel sola a los 10 minutos si se rechaza, o cuando se marca como entregada si se aprueba.
- **Equipos Temporales**: un grupo de equipos adicionales, ocultos por defecto, que el administrador activa/desactiva según necesidad — aparecen al instante para todos.
- El administrador puede **agregar proyectos/obras nuevos** a la lista sin tocar código (se guardan siempre en mayúscula).
- Modo administrador (protegido con código maestro, verificado en el servidor) para editar, aprobar urgencias, marcar equipos fuera de servicio, aprobar/rechazar solicitudes de renta, agregar proyectos, personalizar logo/favicon, y generar reportes mensuales en Excel con el costo de cada asignación.
- Todo se sincroniza en vivo entre todos los que tengan la página abierta (Supabase Realtime), con una sincronización de respaldo cada 60 segundos.

## Tecnología

Es una aplicación de una sola página (**`index.html`**), sin proceso de build ni dependencias que instalar:

- HTML + CSS + JavaScript "vanilla" (sin framework), con tipografía Inter.
- [Supabase](https://supabase.com) (Postgres) como base de datos y backend — se conecta directo desde el navegador con el cliente JS de Supabase.
- Las acciones de administrador siempre pasan por funciones de Postgres (`SECURITY DEFINER`) que validan el código maestro en el servidor, nunca en el navegador. Las reglas de negocio más importantes también están reforzadas con constraints y triggers en Postgres, no solo en el cliente.
- Se despliega automáticamente en [Vercel](https://vercel.com) (producción) con cada push a `main`; Netlify genera una vista previa de cada pull request.

## Desarrollo

No hay build ni instalación: basta con abrir `index.html` en un navegador, o servirlo con cualquier servidor estático (por ejemplo `python3 -m http.server`).

Un workflow de GitHub Actions (`.github/workflows/bump-version.yml`) sube automáticamente el número de versión ("SamKill X.X") en cada push a `main` que modifique `index.html`.

## Empresa

**Grupo Dupla** — Constructora Dupla, Porto Valencia · República Dominicana
[Instagram](https://www.instagram.com/grupodupla/) · [Facebook](https://www.facebook.com/grupodupla/) · [LinkedIn](https://www.linkedin.com/company/grupodupla)
