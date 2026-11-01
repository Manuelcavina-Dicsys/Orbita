# Diseño del MVP de Órbita

Acordado el 2026-11-01.

## Visión

Una mezcla de Slack, Miro, Notion y un bot de Telegram que ayuda a tener orden y organización. El MVP es el **módulo personal**; el módulo de equipos viene después.

**Dentro del alcance:** tests, CI, ADRs y logs básicos desde el día 1.
**Fuera del alcance:** facturación y planes, multi-tenant pesado (bases o schemas por cliente, RLS) y widgets.

## Modelo base

### Workspace

- Todo dato pertenece a un **workspace** (`workspace_id`).
- El espacio personal es un workspace de un solo miembro. Los equipos serán workspaces compartidos.
- Los services verifican que el usuario sea miembro del workspace. No hay más aislamiento que ese.

### Tarea y evento

- **Evento**: algo que ocupa un horario (dentista de 10 a 11). No se "completa".
- **Tarea**: algo para hacer, con estado, prioridad y fecha límite opcional.
- **Una tarea puede agendarse**: si se le asigna un bloque horario, aparece en el calendario como un evento. Un evento nunca es una tarea.
- El calendario muestra eventos, tareas agendadas y (más adelante) eventos de Google.

### Hora e idioma

- Todo se guarda en **UTC** y se muestra en la zona horaria del usuario (por defecto `America/Argentina/Buenos_Aires`).
- Interfaz solo en español, con los textos centralizados para poder traducirlos después.

## Stack

Ver los [ADRs](adr/) para el porqué de cada decisión.

- **Backend**, igual a Dicsys Core: Python 3.14, FastAPI, Pydantic 2, SQLAlchemy 2, Alembic y PostgreSQL 16, con uv, Ruff y pytest. Cada módulo sigue `routers → dependencies → schemas → services → models`.
- **Frontend**: Vue 3, Vite, TypeScript, Tailwind v4, shadcn-vue, Pinia y TanStack Query, con un cliente generado desde OpenAPI.
- **Auth**: login con Google o cuenta propia (email y contraseña). JWT con refresh token y bcrypt. Mails con Resend en producción y Mailpit en local. Sin 2FA por ahora.
- **Infra**: contenedores `api`, `scheduler` y `bot` con la misma imagen, en Docker Compose. Desarrollo local primero y después una VM chica (~10–20 USD/mes).

## Orden de construcción

1. **Esqueleto**: repo, Docker, CI, auth y workspace personal.
2. **Tareas, eventos y calendario web.**
3. **Hábitos**: frecuencia (diaria, días específicos, X veces por semana), rachas e historial, marcados desde la web.
4. **Notas**: editor por bloques con TipTap, etiquetas y carpetas.
5. **Google Calendar** en solo lectura.
6. **Mate**: sesión de diseño del personaje y construcción del bot.

Los recordatorios de hábitos y el resumen matutino salen por Telegram, así que llegan con la fase 6.

## Mate 🧉 (fase 6)

Ideas ya acordadas. La personalidad de Mate como personaje se define en su propia sesión de diseño.

- **Lenguaje natural** desde el inicio, con comandos (`/hoy`, `/nota`) como atajo. El LLM elige entre las acciones del backend (tool use).
- **Gemini** detrás de un adaptador `LLMProvider`, para poder cambiar de proveedor sin tocar el resto.
- **Entradas**: texto, audios (los transcribe Gemini) y mensajes reenviados. Fotos y archivos, más adelante.
- **Proactividad**: resumen matutino, check-in nocturno de hábitos, recordatorios y "no molestar". La revisión semanal viene después.
- **Consultas**: agenda y hábitos ("¿qué tengo el jueves?"). La búsqueda inteligente en notas viene después.
- **Confirmaciones**: crear se hace directo con un botón "Deshacer"; modificar o borrar pide confirmación; si el pedido es ambiguo, pregunta.
- **Memoria corta**: los últimos ~10 mensajes.
- **Vinculación** con la cuenta mediante un link con token de un solo uso.
- **Límite diario** de llamadas al LLM por usuario y registro de consumo.

## Después del MVP

- Módulo de equipos: kanban, lluvia de ideas, calendario compartido, almacén de archivos y conectores.
- Widgets (en la web y de escritorio).
- Google Calendar con escritura.
- 2FA.
