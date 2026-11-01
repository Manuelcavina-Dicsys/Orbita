# 🪐 Órbita

Sistema personal de organización: calendario, tareas, notas y hábitos, con **Mate** 🧉, un asistente por Telegram que entiende lenguaje natural.

Proyecto personal construido con ingeniería de producto: tests, CI, decisiones documentadas y logs desde el día 1.

## Estado

🟡 Diseño cerrado. Próximo paso: esqueleto del proyecto (fase 1).

## Documentación

- [Diseño del MVP](docs/design.md): visión, modelo, stack y orden de construcción.
- [Estructura del repo](docs/structure.md): qué va en cada carpeta.
- [Decisiones de arquitectura (ADRs)](docs/adr/): por qué se eligió cada cosa.

## Stack

| Capa | Tecnología |
|---|---|
| Backend | Python 3.14 · FastAPI · Pydantic 2 · SQLAlchemy 2 · Alembic |
| Base de datos | PostgreSQL 16 |
| Frontend | Vue 3 · Vite · TypeScript · Tailwind v4 · shadcn-vue · Pinia · TanStack Query |
| Bot | Telegram · Gemini (detrás de un adaptador `LLMProvider`) |
| Infra | Docker Compose (`api`, `scheduler`, `bot`) · GitHub Actions |
| Herramientas | uv · Ruff · pytest · Vitest · Playwright |
